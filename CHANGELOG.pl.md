# Informacje o wydaniu

[Instrukcja](https://github.com/bryn1u/live-values-results-for-terraform/blob/main/README.pl.md) · [English](https://github.com/bryn1u/live-values-results-for-terraform/blob/main/CHANGELOG.md)

## 0.0.15 — 24 września 2026

- Dodano odtwarzacze filmów po angielsku i po polsku bezpośrednio do opisu rozszerzenia, z przyciskami odtwarzania i miniaturami.
- Dołączono nową nazwę Terraform Live Values & Results oraz ikonę. Instalacje Marketplace są aktualizowane pod tym samym ID `bryn1u.valuescope-iac`.

Filmy prowadzą od prostych przykładów do bardziej złożonych konfiguracji i pokazują wersję 0.0.11 pod poprzednią nazwą. Sposób obliczania wyników pozostaje taki jak w 0.0.13.

## 0.0.14 — 24 września 2026

- Zmieniono nazwę na **Terraform Live Values & Results** i dodano ikonę rozszerzenia.
- Zaktualizowano nazwę w panelu wyników, poleceniach i dokumentacji PL/EN.
- Zachowano identyfikator `bryn1u.valuescope-iac`, ustawienia i zapisane wybory. Instalacje z Marketplace otrzymują zwykłą aktualizację.

Sposób obliczania wyników pozostaje taki jak w 0.0.13.

## 0.0.13 — 24 września 2026

- Wydanie dla Marketplace pod identyfikatorem `bryn1u.valuescope-iac`. Nazwa wtyczki i ustawienia `valuescope.*` pozostają bez zmian.
- Dodano publiczne adresy dokumentacji i zgłoszeń oraz odnośniki do filmów PL/EN.
- Przebudowano paczki dla Linux x64, Windows x64, macOS ARM64 i macOS x64.

Starszą lokalną instalację `valuescope.valuescope-iac` należy wyłączyć lub odinstalować, aby uniknąć dwóch aktywnych kopii.

## 0.0.12 — 24 września 2026

To pierwsze publiczne wydanie w tym repozytorium.

- Podgląd zmiennych, locals, obsługiwanych wyrażeń, argumentów konfiguracji zasobów i outputów lokalnych modułów w VS Code.
- Podgląd deklaracji zmiennej przez nagłówek, ograniczenie typu lub zaznaczenie całego bloku pokazuje wartość dla bieżących danych wejściowych. Wyrażenia wewnątrz `default` można sprawdzać osobno.
- Interfejs po polsku i angielsku oraz wybór danych wejściowych przez pliki tfvars lub profile.
- Paczki dla Linux x64, Windows x64 oraz macOS z procesorem Apple Silicon lub Intel. Każda zawiera silnik obliczeń.

Z aplikacji można korzystać bez opłat prywatnie i komercyjnie na zasadach [licencji produktu](https://github.com/bryn1u/live-values-results-for-terraform/blob/main/LICENSE.txt). Biblioteki zachowują własne licencje; każda paczka zawiera wymagane informacje i archiwum niezmienionych źródeł HCL.

Testy integracyjne VS Code przeszły na Linuksie. Paczki Windows i macOS skompilowano na innym systemie i sprawdzono ich zawartość; tego wydania nie uruchamiano na tych platformach.
