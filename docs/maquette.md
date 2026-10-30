# Plan de la maquette Figma

Objectif : montrer au client une première direction visuelle et recueillir son avis.

## Frames

- **Accueil — Desktop** (1440 px)
- **Accueil — Mobile** (390 px) — prioritaire, beaucoup d'achats se font sur téléphone
- **Page produit — Desktop + Mobile**

## Styles à définir

- Couleurs : principale, fond, texte, accent (boutons)
- Textes : titres, texte courant
- Composant réutilisable : carte produit (photo, nom, prix)

## Page d'accueil (de haut en bas)

1. Barre de navigation : logo, Homme / Femme / Collections, recherche, panier
2. Bannière plein écran : photo forte, slogan court, bouton d'action
3. Grille de 3–4 produits phares
4. Bloc univers / collections (esprit Macron)
5. Bloc « l'histoire de la marque »
6. Newsletter
7. Footer : réseaux, contact, livraison et retours, mentions légales

## Page produit

- Galerie photos
- Nom, prix
- Choix taille et couleur
- Bouton « Ajouter au panier »
- Guide des tailles
- Description, matière, entretien
- Produits associés

## Prototype

- Relier une carte produit de l'accueil à la page produit
- Partager le lien du prototype au client (lecture + commentaires)

## Images temporaires

En attendant les photos du client : images libres de droits (Unsplash, Pexels).
Ne jamais utiliser de visuels Nike ou Macron.

## État de la maquette v1 (30/10/2026)

Fichier Figma : « ESSOR — Maquette v1 (direction Impact) »
https://www.figma.com/design/eJajkcdg88JyZTawINA73P

Nom de marque (ESSOR), textes, prix et produits sont **provisoires**.

### Page « Styles & composants »

- Planche **Palette & typographie** (couleurs et styles de texte documentés)
- Variables de couleur `couleur/noir`, `surface`, `surface-2`, `blanc`, `gris`, `orange`, `ligne`
- Styles de texte `Desktop/…`, `Mobile/…`, `Texte/…`, `Label/…` (Anton + Inter)
- Composants : logo provisoire, 12 icônes, Bouton (Principal / Contour / Sombre), Badge,
  **Carte produit** (Grand = desktop, Compact = mobile ; nom, catégorie, prix, badge),
  Pastille couleur, Taille (Disponible / Sélectionnée / Épuisée), Accordéon,
  Entête desktop et mobile (fond transparent ou plein), Pied de page (desktop / mobile)

### Page « Maquette v1 »

| Frame | Contenu |
|---|---|
| Accueil — Desktop (1440) | campagne plein écran, incontournables, univers + collections AH 26 / PE 27, histoire, newsletter, pied de page |
| Accueil — Mobile (390) | mêmes blocs, adaptés (grilles 2 colonnes, boutons pleine largeur) |
| Page produit — Desktop (1440) | fil d'Ariane, galerie (vignettes + photo), nom, prix, couleur, taille, guide des tailles, panier, favoris, détails en accordéon, produits associés |
| Page produit — Mobile (390) | galerie plein écran avec pagination, mêmes éléments empilés |
| Guide des tailles — Desktop (fenêtre) / Mobile (panneau) | tableau indicatif à remplacer par celui du client |

### Prototype

- Points de départ : « Parcours desktop » et « Parcours mobile »
- Cartes produit et bouton « Acheter » de l'accueil → page produit
- Logo et fil d'Ariane de la page produit → accueil
- « Guide des tailles » → ouvre la fenêtre ; croix → la referme
- Tout pointe vers l'unique page produit (veste Rafale) : c'est voulu pour la démo
- À régler à la main dans Figma si besoin : position du panneau mobile du guide des tailles
  en « Bas » (l'API ne permet que le centrage)

### Photos

Emplacements vides nommés `Photo / …` (campagne, univers, collections, histoire, produits,
galerie). Chacun contient un calque « Indication photo » qui décrit la photo attendue.
Pour les remplir : plugin Figma « Unsplash » (sélectionner le calque, choisir la photo),
ou laisser Claude les poser une fois `images.unsplash.com` et `mcp.figma.com` autorisés
dans le réseau de l'environnement cloud et l'e-mail Unsplash confirmé. Supprimer ensuite
les calques « Indication photo ».
