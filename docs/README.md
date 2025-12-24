# Kalkulator Wrath & Glory – instrukcja użytkownika

Ten projekt to zestaw statycznych stron HTML do planowania rozwoju postaci w systemie **Wrath & Glory**. Aplikacja działa w całości lokalnie w przeglądarce, bez serwera i bez instalacji bibliotek. Wystarczy otworzyć pliki HTML.

## Jak uruchomić aplikację
1. Otwórz `index.html` w przeglądarce (dwuklik lub przeciągnięcie pliku do okna przeglądarki).
2. Z ekranu startowego wybierz narzędzie:
   - **Kalkulator XP** (`KalkulatorXP.html`) – liczy koszt rozwoju atrybutów i umiejętności na podstawie wartości aktualnych i docelowych.
   - **Tworzenie Postaci** (`TworzeniePostaci.html`) – arkusz planowania postaci z pulą XP, tabelą atrybutów, listą umiejętności oraz kosztami talentów i innych elementów.

> ℹ️ **Uwaga dotycząca urządzeń mobilnych**
>
> Autodopasowanie pól w `TworzeniePostaci.html` pogarsza wygląd arkusza w pionowej orientacji ekranów mobilnych. Aplikację najlepiej otwierać na komputerze.

## Jak korzystać z narzędzi
### Kalkulator XP
1. Wpisz aktualną oraz docelową wartość w kolumnach tabel **Atrybuty** i **Umiejętności**.
2. Koszt XP w każdym wierszu oraz suma całkowita aktualizują się automatycznie.
3. Przycisk **Resetuj wartości** czyści wszystkie pola (ustawia je na `0`).

### Tworzenie Postaci
1. Ustaw **pulę XP do wydania**.
2. Wypełnij atrybuty i umiejętności – koszt oblicza się automatycznie.
3. Dodaj koszty talentów, mocy, archetypów lub innych elementów w tabeli **Talenty…**.
4. Aplikacja sygnalizuje:
   - przekroczenie puli XP,
   - złamanie zasady „Drzewa Nauki” (wymóg liczby aktywnych umiejętności względem ich poziomu).
5. Przełącznik języka (PL/EN) resetuje wszystkie dane po potwierdzeniu.

## Aktualizowanie aplikacji (dla użytkownika)
Aplikacja jest statyczna – „aktualizacja” oznacza podmianę plików lub ręczną edycję HTML/CSS.

### Aktualizacja plików
- Pobierz najnowszą wersję plików i **zamień** stare `index.html`, `KalkulatorXP.html`, `TworzeniePostaci.html` oraz `kalkulatorxp.css` na nowe.
- Jeśli trzymasz własne zmiany (np. inne tabele), zrób kopię i przenieś je do nowej wersji.

### Dostosowanie działania
- **Zmiana kosztów XP**:
  - `KalkulatorXP.html` → sekcja `<script>`: obiekty `attributeCosts` i `skillCosts`.
  - `TworzeniePostaci.html` → sekcja `<script>`: obiekty `attributeCosts` i `skillCosts`.
- **Zmiana liczby wierszy w tabelach**:
  - `KalkulatorXP.html` – możesz dodać wiersze w tabelach, skrypt sam odczytuje wszystkie wiersze.
  - `TworzeniePostaci.html` – po dodaniu nowych wierszy musisz zaktualizować listy/zakresy w skrypcie (pętle `for` używające liczby `9` dla umiejętności i `10` dla talentów).
- **Zmiana wyglądu**:
  - `kalkulatorxp.css` odpowiada za styl `KalkulatorXP.html` i `TworzeniePostaci.html`.
  - `index.html` ma wbudowany CSS w sekcji `<style>`.

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
└── style.css                # starszy arkusz stylów (nieużywany)
```

## Disclaimer
To narzędzie jest nieoficjalnym, fanowskim projektem stworzonym jako pomoc dla MG w systemie Wrath & Glory. Aplikacja jest udostępniana za darmo wyłącznie do prywatnego, niekomercyjnego użytku. Projekt nie jest licencjonowany, nie jest powiązany ani wspierany przez Games Workshop, Cubicle 7 Entertainment Ltd. ani Copernicus Corporation.
Warhammer 40,000 oraz powiązane nazwy i znaki towarowe są własnością Games Workshop Limited; Wrath & Glory jest własnością odpowiednich właścicieli praw.
