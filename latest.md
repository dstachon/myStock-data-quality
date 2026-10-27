# Audyt jakości danych `stock`

Wygenerowano: **2026-10-27 21:00 CET**. Zakres: od początku każdego źródła **do 2026-10-27 włącznie**. Raport jest wynikiem odczytowej kontroli całej dostępnej historii w tym zakresie.

## Wynik w skrócie

| Źródło | Pierwsza data | Ostatnia data | Sesje | Rekordy | Rekordy z błędem | Znane wyjątki / wyłączenia | Ostrzeżenia |
|---|---|---|---:|---:|---:|---:|---:|
| `daily_quotes_gpw` | 2001-01-02 | 2026-10-26 | 6,464 | 2,449,225 | 6,343 | 0 | 0 |
| `statica_trades` | 2026-09-16 | 2026-10-07 | 16 | 4,073,554 | 0 | 348 plików | 2 |

**Interpretacja:** „błąd” oznacza wartości naruszające podstawowe reguły źródła; „ostrzeżenie” oznacza lukę lub odstępstwo wymagające oceny. Brak błędów nie certyfikuje wykonalności transakcji ani poprawności każdego instrumentu.

**Znane wyłączenia Statica:** 348 historycznych plików (282,509 usuniętych wierszy) jest pokazanych osobno, bez ostrzeżenia o bieżącej niespójności. Każdy plik jest porównywany z dokładnym stanem w `configs/data_quality_statica_known_exclusions.csv`; zmiana liczników, metadanych lub zakresu zachowanych linii ponownie uruchomi ostrzeżenie.

**OSTRZEŻENIE:** żadne źródło nie ma danych dla 2026-10-27; możliwy dzień wolny od handlu albo wspólne opóźnienie importów. Wymaga potwierdzenia kalendarzem GPW.

## Ustalenia według źródeł

### `daily_quotes_gpw`

- **BŁĄD:** 6343 rekordów z niedozwolonymi/pustymi wartościami w 698 sesjach (np. 2001-01-02: 76, 2001-01-03: 75, 2001-01-04: 80, 2001-01-05: 74, 2001-01-08: 73, 2001-01-09: 74, 2001-01-10: 78, 2001-01-11: 75).

| Okres | Sesje | Rekordy | Rekordy z błędem | Znane wyjątki | Bez transakcji* |
|---|---:|---:|---:|---:|---:|
| 2001 | 250 | 56,579 | 5,618 | 0 | 6,681 |
| 2002 | 249 | 55,682 | 246 | 0 | 11,665 |
| 2003 | 251 | 51,173 | 127 | 0 | 7,591 |
| 2004 | 255 | 52,774 | 41 | 0 | 3,609 |
| 2005 | 251 | 60,074 | 27 | 0 | 2,815 |
| 2006 | 251 | 64,410 | 4 | 0 | 1,511 |
| 2007 | 249 | 75,149 | 14 | 0 | 1,480 |
| 2008 | 251 | 89,158 | 22 | 0 | 4,220 |
| 2009 | 252 | 93,414 | 35 | 0 | 3,715 |
| 2010 | 253 | 96,037 | 46 | 0 | 3,780 |
| 2011 | 251 | 103,249 | 50 | 0 | 4,648 |
| 2012 | 249 | 107,445 | 50 | 0 | 8,071 |
| 2013 | 247 | 109,056 | 19 | 0 | 7,387 |
| 2014 | 249 | 114,394 | 0 | 0 | 9,797 |
| 2015 | 251 | 119,647 | 0 | 0 | 12,872 |
| 2016 | 251 | 122,073 | 0 | 0 | 14,321 |
| 2017 | 250 | 121,397 | 0 | 0 | 14,264 |
| 2018 | 247 | 118,097 | 0 | 0 | 19,434 |
| 2019 | 248 | 115,737 | 0 | 0 | 20,725 |
| 2020 | 252 | 112,829 | 0 | 0 | 14,335 |
| 2021 | 251 | 109,932 | 0 | 0 | 9,717 |
| 2022 | 251 | 108,989 | 0 | 0 | 11,934 |
| 2023 | 250 | 105,515 | 0 | 0 | 10,190 |
| 2024 | 249 | 102,739 | 0 | 0 | 10,924 |
| 2025 | 249 | 100,665 | 0 | 0 | 10,200 |
| 2026 | 207 | 83,011 | 44 | 0 | 6,791 |

### `statica_trades`

- **OSTRZEŻENIE:** Brak całej sesji względem kalendarza `daily_quotes_gpw`: 13 dat (pierwsze: 2026-10-08, 2026-10-09, 2026-10-12, 2026-10-13, 2026-10-14, 2026-10-15, 2026-10-16, 2026-10-19, 2026-10-20, 2026-10-21, 2026-10-22, 2026-10-23). To kandydaci do wyjaśnienia, nie automatyczny dowód awarii.
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
