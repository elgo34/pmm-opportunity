# Framework — 6 étapes détaillées

Ce fichier détaille chaque étape du framework `pmm-opportunity`. Le SKILL.md orchestre, ce fichier précise les livrables attendus, les questions à poser et les pièges à éviter.

## Étape 1 — Définir la catégorie

**Objectif** : clarifier sans ambiguïté le périmètre de l'analyse avant tout travail de fond.

**Questions à se poser** :

- S'agit-il d'une catégorie entière (ex. "Photo Books US") ou d'une feature précise dans une catégorie (ex. "AI layout auto pour Photo Books") ?
- Quelles catégories sont **exclues** du périmètre (bornes claires) ?
- Quelles sont les catégories adjacentes dont il faudra parler pour situer, sans les analyser ?

**Livrable attendu** :

- Une phrase de périmètre : "L'analyse couvre **[catégorie]** sur le marché **US** pour l'audience **[macro/micro]**. Sont exclus : [X, Y]."
- Liste des 3-5 catégories voisines pour contextualiser (ex. si Photo Books → stationery, yearbooks, scrapbooking)

**Pièges à éviter** :

- Mélanger catégorie (ce que le user achète) et use case (pourquoi il l'achète)
- Confondre catégorie Pictarine avec catégorie marché (Pictarine peut avoir sa nomenclature interne ; aligner sur la nomenclature marché US publique)

## Étape 2 — Segmentation

**Objectif** : produire un draft de segments du marché cible, croisant trois angles.

**Les trois angles à croiser obligatoirement** :

1. **Psychographique** — motivations, valeurs, occasions (ex. "Memory keepers émotionnels", "Sharers sociaux pragmatiques", "Gifters dernière minute")
2. **Démographique** — âge, revenus, situation familiale, géographie US (ex. "Millennial parents, HHI 75k+, suburbs")
3. **Comportemental** — fréquence d'achat, canal, trigger d'achat (ex. "Achat annuel post-vacances", "Trigger anniversaire/mariage")

**Livrable attendu** : pour chaque segment (viser 3 à 6 segments, pas plus) :

- Nom court et mémorable
- Caractéristiques distinctives sur les 3 angles
- Taille estimée ou "non couvert" si pas de source solide
- **Sources cliquables datées** pour chaque caractéristique distinctive
- Pourquoi ce segment est pertinent pour la catégorie

**Pas de checkpoint bloquant à cette étape.** Le draft de segmentation est produit puis **le skill enchaîne directement sur l'étape 3** sans demander validation intermédiaire. Tout le challenge PM se fait en étape 5 sur le livrable global.

Raison : éviter les interruptions intempestives qui cassent le flow d'analyse. Le PM voit la segmentation proposée dans le livrable final et la challenge alors (ou demande un rerun `/segment` ciblé si la segmentation est fausse à la racine).

**Pièges à éviter** :

- Segments trop larges ("les femmes 35-55") → pas actionnable
- Segments qui se recouvrent fortement → refaire
- Segments inventés sans source sur les caractéristiques → refaire
- Un segment par persona Pictarine sans challenger la nomenclature interne

## Étape 3 — Opportunity framing

**Objectif** : pour chaque segment validé, qualifier le job, les alternatives et où ça casse.

**Pour chaque segment, produire** :

### JTBD — Jobs To Be Done

Formuler le job **du point de vue du segment**, en une phrase avec structure figée :

> "Quand [situation/trigger], je veux [motivation], pour que [résultat souhaité]."

Exigence **absolue** : le JTBD doit être **ancré concrètement** dans :

- **le segment** — trigger et motivation spécifiques à CE segment, pas génériques à la catégorie
- **l'audience** — vocabulaire et réalité de vie de l'audience (parents, millennials, HHI spécifique, contexte géographique US)
- **le job concret** — action physique ou émotionnelle précise, pas une abstraction ("créer un souvenir tangible partageable" > "avoir de belles photos")

Exemple aligné : "Quand je rentre de vacances en Floride avec 400 photos sur mon iPhone et que ma mère me rappelle qu'elle n'a rien reçu depuis Thanksgiving, je veux lui envoyer un livre photo fini en moins de 20 minutes sans revoir chaque page, pour qu'elle ait un objet tangible à poser sur la table basse avant son prochain appel FaceTime."

Exemple trop générique (à éviter) : "Quand j'ai des photos, je veux les imprimer, pour qu'elles durent."

Sourcer le JTBD : au moins une interview utilisateur publique, un thread Reddit représentatif, ou un verbatim presse — US uniquement.

### Alternatives

**Crucial : aller au-delà des concurrents directs.** Lister toutes les solutions que le segment utilise aujourd'hui pour faire le job, y compris :

- concurrents directs de la catégorie
- concurrents indirects (ex. digital frames au lieu de prints)
- solutions non-produit (ex. "je ne fais rien", "j'envoie sur WhatsApp")
- solutions hors catégorie (ex. pour un photo book : album Instagram, screenshots dans Notes)

Pour chaque alternative : nom, mécanisme, pourquoi ça marche (ou pas) pour ce segment.

### Failure signals

**Où et comment les alternatives échouent pour ce segment**, sourcés par social listening. Sources privilégiées :

- threads Reddit (r/photography, r/weddingplanning, r/beyondthebump, r/ParentingInBulk, r/Frugal…)
- vidéos TikTok avec hashtags concurrents
- avis App Store / Google Play datés
- forums spécialisés (ex. Dealerscope, PhotoShelter community)
- Discord communautaires
- Trustpilot, Sitejabber

Format pour chaque failure signal :

> "[Quote ou paraphrase courte]" — [Source cliquable, date] — alternative concernée : [X] — ce que ça révèle sur le job : [...]

**Viser 3 à 5 failure signals par segment**, avec une variété de sources.

## Étape 4 — Scoring

**Objectif** : scorer chaque segment validé sur les 5 critères pondérés, avec rationale et source par cellule.

**Grille complète dans `scoring-grid.md`.** Résumé opérationnel :

Pour chaque segment, remplir un tableau :

| Critère | Pondération | Score (1/2/3) | Rationale | Source cliquable datée |
|---|---|---|---|---|
| Market Opportunity | ×1 | | | |
| Switching Readiness | ×2 | | | |
| Urgency to Act | ×1.5 | | | |
| Frequency of Trigger | ×1 | | | |
| Saturation Risk (inversé) | ×1 | | | |

**Calcul du score total pondéré** :

`Total = (Market × 1) + (Switching × 2) + (Urgency × 1.5) + (Frequency × 1) + (Saturation × 1)`

Échelle : min = 6.5, max = 19.5.

**À présenter systématiquement** :

- Le tableau rempli par segment
- Le score total pondéré et la position dans le classement
- La méthode de calcul explicitement (pour audit)
- Les cellules marquées `low confidence` et pourquoi

**Règles absolues** :

- Pas de score sans rationale écrit
- Pas de rationale sans source cliquable datée
- Si source insuffisante → `low confidence` et alerte au PM
- Pas d'arrondi "au mieux" — si c'est entre 2 et 3, choisir et défendre

## Étape 5 — Challenge

**Objectif** : construire la conviction du PM, pas lui imposer un ranking. **C'est LE moment où le PM challenge toute l'analyse** — segmentation incluse, puisqu'il n'y a pas de checkpoint intermédiaire à l'étape 2.

**Déroulé** :

1. Présenter le livrable global (segmentation + scoring + ranking)
2. Demander explicitement via AskUserQuestion, en trois questions distinctes :
   - "Sur quel(s) segment(s) as-tu une conviction différente du scoring ? Pourquoi ?"
   - "La segmentation elle-même te paraît-elle juste, ou un angle te semble manquant/faux ?"
   - "Y a-t-il un facteur que la grille ne capte pas et qui devrait peser dans ta décision ?"
3. Pour chaque divergence : creuser **la raison** — information supplémentaire du PM, biais dans le scoring, facteur non capté par la grille
4. Documenter les divergences dans le livrable final, sans les résoudre artificiellement. Si la segmentation est contestée à la racine, proposer au PM de relancer `/segment` ciblé plutôt que de patcher.

**Ce qu'il faut éviter absolument** :

- Défendre le ranking contre le PM (ce n'est pas le rôle du skill)
- Modifier silencieusement les scores pour satisfaire le PM (transparence > alignement)
- Accepter une divergence sans creuser (le "pourquoi" est le livrable)

**Format de documentation des divergences** :

> **Segment [X]** — scoring IA : [total] / rang [N]. Conviction PM : [description courte]. Raison : [explication du PM]. Statut : [non résolu / intégré comme observation auteur / à re-tester].

## Étape 6 — Blind spots

**Objectif** : identifier les segments absents des données de commandes actuelles — "des gens qui devraient acheter mais n'achètent pas".

**Protocole** :

1. Demander au PM s'il peut fournir des accès ou extraits de données internes (commandes, cohortes, retargeting)
2. Si oui : croiser les segments identifiés à l'étape 2 avec les segments réels dans les données
3. Si non : raisonner sur signaux externes :
   - données démographiques US (Census, American Community Survey)
   - search trends (Google Trends US)
   - mouvement de tendances (Pinterest Predicts, TikTok trending hashtags)
   - segments ciblés par les concurrents dans leur pub (Meta Ad Library, Google Ads Transparency)

**Livrable attendu** : liste de 2 à 5 blind spots potentiels, chacun avec :

- Nom et brève description
- Pourquoi ce segment devrait a priori acheter (lié au JTBD d'un segment voisin)
- Pourquoi on pense qu'il n'achète pas (hypothèse sourcée ou marquée comme telle)
- Test à faire pour confirmer ou infirmer (interview, analyse cohorte, campagne pilote)

**Étiqueter clairement** chaque blind spot comme `hypothèse à tester` — ce ne sont jamais des `faits sourcés`.
