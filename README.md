# MML1-project-HW2
– Data Processing Pipeline

## Jak spustit

1. Otevřít dataprocessing.ipynb
2. Spustit všechny buňky
3. Otevřít benchmark.ipynb


## Popis projektu
Cílem tohoto úkolu je vytvořit korektní datovou pipeline pro predikci inflace v České republice.

Pipeline zahrnuje:
- načtení dat z veřejných zdrojů (Eurostat, FRED)
- transformaci časových řad (YoY inflace, růst HDP)
- agregaci na kvartální frekvenci
- sloučení datasetů
- vytvoření cílové proměnné (target)
- vytvoření baseline modelu
- rozdělení dat na train, validation a test

Cílová proměnná je inflace v následujícím kvartálu (t+1).

---

## Struktura repozitáře

- `dataprocessing.ipynb`  
  Notebook obsahující kompletní pipeline pro přípravu dat.

- `dataprocessing.html`  
  Export notebooku pro snadné prohlížení.

- `benchmark.ipynb`  
  Notebook obsahující benchmark modely (baseline a lineární regrese).

- `benchmark.html`  
  Export benchmark notebooku.

- `data/`  
  Složka obsahující připravené datasety:
  - `train.csv`
  - `validation.csv`
  - `test.csv`

---

## Data

Data pochází z veřejně dostupných zdrojů:

- Eurostat  
  https://ec.europa.eu/eurostat  

- FRED (Federal Reserve Economic Data)  
  https://fred.stlouisfed.org  

Použité datové sady zahrnují:
- HICP (inflace)
- GDP
- úrokové sazby
- ceny ropy

Data byla stažena ve formátu CSV a následně upravena pro potřeby analýzy.
Data byla převedena na kvartální frekvenci a vyčištěna.
Data pokrývají přibližně období 1997–2025 v kvartální frekvenci.
---

## Metodika

### Preprocessing
- výpočet meziroční inflace (YoY)
- převod na kvartální data
- odstranění chybějících hodnot
- odstranění duplicit
- sjednocení časového indexu

### Leakage
Bylo zajištěno, že všechny vstupní proměnné odpovídají informacím dostupným v čase t.
Cílová proměnná je posunuta o jedno období dopředu (t+1).

### Data split
Data byla rozdělena pomocí časového splitu:
- train: historická data
- validation: novější data pro porovnání modelů
- test: vyhrazeno pro finální vyhodnocení

---

## Benchmark

Byly použity dva benchmarky:
1. Naivní baseline (inflace z předchozího období)
2. Lineární regrese

Modely byly vyhodnoceny pomocí metrik:
- RMSE
- MAE

Benchmarky byly vyhodnoceny pouze na validační sadě.

---

## Výsledky

Baseline model dosahuje lepších výsledků než lineární regrese.
Baseline model dosáhl RMSE ≈ 0.76, zatímco lineární regrese RMSE ≈ 2.24.

To naznačuje, že inflace má silnou setrvačnost a minulá hodnota inflace
je velmi silným prediktorem budoucí hodnoty.

---
