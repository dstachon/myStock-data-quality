# Audyt jakości danych `stock`

Wygenerowano: **2026-10-10 21:00 CEST**. Zakres: od początku każdego źródła **do 2026-10-10 włącznie**. Raport jest wynikiem odczytowej kontroli całej dostępnej historii w tym zakresie.

## Wynik w skrócie

| Źródło | Pierwsza data | Ostatnia data | Sesje | Rekordy | Rekordy z błędem | Znane wyjątki / wyłączenia | Ostrzeżenia |
|---|---|---|---:|---:|---:|---:|---:|
| `daily_quotes` | 1987-01-02 | 2026-10-09 | 10,108 | 1,830,803 | 27 | 34 | 1 |
| `aktualne_kursy` | 2025-08-28 | 2026-10-01 | 177 | 2,716,230 | 0 | 0 | 2 |
| `statica_trades` | 2026-09-16 | 2026-10-07 | 16 | 4,073,554 | 0 | 348 plików | 2 |

**Interpretacja:** „błąd” oznacza wartości naruszające podstawowe reguły źródła; „ostrzeżenie” oznacza lukę lub odstępstwo wymagające oceny. Brak błędów nie certyfikuje wykonalności transakcji ani poprawności każdego instrumentu.

**Znane wyjątki historyczne:** 34 niezmienionych rekordów `daily_quotes` jest pokazanych osobno i nie wchodzi do licznika błędów. Dokładne ID oraz pierwotne wartości są w `configs/data_quality_daily_exceptions.csv`; zmieniony rekord ponownie trafi do błędów.

**Znane wyłączenia Statica:** 348 historycznych plików (282,509 usuniętych wierszy) jest pokazanych osobno, bez ostrzeżenia o bieżącej niespójności. Każdy plik jest porównywany z dokładnym stanem w `configs/data_quality_statica_known_exclusions.csv`; zmiana liczników, metadanych lub zakresu zachowanych linii ponownie uruchomi ostrzeżenie.

## Ustalenia według źródeł

### `daily_quotes`

- **BŁĄD:** 27 rekordów z niedozwolonymi/pustymi wartościami w 5 sesjach (np. 2026-10-05: 4, 2026-10-06: 11, 2026-10-07: 3, 2026-10-08: 4, 2026-10-09: 5).
- **OSTRZEŻENIE:** 1599 dat ma najwyżej jeden symbol (zakres 1987-01-02–2015-06-04); starsza historia nie oznacza automatycznie pokrycia całego rynku.

| Okres | Sesje | Rekordy | Rekordy z błędem | Znane wyjątki | Bez transakcji* |
|---|---:|---:|---:|---:|---:|
| 1987 | 254 | 254 | 0 | 0 | 0 |
| 1988 | 253 | 253 | 0 | 0 | 0 |
| 1989 | 250 | 250 | 0 | 0 | 0 |
| 1990 | 248 | 248 | 0 | 0 | 0 |
| 1991 | 250 | 264 | 0 | 0 | 0 |
| 1992 | 254 | 415 | 0 | 0 | 0 |
| 1993 | 254 | 915 | 0 | 0 | 0 |
| 1994 | 255 | 2,273 | 0 | 0 | 0 |
| 1995 | 253 | 4,431 | 0 | 0 | 0 |
| 1996 | 257 | 6,537 | 0 | 0 | 0 |
| 1997 | 256 | 11,335 | 0 | 0 | 0 |
| 1998 | 257 | 17,878 | 0 | 0 | 0 |
| 1999 | 258 | 21,975 | 0 | 0 | 0 |
| 2000 | 257 | 24,202 | 0 | 0 | 0 |
| 2001 | 257 | 23,541 | 0 | 0 | 0 |
| 2002 | 256 | 21,691 | 0 | 0 | 0 |
| 2003 | 257 | 23,050 | 0 | 0 | 0 |
| 2004 | 261 | 26,777 | 0 | 0 | 0 |
| 2005 | 259 | 31,436 | 0 | 0 | 0 |
| 2006 | 258 | 35,670 | 0 | 0 | 0 |
| 2007 | 257 | 42,712 | 0 | 0 | 0 |
| 2008 | 259 | 50,822 | 0 | 0 | 0 |
| 2009 | 257 | 56,338 | 0 | 0 | 0 |
| 2010 | 260 | 61,554 | 0 | 1 | 0 |
| 2011 | 257 | 68,440 | 0 | 0 | 0 |
| 2012 | 257 | 71,160 | 0 | 0 | 0 |
| 2013 | 255 | 75,290 | 0 | 0 | 0 |
| 2014 | 255 | 79,324 | 0 | 0 | 0 |
| 2015 | 253 | 82,670 | 0 | 0 | 0 |
| 2016 | 251 | 84,953 | 0 | 0 | 0 |
| 2017 | 250 | 86,797 | 0 | 0 | 0 |
| 2018 | 247 | 84,087 | 0 | 0 | 0 |
| 2019 | 248 | 84,075 | 0 | 32 | 0 |
| 2020 | 252 | 92,066 | 0 | 0 | 0 |
| 2021 | 251 | 97,186 | 0 | 1 | 0 |
| 2022 | 251 | 96,707 | 0 | 0 | 0 |
| 2023 | 250 | 96,173 | 0 | 0 | 0 |
| 2024 | 249 | 92,296 | 0 | 0 | 0 |
| 2025 | 249 | 95,945 | 0 | 0 | 5,368 |
| 2026 | 196 | 78,813 | 27 | 0 | 6,438 |

### `aktualne_kursy`

- **OSTRZEŻENIE:** Brak całej sesji względem kalendarza `daily_quotes`: 104 dat (pierwsze: 2025-09-05, 2025-12-11, 2025-12-12, 2025-12-15, 2025-12-16, 2025-12-17, 2025-12-18, 2025-12-19, 2025-12-22, 2025-12-23, 2025-12-29, 2025-12-30). To kandydaci do wyjaśnienia, nie automatyczny dowód awarii.
- **OSTRZEŻENIE:** 6 sesji ma <80% mediany liczby zajętych przedziałów (43); pierwsze: 2025-11-18: 31, 2025-11-24: 10, 2025-12-10: 22, 2026-01-27: 2, 2026-06-08: 11, 2026-10-01: 2. Krótka sesja lub inny harmonogram mogą być poprawne.

| Okres | Sesje | Rekordy | Rekordy z błędem | Znane wyjątki | Bez transakcji* |
|---|---:|---:|---:|---:|---:|
| 2025-08 | 2 | 35,002 | 0 | 0 | 0 |
| 2025-09 | 21 | 366,169 | 0 | 0 | 0 |
| 2025-10 | 23 | 392,604 | 0 | 0 | 0 |
| 2025-11 | 19 | 266,477 | 0 | 0 | 0 |
| 2025-12 | 8 | 112,870 | 0 | 0 | 0 |
| 2026-01 | 4 | 46,372 | 0 | 0 | 0 |
| 2026-02 | 20 | 300,396 | 0 | 0 | 0 |
| 2026-03 | 22 | 327,687 | 0 | 0 | 0 |
| 2026-04 | 20 | 303,288 | 0 | 0 | 0 |
| 2026-05 | 20 | 298,646 | 0 | 0 | 0 |
| 2026-06 | 5 | 63,295 | 0 | 0 | 0 |
| 2026-09 | 12 | 202,798 | 0 | 0 | 0 |
| 2026-10 | 1 | 626 | 0 | 0 | 0 |

### `statica_trades`

- **OSTRZEŻENIE:** Brak całej sesji względem kalendarza `daily_quotes`: 2 dat (pierwsze: 2026-10-08, 2026-10-09). To kandydaci do wyjaśnienia, nie automatyczny dowód awarii.
- **OSTRZEŻENIE:** 1 sesji ma <80% mediany liczby zajętych przedziałów (95); pierwsze: 2026-10-07: 48. Krótka sesja lub inny harmonogram mogą być poprawne.

| Okres | Sesje | Rekordy | Rekordy z błędem | Znane wyjątki | Bez transakcji* |
|---|---:|---:|---:|---:|---:|
| 2026-09 | 11 | 2,677,732 | 0 | 0 | 0 |
| 2026-10 | 5 | 1,395,822 | 0 | 0 | 0 |

## Uzgodnienie plików transakcyjnych

Porównanie `statica_import_files.row_count` z liczbą zachowanych wierszy `statica_trades` dla każdego pliku. Data oznacza **import**, nie dzień transakcji.

| Data importu | Pliki | Nowe niezgodności | Różnica wierszy | Znane wyłączenia | Znane usunięte wiersze |
|---|---:|---:|---:|---:|---:|
| 2026-09-16 | 5,451 | 0 | 0 | 348 | 282,509 |
| 2026-09-17 | 12,890 | 0 | 0 | 0 | 0 |
| 2026-09-18 | 13,084 | 0 | 0 | 0 | 0 |
| 2026-09-21 | 13,778 | 0 | 0 | 0 | 0 |
| 2026-09-22 | 12,852 | 0 | 0 | 0 | 0 |
| 2026-09-23 | 12,299 | 0 | 0 | 0 | 0 |
| 2026-09-24 | 11,894 | 0 | 0 | 0 | 0 |
| 2026-09-25 | 12,566 | 0 | 0 | 0 | 0 |
| 2026-09-28 | 12,495 | 0 | 0 | 0 | 0 |
| 2026-09-29 | 12,343 | 0 | 0 | 0 | 0 |
| 2026-09-30 | 12,880 | 0 | 0 | 0 | 0 |
| 2026-10-01 | 13,357 | 0 | 0 | 0 | 0 |
| 2026-10-07 | 367 | 0 | 0 | 0 | 0 |

## Zakres kontroli i ograniczenia

- `daily_quotes`: każda zapisana data od początku źródła; puste/niedodatnie ceny OHLC, niespójność minimum/maksimum, ujemne wartości wolumenu, liczby transakcji lub obrotu. Wyjątek: wiersz z zerowym obrotem i liczbą transakcji, zerowym OHLC i dodatnim `close_price` oznacza brak handlu oraz cenę przeniesioną; jest liczony osobno (*) i nie stanowi świecy możliwej do wykonania. Bez zewnętrznego kalendarza GPW brakujący dzień roboczy nie jest automatycznie błędem.
- 34 imiennie wymienione anomalie starszego źródła `daily_quotes` są liczone jako znane wyjątki tylko przy niezmienionym ID, dacie, symbolu, OHLC, wolumenie oraz pustych `trns`/`value`; każda inna nieprawidłowość nadal jest błędem. Baza nie jest modyfikowana przez audyt.
- `aktualne_kursy`: każda zapisana data od początku źródła; dodatniość ceny, nieujemność licznika, liczba symboli i zajętych przedziałów 10-minutowych. Czas pobrania migawki nie jest czasem transakcji.
- `statica_trades`: każda zapisana data od początku źródła; dodatniość ceny i wolumenu, liczba symboli i zajętych przedziałów 5-minutowych, osobne uzgodnienie liczników plików. Brak transakcji jednej spółki nie oznacza luki w imporcie.
- Uzgodnienie plików Statica zachowuje oryginalne `row_count`. Dokładnie 348 utrwalonych stanów po historycznym usunięciu początku plików jest wykazywanych osobno. Każda inna różnica liczników pozostaje ostrzeżeniem; audyt nie przywraca usuniętych transakcji.
- Daty całkowicie nieobecne w źródłach intraday są porównywane do dat `daily_quotes` dopiero od rozpoczęcia danego źródła. Pojedyncze dni o <80% mediany zajętych przedziałów są wskazywane do wyjaśnienia.
- Kontrola nie potwierdza mapowania symboli między źródłami, korekt korporacyjnych, integralności każdej świecy, dostępności arkusza zleceń ani ceny możliwej do wykonania. Te kwestie wymagają osobnych badań.

Raport nie zawiera hasła ani danych uwierzytelniających.
