# Grille de scoring — 5 critères pondérés

**Version de la grille : `v1.0`**

Chaque livrable produit par ce skill doit mentionner la version de la grille utilisée (ex. "Grille scoring : v1.0"). Si la grille évolue (pondérations, critères, échelles), la version est bumpée et les livrables précédents restent identifiables comme pré-nouvelle-version — évitant toute comparaison naïve entre scorings incompatibles.

Grille utilisée à l'étape 4 du framework. Chaque segment est scoré sur les 5 critères. Chaque cellule produit :

1. un score **1, 2 ou 3** (pas de demi-niveau)
2. un **rationale** écrit en 2 à 4 lignes
3. **au moins une source cliquable et datée**
4. une mention `low confidence` si la source est insuffisante

## Les 5 critères

### 1. Market Opportunity — ×1

**Ce qu'on mesure** : taille et momentum de croissance de l'audience cible sur le marché US.

| Score | Définition |
|---|---|
| 1 — Low | Audience petite ou niche, faible fréquence d'usage, tendance décroissante |
| 2 — Medium | Taille correcte, demande stable, pas de momentum clair |
| 3 — High | Large audience, forte fréquence d'usage, momentum de croissance clair |

**Sources type** : Keypoint Intelligence, Statista (US only), IDC, Euromonitor, rapports de cabinets d'analyste, Census Bureau, ACS, Google Trends US.

### 2. Switching Readiness — ×2 (critère le plus pondéré)

**Ce qu'on mesure** : à quel point les alternatives actuelles échouent à satisfaire le segment. Plus elles échouent, plus le segment est prêt à switcher.

| Score | Définition |
|---|---|
| 1 — Low | Les alternatives fonctionnent bien, peu de frustration observable |
| 2 — Medium | Solutions partielles avec gaps clairs, frustration modérée |
| 3 — High | Alternatives fondamentalement cassées pour ce besoin, frustration forte et généralisée |

**Sources type** : failure signals de l'étape 3 (Reddit, TikTok, avis stores, Trustpilot, presse spécialisée). NPS publics des concurrents si disponibles.

**Note** : la pondération ×2 reflète que le switching est le signal le plus prédictif de l'appétit marché. Ne pas compenser un faible score ici par de forts scores ailleurs.

### 3. Urgency to Act — ×1.5

**Ce qu'on mesure** : force du trigger qui pousse le segment à agir maintenant vs plus tard.

| Score | Définition |
|---|---|
| 1 — Low | Les users vivent avec la douleur, aucun push pour la résoudre |
| 2 — Medium | Les users ont l'intention d'agir mais reportent régulièrement |
| 3 — High | Les users se sentent obligés d'agir immédiatement (deadline, événement, pic émotionnel) |

**Sources type** : threads Reddit / TikTok autour d'événements déclencheurs (mariage, naissance, décès, déménagement, anniversaires), search trends saisonniers, calendrier gifting US.

### 4. Frequency of Trigger — ×1

**Ce qu'on mesure** : à quelle fréquence le besoin ré-apparaît dans la vie du segment.

| Score | Définition |
|---|---|
| 1 — Low | Une fois dans une vie ou très rare (ex. livre de mariage) |
| 2 — Medium | Quelques fois par an (ex. holidays, anniversaires majeurs) |
| 3 — High | Mensuel ou continu (ex. retirage de prints, partage familial) |

**Sources type** : études de comportement d'achat photo US (Keypoint Intelligence PMA, InfoTrends), cohort data publique, enquêtes de consommation (Nielsen, Circana).

**Piège à éviter** : ne pas confondre fréquence d'achat chez un concurrent avec fréquence du trigger sous-jacent. Le trigger peut être mensuel mais la conversion annuelle.

### 5. Saturation Risk — ×1 (inversé)

**Ce qu'on mesure** : niveau de concurrence sur le segment. **Critère inversé** : plus la concurrence est faible, plus le score est haut.

| Score | Définition |
|---|---|
| 1 — Low | Nombreux substituts forts, barrières de switching élevées — dur à gagner |
| 2 — Medium | Concurrence partielle ou substituts, pas de leader écrasant |
| 3 — High | Pas de player fort sur ce segment spécifique — white space clair |

**Sources type** : share of voice publicitaire (Meta Ad Library, Google Ads Transparency), mentions concurrentielles sur Reddit / TikTok, analyse des positions SERP US sur requêtes du segment, Crunchbase pour mouvements M&A.

**Attention à la granularité** : un marché saturé au niveau catégorie peut avoir des segments entiers non servis. Scorer au niveau segment, pas catégorie.

## Calcul du score total pondéré

```
Total = (Market × 1) + (Switching × 2) + (Urgency × 1.5) + (Frequency × 1) + (Saturation × 1)
```

| Borne | Valeur |
|---|---|
| Score minimum (tous critères à 1) | 6.5 |
| Score médian (tous critères à 2) | 13.0 |
| Score maximum (tous critères à 3) | 19.5 |

## Règles opérationnelles

- Toujours afficher le **tableau détaillé** avec rationales et sources, pas juste le total
- Afficher la **méthode de calcul** sous le tableau pour audit
- Si ≥ 2 cellules sont `low confidence`, signaler que le score total est `score indicatif — confiance limitée`
- **Ne jamais arrondir** un score entre deux niveaux. Choisir 1, 2 ou 3 et défendre. Si impossible, `low confidence`.
- Pour deux segments à scores proches (écart < 1 point), ne pas trancher le ranking — les afficher ex-æquo et demander au PM de trancher via l'étape 5

## Exemple de cellule scorée correcte

> **Switching Readiness — Segment "Millennial parents gifters" — Score : 3 — Pondéré : 6**
>
> Rationale : les avis App Store US sur Shutterfly sur les 12 derniers mois concentrent les plaintes sur la lenteur de l'éditeur mobile et les erreurs de livraison sur les mugs et photo blocks. Mixbook n'a pas de mobile-first workflow. Chatbooks satisfait uniquement le cas "monthly memories" et échoue sur les gifts customisés multi-occasions.
>
> Sources :
> - [Shutterfly App Store reviews US, consultés 2026-04-17](https://apps.apple.com/us/app/shutterfly-prints-cards-gifts/id499221956) (`fait sourcé`)
> - [r/ShutterflyUsers thread 2025-11, 237 upvotes](https://reddit.com/...) (`fait sourcé`)
> - [Mixbook blog — mobile roadmap 2025](https://blog.mixbook.com/...) consulté 2026-04-17 (`fait sourcé`)
