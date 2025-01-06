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
- **`dim_movies`**: Obsahuje informácie o filmoch ako napríklad: id filmu, názov a rok vydania
- **`dim_tags`**: Obsahuje značky (tags), ktoré môžu slúžiť na analýzu nálad alebo na dodatočné triedenie filmov.
- **`dim_genres`**: Obsahuje informácie o žánroch, čiže id žánru a názov
- **`dim_users`**: Obsahuje demografické údaje o používateľoch, ako sú vek, vekové kategórie, pohlavie, PSČ a povolanie.
- **`dim_date`**: Obsahuje údaje o hodnotiacich dátumoch, ako sú deň, mesiac, rok, názvy mesiacov a dni v týždni.
- **`dim_time`**: Obsahuje podrobné informácie o tag-och, ako napríklad: tagy, dátum a čas vytvorenia.








Štruktúra hviezdicového modelu je znázornená na diagrame nižšie. Diagram ukazuje prepojenia medzi faktovou tabuľkou a dimenziami, čo zjednodušuje pochopenie a implementáciu modelu.

<p align="center">
  <img src="https://github.com/JKabathova/AmazonBooks-ETL/blob/master/star_schema.png" alt="Star Schema">
  <br>
  <em>Obrázok 2 Schéma hviezdy pre AmazonBooks</em>
</p>

---
