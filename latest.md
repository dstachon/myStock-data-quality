# Audyt jakości danych `stock`

Wygenerowano: **2026-10-15 21:00 CEST**. Zakres: od początku każdego źródła **do 2026-10-15 włącznie**. Raport jest wynikiem odczytowej kontroli całej dostępnej historii w tym zakresie.

## Wynik w skrócie

| Źródło | Pierwsza data | Ostatnia data | Sesje | Rekordy | Rekordy z błędem | Znane wyjątki / wyłączenia | Ostrzeżenia |
|---|---|---|---:|---:|---:|---:|---:|
| `daily_quotes_gpw` | 2000-01-03 | 2026-10-14 | 6,706 | 2,523,990 | 40,141 | 0 | 0 |
| `statica_trades` | 2026-09-16 | 2026-10-07 | 16 | 4,073,554 | 0 | 348 plików | 2 |

**Interpretacja:** „błąd” oznacza wartości naruszające podstawowe reguły źródła; „ostrzeżenie” oznacza lukę lub odstępstwo wymagające oceny. Brak błędów nie certyfikuje wykonalności transakcji ani poprawności każdego instrumentu.

**Znane wyłączenia Statica:** 348 historycznych plików (282,509 usuniętych wierszy) jest pokazanych osobno, bez ostrzeżenia o bieżącej niespójności. Każdy plik jest porównywany z dokładnym stanem w `configs/data_quality_statica_known_exclusions.csv`; zmiana liczników, metadanych lub zakresu zachowanych linii ponownie uruchomi ostrzeżenie.

**OSTRZEŻENIE:** żadne źródło nie ma danych dla 2026-10-15; możliwy dzień wolny od handlu albo wspólne opóźnienie importów. Wymaga potwierdzenia kalendarzem GPW.

## Ustalenia według źródeł

### `daily_quotes_gpw`

- **BŁĄD:** 40141 rekordów z niedozwolonymi/pustymi wartościami w 979 sesjach (np. 2000-01-03: 129, 2000-01-04: 128, 2000-01-05: 131, 2000-01-06: 129, 2000-01-07: 129, 2000-01-10: 125, 2000-01-11: 131, 2000-01-12: 132).

| Okres | Sesje | Rekordy | Rekordy z błędem | Znane wyjątki | Bez transakcji* |
|---|---:|---:|---:|---:|---:|
| 2000 | 250 | 55,596 | 33,693 | 0 | 589 |
| 2001 | 250 | 57,283 | 5,679 | 0 | 6,844 |
| 2002 | 249 | 56,429 | 260 | 0 | 12,001 |
| 2003 | 251 | 51,926 | 141 | 0 | 7,875 |
| 2004 | 255 | 53,539 | 46 | 0 | 3,787 |
| 2005 | 251 | 60,827 | 33 | 0 | 2,968 |
| 2006 | 251 | 65,163 | 7 | 0 | 1,575 |
| 2007 | 249 | 75,959 | 14 | 0 | 1,480 |
| 2008 | 251 | 90,162 | 22 | 0 | 4,271 |
| 2009 | 252 | 94,422 | 35 | 0 | 3,740 |
| 2010 | 253 | 97,049 | 46 | 0 | 3,817 |
| 2011 | 251 | 104,253 | 50 | 0 | 4,719 |
| 2012 | 249 | 108,441 | 52 | 0 | 8,082 |
| 2013 | 247 | 110,044 | 19 | 0 | 7,399 |
| 2014 | 249 | 115,390 | 0 | 0 | 9,851 |
| 2015 | 251 | 120,651 | 0 | 0 | 12,914 |
| 2016 | 251 | 123,077 | 0 | 0 | 14,377 |
| 2017 | 250 | 122,397 | 0 | 0 | 14,290 |
| 2018 | 247 | 119,085 | 0 | 0 | 19,510 |
| 2019 | 248 | 116,729 | 0 | 0 | 21,055 |
| 2020 | 252 | 113,837 | 0 | 0 | 14,415 |
| 2021 | 251 | 110,936 | 0 | 0 | 9,727 |
| 2022 | 251 | 109,993 | 0 | 0 | 12,192 |
| 2023 | 250 | 106,463 | 0 | 0 | 10,358 |
| 2024 | 249 | 103,486 | 0 | 0 | 10,949 |
| 2025 | 249 | 101,058 | 0 | 0 | 10,403 |
| 2026 | 199 | 79,795 | 44 | 0 | 6,526 |

### `statica_trades`

- **OSTRZEŻENIE:** Brak całej sesji względem kalendarza `daily_quotes_gpw`: 5 dat (pierwsze: 2026-10-08, 2026-10-09, 2026-10-12, 2026-10-13, 2026-10-14). To kandydaci do wyjaśnienia, nie automatyczny dowód awarii.
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

- `daily_quotes_gpw`: każda zapisana data od początku źródła; puste/niedodatnie ceny OHLC, niespójność minimum/maksimum, ujemne wartości wolumenu, liczby transakcji lub obrotu. Wyjątek: wiersz z zerowym obrotem i liczbą transakcji, zerowym OHLC i dodatnim `close_price` oznacza brak handlu oraz cenę przeniesioną; jest liczony osobno (*) i nie stanowi świecy możliwej do wykonania. Bez zewnętrznego kalendarza GPW brakujący dzień roboczy nie jest automatycznie błędem.
- `statica_trades`: każda zapisana data od początku źródła; dodatniość ceny i wolumenu, liczba symboli i zajętych przedziałów 5-minutowych, osobne uzgodnienie liczników plików. Brak transakcji jednej spółki nie oznacza luki w imporcie.
- Uzgodnienie plików Statica zachowuje oryginalne `row_count`. Dokładnie 348 utrwalonych stanów po historycznym usunięciu początku plików jest wykazywanych osobno. Każda inna różnica liczników pozostaje ostrzeżeniem; audyt nie przywraca usuniętych transakcji.
- Daty całkowicie nieobecne w źródłach intraday są porównywane do dat `daily_quotes_gpw` dopiero od rozpoczęcia danego źródła. Pojedyncze dni o <80% mediany zajętych przedziałów są wskazywane do wyjaśnienia.
- Kontrola nie potwierdza mapowania symboli między źródłami, korekt korporacyjnych, integralności każdej świecy, dostępności arkusza zleceń ani ceny możliwej do wykonania. Te kwestie wymagają osobnych badań.

- Źródłem dziennym jest surowe GPW po ISIN; dawne wyjątki według ID daily_quotes nie są stosowane do GPW.
Raport nie zawiera hasła ani danych uwierzytelniających.
