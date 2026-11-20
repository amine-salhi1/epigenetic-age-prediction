# Prédiction de l'âge épigénétique (méthylation de l'ADN)

Notebook unique : `epigenetic_age.ipynb` (Google Colab, CPU, ~20 minutes ; les données sont téléchargées automatiquement).

Horloge épigénétique dans la continuité de la compétition Epiclock : prédire l'âge d'une personne à partir de la méthylation de son ADN. Régression en grande dimension (beaucoup plus de sites CpG que d'échantillons), transformation de l'âge de Horvath, présélection des CpG **refaite dans chaque pli** (pas de fuite), ElasticNet / Lasso / gradient boosting / ensemble, validation croisée imbriquée, métrique principale : **MAE en années**. Un contrôle avec des âges mélangés au hasard vérifie l'absence de fuite.

## Données

Jeu public **GSE40279** (Hannum et al., 2013, base GEO du NCBI) : 656 échantillons de sang, 19 à 101 ans, puce Illumina 450k (~485 000 CpG). Le notebook le télécharge, retire les CpG avec plus de 5 % de valeurs manquantes et garde les 50 000 plus variables (filtre non supervisé, sans utiliser l'âge).

## Résultats (validation croisée à 5 plis)

| Modèle | MAE (ans) | RMSE | Pearson r |
|---|---|---|---|
| Référence : âge moyen | 11,91 | 14,73 | – |
| **ElasticNet** | **4,13** | **5,68** | **0,923** |
| Lasso | 4,13 | 5,68 | 0,923 |
| Gradient boosting | 4,71 | 6,24 | 0,906 |
| Ensemble | 4,21 | 5,68 | 0,923 |

- Les modèles linéaires régularisés divisent l'erreur par près de 3 par rapport à la référence ; le gradient boosting, qui ne sait pas extrapoler aux âges extrêmes, fait moins bien.
- L'horloge finale n'utilise que **156 CpG** ; le plus important (cg16867657) est situé dans le gène **ELOVL2**, le marqueur d'âge le plus connu de la littérature.
- Contrôle anti-fuite réussi : avec des âges mélangés, le modèle ne bat pas la moyenne (MAE 12,96 contre 11,91 ans).

## Lancer

Ouvrir le notebook dans Google Colab (ou en local après `pip install -r requirements.txt`) et tout exécuter.
