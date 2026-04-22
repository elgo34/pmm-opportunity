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
