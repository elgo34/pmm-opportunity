# Changelog

Toutes les évolutions notables de `pmm-opportunity` sont documentées ici.

Le format s'inspire de [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
et ce projet suit le [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

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

[0.1.0]: https://github.com/pictarine/pmm-opportunity/releases/tag/v0.1.0
