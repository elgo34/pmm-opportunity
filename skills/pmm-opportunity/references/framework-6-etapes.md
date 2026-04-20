# Framework — 6 étapes détaillées

Ce fichier détaille chaque étape du framework `pmm-opportunity`. Le SKILL.md orchestre, ce fichier précise les livrables attendus, les questions à poser et les pièges à éviter.

**Méthode de segmentation : v1.1** (bump lié à l'introduction de l'étape 2a — matrice d'axes obligatoire). Toute version précédente des livrables est antérieure à ce garde-fou et ne doit pas être comparée naïvement à un livrable v1.1.

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

## Étape 2a — Matrice d'axes (OBLIGATOIRE avant toute segmentation nommée)

**Règle absolue 7 du SKILL.md.** Aucune segmentation nommée ne peut être produite avant d'avoir construit cette matrice.

**Objectif** : garantir qu'on balaye l'espace des segments possibles avant de les nommer, pour ne pas rater de segments orthogonaux.

### Principe

Un segment se définit au croisement d'au moins deux axes. Nommer des segments "au fil de la plume" (un par persona supposé) fait systématiquement rater les cases orthogonales. La matrice 2D force à **scanner l'espace** avant de le peupler.

### Axes par défaut

**Axe 1 — "Qui"** : destinataire / acheteur / utilisateur final. Distinguer si nécessaire :

- destinataire du produit (qui reçoit le cadeau)
- acheteur (qui paie)
- utilisateur (qui consomme)

Pour un produit gifting, ces trois peuvent être différentes personnes. L'axe "qui" peut alors être décomposé.

**Axe 2 — "Quand / pourquoi"** : trigger d'achat. Typologie de triggers :

- **Calendaire** (date fixe) : Mother's Day, Father's Day, Christmas, Valentine's Day, anniversaires, rentrée scolaire
- **Milestone / événement** : naissance, mariage, diplôme, déménagement, décès
- **Rituel quotidien ou récurrent** : bedtime, weekend, vacances
- **Impulsion / envie** : découverte produit, inspiration social media, coup de cœur

### Axes alternatifs selon la catégorie

La matrice par défaut *qui × trigger* convient aux catégories gifting. Pour d'autres catégories, adapter :

- **Catégorie utilitaire** (ex. prints à la demande) : *qui* × *usage final* (archivage / affichage / partage)
- **Catégorie feature** (ex. AI layout auto) : *qui* × *volume d'input* (10 photos / 100 / 500)
- **Catégorie abonnement** (ex. Chatbooks monthly) : *qui* × *fréquence souhaitée*

Choisir les axes en cohérence avec le JTBD anticipé. Si tu hésites, construire deux matrices alternatives et choisir celle qui fait émerger le plus de cases actionnables.

### Livrable attendu de l'étape 2a

Un tableau visuel (markdown table ou grille) avec :

1. **Les axes explicités** (intitulé de l'axe + valeurs couvertes)
2. **Chaque case** marquée avec un statut :
   - ✅ **Instanciée** : un segment nommé adresse cette case → ce segment sera détaillé à l'étape 2b
   - ⚪ **Hors scope** : case volontairement exclue (avec justification d'une ligne)
   - ❓ **Non couvert** : case pertinente mais sans donnée suffisante pour instancier
   - 🔍 **À investiguer** : case potentielle, demander au PM si on l'instancie ou on la blind-spot
3. **Justification courte pour toute case non instanciée** — pourquoi on ne segmente pas là.

### Exemple (catégorie storybook enfant, run 2026-04-20 corrigé)

| Destinataire ↓ / Trigger → | Rituel quotidien | Milestone bébé | Milestone enfant | Occasion calendaire adulte | Activité loisir |
|---|---|---|---|---|---|
| Enfant 0-2 | ⚪ Hors scope (pas de rituel à cet âge) | ✅ Segment C Newborn | ⚪ Hors scope | ⚪ Hors scope | ⚪ Hors scope |
| Enfant 3-6 | ✅ Segment A Bedtime | ⚪ Hors scope | ✅ inclus dans Segment B | ❓ Non instancié | ✅ Segment E Co-Create |
| Enfant 4-8 | ⚪ | ⚪ | ❓ Segment D Educational (deal-breaker AI text) | ❓ Non instancié | ✅ inclus dans E |
| Parent / adulte caregiver | ⚪ Hors scope (pas destinataire du livre lecture) | ⚪ | ⚪ | 🔍 **Segment F potentiel (Mother's Day, Father's Day)** | ⚪ |

La case **Parent × Occasion calendaire** aurait été marquée 🔍 *à investiguer* → obligation d'en parler explicitement au PM avant de skipper. C'est exactement ce qui manquait dans le run initial.

### Pièges à éviter en étape 2a

- **Fusionner "héros du contenu" et "destinataire"** : un produit peut avoir l'enfant comme héros mais être destiné au parent. Bien séparer.
- **Matrice avec un seul axe réel** : si la "matrice" est en fait une liste 1D (ex. par âge uniquement), elle ne sert pas son rôle.
- **Matrice trop fine** (ex. 7 valeurs × 7 valeurs = 49 cases) : non actionnable. Viser 3-5 valeurs par axe.
- **Cases instanciées sans label de segment** : si une case est marquée ✅, elle doit pointer vers un nom de segment de l'étape 2b.
- **Passer l'étape sous prétexte de "c'est évident"** : le garde-fou existe précisément pour les cas où ça semble évident.

## Étape 2b — Segmentation nommée

**Objectif** : produire le draft de segments à partir des cases ✅ de la matrice 2a, en croisant les trois angles classiques.

**Les trois angles à croiser obligatoirement** (sur chaque segment nommé) :

1. **Psychographique** — motivations, valeurs, occasions (ex. "Memory keepers émotionnels", "Sharers sociaux pragmatiques", "Gifters dernière minute")
2. **Démographique** — âge, revenus, situation familiale, géographie US (ex. "Millennial parents, HHI 75k+, suburbs")
3. **Comportemental** — fréquence d'achat, canal, trigger d'achat (ex. "Achat annuel post-vacances", "Trigger anniversaire/mariage")

**Livrable attendu** : pour chaque segment (viser 3 à 6 segments, pas plus) :

- Nom court et mémorable
- Pointeur explicite vers la case de la matrice 2a qu'il instancie
- Caractéristiques distinctives sur les 3 angles
- Taille estimée ou "non couvert" si pas de source solide
- **Sources cliquables datées** pour chaque caractéristique distinctive
- Pourquoi ce segment est pertinent pour la catégorie

**Pas de checkpoint bloquant à cette étape.** Le draft de segmentation est produit puis **le skill enchaîne directement sur l'étape 3** sans demander validation intermédiaire. Tout le challenge PM se fait en étape 5 sur le livrable global — y compris le challenge sur la matrice 2a.

Raison : éviter les interruptions intempestives qui cassent le flow d'analyse. Le PM voit la segmentation ET la matrice dans le livrable final et challenge alors (ou demande un rerun `/segment` ciblé si la segmentation est fausse à la racine).

**Pièges à éviter** :

- Segments trop larges ("les femmes 35-55") → pas actionnable
- Segments qui se recouvrent fortement → refaire
- Segments inventés sans source sur les caractéristiques → refaire
- Un segment par persona Pictarine sans challenger la nomenclature interne
- **Segment nommé sans correspondance dans la matrice 2a** → violation de l'étape 2a

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

**Objectif** : construire la conviction du PM, pas lui imposer un ranking. **C'est LE moment où le PM challenge toute l'analyse** — matrice d'axes et segmentation incluses, puisqu'il n'y a pas de checkpoint intermédiaire aux étapes 2a/2b.

**Déroulé** :

1. Présenter le livrable global (matrice d'axes + segmentation + scoring + ranking)
2. Demander explicitement via AskUserQuestion, en **quatre questions distinctes** :
   - "Sur quel(s) segment(s) as-tu une conviction différente du scoring ? Pourquoi ?"
   - "La segmentation elle-même te paraît-elle juste, ou un angle te semble manquant/faux ?"
   - "Y a-t-il un facteur que la grille ne capte pas et qui devrait peser dans ta décision ?"
   - **"Regarde la matrice d'axes (block 3.0). Y a-t-il une case que j'ai oubliée, mal nommée ou mal statuée (instanciée / hors scope / non couvert / à investiguer) ?"** ← question dédiée au garde-fou 2a, dernière chance d'intercepter un segment orthogonal manquant
3. Pour chaque divergence : creuser **la raison** — information supplémentaire du PM, biais dans le scoring, facteur non capté par la grille, case de matrice mal traitée
4. Documenter les divergences dans le livrable final, sans les résoudre artificiellement. Si la segmentation est contestée à la racine (y compris via la matrice), proposer au PM de relancer `/segment` ciblé plutôt que de patcher.

**Ce qu'il faut éviter absolument** :

- Défendre le ranking contre le PM (ce n'est pas le rôle du skill)
- Modifier silencieusement les scores pour satisfaire le PM (transparence > alignement)
- Accepter une divergence sans creuser (le "pourquoi" est le livrable)
- Skipper la question 4 sur la matrice d'axes

**Format de documentation des divergences** :

> **Segment [X]** — scoring IA : [total] / rang [N]. Conviction PM : [description courte]. Raison : [explication du PM]. Statut : [non résolu / intégré comme observation auteur / à re-tester].

> **Matrice d'axes** — case [Destinataire × Trigger] : statut initial [X]. Challenge PM : [description]. Action : [instanciée en nouveau segment F / confirmée hors scope / passée en blind spot V2].

## Étape 6 — Blind spots

**Objectif** : identifier les segments absents des données de commandes actuelles — "des gens qui devraient acheter mais n'achètent pas".

**Protocole** :

1. Demander au PM s'il peut fournir des accès ou extraits de données internes (commandes, cohortes, retargeting)
2. Si oui : croiser les segments identifiés à l'étape 2b avec les segments réels dans les données, **et vérifier qu'aucune case `❓ non couvert` ou `🔍 à investiguer` de la matrice 2a n'a été oubliée**
3. Si non : raisonner sur signaux externes :
   - données démographiques US (Census, American Community Survey)
   - search trends (Google Trends US)
   - mouvement de tendances (Pinterest Predicts, TikTok trending hashtags)
   - segments ciblés par les concurrents dans leur pub (Meta Ad Library, Google Ads Transparency)

**Livrable attendu** : liste de 2 à 5 blind spots potentiels, chacun avec :

- Nom et brève description
- **Si issu d'une case `🔍 à investiguer` de la matrice 2a : le mentionner explicitement**
- Pourquoi ce segment devrait a priori acheter (lié au JTBD d'un segment voisin)
- Pourquoi on pense qu'il n'achète pas (hypothèse sourcée ou marquée comme telle)
- Test à faire pour confirmer ou infirmer (interview, analyse cohorte, campagne pilote)

**Étiqueter clairement** chaque blind spot comme `hypothèse à tester` — ce ne sont jamais des `faits sourcés`.
