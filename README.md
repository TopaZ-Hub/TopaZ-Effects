<p align="center">
  <img src="logo.png" width="128" alt="TopaZ Effects 26">
</p>

<h1 align="center">TopaZ Effects 26</h1>

<p align="center">
  Animacja, compositing i efekty wizualne dla Windows, w stylu After Effects.<br>
  <b>Windows 10 / 11 (64-bit)</b> · wersja <b>26.1</b>
</p>

<p align="center">
  <a href="https://github.com/TopaZ-Hub/TopaZ-HUB"><b>⬇️ Zainstaluj przez TopaZ Creative Hub (zalecane)</b></a>
  &nbsp;·&nbsp;
  <a href="https://github.com/TopaZ-Hub/TopaZ-Editing-Pro/releases/tag/TFX-26.1">Pobierz instalator bezpośrednio</a>
</p>

---

## ✨ Co potrafi

**Kompozycje i warstwy**
- Kompozycje i prekompozycje (Ctrl+Shift+C), od 720p do 8K, 23,976–120 kl./s.
- Warstwy: wideo, obraz, audio, tekst, kształt, jednolity kolor, null, kamera, światło, korekcyjna.
- Rodzice warstw z pickwhipem, tryby mieszania, track matte (alfa i luminancja), warstwy nieśmiałe, solo.

**Animacja**
- Klatki kluczowe dla każdej właściwości: łagodne przejście (F9), wejście, wyjście, wstrzymanie.
- Ścieżka ruchu widoczna w podglądzie.
- **Wyrażenia** w JavaScript jak w After Effects: `wiggle()`, `loopOut()`, `linear()`, `ease()`, `valueAtTime()`, `thisComp.layer(…)`.
- Skróty P, S, R, T, A, U pokazują wybrane właściwości na osi czasu.

**Tekst i kształty**
- Animatory tekstu litera po literze: położenie, skala, obrót, krycie, kolor, rozmycie, odstępy.
- Kształty: prostokąt, elipsa, gwiazda, wielokąt, ścieżka piórem.
- Wypełnienie, obrys, **przycinanie ścieżek** (efekt „rysowania” linii) i **powielacz**.

**3D, maski i efekty**
- Warstwy 3D z kamerą, punktem zainteresowania i światłami (punktowe, reflektor, równoległe, otoczenia).
- Rozmycie ruchu.
- Maski rysowane piórem albo prostokątem i elipsą, z wtapianiem, rozszerzeniem i trybami.
- **90+ efektów GPU** (rozmycia, poświata, glitch, VHS, green screen, zniekształcenia, korekcja kolorów) i ustawienia wstępne animacji.

**Szybki podgląd i render**
- Cały obraz liczy się na karcie graficznej (WebGL 2).
- **Podgląd RAM** jak w After Effects: pierwsze odtworzenie zapisuje klatki (zielony pasek), kolejne pętle grają płynnie w czasie rzeczywistym.
- **Kolejka renderowania** (Ctrl+M) z kodowaniem na karcie graficznej (AMD AMF, NVIDIA NVENC, Intel Quick Sync):
  - MP4 H.264, H.265 i AV1, do 8K;
  - sekwencja PNG z przezroczystością;
  - WAV.

## 🔗 Dynamic Link z TopaZ Editing Pro

TopaZ Effects współpracuje z [TopaZ Editing Pro](https://github.com/TopaZ-Hub/TopaZ-Editing-Pro) od wersji 26.2:

- W Editing kliknij prawym przyciskiem klip → **„Zastąp kompozycją TopaZ Effects”**. Klip otworzy się tutaj jako kompozycja.
- Po zapisaniu w Effects (Ctrl+S) zmiany **same pojawią się w Editing**, bez renderowania pliku pośredniego.
- W Editing: **Plik → Importuj kompozycję TopaZ Effects…** dodaje dowolną kompozycję z pliku `.tzfx`.

## 🧩 Wtyczki

W prawej kolumnie jest zakładka **Wtyczki**. Przycisk **„+ Nowa wtyczka”** tworzy gotowy szablon. Wtyczka może dodać:

- **efekt GPU**, czyli krótki shader GLSL;
- **polecenie** w menu Wtyczki;
- **ustawienie wstępne animacji**;
- **własny panel**;
- **funkcję do wyrażeń**.

Program ma 3 przykładowe wtyczki: **Neon Pro** (efekty), **Narzędzia animatora** (polecenia) i **Licznik i zegar** (panel).

Wtyczki trzymasz w `Dokumenty\TopaZ Effects\Plugins`. Pełna instrukcja jest w pliku **[PLUGINS.md](PLUGINS.md)**.

> Wtyczki działają z pełnymi uprawnieniami programu. Instaluj tylko wtyczki z zaufanych źródeł.

## 📥 Instalacja

### Sposób 1: przez TopaZ Creative Hub (zalecany)
1. Pobierz Hub z repozytorium **[TopaZ-HUB](https://github.com/TopaZ-Hub/TopaZ-HUB)**.
2. W Hubie kliknij **„Zainstaluj”** przy TopaZ Effects 26.

Hub sam będzie informował o nowych wersjach.

### Sposób 2: ręcznie
Pobierz `TopaZ_Effects_26.1_Setup.exe` z **[wydania TFX-26.1](https://github.com/TopaZ-Hub/TopaZ-Editing-Pro/releases/tag/TFX-26.1)** i uruchom go.

## ⚠️ Czerwone okno „System Windows ochronił ten komputer”

To okno **nie oznacza, że wykryto wirusa**. Pojawia się, bo:
- program **nie ma płatnego certyfikatu podpisu cyfrowego** (stąd „Nieznany wydawca”). Taki certyfikat kosztuje kilkaset złotych rocznie, a TopaZ to mały, niezależny projekt;
- plik jest **nowy i pobrało go jeszcze niewiele osób**.

Kliknij **„Więcej informacji” → „Uruchom mimo to”**.

### Sprawdź sam

1. **VirusTotal**: wrzuć instalator na [virustotal.com](https://www.virustotal.com). Sprawdzi go ponad 60 antywirusów naraz.
2. **Suma kontrolna**: w PowerShellu wpisz:

   ```powershell
   Get-FileHash .\TopaZ_Effects_26.1_Setup.exe -Algorithm SHA256
   ```

   Wynik musi być taki sam jak ten:

   ```
   DA797829500567490449BC77B852660DF9CCF9D80F83DC72BCF45F5187303879
   ```

**Prywatność:** program działa w całości na Twoim komputerze. Twoje filmy i projekty nigdy nie są wysyłane do internetu, nie ma reklam ani zbierania danych.

## 💻 Wymagania

| | Minimalne | Zalecane |
|---|---|---|
| System | Windows 10 64-bit | Windows 11 64-bit |
| Procesor | 4 rdzenie | 6+ rdzeni (np. Ryzen 5 5600X) |
| RAM | 8 GB | 16 GB+ (więcej = dłuższy podgląd RAM) |
| Karta graficzna | zgodna z DirectX 11 | AMD RX 6000 / NVIDIA RTX / Intel Arc |
| Dysk | ok. 300 MB na program | dysk SSD na projekty |

## ⌨️ Najważniejsze skróty

| Skrót | Działanie |
|---|---|
| Spacja | Podgląd RAM |
| Ctrl+N / Ctrl+K | Nowa kompozycja / ustawienia kompozycji |
| V W Y G Q / Ctrl+T | Zaznaczanie, obrót, punkt zaczepienia, pióro, kształty / tekst |
| P S R T A U | Położenie, skala, obrót, krycie, punkt zaczepienia, animowane |
| Alt+Shift+P/S/R/T | Dodaj klatkę kluczową |
| F9 | Łagodne przejście klatek |
| Alt+klik na stoperze | Wyrażenie |
| Ctrl+Y / Ctrl+Alt+Y | Jednolity kolor / warstwa korekcyjna |
| Ctrl+D / Ctrl+Shift+D | Duplikuj / podziel warstwę |
| Ctrl+M | Dodaj do kolejki renderowania |
| Ctrl+, | Preferencje (GPU/CPU, RAM, pamięć podglądu) |

## 🚧 Czego jeszcze nie ma

TopaZ Effects to pierwsza wersja. Względem After Effects brakuje na razie:
- edytora wykresów prędkości, śledzenia ruchu i narzędzia Puppet;
- przecinania się warstw 3D (warstwy są układane od najdalszej do najbliższej);
- cieni rzucanych przez światła.

Te funkcje są w planach na kolejne wersje.

## 🐞 Zgłaszanie błędów

Coś nie działa? Załóż zgłoszenie w zakładce **Issues**. Napisz:
- co robiłeś, gdy pojawił się błąd;
- jaką masz kartę graficzną.

Zrzut ekranu i plik projektu `.tzfx` bardzo pomagają.

---

<p align="center"><sub>© 2026 TopaZ · Projekt niezależny, niezwiązany z Adobe.</sub></p>
