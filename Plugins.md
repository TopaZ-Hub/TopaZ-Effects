# Tworzenie wtyczek do TopaZ Effects 26 (TFX Plugin API v1)

Wtyczka to **folder** w `Dokumenty\TopaZ Effects\Plugins\` z dwoma plikami:

```
Dokumenty\TopaZ Effects\Plugins\
  moja-wtyczka\
    plugin.json
    main.js
```

Najszybciej: w programie otwórz panel **Wtyczki** (prawa kolumna) i kliknij **+ Nowa wtyczka**.
Program utworzy folder z gotowym szablonem. Po zmianach w `main.js` kliknij **Przeładuj**.

## plugin.json

```json
{
  "id": "moja-wtyczka",
  "name": "Moja wtyczka",
  "version": "1.0.0",
  "author": "Ty",
  "description": "Co robi wtyczka",
  "api": 1,
  "main": "main.js"
}
```

## main.js

Kod dostaje obiekt `tfx`. Możesz w nim rejestrować:

### 1. Efekty GPU (shader GLSL)

```js
tfx.registerEffect({
  id: 'zloty',
  name: 'Złoty blask',
  category: 'Moje efekty',
  params: [
    tfx.num('amount', 'Siła', 0, 100, 60),
    tfx.color('c', 'Kolor', '#ffcc33'),
    tfx.check('keep', 'Zachowaj oryginał', true)
  ],
  glsl: `
    vec3 gold = u_c0 * luma(X) * 1.5;
    o = pre(mix(X, gold, P(0) / 100.0), C.a);
  `
});
```

- Parametry liczbowe, listy (`tfx.select`) i pola wyboru (`tfx.check`) trafiają **po kolei** do `P(0)`, `P(1)`, `P(2)`…
  Kolory nie zajmują numeru – trafiają do `u_c0`, `u_c1`, `u_c2`.
- W shaderze masz: `uv` (0..1), `px` (rozmiar piksela), `C` (kolor piksela, premultiplied), `X` (kolor bez alfy),
  `T(uv)` (próbkowanie warstwy), `T2(uv)` (bufor pomocniczy), `u_time` (czas kompozycji), `u_lt` (czas warstwy),
  `u_res` (rozmiar bufora), `u_k` (skala rozdzielczości – mnóż przez nią promienie w pikselach).
- Funkcje: `luma()`, `pre(rgb, a)`, `unp(c)`, `hash()`, `vnoise()`, `rgb2hsv()`, `hsv2rgb()`, `aspect()`.
- Wynik zapisz do `o` (kolor z alfą premultiplied).

Efekt wieloprzebiegowy: zamiast `glsl` podaj `run(G, P)` i wywołuj gotowe przebiegi, np.
`G.pass('blur1d', [promien, 1, 0]); G.pass('blur1d', [promien, 0, 1]);` (rozmycie gaussowskie poziomo i pionowo).

Efekty z wtyczek działają też w **TopaZ Editing Pro** (Dynamic Link) – Editing wczytuje te same wtyczki.

### 2. Polecenia (menu **Wtyczki**)

```js
tfx.registerCommand({
  name: 'Wyśrodkuj zaznaczone warstwy',
  run() {
    const comp = tfx.app.comp();
    for (const L of tfx.app.selectedLayers())
      tfx.app.setValue(L.tr.position, [comp.w / 2, comp.h / 2, 0], L);
    tfx.app.commit('Wyśrodkuj');
  }
});
```

### 3. Ustawienia wstępne (panel Efekty i ustawienia wstępne → Wtyczki)

```js
tfx.registerPreset({ name: 'Wjazd z góry', apply(layer, time, comp) {
  const lt = time - layer.start;
  layer.tr.position.k = [{ t: lt, v: [comp.w / 2, -200, 0], e: 'ease' }, { t: lt + 1, v: [comp.w / 2, comp.h / 2, 0], e: 'ease' }];
} });
```

### 4. Własne panele

```js
tfx.registerPanel({ title: 'Mój panel', render(el) {
  const { h } = tfx.app;
  el.append(h('button', { class: 'btn small', onclick: () => tfx.app.toast('Hej!') }, 'Kliknij'));
} });
```

### 5. Funkcje wyrażeń

```js
tfx.registerExpressionFunction('bounce', (t, f = 2) => Math.abs(Math.sin(t * f * Math.PI)));
// w wyrażeniu: s = 100 + bounce(time) * 20; [s, s, 100]
```

## tfx.app

| Funkcja | Opis |
|---|---|
| `comp()`, `project()`, `layers()`, `selectedLayers()` | dostęp do projektu |
| `time()`, `setTime(t)` | bieżący czas |
| `addLayer(type, opts)` | `'text'`, `'shape'`, `'solid'`, `'null'`, `'camera'`, `'light'` |
| `newShapeItem(kind)`, `newAnimator()`, `newMask(path)`, `newEffect(id)` | nowe elementy |
| `setValue(prop, value, layer)` | ustawia wartość (tworzy klatkę, gdy właściwość jest animowana) |
| `key(prop, t, value, ease)` | dodaje klatkę kluczową (`ease`: `'linear'`, `'ease'`, `'in'`, `'out'`, `'hold'`) |
| `commit(label)` | zapisuje krok w historii (Cofnij) |
| `toast(msg)`, `alert(msg)`, `prompt(title, value)`, `confirm(msg)` | komunikaty |
| `h(tag, attrs, ...children)` | tworzenie elementów interfejsu |

Właściwości warstwy: `L.tr.anchor`, `L.tr.position`, `L.tr.scale`, `L.tr.rotation`, `L.tr.opacity` (+ `xRot`, `yRot`, `orient` dla 3D).
Każda właściwość to obiekt `{ v: wartość, k: [klatki], x: 'wyrażenie' }`.

> Wtyczki działają z pełnymi uprawnieniami programu. Instaluj tylko wtyczki z zaufanych źródeł.
