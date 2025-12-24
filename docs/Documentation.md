# Documentation – szczegółowy opis kodu narzędzi Wrath & Glory

## 1. Przegląd architektury
Aplikacja to zestaw **statycznych plików HTML i CSS**, bez backendu i bez procesu budowania. Cała logika działa **po stronie przeglądarki** w skryptach wbudowanych w HTML. Pliki korzystają z opcjonalnych fontów Google Fonts (z fallbackami), ale działają również offline.

Najważniejsze elementy:
- `index.html` – strona startowa z przyciskami do narzędzi.
- `KalkulatorXP.html` – kalkulator kosztów XP (atrybuty i umiejętności).
- `TworzeniePostaci.html` – arkusz planowania postaci z pulą XP, tabelami i walidacjami.
- `kalkulatorxp.css` – wspólny arkusz stylów dla dwóch narzędzi.
- `style.css` – starszy arkusz (nieużywany).

## 2. Opis plików
### 2.1 `index.html`
**Cel:** wejściowa strona nawigacyjna.

**Struktura:**
- `<style>` w nagłówku zawiera cały CSS dla strony.
- `<main>` z logo (`Skull.png`) oraz dwoma przyciskami prowadzącymi do narzędzi.

**Kluczowe elementy:**
- `.logo` – wyświetla grafikę logo.
- `.btn` – przyciski (linki) do `KalkulatorXP.html` i `TworzeniePostaci.html`.

**Logika:** brak JavaScript – strona jest czysto statyczna.

---

### 2.2 `KalkulatorXP.html`
**Cel:** obliczanie kosztu XP dla atrybutów i umiejętności na podstawie wartości aktualnej i docelowej.

**Struktura HTML:**
- Nagłówek `.topbar` z tytułem i przyciskiem **Resetuj wartości**.
- Panel boczny `.panel` z instrukcjami i polem sumy XP.
- Sekcja `.workspace` z dwiema tabelami: **Atrybuty** i **Umiejętności**.

**Wejścia użytkownika:**
- `input.current` i `input.target` – wartości aktualne i docelowe.
- Walidacja przez `min`/`max` w HTML i dodatkowo przez skrypt (`clampValue`).

**Logika JavaScript (wbudowana w plik):**
1. **Słowniki kosztów**
   - `attributeCosts` – mapa kosztów atrybutów dla wartości `0–12`.
   - `skillCosts` – mapa kosztów umiejętności dla wartości `0–8`.
2. **Funkcje pomocnicze**
   - `clampValue(value, min, max)` – zamienia wejście na liczbę i ogranicza zakres.
   - `calculateRowCost(current, target, costs)` – zwraca różnicę kosztów między wartością docelową i aktualną.
3. **Przeliczanie**
   - `recalcTable(tableId, costs, min, max)` – przechodzi po wierszach tabeli, waliduje wartości i sumuje koszt.
   - `recalcAll()` – sumuje koszty atrybutów i umiejętności i aktualizuje `#totalXp`.
4. **Zdarzenia**
   - `input` i `change` na polach w tabelach wywołują `recalcAll()`.
   - Kliknięcie `#btnReset` ustawia wszystkie pola na `0` i przelicza sumę.

**Uwagi implementacyjne:**
- Kalkulator nie zapisuje danych (brak localStorage).
- Skrypt sam odczytuje wszystkie wiersze tabeli, więc można je dodawać bez modyfikacji JS.

---

### 2.3 `TworzeniePostaci.html`
**Cel:** arkusz planowania postaci i kontroli wydatków XP z obsługą dwóch języków.

**Struktura HTML:**
- `.wrapper` – główny kontener.
- `.language-switcher` – przełącznik języka PL/EN.
- Sekcje:
  - **Pula XP** (`#xpPool`) i pozostałe XP (`#xpRemaining`).
  - **Atrybuty** – tabela z 7 polami.
  - **Umiejętności** – tabela z 18 polami (2 kolumny × 9 wierszy).
  - **Talenty…** – tabela 10 wierszy z nazwą i kosztem.
- `.error-message` – miejsce na komunikaty o błędach.

**Logika JavaScript (wbudowana w plik):**
1. **`translations`** – obiekt z tłumaczeniami (PL i EN):
   - etykiety, nagłówki, nazwy atrybutów i umiejętności,
   - komunikaty błędów,
   - podpis stopki.
2. **`updateLanguage(lang)`**
   - Ustawia teksty na stronie zgodnie z wybranym językiem.
   - Aktualizuje podpisy tabel i elementów UI.
3. **`resetAll()`**
   - Przywraca domyślne wartości pól: XP=100, atrybuty=1, umiejętności=0, talenty=0.
   - Wywołuje `recalcXP()`.
4. **`recalcXP()`**
   - Pobiera pulę XP (`#xpPool`) i waliduje zakresy.
   - Sumuje koszty atrybutów (`attributeCosts`), umiejętności (`skillCosts`) i kosztów talentów.
   - Aktualizuje `#xpRemaining`.
   - Jeśli XP < 0 → wyświetla komunikat o przekroczeniu puli.
   - Jeśli XP ≥ 0 → uruchamia `checkSkillTree()`.
   - Dodatkowo: oznacza atrybuty > 8 klasą `attribute-high` (obecnie brak stylu w CSS – klasa jest przygotowana, ale nieużywana).
5. **`displayError(msg)`**
   - Wstawia komunikat do `#errorMessage`.
6. **`checkSkillTree()`**
   - Zlicza liczbę aktywnych umiejętności (wartość > 0).
   - Sprawdza zasadę „Drzewa Nauki”: jeśli poziom umiejętności > 1, liczba aktywnych umiejętności musi być ≥ poziomowi.
   - W razie naruszenia pokazuje odpowiedni komunikat.
7. **`attachDefaultOnBlur(selector, defaultValue)`**
   - Ustawia wartości domyślne po utracie fokusu, gdy pole jest puste lub niepoprawne.
8. **`adjustTalentFontSize(el)`**
   - Zmniejsza czcionkę w polach tekstowych talentów, aby zmieścić dłuższy tekst.
9. **Obsługa zdarzeń**
   - `change` na `#languageSelect` → ostrzeżenie o resecie danych → `updateLanguage` + `resetAll`.
   - `input`/`change` na wszystkich polach → `recalcXP()`.
   - `input` na polach talentów → `adjustTalentFontSize()`.

**Uwagi implementacyjne:**
- Liczba wierszy umiejętności i talentów jest „na sztywno” zakodowana w pętlach (`1..9`, `1..10`). Jeśli dodajesz wiersze w HTML, musisz zaktualizować te pętle.
- Zmiana języka zawsze resetuje dane (świadomy mechanizm ochrony przed niespójnością tłumaczeń).

---

### 2.4 `kalkulatorxp.css`
**Cel:** wspólna warstwa stylistyczna dla `KalkulatorXP.html` i `TworzeniePostaci.html`.

**Najważniejsze elementy:**
- Zmienne CSS w `:root` – paleta kolorów, cienie, gradienty, wysokości wierszy.
- Style komponentów wspólnych: przyciski, nagłówki, tabele, panele.
- Układ responsywny: media query `@media (max-width: 980px)` składa layout w jedną kolumnę.

**Uwagi:**
- Klasa `.attribute-high` nie jest zdefiniowana – jeśli chcesz wyróżniać wysokie wartości atrybutów, dodaj regułę w tym pliku.

---

### 2.5 `style.css`
**Cel:** starszy arkusz stylów, obecnie **nieużywany** przez aktywne strony.

**Uwagi:**
- W przeszłości odpowiadał za wygląd arkusza postaci.
- Można go usunąć, jeśli nie jest potrzebny jako referencja historyczna.

---

### 2.6 `Old/`
**Cel:** archiwum poprzedniej wersji narzędzia.

Zawartość:
- `HowToUse_Org.pdf` – pierwotne materiały instruktażowe.
- `Kalkulator_Org.html` – wcześniejsza wersja kalkulatora.

## 3. Logika danych i aktualizacja wartości
### 3.1 Koszty XP
- `KalkulatorXP.html` i `TworzeniePostaci.html` mają **oddzielne** słowniki kosztów (`attributeCosts`, `skillCosts`).
- Zmiana wartości w jednym pliku **nie wpływa** na drugi – należy je aktualizować w obu, jeśli mają być spójne.

### 3.2 Domyślne wartości
- `KalkulatorXP.html` startuje od `0` dla każdego pola.
- `TworzeniePostaci.html` startuje od `100` XP, atrybutów `1` i umiejętności/talentów `0`.

### 3.3 Walidacja
- HTML wymusza zakresy przez atrybuty `min`/`max`.
- JavaScript dodatkowo **koryguje** dane (np. `clampValue` w kalkulatorze XP).

## 4. Przykładowe punkty rozszerzeń
- **Dodanie nowych sekcji**: kopiowanie istniejących bloków tabel w HTML + aktualizacja logiki JS.
- **Zmiana języków**: dodanie nowej sekcji w `translations` oraz mapowanie etykiet.
- **Wyróżnienie wysokich wartości**: styl `.attribute-high` w `kalkulatorxp.css`.
