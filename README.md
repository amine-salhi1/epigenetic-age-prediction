# Prédiction de l'âge épigénétique (méthylation de l'ADN)

Notebook unique : `epigenetic_age.ipynb`.

Horloge épigénétique dans la continuité de la compétition Epiclock : régression en grande dimension (beaucoup plus de sites CpG que d'échantillons), transformation de l'âge de Horvath, présélection des CpG **refaite dans chaque pli** (pas de fuite), ElasticNet / Lasso / gradient boosting / ensemble, validation croisée imbriquée, métrique principale : **MAE en années**. Un contrôle avec des âges mélangés au hasard vérifie l'absence de fuite.

## Résultats

<!-- Coller ici le tableau de la section 4, obtenu sur de vraies données. -->
