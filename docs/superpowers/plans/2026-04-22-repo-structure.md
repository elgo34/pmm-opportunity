# Repo structure & documentation Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Augmenter le README, créer CONTRIBUTING.md, intégrer un protocole de recherche itérative dans SKILL.md et sourcing-rules.md, bumper la version en 0.3.0.

**Architecture:** Repo markdown-only. Pas de code, pas de tests automatisés. Chaque tâche = modification de fichiers + vérification manuelle (lecture) + commit. Pas de TDD applicable — les étapes de vérification consistent à relire le fichier modifié pour confirmer la cohérence.

**Tech Stack:** Markdown, git, Claude Code (Edit, Write, Read, Bash)

---

## File Map

| Fichier | Action | Rôle |
|---|---|---|
| `README.md` | Modify | +3 sections, renommage Installation, tip Deep Research |
| `CONTRIBUTING.md` | Create | Guide de contribution interne |
| `skills/pmm-opportunity/SKILL.md` | Modify | +protocole de recherche itérative (steps 3 & 4) |
| `skills/pmm-opportunity/references/sourcing-rules.md` | Modify | +section "Recherche itérative" |
| `.claude-plugin/plugin.json` | Modify | Version 0.2.0 → 0.3.0 |
| `.claude-plugin/marketplace.json` | Modify | Version 0.2.0 → 0.3.0 |
| `CHANGELOG.md` | Modify | Entrée [0.3.0] |

---

### Task 1 : README — renommer Installation + ajouter tip Deep Research

**Files:**
- Modify: `README.md`

- [ ] **Step 1 : Lire le fichier**

```bash
# Vérifier la ligne exacte de la section Installation
grep -n "## Installation" README.md
```

Expected output : `25:## Installation` (numéro approximatif)

- [ ] **Step 2 : Renommer la section**

Trouver `## Installation` et le remplacer par `## Installation dans Cowork`.

- [ ] **Step 3 : Ajouter le tip Deep Research**

Ajouter ce bloc **à la fin de la section `## Installation dans Cowork`**, juste avant la section `## Comment le déclencher` :

```markdown
> **Tip Deep Research** — Pour une couverture sources maximale, lance le skill depuis Claude.ai en activant le mode **Deep Research** avant d'invoquer une sous-commande. Le skill bénéficie automatiquement du multi-pass autonome de recherche web.
```

- [ ] **Step 4 : Vérifier**

Lire `README.md` — confirmer que :
- `## Installation dans Cowork` est présent (plus `## Installation`)
- Le tip Deep Research apparaît avant `## Comment le déclencher`

- [ ] **Step 5 : Commit**

```bash
git add README.md
git commit -m "docs(readme): rename Installation section + add Deep Research tip"
```

---

### Task 2 : README — ajouter la section Liste des skills

**Files:**
- Modify: `README.md`

- [ ] **Step 1 : Localiser le point d'insertion**

La section `## Liste des skills` doit s'insérer **après `## À qui il s'adresse`** et **avant `## Installation dans Cowork`**.

```bash
grep -n "## À qui il s'adresse\|## Installation dans Cowork" README.md
```

- [ ] **Step 2 : Insérer la section**

Ajouter ce bloc entre `## À qui il s'adresse` et `## Installation dans Cowork` :

```markdown
## Liste des skills

| Skill | Description | Sous-commandes |
|---|---|---|
| `pmm-opportunity` | Framework d'évaluation et priorisation d'opportunités produit (marché photo US) | `/opportunity`, `/frame`, `/segment`, `/score`, `/challenge`, `/blind-spots` |
```

- [ ] **Step 3 : Vérifier**

Lire `README.md` — confirmer que la table apparaît entre `## À qui il s'adresse` et `## Installation dans Cowork`.

- [ ] **Step 4 : Commit**

```bash
git add README.md
git commit -m "docs(readme): add Liste des skills section"
```

---

### Task 3 : README — ajouter la section Contribution

**Files:**
- Modify: `README.md`

- [ ] **Step 1 : Localiser le point d'insertion**

La section `## Contribution` doit s'insérer **avant `## Auteur`**.

```bash
grep -n "## Auteur" README.md
```

- [ ] **Step 2 : Insérer la section**

Ajouter ce bloc juste avant `## Auteur` :

```markdown
## Contribution

Voir [CONTRIBUTING.md](CONTRIBUTING.md) pour les conventions de contribution, le versioning et le process de review interne.

```

- [ ] **Step 3 : Vérifier**

Lire `README.md` — confirmer que la section `## Contribution` apparaît avant `## Auteur`.

- [ ] **Step 4 : Commit**

```bash
git add README.md
git commit -m "docs(readme): add Contribution section"
```

---

### Task 4 : Créer CONTRIBUTING.md

**Files:**
- Create: `CONTRIBUTING.md`

- [ ] **Step 1 : Créer le fichier**

Créer `CONTRIBUTING.md` à la racine avec le contenu suivant :

```markdown
# Contribuer à pmm-opportunity

## Qui peut contribuer

PMs et collaborateurs Pictarine avec accès au repo GitHub privé.

## Quoi modifier

| Fichier | Quand le toucher |
|---|---|
| `skills/pmm-opportunity/SKILL.md` | Règles absolues, routing des sous-commandes, comportement général du skill |
| `references/framework-6-etapes.md` | Détail opérationnel des 6 étapes (matrice d'axes, segmentation, JTBD, etc.) |
| `references/scoring-grid.md` | Critères ou pondérations de la grille de scoring |
| `references/sourcing-rules.md` | Règles de sourcing, fair use, anti-hallucination, protocole itératif |
| `references/sources-list.md` | Nouvelles sources à explorer systématiquement |
| `references/output-format.md` | Structure et format du livrable |
| `references/tone-and-posture.md` | Posture, ton, règles de communication avec le PM |

## Versioning

Ce repo suit [Semantic Versioning](https://semver.org/) :

- **PATCH** (`0.2.x`) — correction d'un comportement, ajout/retrait d'une source, fix d'une règle existante
- **MINOR** (`0.x.0`) — nouvelle règle, nouveau fichier de référence, nouveau routing, nouveau protocole
- **MAJOR** (`x.0.0`) — refonte du framework, breaking change sur les sous-commandes ou la structure du livrable

À chaque release : mettre à jour `version` dans `.claude-plugin/plugin.json` ET `.claude-plugin/marketplace.json`, et ajouter une entrée dans `CHANGELOG.md`.

## Process de contribution

1. Créer une branche : `fix/<description>` ou `feat/<description>`
2. Modifier les fichiers concernés
3. Mettre à jour `CHANGELOG.md` (section `[Unreleased]` ou entrée versionnée directement)
4. Ouvrir une Pull Request — reviewer : Elyes Gannoun
5. Merge → bump de version dans `plugin.json` et `marketplace.json` → tag git

## Conventions de commit

```
feat(scoring): ajouter critère d'analyse concurrentielle
fix(sourcing): corriger règle de quota fair use Reddit
docs(references): mettre à jour sources-list avec Crunchbase
docs(readme): ajouter exemple d'invocation /frame
```

Format : `type(scope): description en minuscules`

Types : `feat` / `fix` / `docs` / `refactor`
Scopes courants : `skill`, `scoring`, `sourcing`, `references`, `readme`, `framework`
```

- [ ] **Step 2 : Vérifier**

Lire `CONTRIBUTING.md` — confirmer que les 5 sections sont présentes et cohérentes avec les conventions déjà en place dans `CHANGELOG.md`.

- [ ] **Step 3 : Commit**

```bash
git add CONTRIBUTING.md
git commit -m "docs: add CONTRIBUTING.md"
```

---

### Task 5 : SKILL.md — ajouter le protocole de recherche itérative

**Files:**
- Modify: `skills/pmm-opportunity/SKILL.md`

- [ ] **Step 1 : Localiser le point d'insertion**

Le protocole s'insère dans la section `## Sources à explorer systématiquement`, après la liste des sources existantes et avant `## Ton et posture`.

```bash
grep -n "## Sources à explorer\|## Ton et posture" skills/pmm-opportunity/SKILL.md
```

- [ ] **Step 2 : Ajouter le protocole**

Ajouter ce bloc **à la fin de la section `## Sources à explorer systématiquement`**, juste avant `## Ton et posture` :

```markdown
### Protocole de recherche itérative (steps 3 & 4)

Pour les étapes de recherche intensive (step 3 : opportunity framing, step 4 : scoring), ne pas se limiter à une passe unique. Dérouler le protocole suivant :

1. **Recherche initiale large** — `WebSearch` sur le sujet principal et les segments identifiés. Collecter les 5-8 premiers résultats pertinents.
2. **Fetch des sources prometteuses** — `WebFetch` sur les 3-5 URLs les plus solides (rapports, pages concurrents, app store listings, articles spécialisés).
3. **Analyse des gaps** — Identifier explicitement : quels segments ou critères ne sont pas couverts par les sources collectées ? Quels angles (pricing, social listening, TAM, avis stores) manquent ?
4. **Requêtes de raffinement** — Lancer de nouvelles `WebSearch` ciblées sur les gaps identifiés (ex. `"[concurrent] pricing US 2025"`, `"[catégorie] reddit complaints"`, `"[segment] photo gifts US market size"`).
5. **Fetch complémentaire** — `WebFetch` sur les nouvelles URLs identifiées au step 4.
6. **Arrêt de la collecte** — Stopper quand les nouvelles requêtes renvoient des sources déjà vues ou des données redondantes. Ne pas chercher l'exhaustivité — chercher la couverture des angles clés.

**Tracer les gaps résiduels** : toute zone non couverte après le protocole doit être listée dans "Limites et zones non couvertes" du livrable, avec la raison (source payante, donnée non publique, segment trop niche pour avoir des données US publiées).

**Si le PM utilise Deep Research** (mode Claude.ai) : le protocole itératif est exécuté automatiquement par Claude avant que le skill reçoive les résultats. Dans ce cas, sauter les steps 1-5 du protocole manuel et traiter les résultats fournis comme une collecte déjà enrichie.
```

- [ ] **Step 3 : Vérifier**

Lire `skills/pmm-opportunity/SKILL.md` sections `## Sources à explorer systématiquement` et `## Ton et posture` — confirmer que le protocole est inséré entre les deux, sans casser la structure.

- [ ] **Step 4 : Commit**

```bash
git add skills/pmm-opportunity/SKILL.md
git commit -m "feat(skill): add iterative research protocol for steps 3 & 4"
```

---

### Task 6 : sourcing-rules.md — ajouter la section recherche itérative

**Files:**
- Modify: `skills/pmm-opportunity/references/sourcing-rules.md`

- [ ] **Step 1 : Localiser le point d'insertion**

La nouvelle section s'insère **avant `## Ordre de préférence des sources`** (dernière section du fichier).

```bash
grep -n "## Ordre de préférence" skills/pmm-opportunity/references/sourcing-rules.md
```

- [ ] **Step 2 : Ajouter la section**

Insérer ce bloc juste avant `## Ordre de préférence des sources` :

```markdown
## Recherche itérative — règles de collecte

Le protocole de recherche itérative (défini dans `SKILL.md`) produit plusieurs vagues de sources. Les règles suivantes s'appliquent à chaque vague :

- **Chaque source fetchée compte comme une passe de vérification** — si le `WebFetch` retourne un contenu incohérent avec le résumé `WebSearch`, ne pas insérer la donnée. Relancer une recherche sur une source alternative.
- **Ne pas sur-indexer la première vague** — les résultats des premières requêtes sont souvent les plus mainstream. Les requêtes de raffinement (step 4 du protocole) atteignent des sources plus spécialisées et souvent plus crédibles.
- **Pas de doublon de source** — si deux résultats pointent vers le même rapport ou la même étude, une seule citation dans le livrable. Consolider, ne pas dupliquer.
- **Tracer les requêtes de recherche utilisées** — pour audibilité, noter dans la section "Limites" du livrable les requêtes `WebSearch` clés utilisées lors du step 4 (raffinement). Cela permet au PM de reproduire ou d'approfondir la collecte.

```

- [ ] **Step 3 : Vérifier**

Lire `skills/pmm-opportunity/references/sourcing-rules.md` — confirmer que la section est insérée avant `## Ordre de préférence des sources` et cohérente avec les règles existantes.

- [ ] **Step 4 : Commit**

```bash
git add skills/pmm-opportunity/references/sourcing-rules.md
git commit -m "feat(sourcing): add iterative research rules section"
```

---

### Task 7 : Bump version 0.2.0 → 0.3.0 + CHANGELOG

**Files:**
- Modify: `.claude-plugin/plugin.json`
- Modify: `.claude-plugin/marketplace.json`
- Modify: `CHANGELOG.md`

- [ ] **Step 1 : Bumper plugin.json**

Dans `.claude-plugin/plugin.json`, remplacer `"version": "0.2.0"` par `"version": "0.3.0"`.

- [ ] **Step 2 : Bumper marketplace.json**

Dans `.claude-plugin/marketplace.json`, remplacer `"version": "0.2.0"` par `"version": "0.3.0"` (dans l'entrée du plugin dans le tableau `plugins`).

- [ ] **Step 3 : Ajouter l'entrée CHANGELOG**

Dans `CHANGELOG.md`, ajouter cette entrée **en tête du fichier** (après le titre et le préambule, avant `## [0.2.0]`) :

```markdown
## [0.3.0] — 2026-04-22

Documentation et protocole de recherche itérative.

### Added

- **CONTRIBUTING.md** : guide de contribution interne — fichiers modifiables, conventions semver, process de PR, conventions de commit
- **Protocole de recherche itérative** dans `SKILL.md` (section "Sources à explorer systématiquement") : multi-pass WebSearch + WebFetch pour les steps 3 & 4, avec détection de gaps et arrêt de collecte raisonné
- **Règles de collecte itérative** dans `references/sourcing-rules.md` : pas de doublon de source, traçabilité des requêtes de raffinement, consigne sur la première vague mainstream
- **Note Deep Research** dans `SKILL.md` : si le PM active Deep Research (Claude.ai), le skill saute le protocole manuel et traite les résultats comme une collecte enrichie

### Changed

- `README.md` : section `## Installation` renommée `## Installation dans Cowork`
- `README.md` : ajout section `## Liste des skills` (table extensible)
- `README.md` : ajout section `## Contribution` (lien vers CONTRIBUTING.md)
- `README.md` : ajout tip Deep Research dans `## Installation dans Cowork`

### Why

Session de refactoring documentaire 2026-04-22 : structuration du repo pour le partage interne Pictarine, et formalisation du comportement de recherche itérative (auparavant implicite) en règle explicite dans le skill et les références.

```

Ajouter aussi le lien de comparaison en bas du fichier :

```markdown
[0.3.0]: https://github.com/pictarine/pmm-opportunity/releases/tag/v0.3.0
```

- [ ] **Step 4 : Vérifier**

Lire `CHANGELOG.md` tête de fichier — confirmer que `[0.3.0]` est bien la première entrée.
Lire `.claude-plugin/plugin.json` et `.claude-plugin/marketplace.json` — confirmer `"version": "0.3.0"`.

- [ ] **Step 5 : Commit + tag**

```bash
git add .claude-plugin/plugin.json .claude-plugin/marketplace.json CHANGELOG.md
git commit -m "chore(release): bump version to 0.3.0"
git tag v0.3.0
```

---

## Self-Review

**Couverture du spec :**

| Requirement spec | Tâche |
|---|---|
| Renommer `## Installation` → `## Installation dans Cowork` | Task 1 |
| Ajouter `## Liste des skills` | Task 2 |
| Ajouter `## Contribution` | Task 3 |
| Créer `CONTRIBUTING.md` | Task 4 |
| Protocole recherche itérative dans SKILL.md (Option 1) | Task 5 |
| Protocole recherche itérative dans sourcing-rules.md (Option 1) | Task 5 + 6 |
| Tip Deep Research dans README (Option 2) | Task 1 |
| Note Deep Research dans SKILL.md (Option 2) | Task 5 |
| Bump version (MINOR — nouvelle règle) | Task 7 |
| .gitignore — aucune modification (déjà complet) | — |
| Licence — aucune modification (Proprietary confirmé) | — |

**Placeholders :** aucun — chaque step contient le contenu exact à insérer.

**Cohérence :** les chemins de fichiers sont identiques dans toutes les tâches. Le numéro de version `0.3.0` est cohérent entre plugin.json, marketplace.json et CHANGELOG.md.
