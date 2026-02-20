# Progress - Speed Dating Analysis

## Contexte du projet

Analyse du dataset speed dating de Columbia University (2002-2004, 21 waves).

**Objectif** : Comprendre ce qui mène deux personnes à accepter un second date ensemble.

**Dataset** : `data/input/Speed_Dating_Data.csv`
**Documentation** : `data/input/Speed+Dating+Data+Key.pdf`

---

## Definition of Done

### Par notebook
- [ ] Code s'exécute sans erreur (avec uv run python)
- [ ] Visualisations ont titre + labels axes + légende
- [ ] Captions explicatifs sous chaque visualisation (interprétation humaine)
- [ ] Mappings utilisés : pas de chiffres bruts (goal=1 → "Seemed like a fun night out")
- [ ] Statistiques descriptives claires (mean, median, std quand pertinent)
- [ ] Matrices corrélation avec interprétations
- [ ] Réponses aux questions du notebook documentées en markdown
- [ ] **PROGRESS.md mis à jour** après complétion du notebook

### Projet global
- [ ] Toutes les questions initiales traitées
- [ ] Règles de nettoyage appliquées et documentées
- [ ] Biais identifiés et documentés
- [ ] README à jour avec objectifs, questions et conclusions
- [ ] PROGRESS.md complet (décisions, insights, questions en suspens)
- [ ] data/MAPPINGS.json créé

---

## Questions à explorer

### Questions initiales (dataset description)
- [ ] Quels sont les attributs les moins désirables chez un partenaire masculin ? Diffèrent-ils pour un partenaire féminin ?
- [ ] Quelle importance les gens accordent-ils à l'attractivité vs son impact réel sur leurs décisions ?
- [ ] Les intérêts partagés sont-ils plus importants qu'une même origine ethnique ?
- [ ] Les gens peuvent-ils prédire avec précision leur propre valeur perçue sur le marché du dating ?
- [ ] Est-il préférable d'être le premier ou le dernier date de la soirée ?

### Questions additionnelles
- [ ] La saison (hiver/été/printemps/automne) a-t-elle une incidence sur l'attraction ?
- [ ] Les variations expérimentales influent-elles sur la décision ?
  - [ ] Budget (wave 12) : limitation à 50% de "yes"
  - [ ] "Different M.C." (waves 13-14) : signification et impact
  - [ ] Magazine/book (waves 18-21)
- [ ] Le niveau ou la thématique d'études (field) influe-t-il sur la décision ou le jugement du partenaire ?
- [ ] Le domaine de carrière influe-t-il sur les décisions ?
- [ ] Les hobbies/activités influent-ils sur le matching ?
- [ ] Biais de sélection Time2 : qui ne remplit pas le follow-up et pourquoi ?

---

## Règles de nettoyage (CRITIQUES)

### Validation données
1. **100 points** : Pour waves avec distribution 100 pts, **DROP les lignes si somme ≠ 100**
   - Concerne : attr1_1+sinc1_1+intel1_1+fun1_1+amb1_1+shar1_1 = 100
   - Et autres séries similaires (attr4_1, attr2_1, attr7_2, etc.)
2. **Pas d'imputation** : JAMAIS inventer des valeurs manquantes
3. **Justifier les drops** : documenter pourquoi chaque filtre est appliqué
4. **Valeurs manquantes légitimes** :
   - Exemple : `date_3` (Have you been on a date with any of your matches?) peut être NaN si la personne n'a pas eu de match → ne PAS drop
   - Identifier et documenter ces cas

### Mappings obligatoires

**Pas de chiffres bruts affichés** : toujours mapper vers labels humains.

Exemples :
- `goal=1` → "Seemed like a fun night out"
- `race=2` → "European/Caucasian-American"
- `field_cd=1` → "Law"
- `career_c=7` → "Banking/Consulting/Finance/Marketing/Business/CEO/Entrepreneur/Admin"
- `gender=0` → "Female", `gender=1` → "Male"

**Expliquer les échelles** :
- `sinc5_1` : que signifie le "5" (perceive by others) et le "1" (Time1/signup) ?
- Documenter pour chaque série d'attributs

### Normalisation
- Échelles 1-10 (waves 6-9) → normaliser vers 100 pour comparaison cross-waves si nécessaire

---

## Structure des notebooks

### 01_exploration_nettoyage.ipynb
**Objectif** : Comprendre les données, nettoyer, préparer pour analyses

- [ ] Chargement dataset, shape, colonnes, types
- [ ] Création mappings complets (goal, race, field_cd, career_c, date, go_out, etc.)
- [ ] Export mappings vers `data/MAPPINGS.json`
- [ ] Identifier waves et leurs caractéristiques (dates, échelles, variations)
- [ ] **Validation 100 points** : appliquer règle et drop lignes invalides
- [ ] Analyse valeurs manquantes :
  - Lesquelles sont normales (date_3, numdat_3, etc.) ?
  - Lesquelles indiquent problème de qualité ?
  - Patterns par wave, par genre, par variable
- [ ] **Biais sélection Time2** :
  - Profil des non-répondants Time2 (pas de follow-up = pas de matches envoyés)
  - Comparaison avec répondants (dec, attr_o, age, race, field, etc.)
  - Impact sur analyses Time2/Time3

### 02_analyse_variations_experimentales.ipynb
**Objectif** : Comprendre l'impact des variations expérimentales sur les décisions

- [ ] **"Different M.C."** (waves 13-14) :
  - Comparaison empirique avec waves 10-11 (similaires)
  - Différences structurelles (colonnes remplies, patterns de décision)
  - Hypothèses sur signification (Meeting Criteria, Matching Conditions, etc.)
- [ ] **Budget** (wave 12 vs 11) :
  - Limitation 50% "yes" oriente-t-elle les choix ?
  - Profil des personnes acceptées différent ?
- [ ] **Magazine/book** (waves 18-21) :
  - Impact sur décisions ou qualité d'interaction ?
- [ ] **Échelles différentes** :
  - Comparaison 1-10 vs 100 points
  - Besoin de normalisation ?

### 03_attributs_et_genre.ipynb
**Objectif** : Analyser les préférences d'attributs et différences par genre

- [ ] **Attributs désirables/indésirables par genre** :
  - Ce que cherchent hommes vs femmes (attr1_1 par gender)
  - Attributs les moins désirés (scores faibles)
- [ ] **Attractivité : perception vs réalité** :
  - Importance perçue (attr1_1) vs corrélation avec décision (dec)
  - Les gens surestiment-ils l'importance de l'attractivité ?
- [ ] **Auto-évaluation vs perception réelle** :
  - attr3_1 (self-rating) vs attr_o (partner rating)
  - attr5_1 (how others perceive me) vs attr_o (reality)
  - Par attribut et par genre
- [ ] **Matrices corrélation** :
  - 6 attributs (attr, sinc, intel, fun, amb, shar) vs dec
  - Corrélations croisées entre attributs
  - Interprétations claires (pas juste la matrice)

### 04_interets_demographiques.ipynb
**Objectif** : Analyser l'impact des facteurs démographiques et intérêts

- [ ] **Intérêts partagés vs même origine ethnique** :
  - int_corr (correlation interests) vs samerace
  - Quel facteur prédit mieux dec ?
  - Importance perçue (shar1_1) vs réelle
- [ ] **Field d'étude** :
  - field_cd impact sur probabilité de match
  - Certains fields plus/moins sélectifs ?
  - Préférences croisées (Law date Law ?)
- [ ] **Carrière** :
  - career_c impact sur décisions
  - Patterns similaires à field ?
- [ ] **Hobbies et activités** :
  - Sports, dining, museums, art, etc. (18 activités)
  - Lesquels corrèlent avec matching success ?
  - Différences par genre

### 05_facteurs_situationnels.ipynb
**Objectif** : Analyser les facteurs contextuels/situationnels

- [ ] **Position dans la soirée** :
  - order (1er date vs dernier) impact sur dec
  - Fatigue ? Serial position effect ?
- [ ] **Effet saison** :
  - Parser dates des waves
  - Hiver/printemps/été/automne
  - Patterns d'attraction différents ?
- [ ] **Autres facteurs situationnels** :
  - met (already met before) impact
  - Durée événement, nombre de participants

---

## Décisions de nettoyage prises

_À remplir au fur et à mesure_

**Exemple format :**
- `2026-02-02` : Dropped 234 rows où somme attributs ≠ 100 (waves 1-5, 10-21)
- `2026-02-02` : Gardé NaN pour date_3 car légitime si pas de match

---

## Mappings créés

**Statut** : Définis dans notebook 01, seront créés dans `data/MAPPINGS.json` après exécution.

Mappings inclus (voir notebook 01 pour détails complets) :

**Exemple format :**
```python
{
  "goal": {
    1: "Seemed like a fun night out",
    2: "To meet new people",
    3: "To get a date",
    4: "Looking for a serious relationship",
    5: "To say I did it",
    6: "Other"
  },
  ...
}
```

---

## Insights clés

_À remplir après chaque notebook_

### Notebook 01 : Exploration/nettoyage
- ...

### Notebook 02 : Variations expérimentales
- ...

### Notebook 03 : Attributs et genre
- ...

### Notebook 04 : Intérêts démographiques
- ...

### Notebook 05 : Facteurs situationnels
- ...

---

## Hypothèses "Different M.C."

_À remplir après analyse empirique waves 13-14_

**Hypothèses possibles :**
1. Meeting Criteria
2. Matching Conditions
3. Multiple Choice
4. Meeting Configuration

**Résultats analyse :**
- ...

---

## Questions en suspens

_À remplir au fur et à mesure_

**Exemple format :**
- Pourquoi certaines colonnes (undergra, mn_sat, tuition) ont beaucoup de NaN ?
- ...

---

## À faire

- [x] PROGRESS.md créé
- [x] Quick reference créé
- [x] Notebook 01 : Exploration/nettoyage (créé, **à exécuter**)
- [x] Notebook 02 : Variations expérimentales (créé, **à exécuter**)
- [ ] Notebook 03 : Attributs et genre
- [ ] Notebook 04 : Intérêts démographiques
- [ ] Notebook 05 : Facteurs situationnels
- [ ] README.md mis à jour
- [ ] Vérification finale (review sans exécution)

**État actuel** : Notebooks 01 et 02 créés. Ils doivent être exécutés pour générer `data/MAPPINGS.json` et `data/speed_dating_clean.csv`, puis remplis avec les insights.
