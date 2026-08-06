# Impact-ATT---MOXY-VALOXY

Pipeline NIRS (Python + R) comparant DPF fixe vs dynamique et régression OLS des canaux courts, sur deux protocoles (VALOXY isométrique, Oxymove concentrique/excentrique). Extraction de features (AUC, pics, pente, SmO2) et classification Random Forest en LOSO de l'intensité et de la phase de contraction.

## Résumé des traitements à utiliser d'après les résultats des analyses exploratoires

- **Prédiction du mode de contraction** (MOXY, concentrique/excentrique) : DPF dynamique + OLS + filtre passe-bas 1Hz
- **Prédiction de l'intensité** (VALOXY, 20/40/60% ; MOXY, 30/50%) : DPF dynamique + pas d'OLS + filtre passe-bas 1Hz + intervalle de 5-15s

## Points de vigilance

- **LOSO (Leave-One-Subject-Out)** utilisé pour toutes les évaluations : chaque sujet testé est totalement absent de l'entraînement, pour éviter toute fuite de données inter-sujets - à garder en tête si les accuracy semblent modestes, c'est le test le plus strict possible.
- **Normalisation z-score intra-sujet** appliquée avant classification (VALOXY) 
- Sujet 11 (MOXY) exclu des analyses utilisant l'ATT (mesure manquante).
- La sélection des canaux SmO2 est automatique (par géométrie réelle de la sonde) - vérifier la colonne `SmO2_Channels` avant d'interpréter ces features.

## Reproductibilité

Les chemins de fichiers (`BASE_ROOT`, `CHEMIN_DPF`, `chemin_fichier`, etc.) sont marqués `--- PARAMÈTRE ---` dans le code et doivent être adaptés à votre machine avant de relancer le pipeline.
