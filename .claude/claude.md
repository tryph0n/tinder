# Speed Dating Analysis

## Source de vérité
**→ Lis PROGRESS.md en priorité** (contexte complet, questions, DoD, état d'avancement)

## Règles NON-NÉGOCIABLES

1. **Pas d'imputation** de valeurs manquantes (jamais inventer des données)
2. **Validation 100 points** : DROP si somme ≠ 100 pour waves 1-5, 10-21
3. **Mappings obligatoires** : jamais de chiffres bruts affichés
   - `goal=1` → "Seemed like a fun night out"
   - `race=2` → "European/Caucasian-American"
   - Voir `data/MAPPINGS.json` pour tous les mappings
4. **Visualisations** : titre + labels axes + caption interprétative TOUJOURS
5. **Expliquer les échelles** : `sinc5_1` signifie quoi (5 = perception by others, 1 = Time1)

## Fichiers critiques

- **Specs complètes** : `PROGRESS.md`
- **Mappings** : `data/MAPPINGS.json`
- **Dataset nettoyé** : `data/speed_dating_clean.csv` (après exécution notebook 01)
- **Dataset original** : `data/input/Speed_Dating_Data.csv`
- **Documentation** : `data/input/Speed+Dating+Data+Key.pdf`

## Notebooks

1. `01_exploration_nettoyage.ipynb` - Chargement, mappings, validation, biais Time2
2. `02_analyse_variations_experimentales.ipynb` - Different M.C., budget, saison
3. `03_attributs_et_genre.ipynb` - Préférences, attractivité, auto-évaluation
4. `04_interets_demographiques.ipynb` - Intérêts, race, field, carrière, hobbies
5. `05_facteurs_situationnels.ipynb` - Position soirée, saison, contexte

## Commandes

- Exécution : `uv run python notebook.ipynb`
- Focus : **compréhension** > prédiction (pas de ML)
- Stats : matrices corrélation suffisent (pas de tests complexes)

## Philosophie

Simplicité > sophistication. KISS > YAGNI.
Le but : comprendre les données et répondre aux questions, pas impressionner avec des stats.
