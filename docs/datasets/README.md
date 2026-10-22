# Données du cours Data Science sous R

| Fichier | Contenu | Lignes | Format |
|:--------|:--------|-------:|:-------|
| `boutique_clients.csv` | clients d'une boutique en ligne fictive, un client par ligne | 2 000 | CSV, séparateur `,` |
| `boutique_commandes.csv` | commandes passées en 2025, une commande par ligne | 9 508 | CSV, séparateur `,` |
| `boutique_categories.csv` | table de référence des catégories de produits | 6 | CSV, séparateur `,` |
| `boutique_campagne.csv` | test A/B d'un emailing (novembre 2025), un abonné à la newsletter par ligne | 944 | CSV, séparateur `,` |
| `phbirths.dat` | poids de naissance de bébés nés à Philadelphie, un bébé par ligne | 1 115 | texte, colonnes séparées par des espaces |

## La boutique en ligne

Les données de la boutique sont **fictives** : elles imitent l'activité d'un
site de vente en ligne français en 2025 et servent d'exemple marketing fil
rouge dans les notes. Les clients appartiennent à quatre segments « cachés »
(non fournis) qui déterminent leur comportement d'achat.

Les tables sont reliées par des clés : `client_id` relie les commandes et la
campagne aux clients, `categorie` relie les commandes aux catégories.

### `boutique_clients.csv`

| Variable | Type | Description |
|:---------|:-----|:------------|
| `client_id` | texte | identifiant du client (`C0001` à `C2000`) |
| `age` | numérique | âge en années ; non renseigné (`NA`) pour 60 clients |
| `region` | texte | région de résidence (7 régions et « Autres régions ») |
| `canal_acquisition` | texte | canal par lequel le client est arrivé : `Direct`, `Email`, `Moteur de recherche`, `Réseaux sociaux`, `Affiliation` |
| `date_inscription` | date | date de création du compte (2021 à 2025) |
| `newsletter` | texte | abonnement à la newsletter : `Oui` / `Non` |

### `boutique_commandes.csv`

| Variable | Type | Description |
|:---------|:-----|:------------|
| `commande_id` | texte | identifiant de la commande (`K00001`…) |
| `client_id` | texte | client qui a passé la commande (clé vers `boutique_clients.csv`) |
| `date` | date | date de la commande (du 01/01/2025 au 31/12/2025) |
| `categorie` | texte | catégorie de produits : `Mode`, `Maison`, `Beauté`, `High-tech`, `Sport` |
| `nb_articles` | entier | nombre d'articles dans la commande |
| `promo` | logique | `TRUE` si un code promo (20 % de remise) a été utilisé |
| `montant` | numérique | montant payé, en euros TTC, après remise éventuelle |

### `boutique_categories.csv`

| Variable | Type | Description |
|:---------|:-----|:------------|
| `categorie` | texte | nom de la catégorie (clé) ; `Jardin` n'a aucune commande |
| `taux_marge` | numérique | marge brute, en proportion du montant hors taxes |
| `univers` | texte | regroupement de catégories : `Personne`, `Habitat`, `Technologie`, `Loisirs` |

### `boutique_campagne.csv`

| Variable | Type | Description |
|:---------|:-----|:------------|
| `client_id` | texte | client destinataire (clé vers `boutique_clients.csv`) |
| `version` | texte | version reçue, tirée au hasard : `A` (objet habituel) ou `B` (objet personnalisé avec le prénom) |
| `ouvert` | logique | l'email a été ouvert |
| `clic` | logique | le client a cliqué sur un lien de l'email (implique `ouvert`) |
| `achat` | logique | le client a acheté après avoir cliqué (implique `clic`) |

## Poids de naissance : `phbirths.dat`

| Variable | Type | Description |
|:---------|:-----|:------------|
| `black` | logique | la mère est noire |
| `educ` | entier | nombre d'années d'études de la mère |
| `smoke` | logique | la mère fume |
| `gestate` | entier | durée de la gestation, en semaines |
| `grams` | entier | poids de naissance, en grammes |

La première ligne du fichier contient les noms des variables ; chaque ligne
suivante commence par un numéro d'observation. Lecture en R :
`read.table("phbirths.dat")`.
