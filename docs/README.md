# Kalkulator Wrath & Glory – przegląd użytkowy

Ten projekt to zbiór statycznych stron HTML do obliczania kosztów rozwoju postaci oraz szybkiego planowania atrybutów i umiejętności w systemie **Wrath & Glory**. Wszystko działa lokalnie w przeglądarce – nie wymaga serwera ani dodatkowych bibliotek.

## Jak korzystać z aplikacji
1. Otwórz `index.html` bezpośrednio w przeglądarce (dwuklik lub przeciągnięcie pliku do okna przeglądarki).
2. Z ekranu startowego wybierz odpowiednią stronę narzędzia:
   - **KalkulatorXP.html** – liczy koszt rozwoju atrybutów i umiejętności na podstawie wartości początkowych oraz docelowych.
   - **TworzeniePostaci.html** – arkusz do spisywania kluczowych elementów postaci i planowania wydatków XP.
3. Strony korzystają z lokalnego CSS (`kalkulatorxp.css`) i wbudowanych skryptów, więc działają offline (fonty z Google Fonts mają własny fallback).

> ℹ️ **Uwaga dotycząca urządzeń mobilnych**
> 
> Autodopasowanie pól w `TworzeniePostaci.html` pogarsza wygląd arkusza w pionowej orientacji ekranów mobilnych. Korzystanie z tej strony w takim układzie nie jest zalecane – aplikację najlepiej otwierać na komputerze PC.

## Aktualizowanie danych i dostosowywanie narzędzi
- **Zmiana limitów lub tabel**: edytuj odpowiednie tabele w plikach HTML; logika przeliczeń jest osadzona w samych stronach, więc korekty kolumn/wierszy można robić bez dodatkowych zależności.
- **Dodawanie nowych sekcji**: kopiuj istniejące bloki formularzy w `KalkulatorXP.html` lub `TworzeniePostaci.html`, pamiętając o zachowaniu klas i identyfikatorów używanych przez skrypty.
- **Styl wizualny**: modyfikacje kolorów, czcionek lub siatki układu wykonuj w `kalkulatorxp.css`, co automatycznie odświeży wygląd `KalkulatorXP.html` i `TworzeniePostaci.html`.

## Struktura katalogów
```
.
├── docs/
│   ├── README.md            # instrukcje użytkowe (ten plik)
│   └── Documentation.md     # szczegółowy opis kodu i logiki
├── Old/                     # materiały źródłowe poprzedniej wersji
│   ├── HowToUse_Org.pdf
│   └── Kalkulator_Org.html
├── index.html               # strona startowa ze stylami inline
├── KalkulatorXP.html        # kalkulator wydatków XP
├── TworzeniePostaci.html    # arkusz tworzenia postaci
├── kalkulatorxp.css         # główny arkusz stylów dla obu narzędzi
└── style.css                # poprzednia wersja stylu (archiwum)
```
