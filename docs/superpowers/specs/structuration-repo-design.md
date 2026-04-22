---
title: Repo structure & documentation — pmm-opportunity
date: 2026-04-22
status: approved
---

# Repo structure & documentation — pmm-opportunity

## Contexte

Plugin Claude Code interne Pictarine. Usage : PMs Pictarine qui évaluent et priorisent des opportunités produit sur le marché photo US. Distribution : repo GitHub privé Pictarine. Interfaces cibles : Claude Code CLI, Claude Desktop, Claude web (même système de plugins).

## Décisions de design

### 1. Organisation de dossiers — Approche A (statu quo + CONTRIBUTING.md)

**Structure retenue :**

```
.claude-plugin/          # métadonnées plugin (plugin.json, marketplace.json)
skills/
  pmm-opportunity/
    SKILL.md
    references/          # références spécifiques à ce skill
docs/
  superpowers/
    specs/               # design docs (dont ce fichier)
README.md
CHANGELOG.md
LICENSE
CONTRIBUTING.md          # nouveau
.gitignore
```

**Pourquoi cette structure :**
- Le dossier `skills/` peut accueillir des skills futurs (`skills/pmm-positioning/` etc.) sans refactoring.
- Les `references/` restent au niveau du skill — elles sont 100% spécifiques à `pmm-opportunity`. Remonter les références au niveau racine n'a de sens que si des références sont partagées entre skills.
- Pas de `docs/adr/` ni de structure complexe — rien à y mettre aujourd'hui.

**Alternatives écartées :**
- Approche B (ajout `docs/`) : overkill pour l'instant, aucun contenu à y mettre immédiatement.
- Approche C (references à la racine) : casse les chemins existants dans `SKILL.md`, migration non triviale, bénéfice nul tant que les références sont mono-skill.

### 2. README.md — augmentation (pas de réécriture)

**Modifications :**
1. Renommer `## Installation` → `## Installation dans Cowork`
2. Ajouter `## Liste des skills` (table extensible) après `## À qui il s'adresse`
3. Ajouter `## Contribution` avant `## Auteur`, pointant vers `CONTRIBUTING.md`

**Pourquoi augmenter plutôt que réécrire :** le README existant est bien structuré et couvre déjà l'essentiel (cheat sheet des sous-commandes, règle d'or, limites). Une réécriture ferait perdre du contenu utile sans gain.

### 3. CONTRIBUTING.md — nouveau fichier

**Contenu :**
- Tableau des fichiers modifiables avec leur rôle
- Conventions de versioning (semver : PATCH/MINOR/MAJOR avec exemples concrets)
- Process de contribution (branche → PR → merge → tag)
- Conventions de commit (feat/fix/docs + scope)
- Rappel : mettre à jour `plugin.json` et `CHANGELOG.md` à chaque release

**Pourquoi léger :** audience = PMs internes, pas des développeurs. Le fichier doit être lisible en 2 minutes.

### 4. .gitignore — aucune modification

Le `.gitignore` actuel couvre déjà tous les cas utiles pour un repo markdown-only :
- Artifacts de packaging (`*.plugin`, `*.zip`)
- OS et éditeurs
- Checkpoints de run (`.pmm-opportunity-run-*.md`)
- Secrets

Les specs `docs/superpowers/` sont **committées** volontairement — elles documentent les décisions de design, cohérent avec la philosophie du `CHANGELOG.md` qui trace déjà les "Why" de chaque version.

### 5. Intégration Deep Research

Deep Research est un mode d'interface Claude.ai — il n'est pas invocable comme outil depuis un SKILL.md. Les deux approches sont complémentaires et toutes deux retenues.

**Approche 1 — Émulation dans SKILL.md (recherche itérative multi-pass)**

Enrichir les étapes de recherche intensive (step 3 : opportunity framing, step 4 : scoring) avec un pattern explicite :
1. Recherche initiale large (`WebSearch`)
2. Fetch des 3-5 liens les plus prometteurs (`WebFetch`)
3. Analyse des gaps — quelles sources manquent, quels angles ne sont pas couverts
4. Requêtes de raffinement ciblées (`WebSearch`)
5. Fetch complémentaire sur les nouvelles sources identifiées

Ce pattern s'ajoute à la liste des sources à explorer dans `SKILL.md` (section "Sources à explorer systématiquement") et dans `references/sourcing-rules.md`. Il ne remplace pas les règles existantes — il les complète avec un protocole d'itération.

**Approche 2 — Documentation du workflow Deep Research en amont**

Ajouter dans le README une section (ou note dans `## Installation dans Cowork`) expliquant que le PM peut activer Deep Research dans Claude.ai avant d'invoquer le skill. Dans ce contexte, le skill bénéficie automatiquement du multi-pass autonome sans modification de ses instructions.

Documentation à ajouter : tip dans `## Installation dans Cowork` ou dans la cheat sheet des sous-commandes — "Pour une couverture sources maximale, lancer depuis Claude.ai en mode Deep Research."

### 6. Licence — Proprietary (inchangée)

Usage strictement interne Pictarine. La licence Proprietary actuelle est appropriée. Si le périmètre change (marketplace public, contribution externe), basculer vers MIT à ce moment-là.
