# Format du livrable

Structure identique quelle que soit la destination (Notion / .md local / conversation). Seule la forme d'encodage change.

## Structure obligatoire — 8 blocs

### 1. Synthèse exécutive (5 lignes max)

Top-of-page. Capture :

- Le sujet analysé + périmètre
- Les 2-3 segments les mieux scorés
- Le ou les blind spots saillants
- Les zones `non couvert` majeures

Ne **jamais** y glisser une recommandation d'action. Interdiction formelle de commencer par "Nous recommandons…" ou "Il faudrait…".

### 2. Cadrage

- Catégorie retenue (étape 1)
- Périmètre et exclusions
- Catégories voisines pour contexte
- Inputs du PM reformulés : sujet, niveau, origine, contexte business, objet du test

### 3. Segmentation

Une sous-section par segment retenu, format :

```
### Segment — [Nom court]

**Psychographique** : [description] ([Source, date])
**Démographique** : [description] ([Source, date])
**Comportemental** : [description] ([Source, date])
**Taille estimée** : [X users / non couvert]
**Pourquoi pertinent** : [1-2 lignes]

Étiquettes : `fait sourcé` où applicable.
```

### 4. Opportunity framing par segment

Pour chaque segment :

```
### [Nom segment] — Opportunity framing

**JTBD** : "Quand [trigger], je veux [motivation], pour que [résultat]."
(Source du JTBD : [lien, date])

**Alternatives utilisées aujourd'hui** :
| Alternative | Mécanisme | Pourquoi ça marche/pas | Source |
| ... | ... | ... | ... |

**Failure signals** :
- "[Quote]" — [Source, date] — alternative : [X] — révèle : [...]
- ...
```

Viser 3 à 5 failure signals par segment.

### 5. Scoring

Un tableau par segment + un récapitulatif global.

**Mention obligatoire en en-tête de la section** : `Grille scoring : v1.0` (ou version en vigueur au moment du run). Cette mention garantit que deux livrables produits avec des versions de grille différentes ne sont jamais comparés à tort.


**Tableau détaillé par segment** :

```
### Scoring — [Nom segment]

| Critère | Pondération | Score | Pondéré | Rationale | Source |
|---|---|---|---|---|---|
| Market Opportunity | ×1 | [1-3] | [val] | [2-4 lignes] | [lien, date] |
| Switching Readiness | ×2 | [1-3] | [val] | ... | ... |
| Urgency to Act | ×1.5 | [1-3] | [val] | ... | ... |
| Frequency of Trigger | ×1 | [1-3] | [val] | ... | ... |
| Saturation Risk (inv.) | ×1 | [1-3] | [val] | ... | ... |
| **Total pondéré** | | | **[total]** | | |

Méthode : Total = (M × 1) + (S × 2) + (U × 1.5) + (F × 1) + (Sat × 1). Range 6.5 → 19.5.
```

**Récapitulatif global** :

```
### Ranking

| Rang | Segment | Total pondéré | Confiance |
|---|---|---|---|
| 1 | ... | ... | haute / `low confidence` |
| 2 | ... | ... | ... |
```

### 6. Challenge du PM

```
### Zones de divergence PM / scoring IA

**[Segment X]** — scoring IA : [total] / rang [N].
Conviction PM : [description courte]
Raison : [explication]
Statut : [non résolu / intégré comme observation auteur / à re-tester]

[Répéter pour chaque divergence. S'il n'y en a pas : "Aucune divergence identifiée sur cette analyse."]
```

### 7. Blind spots identifiés

```
### Blind spots — `hypothèse à tester`

**[Nom blind spot 1]**
- Description : [...]
- Devrait acheter parce que : [...] (lié au JTBD de [segment voisin])
- Pense-t-on qu'il n'achète pas parce que : [...] (sourcé ou marqué `hypothèse à tester`)
- Test proposé : [interview / cohorte / pilote]

[Répéter pour chaque blind spot, viser 2 à 5]
```

### 8. Limites et zones non couvertes

Section courte mais obligatoire. Lister :

- Données manquantes critiques (ex. "TAM digital frames US 55+ — rapport payant, non accédé")
- Sources inaccessibles au moment du run (ex. "Meta Ad Library — erreur 503 le 2026-04-17")
- Hypothèses qui devraient être vérifiées par le PM
- Segments ou sous-catégories non traités par manque de temps

## Encodage selon destination

### Page Notion

- Créer une sous-page sous le parent fourni par le PM via `notion-create-pages`
- Titre : `Opportunity — [Sujet] — [YYYY-MM-DD]`
- Utiliser les blocs Notion natifs : `heading_1` pour les 8 blocs principaux, `heading_2` pour les segments, `table` pour les scorings
- Les liens doivent être de vrais liens Notion (pas du texte en markdown)
- Ajouter un toggle "Sources consultées" en fin de page listant tous les liens pour audit rapide

### Fichier .md local

- Créer dans le dossier de sortie de la session (workspace Cowork)
- Nom : `opportunity-[sujet-slug]-[YYYY-MM-DD].md`
- Markdown standard, tableaux en pipe syntax
- Liens en `[texte](url)`
- Coder les étiquettes en `code` inline pour lisibilité : `` `fait sourcé` ``

### Conversation

- Markdown dense dans la réponse
- Prévoir la lecture en app Cowork : pas de tableaux trop larges, préférer des listes quand > 5 colonnes
- Segments possiblement pliables via résumés si très longs — demander au PM s'il préfère tout ou synthétique

## Règles transverses

- **Timestamping** : mettre la date `YYYY-MM-DD` du run en en-tête du livrable
- **Auditabilité** : chaque chiffre doit être remontable à une URL et une date
- **Pas d'emojis** dans le livrable (sauf demande explicite du PM)
- **Concision et impact** : pas de borne de mots — le signal prime sur le volume. Chaque phrase porte une information. Si une section peut être coupée sans perte, la couper.
- **Langue** : analyse en français, **citations sources en anglais**, non traduites (fidélité au verbatim). Les titres, structure et commentaires sont en FR.
- **Format visuel** : mix prose dense + tableaux. Les tableaux sont réservés au scoring et aux comparaisons d'alternatives. Le reste (cadrage, JTBD, failure signals, challenge, blind spots) est en prose courte et percutante. Pas de puces sauf pour des listes factuelles de 2-5 items.
- **Contexte Notion** en en-tête du livrable :
  - Si chargé : "Contexte stratégique Pictarine : [titre page] — chargé à [timestamp]."
  - Si non fourni par le PM : "Contexte stratégique Pictarine : non chargé pour ce run (choix PM)."
