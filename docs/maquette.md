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

Photos Unsplash provisoires (licence Unsplash : usage gratuit, crédit apprécié), posées le
30/10/2026. Toutes vérifiées à l'œil : aucun logo de marque visible (plusieurs candidates
écartées pour un logo Nike, adidas, On ou The North Face). À remplacer par les photos du
client : chaque emplacement est un calque `Photo / …`, avec une « Indication photo » masquée
qui décrit la photo attendue. Les fichiers sources sont rangés dans la « Photothèque » de la
page Styles & composants.

| Emplacement | Photographe | Lien |
|---|---|---|
| Campagne (desktop et mobile) | Hansheng Zhao | https://unsplash.com/photos/9FcKpisH7Bo |
| Univers Running | Greg Rosenke | https://unsplash.com/photos/E9PdTVfEujI |
| Univers Training | Mohamed Fareed | https://unsplash.com/photos/rbSNsoXk-3A |
| Univers Sports d'équipe | arh Lee | https://unsplash.com/photos/E3dSiTSlgBI |
| Univers Lifestyle | Sinitta Leunen | https://unsplash.com/photos/zKlUaEzp0-0 |
| Collection Automne-Hiver 26, vignette 4 de la veste | lucas Favre | https://unsplash.com/photos/JnoNcfFwrNA |
| Collection Printemps-Été 27 | Gabin Vallet | https://unsplash.com/photos/J154nEkpzlQ |
| Histoire de la marque (passée en noir et blanc) | Tyler Raye | https://unsplash.com/photos/Xb1d-N04Quc |
| Veste Rafale (carte, photo principale, vignette 1) | Michael Kyule | https://unsplash.com/photos/wap-C1Bv_tw |
| Veste Rafale, vignette 2 | Bobbi Wu | https://unsplash.com/photos/R73HITZ9E7M |
| Veste Rafale, vignette 3 | Jisu Han | https://unsplash.com/photos/7BlfHlujv2c |
| T-shirt Souffle | Tim Bernhard | https://unsplash.com/photos/pYDQyzThtLE |
| Legging Ancrage | engin akyurt | https://unsplash.com/photos/oLBDdtWYUEo |
| Sweat Base | Logan Weaver | https://unsplash.com/photos/N6BP12FB_XU |
| Short Allure | Florian Kurrasch | https://unsplash.com/photos/zkctapwhzxc |
| Brassière Maintien | engin akyurt | https://unsplash.com/photos/Str8IYrWG0U |

Remarque : les vignettes de la page produit montrent des vestes différentes (banque d'images) ;
avec le shooting du client, ce seront 4 vues du même produit.
