# Terraform Live Values & Results

<img src="https://github.com/bryn1u/live-values-results-for-terraform/raw/refs/heads/main/media/icon.png" alt="Terraform Live Values &amp; Results" width="96" height="96">

[English](https://github.com/bryn1u/live-values-results-for-terraform/blob/main/README.md) · [Historia wersji](https://github.com/bryn1u/live-values-results-for-terraform/blob/main/CHANGELOG.pl.md)

Sprawdź, jakie wartości daje Twój kod Terraform, bezpośrednio podczas pisania. Zaznacz wyrażenie albo ustaw w nim kursor, żeby zobaczyć wynik w VS Code. Podgląd uwzględnia również niezapisane zmiany.

Możesz sprawdzać zmienne, locals, wywołania funkcji, przekształcenia kolekcji, outputy lokalnych modułów i argumenty zasobów. Wtyczka oblicza je na podstawie kodu oraz wybranych danych wejściowych. Pozwala sprawdzić filtr `for`, prześledzić wartość przez moduły albo obejrzeć argumenty instancji `for_each` bez dopisywania pomocniczego outputu i uruchamiania planu.

Bieżąca wersja: **0.0.15**. Identyfikator rozszerzenia to `bryn1u.valuescope-iac`, a ustawienia mają prefiks `valuescope.*`.

Wcześniejsza nazwa to **Live Values & Results for Terraform**. Wersja 0.0.15 zmienia nazwę i ikonę; identyfikator rozszerzenia, ustawienia i zapisane wybory pozostają takie same.

Autor: **Michal 'bryn1u' Bryniarski** · [michal.bryniarski@gmail.com](mailto:michal.bryniarski@gmail.com).

Jeśli masz starszą lokalną wersję `valuescope.valuescope-iac`, wyłącz ją lub odinstaluj przed użyciem wydania Marketplace. Nowy identyfikator oznacza osobną instalację. Ustawienia `valuescope.*` pozostają zgodne, ale lokalne wybory i sekrety zapisane przez poprzednie rozszerzenie nie są przenoszone automatycznie.

## Pierwszy podgląd

1. Zainstaluj [Terraform Live Values & Results](https://marketplace.visualstudio.com/items?itemName=bryn1u.valuescope-iac) od wydawcy **bryn1u** w panelu rozszerzeń VS Code. Lokalną paczkę możesz zainstalować przez **Extensions: Install from VSIX…**.
2. Otwórz folder z konfiguracją Terraform.
3. Jeśli dane wejściowe znajdują się np. w `environment/prod.tfvars`, wybierz ten plik przyciskiem **Plik .tfvars** w panelu wyników.
4. Ustaw kursor w wyrażeniu i naciśnij **Ctrl+Alt+V** (**Cmd+Alt+V** na macOS). Możesz też zaznaczyć wyrażenie, najechać na nie myszą albo kliknąć **Podgląd** nad obsługiwanym blokiem.

Panel podąża za wskazanym fragmentem kodu. Przypnij wynik, jeśli chcesz nadal oglądać to samo źródło podczas poruszania się po pliku. Możesz zmienić szerokość panelu, włączyć zawijanie i skopiować wyświetloną wartość.

Paczka zawiera silnik obliczeń. Do używania wtyczki wystarczy VS Code 1.90 lub nowszy; Go, Node.js i Terraform CLI nie są potrzebne. Dobierz paczkę do systemu i architektury uruchomionego VS Code.

| System / architektura VS Code | Paczka |
|---|---|
| Linux x64 | [valuescope-iac-0.0.15-linux-x64.vsix](https://github.com/bryn1u/live-values-results-for-terraform/releases/download/v0.0.15/valuescope-iac-0.0.15-linux-x64.vsix) |
| Windows x64 | [valuescope-iac-0.0.15-win32-x64.vsix](https://github.com/bryn1u/live-values-results-for-terraform/releases/download/v0.0.15/valuescope-iac-0.0.15-win32-x64.vsix) |
| macOS Apple Silicon (ARM64) | [valuescope-iac-0.0.15-darwin-arm64.vsix](https://github.com/bryn1u/live-values-results-for-terraform/releases/download/v0.0.15/valuescope-iac-0.0.15-darwin-arm64.vsix) |
| macOS Intel (x64) | [valuescope-iac-0.0.15-darwin-x64.vsix](https://github.com/bryn1u/live-values-results-for-terraform/releases/download/v0.0.15/valuescope-iac-0.0.15-darwin-x64.vsix) |

[Sumy SHA-256](https://github.com/bryn1u/live-values-results-for-terraform/releases/download/v0.0.15/SHA256SUMS.txt).

VS Code dobiera wariant Marketplace do systemu i architektury. macOS wymaga wersji 13 lub nowszej.

Wszystkie cztery paczki zawierają poprawkę podglądu deklaracji zmiennych. Wersja 0.0.15 przeszła testy integracyjne VS Code na Linuksie. Paczki Windows i macOS skompilowano na innym systemie i sprawdzono ich zawartość; tego wydania nie uruchamiano na tych platformach.

**Linux:** wyczerpany limit `inotify` może sprawić, że podgląd nadal pokaże stare wartości po zmianie pliku na dysku. Jeśli limit wynosi 128, na stanowisku z wieloma uruchomionymi aplikacjami warto rozważyć zwiększenie go do 1024. Wyjaśnienie i polecenia znajdziesz w sekcji [Linux: inotify](#linux-inotify).

## Filmy pokazujące działanie

Oba filmy prowadzą od najprostszych przykładów do bardziej złożonych konfiguracji Terraform: od zmiennych i locals, przez funkcje na kolekcjach i instancje zasobów, do outputów modułu. Kółka wskazują kliknięcia, a ramka wyróżnia wynik. Każde nagranie trwa około siedmiu minut, ma podpisy i nie zawiera lektora.

### English

https://github.com/user-attachments/assets/053890a4-5486-4252-838f-b23e8b3d6fce

### Polski

https://github.com/user-attachments/assets/b6d40e2f-8e48-423e-b10a-d1ca584078c4

[Obejrzyj po angielsku](https://github.com/bryn1u/live-values-results-for-terraform/blob/main/demo-video.en.md) · [Opis filmu po polsku](https://github.com/bryn1u/live-values-results-for-terraform/blob/main/demo-video.pl.md)

[Pobierz oryginalny MP4 po polsku](https://github.com/bryn1u/live-values-results-for-terraform/raw/refs/heads/main/media/demo-pl-1080p.mp4) · [Pobierz oryginalny MP4 po angielsku](https://github.com/bryn1u/live-values-results-for-terraform/raw/refs/heads/main/media/demo-en-1080p.mp4)

Nagrania pokazują wersję 0.0.11 pod poprzednią nazwą Live Values & Results for Terraform. To wydanie ma numer 0.0.15.

## Przykład

```hcl
variable "routes" {
  default = {
    internet = { enabled = true,  prefix = "0.0.0.0/0" }
    internal = { enabled = false, prefix = "10.0.0.0/8" }
  }
}

locals {
  enabled_routes = {
    for name, route in var.routes :
    name => route
    if route.enabled
  }
}
```

Podejrzyj `local.enabled_routes`. Wynik zawiera `internet`; filtr usuwa `internal`. Zmień flagę `enabled` i sprawdź wynik ponownie. Kolejne obliczenie użyje bieżącej treści edytora, nawet przed zapisaniem pliku.

Tak samo sprawdzisz obsługiwane wywołania `merge`, `flatten`, `concat` czy `zipmap`. Przy powtarzanych zasobach wybierz instancję, aby zobaczyć jej `each.key`, `each.value` lub `count.index`.

## Co pokazuje podgląd

| Miejsce otwarcia | Zawartość |
|---|---|
| Wyrażenie, zmienna, local lub zaznaczenie | Obliczona wartość, jej typ i nierozstrzygnięte fragmenty |
| Nagłówek bloku resource lub data | Argumenty zapisane w konfiguracji, obliczone dla wybranych wejść i instancji, oraz obsługiwane bloki zagnieżdżone i `dynamic` |
| Nagłówek modułu | Istniejące outputy modułu, w tym skonfigurowane argumenty zasobów przekazywanych przez obsługiwane outputy |

Podgląd zasobu opisuje konfigurację z kodu. Nie obejmuje domyślnych wartości providera, wygenerowanych ID ani rzeczywistego stanu zasobu w chmurze. Nagłówek modułu pokazuje jego istniejące outputy, a nie spis wszystkich zasobów.

W deklaracji `variable` nagłówek, deklaracja `type` i zaznaczenie całego bloku pokazują wartość zmiennej z bieżących wejść oraz kontekstu modułu. Wyrażenie w `default` można sprawdzić osobno; jego wynik może różnić się od wartości nadpisanej przez tfvars.

Jeśli nie da się obliczyć wartości bezpośredniego odwołania, podgląd może wskazać jego cel, np. `<odwołanie: azurerm_route_table.this["management"].id>`. Obok może pojawić się znana lokalnie nazwa, która nie jest oznaczona jako poufna. Dzięki temu widać powiązanie bez przypisywania mu wymyślonego ID.

Wyrażenia używające całego obiektu zasobu nadal wymagają jego pełnej struktury określonej przez providera. Podgląd modułu może więc pokazać argumenty z kodu, chociaż `jsonencode(module.network.whole_resource)` pozostanie niedostępne. Podgląd konfiguracji nie zmienia niepełnego obiektu w pełną wartość Terraform.

## Gdy wynik jest niepełny

| Status | Znaczenie |
|---|---|
| `known` | Wartość opisywana przez ten podgląd jest znana |
| `partial` | Część wartości jest znana, reszta pozostaje nierozstrzygnięta |
| `unknown` | Wartość Terraform nie może być jeszcze znana |
| `unavailable` | Błąd wyrażenia lub ograniczenie wtyczki uniemożliwia obliczenie |

Panel podaje przyczynę i ścieżkę do problemu. Brak zmiennej, niepoprawne wyrażenie i nieobsługiwana funkcja wymagają różnych działań. Bez schematu providera pole może być niedostępne, choć Terraform potrafiłby je obliczyć po uzyskaniu tej informacji. Sama nazwa `id` nie oznacza znanej wartości tekstowej.

Błąd poza zależnościami wskazanego wyrażenia nie powinien blokować wyniku. Duże wartości są skracane i oznaczane jako ucięte; niewidoczne elementy nadal wpływają na status. Jeśli silnik nie potrafi dokładnie prześledzić pochodzenia nieznanej wartości po przekształceniu, wynik o tym informuje.

## Dane wejściowe i kontekst

Wtyczka automatycznie czyta `terraform.tfvars`, `terraform.tfvars.json` oraz uporządkowane pliki `*.auto.tfvars` / `*.auto.tfvars.json` w module głównym. Pozostałe pliki trzeba wybrać jawnie. Zmiana katalogu tfvars zmienia listę wyboru plików, a nie aktywne środowisko. Domyślny katalog to `environment` przy module głównym.

Wybrany plik jest zapamiętywany lokalnie, osobno dla każdego modułu głównego. W zaufanym projekcie możesz jawnie wybrać pojedynczy lokalny plik tfvars spoza projektu. Nie udostępnia to całego jego katalogu ani nie rozszerza dostępu dla `file()` i `templatefile()`.

Profile pozwalają nazwać zestawy danych wejściowych. Przykład:

```json
{
  "valuescope.profiles": [
    {
      "id": "lab",
      "name": "Local lab",
      "varFiles": ["environment/lab.tfvars"],
      "vars": {
        "environment": "lab",
        "zones": "[\"a\", \"b\"]"
      }
    }
  ]
}
```

Kolejność nadpisywania wejść to: wartości domyślne, skonfigurowane `TF_VAR_*`, automatyczne pliki zmiennych, pliki profilu w podanej kolejności i jawne `vars` profilu. Wartości tekstowe wpisuje się jako tekst, a kolekcje w składni HCL. Do chronionych wejść służy **Ustaw wartość sekretu**. W ustawieniach profilu zapisuj tylko nazwy sekretów.

Jeśli moduł jest wywoływany kilka razy, wybierz moduł główny, kontekst modułu i właściwą instancję. Wejścia modułu potomnego są obliczane w kontekście wywołującej go instancji. Podgląd przechodzi przez lokalne moduły; nie pobiera modułów zdalnych.

## Język i współpraca z edytorem

Przyciskiem **Język** wybierzesz polski, angielski albo wybór automatyczny. Ustawienie jest zapamiętywane lokalnie. Bazowa opcja `valuescope.language` przyjmuje `auto`, `en` lub `pl`. Tryb automatyczny wybiera polski dla polskiego VS Code, a w pozostałych przypadkach angielski.

Zmiana języka zachowuje wynik, plik wejściowy i przypięcie. **O rozszerzeniu** otwiera ten opis w wybranym języku. Nazwy poleceń i opisy ustawień zależą od języka samego VS Code; panel może używać innego. Wartości, składnia HCL i surowe diagnostyki silnika pozostają bez zmian.

Wtyczka współpracuje z rozszerzeniem językowym Terraform. Nie zmienia skojarzeń plików, kolorowania ani formatowania. Rozpoznaje pliki `.tf`, `.tfvars`, `.tf.json`, `.tfvars.json` oraz identyfikatory języka Terraform. Za uzupełnianie i kolorowanie składni odpowiada rozszerzenie językowe.

## Pełny katalog zarejestrowanych funkcji

Rejestr zawiera **118 nazw: 97 funkcji z lokalną implementacją, 4 celowo odroczone oraz 17 jawnie nieobsługiwanych**. Nie oznacza to 118 w pełni obsługiwanych funkcji Terraform. Implementacja w testowanym podzbiorze nie gwarantuje pełnej zgodności z każdą wersją Terraform, providerem i każdym możliwym wejściem.

### Lokalnie zaimplementowane: 97

| Kategoria | Funkcje |
|---|---|
| Liczbowe — 9 | `abs`, `ceil`, `floor`, `log`, `max`, `min`, `parseint`, `pow`, `signum` |
| Stringi i wzorce — 21 | `chomp`, `endswith`, `format`, `formatlist`, `indent`, `join`, `lower`, `regex`, `regexall`, `replace`, `split`, `startswith`, `strcontains`, `strrev`, `substr`, `title`, `trim`, `trimprefix`, `trimspace`, `trimsuffix`, `upper` |
| Kolekcje i wybór wartości — 28 | `alltrue`, `anytrue`, `chunklist`, `coalesce`, `coalescelist`, `compact`, `concat`, `contains`, `distinct`, `element`, `flatten`, `index`, `keys`, `length`, `lookup`, `merge`, `one`, `range`, `reverse`, `setintersection`, `setproduct`, `setsubtract`, `setunion`, `slice`, `sort`, `transpose`, `values`, `zipmap` |
| Konwersje typu — 6 | `tobool`, `tolist`, `tomap`, `tonumber`, `toset`, `tostring` |
| Tekst strukturalny — 3 | `csvdecode`, `jsondecode`, `jsonencode` |
| Kodowanie tekstu — 3 | `base64decode`, `base64encode`, `urlencode` |
| Skróty — 6 | `base64sha256`, `base64sha512`, `md5`, `sha1`, `sha256`, `sha512` |
| Jawne wejścia daty/czasu — 2 | `formatdate`, `timeadd` |
| Lokalne pliki i szablony — 10 | `file`, `filebase64`, `filebase64sha256`, `filebase64sha512`, `fileexists`, `filemd5`, `filesha1`, `filesha256`, `filesha512`, `templatefile` |
| Ścieżki — 3 | `abspath`, `basename`, `dirname` |
| Obsługa błędów — 2 | `can`, `try` |
| Sensitive/ephemeral — 4 | `ephemeralasnull`, `issensitive`, `nonsensitive`, `sensitive` |

Ważne zastrzeżenia:

- `try`/`can` odróżniają przechwytywalne błędy dynamiczne od statycznych błędów i ograniczeń narzędzia. Brak schemy lub niezaimplementowana funkcja nie zamieniają się po cichu w udany fallback.
- `file`/`templatefile` wymagają UTF-8; `filebase64` obsługuje dane binarne. Odczyt wymaga zaufanego workspace, dozwolonej ścieżki i pliku do 4 MiB. Funkcje nie zapisują danych.
- Ścieżki względne i `abspath` używają root module jako katalogu bazowego. `path.cwd` opisuje kontekst uruchomienia, ustawiany też w profilu. `path.root`/`path.module` zachowują testowaną względną reprezentację w stylu Terraform.
- `templatefile` korzysta z przekazanych zmiennych i dostępnego rejestru funkcji. Rekurencyjne wywołania szablonu nie są obsługiwane.
- `range` zachowuje limit biblioteki: 1024 elementy. Znany wynik `setproduct` jest ograniczony do 10000 kombinacji.
- Wrappery strukturalne zachowują znane liście i ścieżki pochodzenia tam, gdzie jest to obsługiwane. `formatlist`, `split`, operacje regex/decode, `setproduct` i `templatefile` mogą wymagać jawnego fallbacku przypisania pochodzenia dla nierozstrzygniętych wejść.
- `nonsensitive` nie jest ogólną zgodą na ujawnianie sekretów. Marki deklaracji i maskowanie rozpoznanych formatów credentials nadal obowiązują na granicach prezentacji.

### Celowo odroczone: 4

| Funkcje | Zachowanie |
|---|---|
| `timestamp`, `uuid`, `bcrypt` | Unknown z powodem `impure-function`; bez wymyślania czasu, identyfikatora lub skrótu |
| `plantimestamp` | Unknown z powodem `plan-time`; plan nie jest uruchamiany |

### Jawnie nieobsługiwane: 17

`base64gzip`, `cidrcontains`, `cidrhost`, `cidrnetmask`, `cidrsubnet`, `cidrsubnets`, `fileset`, `matchkeys`, `pathexpand`, `rsadecrypt`, `templatestring`, `textdecodebase64`, `textencodebase64`, `timecmp`, `uuidv5`, `yamldecode`, `yamlencode`.

Zwracają jawne ograniczenie narzędzia. Funkcje zdefiniowane przez providera nie są wykonywane. Niezarejestrowana nazwa nie staje się obsługiwana tylko dlatego, że istnieje w którejś wersji Terraform.

## Polecenia

Identyfikatory nie zależą od języka. Tytuły w palecie podążają za językiem VS Code; poniżej opisano działania.

| Działanie | Identyfikator |
|---|---|
| Otwórz panel wyników | `valuescope.openPanel` |
| Oblicz wyrażenie/zaznaczenie | `valuescope.evaluateExpression` |
| Odśwież wynik | `valuescope.refresh` |
| Wybierz plik tfvars | `valuescope.selectTfvars` |
| Wybierz katalog tfvars | `valuescope.selectTfvarsDirectory` |
| Wybierz profil | `valuescope.selectProfile` |
| Wybierz root module | `valuescope.selectRootModule` |
| Wybierz scope modułu | `valuescope.pinScope` |
| Wybierz instancję resource/modułu | `valuescope.selectInstance` |
| Ustaw wartość sekretną | `valuescope.setSecret` |
| Zmień język | `valuescope.selectLanguage` |
| Opis / dokumentacja | `valuescope.openAbout` |
| Zrestartuj silnik | `valuescope.restartEngine` |
| Pokaż logi | `valuescope.showLogs` |

## Ustawienia

| Ustawienie | Domyślnie | Zastosowanie |
|---|---|---|
| `valuescope.language` | `auto` | `auto`, `en`, `pl`; lokalny wybór ma pierwszeństwo |
| `valuescope.tfvars.directory` | `environment` | Katalog listy plików, nie automatyczne ładowanie wejść |
| `valuescope.profiles` | `[]` | Nazwane profile i wejścia zmiennych |
| `valuescope.inheritTfVarEnv` | `false` | Jawne włączenie `TF_VAR_*` procesu VS Code w zaufanym workspace |
| `valuescope.codeLens.enabled` | `true` | Akcje podglądu nad kodem |
| `valuescope.highlight.enabled` | `true` | Delikatny obrys i tło źródła |
| `valuescope.compat` | `auto` | Założony podzbiór 1.16.0 lub jawne `1.16.0`; inne wartości unavailable |
| `valuescope.limits.hoverDeadlineMs` | `2000` | Kooperacyjny limit czasu; silnik ogranicza go do 5000 ms |
| `valuescope.terraform.path` | puste | Rezerwa dla przyszłego jawnego CLI, nie live evaluation |
| `valuescope.trace.server` | `off` | Rezerwa trace; bieżące logi zawierają kody zdarzeń, nie payloady RPC |

## Lokalne obliczenia i prywatność

Silnik oblicza wartości na Twoim komputerze. Podgląd kodu nie uruchamia Terraform, providera, backendu ani zapytań do chmury. Kod, tfvars i wyniki pozostają na Twoim komputerze. Rozszerzenie czyta pliki Terraform; wybór wejść i preferencje interfejsu zapisuje osobno w VS Code.

Sekretne wejścia korzystają z VS Code SecretStorage. Wartości oznaczone jako sensitive lub ephemeral są chronione w wyniku i szczegółach powiązań. Rozpoznane formaty danych uwierzytelniających są dodatkowo maskowane, ale wzorce nie wykryją każdego sekretu. Kopiowanie obejmuje wyświetlony wynik po ukryciu chronionych danych. Logi zawierają kody zdarzeń zamiast wyrażeń czy surowych komunikatów RPC.

W niezaufanym projekcie dostęp do plików jest ograniczony. Suma kontrolna silnika i sprawdzenie wersji wykrywają zmienione lub niedopasowane pliki; nie zastępują podpisu wydawcy.

## Limity i nieobsługiwane przepływy

| Obszar | Bieżąca granica |
|---|---|
| Zewnętrzni providerzy | Brak schema service, defaults/normalizacji providera, jego funkcji i odczytów API |
| State i plany | Brak enrichment przez state/saved plan i podglądu stanu chmury |
| Moduły | Lokalne źródła; brak automatycznej instalacji zdalnej; nagłówek pokazuje istniejące outputy |
| Całe zewnętrzne zasoby | Pełna wartość nadal wymaga schemy; konfiguracja jest oddzielną prezentacją |
| Pętle po polach resource | Bezpośrednie kolekcje resource/data i konkretne pola; całe aliasy i dynamiczny wybór pól pozostają ostrożne w zwykłej ewaluacji |
| Dynamic configuration | Obsługiwane rozwinięcia native HCL; brak etykiet wymagających schemy; krotki są reprezentacją podglądu |
| Zgodność | Testowany podzbiór względem Terraform 1.16.0, nie cały Terraform 1.x ani gwarancja OpenTofu |
| Indeks workspace | 8 MiB/plik, 64 MiB łącznie, 10000 plików konfiguracji, 200000 odwiedzonych wpisów; niekompletny indeks jest raportowany |
| Ewaluacja | 20000 węzłów zależności, 1000 instancji/blok, głębokość modułów 32 |
| Podgląd konfiguracji | Wspólny budżet 1000 rozwinięć i głębokość 64; złożony podgląd może osiągnąć go wcześniej niż limit instancji |
| Prezentacja | Do 200 widocznych elementów/kolekcję, 5000 węzłów, głębokość 64, 65536 bajtów tekstu wartości; ucięcie jest oznaczane |
| Pozostałe przepływy | Brak porównywania profili i interaktywnego stronicowania |

Limit czasu jest kooperacyjny. Skrajnie kosztowne wyrażenie HCL może wymagać restartu silnika; nie jest to pełny sandbox przeciw złośliwym obciążeniom. Obrys może powtórzyć krawędź przy zawijaniu bardzo długiej linii granicznej — ograniczenie stabilnego API dekoracji VS Code.

Silnik nie jest ograniczony do nazw zasobów Azure: pracuje na wartościach HCL i argumentach konfiguracji. Przykłady Azure wynikają z najdokładniej sprawdzanych przepływów, **nie z pełnej certyfikacji Azure, AWS, Google Cloud ani innych providerów**.

## Rozwiązywanie problemów

| Objaw | Co sprawdzić |
|---|---|
| Wymagana zmienna unavailable | Wybierz właściwy tfvars/profil; sprawdź root i argumenty child |
| `schema-not-loaded` | Podejrzyj argument lub nagłówek; pełne wartości providera celowo pozostają niedostępne |
| Nierozstrzygnięty ID lub czas `time_static` | Wartość zależy od providera; tfvars jej nie wytworzy |
| Brak kontekstu `each`/`count` | Zaznacz źródło wewnątrz bloku i wybierz jego scope/instancję |
| Nagłówek różni się od wyrażenia | Sprawdź etykietę configuration-only: to dwa różne rodzaje wyniku |
| Wynik ucięty | Podejrzyj mniejsze wyrażenie; niewidoczne elementy mogą nadal istnieć |
| Odmowa odczytu pliku | Sprawdź trust/ścieżkę; jawnie wybierz zewnętrzny tfvars, nie cały katalog |
| Brak kolorów lub completion | Zachowaj companion Terraform; Terraform Live Values & Results nie jest rozszerzeniem językowym |
| Nieaktualny wynik/zatrzymany silnik | Odśwież, sprawdź bezpieczne kody logów, ewentualnie zrestartuj silnik |
| Linux: zmiana na dysku nie odświeża podglądu lub log obserwatora zawiera `EMFILE` | Sprawdź [limity inotify](#linux-inotify); VS Code może nie móc uruchomić obserwatora plików |
| Inny język panelu i tytułu komendy | Lokalny wybór steruje UI Terraform Live Values & Results; statyczne tytuły podążają za VS Code |

## Linux: inotify

`inotify` powiadamia aplikacje o zmianach plików i katalogów w Linuksie. Limit `fs.inotify.max_user_instances` jest wspólny dla aplikacji działających na tym samym koncie użytkownika. Wartość 128 oznacza 128 instancji, z których każda może obserwować wiele ścieżek. Liczbę obserwowanych ścieżek ogranicza osobne ustawienie `fs.inotify.max_user_watches`. [Dokumentacja Linuksa](https://man7.org/linux/man-pages/man7/inotify.7.html).

Wtyczka korzysta ze zdarzeń VS Code, aby wykrywać zmiany plików Terraform, wybranych tfvars oraz zależności `file()` i `templatefile()`. Jeśli VS Code nie uruchomi potrzebnego obserwatora, po zmianie pliku na dysku podgląd może nadal pokazywać poprzedni wynik. Pisanie w otwartym dokumencie Terraform może go nadal odświeżać dzięki zdarzeniom edytora, więc samo to nie potwierdza działania obserwacji dysku.

Błąd `EMFILE` w logu obserwatora może oznaczać wyczerpanie limitu instancji, ale także limitu deskryptorów plików danego procesu. Sprawdź logi, zanim przypiszesz każdy nieaktualny wynik do inotify. [Znaczenie błędów](https://man7.org/linux/man-pages/man2/inotify_init.2.html).

Jeśli limit instancji wynosi 128, a kilka aplikacji korzysta z obserwatorów plików, warto rozważyć zwiększenie go do **1024**. To rozwiązało problem uruchamiania obserwatorów w naszych testach Linuksa. Jest to punkt wyjścia, a nie wymóg dla każdego komputera. Zachowaj istniejący limit, jeśli jest wyższy.

Sprawdź ustawienia i zanotuj poprzednią wartość:

```bash
sysctl fs.inotify.max_user_instances fs.inotify.max_user_watches
```

Jeśli limit instancji jest mniejszy niż 1024, administrator może zmienić go do ponownego uruchomienia systemu:

```bash
sudo sysctl -w fs.inotify.max_user_instances=1024
```

Polecenie nie zapisuje ustawienia na kolejne uruchomienie systemu. Po tymczasowym teście przywróć zanotowaną wartość przez `sudo sysctl -w fs.inotify.max_user_instances=WARTOŚĆ`. [Polecenia sysctl](https://man7.org/linux/man-pages/man8/sysctl.8.html).

Aby zachować 1024 po restarcie w systemie korzystającym z `sysctl.d`, otwórz lokalny plik konfiguracji:

```bash
sudoedit /etc/sysctl.d/90-live-values-results-inotify.conf
```

Dodaj lub zaktualizuj tę linię i zapisz plik:

```ini
fs.inotify.max_user_instances = 1024
```

Zastosuj ustawienie z tego pliku i sprawdź aktywną wartość:

```bash
sudo sysctl -p /etc/sysctl.d/90-live-values-results-inotify.conf
sysctl fs.inotify.max_user_instances
```

Inne ustawienia systemowe mogą nadpisać tę wartość podczas startu; sprawdź ją również po ponownym uruchomieniu Linuksa. Zobacz [konfigurację sysctl.d](https://man7.org/linux/man-pages/man5/sysctl.d.5.html).

Po zmianie limitu uruchom ponownie VS Code i sprawdź podgląd po zmianie zależnego pliku na dysku. Wtyczka nie zmienia limitów systemowych automatycznie.

## Licencje

Od wersji 0.0.12 własne części aplikacji są udostępniane na [licencji własnościowej](https://github.com/bryn1u/live-values-results-for-terraform/blob/main/LICENSE.txt). Oficjalnych wydań możesz używać bez opłat prywatnie i w pracy komercyjnej. Modyfikacja i redystrybucja własnych części aplikacji podlegają ograniczeniom opisanym w licencji.

Biblioteki zachowują swoje licencje: [informacje o zależnościach](https://github.com/bryn1u/live-values-results-for-terraform/blob/main/THIRD_PARTY_NOTICES.txt) i [dostęp do źródeł](https://github.com/bryn1u/live-values-results-for-terraform/blob/main/SOURCE_AVAILABILITY.txt). Paczka zawiera archiwum niezmienionych źródeł HCL wymagane dla części MPL-2.0. Źródła samej aplikacji pozostają prywatne.

Terraform Live Values & Results nie jest powiązany z HashiCorp, zatwierdzony ani sponsorowany przez tę firmę. Terraform jest znakiem towarowym HashiCorp. Opis zgodności wskazuje język konfiguracji, nie oficjalne powiązanie.
