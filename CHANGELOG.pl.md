# Informacje o wydaniu

[Instrukcja](README.pl.md) · [English](CHANGELOG.md)

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

Z aplikacji można korzystać bez opłat prywatnie i komercyjnie na zasadach [licencji produktu](LICENSE.txt). Biblioteki zachowują własne licencje; każda paczka zawiera wymagane informacje i archiwum niezmienionych źródeł HCL.

Testy integracyjne VS Code przeszły na Linuksie. Paczki Windows i macOS skompilowano na innym systemie i sprawdzono ich zawartość; tego wydania nie uruchamiano na tych platformach.
