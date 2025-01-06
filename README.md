# DT_Mravec - MovieLens
Databázové Technológie - FINAL - Matias Mravec 

Tento repozitár obsahuje implementáciu ETL procesu v Snowflake, určenú na analýzu dát z datasetu MovieLens. Projekt sa sústreďuje na skúmanie používateľského správania a preferencií v čítaní prostredníctvom hodnotení kníh a demografických údajov. Vytvorený dátový model podporuje multidimenzionálnu analýzu a vizualizáciu kľúčových ukazovateľov.

---
## **1. Úvod a popis zdrojových dát**
Cieľom semestrálneho projektu je analyzovať dáta týkajúce sa kníh, používateľov a ich hodnotení. Táto analýza umožňuje identifikovať trendy v čitateľských preferenciách, najpopulárnejšie knihy a správanie používateľov.

Zdrojové dáta pochádzajú z Kaggle datasetu dostupného [tu](https://grouplens.org/datasets/movielens/). Dataset obsahuje osem hlavných tabuliek:
- `age_group`
- `genres`
- `genres_movies`
- `occupations`
- `ratings`
- `tags`
- `users`

Účelom ETL procesu bolo tieto dáta pripraviť, transformovať a sprístupniť pre viacdimenzionálnu analýzu.

---
