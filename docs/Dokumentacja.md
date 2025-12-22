# Dokumentacja narzędzi Wrath & Glory

## Cel projektu
Zestaw stron HTML umożliwia szybkie liczenie kosztów rozwoju postaci oraz przygotowanie arkusza startowego bez konieczności instalowania dodatkowych aplikacji. Wszystkie dane są przetwarzane lokalnie w przeglądarce.

## Strony w projekcie
- **index.html** – ekran powitalny z odnośnikami do kalkulatora XP i kreatora postaci.
- **KalkulatorXP.html** – oblicza koszt rozwoju atrybutów i umiejętności na podstawie wprowadzonych wartości początkowych i docelowych.
- **TworzeniePostaci.html** – arkusz pozwalający spisać kluczowe informacje o postaci (atrybuty, talenty, uzbrojenie itp.).

## Instrukcja korzystania z Kalkulatora XP
1. W tabeli **Atrybuty** podaj bieżącą i docelową wartość każdego atrybutu. Kolumna „Koszt XP” pokaże koszt jednorazowy dla danego wpisu, a pod tabelą znajdziesz sumę wydatków.
2. Analogicznie uzupełnij sekcję **Umiejętności**, aby wyliczyć koszt rozwoju poszczególnych skilli.
3. Wszystkie limity (0–12) są walidowane przez pola formularzy, co pomaga uniknąć błędnych wpisów.

## Instrukcja korzystania z arkusza tworzenia postaci
1. Otwórz plik **TworzeniePostaci.html** i wprowadź podstawowe dane (imię, frakcja, świat pochodzenia).
2. Uzupełnij sekcje atrybutów i umiejętności, a następnie talenty, wyposażenie i notatki.
3. Wartości liczbowych można używać do szybkiego planowania wydatków, zanim zostaną wprowadzone do kalkulatora XP.

## Koszty rozwoju atrybutów
Poniższa tabela zawiera oficjalne koszty rozwoju atrybutów w punktach doświadczenia, wraz z narastającym kosztem do danej wartości.

| Wartość atrybutu | Całkowity koszt XP | Narastający koszt XP |
| --- | --- | --- |
| 1 | 0 | 0 |
| 2 | 4 | 4 |
| 3 | 10 | 6 |
| 4 | 20 | 10 |
| 5 | 35 | 15 |
| 6 | 55 | 20 |
| 7 | 80 | 25 |
| 8 | 110 | 30 |
| 9 | 145 | 35 |
| 10 | 185 | 40 |
| 11 | 230 | 45 |
| 12 | 280 | 50 |

## Wskazówki projektowe
- Warstwa wizualna oparta jest na pliku `style.css` i wykorzystuje neonową kolorystykę podkreślającą futurystyczny klimat Wrath & Glory.
- Możesz swobodnie dostosować tabele (dodanie wierszy, zmiana limitów), ponieważ logika obliczeń jest osadzona w skryptach HTML.
- Narzędzia działają offline, więc są odporne na brak połączenia internetowego podczas sesji.
