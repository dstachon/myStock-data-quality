# Audyt danych do badania strategii GPW

Koniec badanego zbioru: **02.10.2026 włącznie**.

## Dane do użycia

| Dane              | Źródło                                                              | Zakres badawczy                                                                                   |
| ----------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| Notowania dzienne | MySQL `daily_quotes_gpw`                                            | 02.01.2001–02.10.2026; 781 ISIN-ów po ograniczeniu zakresu.                                       |
| Świece 5 min      | MySQL `statica_history_5m_quotes`                                   | Najwcześniej 04.05.2020–02.10.2026; 399 instrumentów, 16,5 mln świec.                             |
| Źródłowe ticki    | Dostępne na żądanie. <br>`C:\envDEV\Statica_GPW\Ticks_archiwum\GPW` | Eksporty wybrane w manifeście katalogu nadrzędnego; do badań przyciąć do powyższej daty końcowej. |

Import daily porównano ze źródłem GPW. Ticki przeskanowano, a agregaty
porównano z zapisanymi świecami i dostępną referencją dzienną.
Zaakceptowane drobne różnice aktywności nie wymagają osobnej obsługi
w podstawowych badaniach strategii. 

## Ograniczenia istotne dla wyniku

1. **Zdarzenia korporacyjne są niekompletne.** Ceny są surowe, bez korekt
   splitów, scaleń i dywidend. Z 2638 grup tylko 7 jest gotowych do rozliczenia,
   a 2 również do wykorzystania zachowanych komunikatów. Nie uznawać wyników
   wieloletniego portfela za ostateczne bez obsługi operacji obejmujących
   badane pozycje i okresy wskaźników. Informacje dla sygnałów udostępniać
   dopiero po `available_at_utc`, z gotowych wersji komunikatów.
2. **Intraday nie obejmuje pełnego historycznego rynku.** Brakuje ticków
   spółek wycofanych; wyniki dotyczą dostępnego zbioru i mogą zawierać efekt
   przeżywalności. Bieżącej segmentacji `daily_quotes_segments` nie stosować
   wstecz jako historycznego składu portfela.
3. **Brak świecy lub transakcji nie daje ceny realizacji.** Nie tworzyć
   sztucznych transakcji ani uzupełniać niepełnego OHLC poprzednią ceną.
   Sesje `no_gpw_reference` nie mają potwierdzonej kompletności względem GPW.
4. **Symulacja wykonania wymaga założeń.** Pełna świeca 5 min jest dostępna
   od `bar_end_utc`. Dane obejmują też fixingi; nie każda świeca pochodzi
   z notowań ciągłych. Ticki nie zawierają pełnej historii bid/ask ani arkusza;
   koszty i poślizg należy określić w modelu testu.

## Zasady odczytu

- Łączyć historię po **ISIN**, z uwzględnieniem daty i waluty. Rozstrzygać
  aliasy słownika przed złączeniem; nie sklejać różnych ISIN-ów po tickerze.
- Przy badaniu obrotu ujednolicić jednostki: docelowo daily `value × 1000 / 2`
  dla lat 2001–2010 i `value × 1000` od 2011, po sprawdzeniu konwencji wejścia.
  Obrót świec 5 min jest już jednostronny, w PLN.

**Ocena:** dane nadają się do badania sygnałów i prototypowania strategii
po zastosowaniu powyższych zasad. Głównym ograniczeniem ostatecznej oceny
rentowności portfela pozostaje niepełna obsługa zdarzeń korporacyjnych.

## Dostęp do MySQL `stock`

| Parametr | Wartość |
|---|---|
| Host | `192.168.0.188` (sieć lokalna) |
| Port | `3306` |
| Użytkownik | `dumpuser` |
| Baza | `stock` |
| Hasło | zmienna środowiskowa `STOCK_DB_PASSWORD`; bez wartości w tym pliku |

Zainstaluj `mysql-connector-python` (`python -m pip install mysql-connector-python`). Agent korzysta z bazy **tylko do odczytu**. Najlepiej docelowo wydać mu osobne konto MySQL z uprawnieniem `SELECT`. Nie zapisuj hasła w pliku, notebooku ani logach; nie wystawiaj portu bazy do internetu.

```python
import os
import mysql.connector

password = os.environ.get("STOCK_DB_PASSWORD")
if not password:
    raise RuntimeError("Brak zmiennej STOCK_DB_PASSWORD")

cn = mysql.connector.connect(
    host="192.168.0.188", port=3306, user="dumpuser",
    password=password, database="stock", connection_timeout=5,
)
try:
    cur = cn.cursor()
    cur.execute("SELECT DATABASE(), CURRENT_DATE()")
    print(cur.fetchone())
finally:
    cn.close()
```
