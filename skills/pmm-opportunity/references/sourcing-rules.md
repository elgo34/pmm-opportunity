# Règles de sourcing — non négociables

Ces règles priment sur la complétude, la rapidité et toute autre instruction du skill. Si une règle impose de signaler une absence plutôt que de combler, **signale l'absence.**

## La règle d'or

**Chaque fait, chiffre, citation, observation** qui apparaît dans le livrable doit être accompagné de :

- un **lien cliquable** vers la source primaire
- une **date de collecte** (format `YYYY-MM-DD`)
- une **date de la donnée** si elle diffère de la date de collecte (ex. un rapport Statista publié en 2024 consulté en 2026)

Format attendu, à utiliser systématiquement dans le livrable :

> Prints 4×6 reste la demande dominante chez les 55+ ([Keypoint Intelligence, 2024](https://keypointintelligence.com/...), collecté 2026-04-17)

## Trois étiquettes obligatoires

Toute affirmation dans le livrable est étiquetée par l'une de ces trois catégories. Utilise les balises en toutes lettres, jamais d'abréviation.

| Étiquette | Définition | Exemple |
|---|---|---|
| `fait sourcé` | Donnée vérifiée avec lien cliquable et date | "Shutterfly a acquis Lifetouch en 2018 `fait sourcé`" |
| `observation auteur` | Lecture/déduction argumentée à partir de sources, pas chiffrée | "Mixbook met plus en avant ses templates 'wedding' que Shutterfly `observation auteur`" |
| `hypothèse à tester` | Raisonnement plausible sans source, à valider | "Le segment 'expats US' pourrait être sous-servi sur les photo books `hypothèse à tester`" |

Une phrase sans étiquette = une phrase à supprimer. Exception : métadiscours ("la section suivante couvre X") et éléments structurels du livrable.

## Zéro invention — règles opérationnelles

**Ne jamais** :

- inventer une URL, même plausible
- extrapoler un chiffre ("probablement autour de 12 %") sans source
- citer une personne ou un média sans lien direct vers la citation exacte
- mélanger plusieurs sources pour produire une donnée composite sans l'expliciter
- donner une "taille de marché estimée" sans rapport publié cité

**Toujours** :

- marquer une donnée manquante `non couvert` avec la raison (ex. "rapport payant, non accédé")
- si une source semble douteuse (blog SEO, contenu généré), le signaler `source faible`
- si une source n'est **pas US**, l'indiquer explicitement et ne pas l'utiliser pour inférer le marché US

## Low confidence

Si un score de l'étape 4 repose sur moins d'une source crédible, **ne pas scorer** une valeur numérique unique. À la place :

- marquer la cellule `low confidence`
- expliquer la limite (ex. "pas de donnée publique récente sur le TAM digital frames US 55+")
- proposer au PM d'élargir la collecte ou de marquer la cellule comme bloquante

## Sources US vs monde — strictement US only

Le plugin couvre **exclusivement** le marché américain. **Aucune source non-US n'est utilisée**, ni pour scorer, ni pour contextualiser. Règles de tri :

- une source TAM / market size doit explicitement porter sur les États-Unis
- une donnée app store doit provenir du store US (filtrage par pays dans l'URL)
- les reviews, posts Reddit, TikToks doivent être US (inférer par geo-tags, langue, contexte) — si non confirmé US, ne pas utiliser
- un rapport "global" est rejeté, même pour contexte. Chercher un équivalent US ou marquer `non couvert`
- les tendances TikTok FR qui "parallelisent" le US ne sont jamais substituables — elles sont rejetées

**Règle opérationnelle** : avant d'insérer une source dans le livrable, vérifier que l'URL ou le contenu confirme le périmètre US. En cas de doute, rejeter. Mieux vaut `non couvert` qu'une source non-US non signalée.

**Exceptions** : aucune. Si le PM demande une analyse qui nécessite une source non-US, signaler que le skill ne la produit pas dans ce cadre et laisser le PM décider.

## Vérifiabilité des liens — WebFetch obligatoire anti-hallucination

**Règle non négociable** : avant d'insérer toute URL dans le livrable, le skill effectue un `WebFetch` sur l'URL pour confirmer qu'elle existe et qu'elle renvoie bien le contenu cité. Cette vérification est **obligatoire**, sans exception.

Protocole :

1. **Fetch** : `WebFetch` sur l'URL candidate.
2. **Succès** (2xx, contenu cohérent) : insérer la citation normalement, avec date de collecte.
3. **Échec réseau transitoire** (timeout, 429, 503) : retry jusqu'à 3 fois avec backoff (1s, 3s, 8s). Si succès après retry, insérer.
4. **Échec dur** (404, 403, contenu incohérent avec ce qui est cité) : **ne jamais insérer l'URL telle quelle**. Deux options :
   - Si une URL alternative existe pour la même donnée (ex. Wayback Machine, mirror), la fetcher et la valider. Ne jamais substituer silencieusement.
   - Sinon, marquer explicitement dans le livrable : `URL non vérifiée le [YYYY-MM-DD] (code HTTP [X])`. La citation reste, mais le PM sait que la vérification n'a pas pu se faire.
5. **Jamais d'URL inventée** : si le skill ne trouve pas l'URL exacte de la source, il marque `non couvert`. Il n'hallucine jamais une URL "probable".

Cette règle ferme le risque principal : qu'une URL plausible mais inventée (ou devenue obsolète) se glisse dans un livrable auditable.

## Fair use des quotes Reddit / TikTok / avis stores

Les citations verbatim (posts, reviews, commentaires) sont autorisées dans le livrable en usage interne Pictarine, sous contraintes strictes :

- **Longueur maximum : ~40 mots par quote.** Au-delà, paraphraser ou extraire le fragment pertinent.
- **Attribution + lien cliquable obligatoires** : auteur (pseudo, handle), plateforme, URL directe vers le post/commentaire, date de collecte.
- **Pas de quote complète d'un thread** : extraire uniquement la partie qui porte le failure signal, pas tout le contexte.
- **Pas de réutilisation des screenshots** : ne pas inclure de captures d'écran de posts tiers dans le livrable. Citer en texte avec lien.
- **Marquer `usage interne Pictarine`** dans l'en-tête du livrable si des quotes verbatim sont incluses.

Si une quote dépasse 40 mots et que la coupure dénature le sens, paraphraser en gardant le lien vers la source originale.

## Sources payantes — protocole

Certains rapports clés du marché photo US sont payants (Keypoint Intelligence, IBISWorld US, Euromonitor US, PitchBook). Règles :

1. **Identifier et lister** dans le livrable les rapports payants pertinents repérés (titre, éditeur, lien vers la page de vente).
2. **Demander au PM** via AskUserQuestion, au début du step 4 (scoring) ou dès que pertinent : "J'ai identifié [rapport X chez Keypoint]. Tu as un accès corporate ou un extrait à me fournir ?"
3. **Si le PM fournit un extrait ou un accès** : utiliser normalement, sourcer avec le lien interne ou un lien vers la page publique du rapport.
4. **Si le PM n'a pas d'accès** : marquer `non couvert — source payante non accédée : [rapport]`. Jamais extrapoler ce que le rapport pourrait dire.
5. **Citations indirectes via presse spécialisée** : si Modern Retail, WhatTheyThink, ou autre source de second rang cite un chiffre d'un rapport payant, utiliser en précisant `chiffre [X] cité par [presse] d'après [rapport payant, non accédé directement]`.

## Ordre de préférence des sources

Quand plusieurs sources sont disponibles pour un même point, privilégier dans l'ordre :

1. Donnée primaire datée (rapport, filing SEC, press release officiel, page concurrent datée)
2. Presse spécialisée reconnue (Printing Impressions, WhatTheyThink, Modern Retail, Dealerscope)
3. Panels / analystes (Keypoint Intelligence, Statista, IDC, Euromonitor)
4. Social listening (Reddit, TikTok, avis stores) — pour les failure signals et le qualitatif
5. Blogs sectoriels non signés — à éviter sauf corroboration croisée
