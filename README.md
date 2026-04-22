# pmm-opportunity

Plugin Cowork à destination des PMs Pictarine pour évaluer et prioriser une opportunité produit sur le marché photo US, selon un framework structuré, sourcé et auditable.

## À quoi il sert

Passer d'une intuition ou d'un signal à une conviction défendable en squad, sans tomber dans le débat "bonne idée / mauvaise idée". Le plugin déroule un framework en 6 étapes, centré sur les besoins utilisateurs et les facteurs marché, qui :

- cadre le périmètre d'une opportunité (produit, feature, verticale)
- segmente le marché cible (psychographique, démographique, comportemental)
- qualifie le JTBD, les alternatives et les failure signals de chaque segment
- score chaque segment sur 5 critères pondérés, avec rationale sourcé par cellule
- challenge le classement avec le PM
- identifie les blind spots (segments qui "devraient acheter mais n'achètent pas")

Le plugin ne donne **jamais** de recommandation d'action — il produit un livrable que le PM utilise pour trancher.

## À qui il s'adresse

Product Managers de Pictarine qui pilotent des sujets sur le marché photo américain : impression photo, photo books, wall art, prints, cadeaux photo, et verticales adjacentes (stationery, home decor, gifting, print-on-demand).

## Liste des skills

| Skill | Description | Sous-commandes |
|---|---|---|
| `pmm-opportunity` | Framework d'évaluation et priorisation d'opportunités produit (marché photo US) | `/opportunity`, `/frame`, `/segment`, `/score`, `/challenge`, `/blind-spots` |

## Installation dans Cowork

Depuis l'app Cowork, ouvre le fichier `pmm-opportunity.plugin` et valide l'installation. Le plugin est autonome — aucune configuration MCP ou hook n'est requise à l'installation.

À **chaque run**, le skill te demandera (tu peux laisser vide) :
- L'URL Notion de la page "Missions des squads Pictarine" pour ancrer l'analyse
- Toute autre page Notion de contexte stratégique (roadmap, OKRs, contraintes)

Pas de persistance : le skill ne stocke aucune URL entre runs. Cela te permet de cibler un contexte différent à chaque analyse.

> **Tip Deep Research** — Pour une couverture sources maximale, lance le skill depuis Claude.ai en activant le mode **Deep Research** avant d'invoquer une sous-commande. Le skill bénéficie automatiquement du multi-pass autonome de recherche web.

## Comment le déclencher

Le plugin contient un seul skill, `pmm-opportunity`, qui s'active automatiquement sur des formulations naturelles ou via sous-commandes :

Formulations naturelles FR :
- "analyse l'opportunité sur…"
- "priorise ce sujet"
- "score cette idée"
- "faut-il qu'on attaque ce segment"
- "on pense lancer X, est-ce que ça vaut le coup"
- "opportunity scoring sur…"

Sous-commandes explicites :
- `/opportunity [sujet]` — framework complet, étapes 1 à 6
- `/frame [sujet]` — étapes 1 à 3 (catégorie, segmentation, JTBD + alternatives)
- `/segment [sujet]` — étape 2 uniquement
- `/score` — applique l'étape 4 sur une segmentation existante
- `/challenge` — étape 5 sur un scoring déjà produit
- `/blind-spots [sujet]` — étape 6 uniquement

### Cheat sheet — quand utiliser quelle sous-commande

| Situation | Commande | Exemple d'invocation |
|---|---|---|
| Je démarre un sujet from scratch, je veux tout | `/opportunity` | `/opportunity lancement wall art dans photo books workflow` |
| J'ai juste besoin de cadrer + segmenter + framer, pas encore scorer | `/frame` | `/frame digital frames pour 55+` |
| Je veux juste une segmentation d'un marché | `/segment` | `/segment cadeaux photo Gen Z` |
| J'ai déjà une segmentation valide, je veux scorer | `/score` | `/score` puis coller la segmentation |
| J'ai un scoring fait par mon équipe, je veux le challenger | `/challenge` | `/challenge` puis coller le tableau |
| Je veux juste identifier des segments qu'on rate | `/blind-spots` | `/blind-spots photo books US` |
| Mon run a été interrompu, je veux reprendre | `/opportunity --resume [fichier]` | `/opportunity --resume ~/.pmm-opportunity-run-2026-04-20-1430.md` |

### Ce que le plugin ne fait pas

- Pas de recommandation d'action — le PM tranche toujours
- Pas de plan GTM, pas de messaging, pas de positioning pur — hors cadre, le skill stoppe
- Pas d'analyse hors marché US — sources strictement US uniquement
- Pas d'invention de sources — si une donnée n'est pas trouvable, elle est marquée `non couvert`

### Coexistence avec l'ancien skill

Ce plugin est conçu pour **remplacer** le skill `pmm-market-partner:pmm-opportunities`. Après installation de `pmm-opportunity`, désinstalle l'ancien pour éviter les collisions sur les déclencheurs naturels.

## Règle d'or

Chaque fait, chiffre, citation, observation est accompagné d'un lien cliquable et d'une date de collecte. Aucune extrapolation, aucune estimation "à la louche", aucune donnée inventée. Si une donnée manque, elle est marquée "non couvert" — jamais fabriquée.

## Limites

Le plugin couvre exclusivement le **marché américain** avec des sources US strictes (aucune source non-US, même pour contextualiser). Il ne produit pas de plan GTM, pas de messaging, pas de positioning pur — si la demande sort du cadre, le skill signale qu'il n'est pas fait pour ça et stoppe. À toi de choisir quel autre outil utiliser.

Le livrable est rédigé en français, avec les **citations de sources conservées en anglais** (fidélité aux verbatims).

## Contribution

Voir [CONTRIBUTING.md](CONTRIBUTING.md) pour les conventions de contribution, le versioning et le process de review interne.

## Auteur

Elyes Gannoun — Pictarine
