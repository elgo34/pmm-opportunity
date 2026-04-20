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

**Mention obligatoire en en-tête de la section** : `Méthode de segmentation : v1.1` (ou version en vigueur au moment du run). Cette mention garantit que deux livrables produits avec des méthodes de segmentation différentes ne sont jamais comparés à tort. La v1.1 impose le block 3.0 ci-dessous.

#### 3.0 Matrice d'axes (OBLIGATOIRE — règle absolue 7)

Sous-bloc en tête du bloc 3. Sans ce sous-bloc, le livrable n'est pas valide — voir `framework-6-etapes.md` étape 2a.

Format attendu :

```
### 3.0 Matrice d'axes

**Axes retenus** : [Axe 1 "qui" — valeurs couvertes] × [Axe 2 "quand/pourquoi" — valeurs couvertes]
**Justification du choix d'axes** : [1-2 lignes]

| [Axe 1] ↓ / [Axe 2] → | Val A2-1 | Val A2-2 | Val A2-3 | ... |
|---|---|---|---|---|
| Val A1-1 | ✅ [Nom segment] | ⚪ Hors scope ([raison]) | ❓ Non couvert | 🔍 À investiguer |
| Val A1-2 | ... | ... | ... | ... |

**Légende** :
- ✅ Instanciée : adressée par un segment nommé au bloc 3.1+
- ⚪ Hors scope : volontairement exclue, justification à côté
- ❓ Non couvert : pertinente mais manque de donnée pour instancier
- 🔍 À investiguer : à challenger avec le PM en étape 5 (question 4)
```

Toute case marquée ⚪, ❓ ou 🔍 doit avoir une **justification d'une ligne** dans la cellule ou juste après le tableau. La matrice figure dans le livrable final quelle que soit la destination (Notion / .md / conversation).

#### 3.1+ Segments nommés

Une sous-section par segment retenu, format :

```
### Segment — [Nom court]

**Case matrice** : [Axe1-val × Axe2-val] (pointeur vers le block 3.0)
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

### Challenge sur la matrice d'axes (block 3.0)

**Case [Axe1-val × Axe2-val]** — statut initial : [X]. Challenge PM : [description]. Action : [instanciée en nouveau segment / confirmée hors scope / passée en blind spot V2].

[Répéter pour chaque case contestée. S'il n'y en a pas : "Matrice confirmée par le PM."]
```

### 7. Blind spots identifiés

```
### Blind spots — `hypothèse à tester`

**[Nom blind spot 1]**
- Description : [...]
- Case matrice d'origine : [Axe1-val × Axe2-val] si issu d'une case `🔍 à investiguer`
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
- **Cases de la matrice 3.0 marquées `❓ non couvert`** — rappeler ici que ces cases restent à documenter

## Encodage selon destination

### Page Notion

- Créer une sous-page sous le parent fourni par le PM via `notion-create-pages`
- Titre : `Opportunity — [Sujet] — [YYYY-MM-DD]`
- Utiliser les blocs Notion natifs : `heading_1` pour les 8 blocs principaux, `heading_2` pour les segments, `table` pour les scorings **et pour la matrice 3.0**
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
- La matrice 3.0 doit rester lisible en conversation : si elle dépasse 5×5 cases, la scinder en sous-matrices thématiques

## Règles transverses

- **Timestamping** : mettre la date `YYYY-MM-DD` du run en en-tête du livrable
- **Versioning** : en tête du block 3, `Méthode de segmentation : v1.1` ; en tête du block 5, `Grille scoring : v1.0`. Les deux versions coexistent et évoluent indépendamment.
- **Auditabilité** : chaque chiffre doit être remontable à une URL et une date
- **Pas d'emojis** dans le livrable (sauf demande explicite du PM, **et sauf pour les codes de statut de la matrice 3.0 — ✅ ⚪ ❓ 🔍 — qui sont conventionnels**)
- **Concision et impact** : pas de borne de mots — le signal prime sur le volume. Chaque phrase porte une information. Si une section peut être coupée sans perte, la couper.
- **Langue** : analyse en français, **citations sources en anglais**, non traduites (fidélité au verbatim). Les titres, structure et commentaires sont en FR.
- **Format visuel** : mix prose dense + tableaux. Les tableaux sont réservés au scoring, aux comparaisons d'alternatives **et à la matrice d'axes 3.0**. Le reste (cadrage, JTBD, failure signals, challenge, blind spots) est en prose courte et percutante. Pas de puces sauf pour des listes factuelles de 2-5 items.
- **Contexte Notion** en en-tête du livrable :
  - Si chargé : "Contexte stratégique Pictarine : [titre page] — chargé à [timestamp]."
  - Si non fourni par le PM : "Contexte stratégique Pictarine : non chargé pour ce run (choix PM)."
