# DT_Mravec - MovieLens
Databázové Technológie - FINAL - Matias Mravec 

Tento repozitár obsahuje implementáciu ETL procesu v Snowflake, určenú na analýzu dát z datasetu MovieLens. Projekt sa sústreďuje na skúmanie používateľského správania a preferencií v čítaní prostredníctvom hodnotení kníh a demografických údajov. Vytvorený dátový model podporuje multidimenzionálnu analýzu a vizualizáciu kľúčových ukazovateľov.

---
## **1. Úvod a popis zdrojových dát**
Cieľom semestrálneho projektu je analyzovať dáta týkajúce sa kníh, používateľov a ich hodnotení. Táto analýza umožňuje identifikovať trendy v čitateľských preferenciách, najpopulárnejšie knihy a správanie používateľov.

Zdrojové dáta pochádzajú z Kaggle datasetu dostupného [tu](https://grouplens.org/datasets/movielens/). Dataset obsahuje osem hlavných tabuliek:
- `movies`
- `age_groups`
- `genres`
- `genres_movies`
- `occupations`
- `ratings`
- `tags`
- `users`

Účelom ETL procesu bolo tieto dáta pripraviť, transformovať a sprístupniť pre viacdimenzionálnu analýzu.

---

### **1.1 Dátová architektúra**

### **ERD diagram**
Surové dáta sú usporiadané v relačnom modeli, ktorý je znázornený na **entitno-relačnom diagrame (ERD)**:

<p align="center">
  <img src="MovieLens_ERD.png" alt="ERD Schema">
  <br>
  <em>Obrázok 1 Entitno-relačná schéma AmazonBooks</em>
</p>

---
## **2 Dimenzionálny model**

Navrhnutý bol **hviezdicový model (star schema)**, pre efektívnu analýzu kde centrálny bod predstavuje faktová tabuľka **`fact_ratings`**, ktorá je prepojená s nasledujúcimi dimenziami:
- **`dim_movies`**: Uchováva údaje o filmoch, ako sú identifikátor filmu, jeho názov a rok vydania.
- **`dim_tags`**: Uchováva značky, ktoré môžu byť využité na analýzu sentimentu alebo triedenie filmov podľa ďalších kritérií.
- **`dim_genres`**: Obsahuje informácie o žánroch, vrátane ich identifikátorov a názvov.
- **`dim_users`**: Poskytuje demografické údaje o používateľoch, ako napríklad ich vek, kategóriu veku, pohlavie, poštové smerovacie číslo a povolanie.
- **`dim_date`**: Zahŕňa dáta súvisiace s hodnotiacimi dátumami, ako sú konkrétny deň, mesiac, rok, názvy mesiacov a dni v týždni.
- **`dim_time`**: Obsahuje detailné informácie o tagoch, ako sú samotné tagy, dátum a čas ich vytvorenia.








Štruktúra hviezdicového modelu je znázornená na diagrame nižšie. Diagram ukazuje prepojenia medzi faktovou tabuľkou a dimenziami, čo zjednodušuje pochopenie a implementáciu modelu.

<p align="center">
  <img src="star_schema.png" alt="Star Schema">
  <br>
  <em>Obrázok 2 Schéma hviezdy pre MovieLens</em>
</p>

---

## **3. ETL proces v Snowflake**
ETL proces sa skladal z troch hlavných krokov: `extrahovanie` (Extract), `transformácia` (Transform) a `načítanie` (Load). Tento postup bol implementovaný v Snowflake a jeho cieľom bolo pripraviť dáta zo staging vrstvy do viacdimenzionálneho modelu, ktorý je optimalizovaný na analýzu a vizualizáciu.

---
### **3.1 Extract (Extrahovanie dát)**
Dáta zo zdrojového datasetu vo formáte `.csv` boli najprv nahrané do Snowflake cez interné stage úložisko s názvom `my_stage`. Stage v Snowflake slúži ako dočasný priestor na import alebo export dát. Vytvorenie stage bolo realizované pomocou príkazu:

#### Príklad kódu:
```sql
CREATE OR REPLACE STAGE snail_stage;
```
Do stage boli následne nahrané súbory obsahujúce údaje o knihách, používateľoch, hodnoteniach, zamestnaniach a úrovniach vzdelania. Tieto dáta boli následne importované do staging tabuliek prostredníctvom príkazu `COPY INTO`. Pre každú tabuľku bol použitý podobný príkaz:

```sql
CREATE OR REPLACE
!!!!!!EŠTE TREBA DOPÍSAŤ KÓD!!!!!!
```

V prípade nekonzistentných záznamov bol použitý parameter `ON_ERROR = 'CONTINUE'`, ktorý umožnil pokračovať v procese aj v prípade výskytu chýb, bez jeho prerušenia.

---
