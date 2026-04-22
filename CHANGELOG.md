# Changelog

Toutes les évolutions notables de `pmm-opportunity` sont documentées ici.

Le format s'inspire de [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
et ce projet suit le [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.3.0] — 2026-04-22

Documentation et protocole de recherche itérative.

### Added

- **CONTRIBUTING.md** : guide de contribution interne — fichiers modifiables, conventions semver, process de PR, conventions de commit
- **Protocole de recherche itérative** dans `SKILL.md` (section "Sources à explorer systématiquement") : multi-pass WebSearch + WebFetch pour les étapes 3 & 4, avec détection de gaps et arrêt de collecte raisonné
- **Règles de collecte itérative** dans `references/sourcing-rules.md` : pas de doublon de source, traçabilité des requêtes de raffinement, consigne sur la première vague mainstream
- **Note Deep Research** dans `SKILL.md` : si le PM active Deep Research (Claude.ai), le skill saute le protocole manuel et traite les résultats comme une collecte enrichie

### Changed

- `README.md` : section `## Installation` renommée `## Installation dans Cowork`
- `README.md` : ajout section `## Liste des skills` (table extensible)
- `README.md` : ajout section `## Contribution` (lien vers CONTRIBUTING.md)
- `README.md` : ajout tip Deep Research dans `## Installation dans Cowork`

### Fixed

- `SKILL.md` : terminologie `(steps 3 & 4)` → `(étapes 3 & 4)` dans le protocole itératif
- `SKILL.md` : ajout cross-référence aux règles anti-hallucination dans le protocole
- `sourcing-rules.md` : cross-référence `## Vérifiabilité des liens`, section canonique "Limites et zones non couvertes", remplacement de "crédibles" par "pertinentes pour les angles de niche"

### Why

Session de refactoring documentaire 2026-04-22 : structuration du repo pour le partage interne Pictarine, et formalisation du comportement de recherche itérative (auparavant implicite) en règle explicite dans le skill et les références.

## [0.2.0] — 2026-04-20

Méthode de segmentation v1.0 → **v1.1** : matrice d'axes 2D obligatoire avant toute segmentation nommée. Grille de scoring inchangée (reste en v1.0).

### Added

- **Règle absolue 7** dans `SKILL.md` : matrice d'axes 2D explicite avant segmentation nommée (default *qui* × *quand/pourquoi*), toute case non instanciée listée avec statut `hors scope` / `non couvert` / `à investiguer`
- **Étape 2a** dans `references/framework-6-etapes.md` : construction de la matrice d'axes, axes default pour gifting, axes alternatifs par catégorie, template de matrice, pièges à éviter, exemple reconstitué (run storybook 2026-04-20)
- Scission de l'étape 2 en **2a (matrice)** + **2b (segmentation nommée)** — chaque segment nommé pointe explicitement vers la case de matrice qu'il instancie
- **Block 3.0 "Matrice d'axes"** obligatoire dans le format de livrable (`references/output-format.md`), en tête de la section Segmentation
- **4e question de challenge au Step 5** : interception dédiée sur la matrice (case oubliée, mal nommée, mal statuée)
- **Mention versioning "Méthode de segmentation : v1.1"** en en-tête du block 3 du livrable, distincte de la grille de scoring v1.0
- Amendement Step 6 pour vérifier les cases `❓ non couvert` et `🔍 à investiguer` de la matrice lors du blind-spot hunting
- Garde-fou de sortie : "Matrice d'axes manquante = livrable invalide" dans les garde-fous du `SKILL.md`

### Why

Run storybook 2026-04-20 (analyse d'opportunité sur produit AI-generated children's book US) : segment **"Occasion-driven parent gift"** (Mother's Day, Father's Day) absent de la segmentation initiale, détecté en post-scoring par le PM. Analyse racine : segmentation faite sur un seul axe (acheteur × âge enfant), sans matrice 2D explicite destinataire × trigger. Ce patch rend le garde-fou structurel plutôt que comportemental.

### Breaking changes

Aucun breaking côté invocation du skill (mêmes sous-commandes, mêmes prompts). Les livrables produits avant 2026-04-20 sont en `Méthode de segmentation : v1.0` (implicite) et ne doivent pas être comparés naïvement à un livrable v1.1.

## [0.1.0] — 2026-04-20

Version initiale du plugin — framework d'évaluation et priorisation d'opportunités produit sur le marché photo US, à destination des PMs Pictarine.

### Added

- Skill principal `pmm-opportunity` avec 6 sous-commandes : `/opportunity`, `/frame`, `/segment`, `/score`, `/challenge`, `/blind-spots`
- Framework en 6 étapes : cadrage, segmentation, opportunity framing, scoring, challenge, blind spots
- Grille de scoring v1.0 à 5 critères pondérés (Market Opportunity ×1, Switching Readiness ×2, Urgency ×1.5, Frequency ×1, Saturation ×1)
- Règles de sourcing strictes : US only, WebFetch obligatoire avant insertion, 3 étiquettes obligatoires (fait sourcé / observation auteur / hypothèse à tester)
- Fair use quotes : max 40 mots, attribution systématique
- Protocole sources payantes : demander accès PM, sinon `non couvert`
- Checkpoints automatiques après chaque étape + option `--resume`
- Gestion des échecs réseau : retry 3× avec backoff, interruption si échecs en série
- Anti-hallucination : WebFetch obligatoire avant insertion de toute URL, marquage `URL non vérifiée` si échec
- Trois destinations de livrable : page Notion, fichier .md local, conversation
- Stamp de version de la grille dans chaque livrable
- Edge cases traités : `/score` et `/challenge` orphelins, `/frame` sur sujet ultra-cadré
- README avec cheat sheet des sous-commandes et exemples d'invocation

### Design notes

- Architecture : un seul skill avec routing interne (pas de commands legacy)
- Pas de persistance du contexte Notion entre runs (demandé à chaque invocation, skippable)
- Pas de stockage des runs précédents
- Pondérations de la grille figées (pas d'override PM)
- Checkpoint étape 2 (segmentation) non bloquant : le PM challenge tout en étape 5
- Tutoiement, français pour l'analyse, citations sources conservées en anglais
- Livrable : concis et impactant, pas de borne de mots
- Ce plugin remplace l'ancien skill `pmm-market-partner:pmm-opportunities`

[0.3.0]: https://github.com/pictarine/pmm-opportunity/releases/tag/v0.3.0
[0.2.0]: https://github.com/pictarine/pmm-opportunity/releases/tag/v0.2.0
[0.1.0]: https://github.com/pictarine/pmm-opportunity/releases/tag/v0.1.0
