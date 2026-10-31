# Plan technique — site développé sur mesure, hébergé chez OVH

Décision d'Antoine (31/10/2026) : le site est **développé par Antoine**, sans plateforme
e-commerce (ni Shopify, ni WooCommerce), et **hébergé chez OVH**. Le type de site (vitrine
ou boutique) reste à décider avec le client : l'architecture ci-dessous permet de commencer
en vitrine et d'ajouter la vente ensuite, sans tout refaire.

Stack proposée, **à confirmer par Antoine** : PHP + Laravel + MySQL.

## Pourquoi cette stack

- L'hébergement mutualisé OVH fait tourner **PHP et MySQL** ; Node.js ou Python n'y sont pas
  garantis (il faudrait un VPS à administrer soi-même).
- Laravel apporte ce qu'un site e-commerce demande sans le recoder : routes, base de données
  (Eloquent, migrations), formulaires et validation, authentification, e-mails, protection CSRF.
- **Filament** (open source, sur Laravel) fournit l'interface d'administration du client
  (produits, tailles, stocks, commandes) : pas de back-office à coder de zéro.
- Alternative équivalente : Symfony + EasyAdmin, si Antoine connaît mieux Symfony.

## Hébergement OVH

- Offre **mutualisée Pro** au minimum : c'est à partir de cette offre que l'accès **SSH** est
  disponible (sans accès root), nécessaire pour déployer avec Git et Composer.
- Inclus en général : PHP 8.x, base MySQL, certificat HTTPS (Let's Encrypt), adresses e-mail,
  tâches planifiées (cron). **À vérifier sur ovhcloud.com avant la commande** : grille
  tarifaire revue en mai 2026 (prix d'appel la première année, renouvellement plus cher ;
  ordre de grandeur relevé : environ 8 € puis 12 € TTC par mois pour l'offre Pro),
  version de PHP, taille de la base, nom de domaine offert ou non la première année.
- Le dossier racine du site doit pointer vers `public/` (réglage « multisite » d'OVH).
- Comptes (hébergement, nom de domaine) **au nom du client**, Antoine en accès technique.

## Paiement (si boutique)

Le site ne traite **jamais** de numéro de carte : le paiement passe par **Stripe Checkout**
(page de paiement hébergée par Stripe, CB, Apple Pay, Google Pay).

- Le site crée une session Stripe à partir du panier, le client paie sur la page Stripe.
- Un **webhook** Stripe (`/stripe/webhook`) confirme le paiement : la commande passe en
  « payée » et le stock est décrémenté à ce moment-là, pas avant.
- Frais Stripe pour les cartes européennes : environ 1,5 % + 0,25 € par paiement (à vérifier
  sur stripe.com). Pas d'abonnement.
- Alternatives possibles : PayPal, Mollie, ou le module de paiement de la banque du client.

## Base de données (MySQL) — première version

| Table | Contenu |
|---|---|
| `univers` | Running, Training, Sports d'équipe, Lifestyle (nom, slug, ordre, photo) |
| `collections` | Automne-Hiver 26, Printemps-Été 27… (nom, slug, saison, statut disponible / bientôt) |
| `produits` | nom, slug, accroche, description, matière, entretien, prix en centimes, genre (homme / femme / mixte), univers, collection, badge « Nouveau », actif |
| `produit_images` | produit, fichier, ordre, texte alternatif |
| `variantes` | produit, couleur, taille, référence (SKU), stock |
| `commandes` | numéro, e-mail, nom, adresse de livraison, mode de livraison, frais de port, total, statut (en attente, payée, expédiée, annulée, remboursée), identifiant de session Stripe, dates |
| `lignes_commande` | commande, variante, copie du nom, de la taille, de la couleur et du prix au moment de l'achat, quantité |
| `users` | comptes d'administration (le client, Antoine) |

Commande **sans compte client** en V1 (e-mail + adresse) ; comptes clients plus tard si besoin.
Newsletter : inscription envoyée à Brevo (pas de liste stockée sur le site).

## Pages (d'après la maquette v1)

| Page | Route | Phase |
|---|---|---|
| Accueil | `/` | 1 |
| Liste des produits : Homme, Femme, par univers, par collection | `/homme`, `/femme`, `/univers/{slug}`, `/collections/{slug}` | 1 |
| Fiche produit (galerie, couleur, taille, guide des tailles) | `/produits/{slug}` | 1 |
| Notre histoire, livraison et retours, contact, guide des tailles | `/histoire`, `/livraison-retours`, `/contact`, `/guide-des-tailles` | 1 |
| Mentions légales, confidentialité, cookies (+ CGV si vente) | `/mentions-legales`, … | 1 |
| Panier | `/panier` | 2 |
| Paiement (redirection Stripe) et confirmation | `/commande`, `/commande/confirmation` | 2 |
| Administration (Filament) | `/admin` | 1 (catalogue), 2 (commandes) |

## Front

- Templates Blade, CSS reprenant les styles Figma (variables CSS `--couleur-noir`, etc.,
  déjà définies comme variables dans Figma), polices Anton et Inter auto-hébergées.
- Vite pour compiler CSS et JS ; **les fichiers sont compilés avant le déploiement**
  (en local ou en CI), pas sur le serveur OVH.
- Peu de JavaScript : menu mobile, galerie, choix taille / couleur, panier (Alpine.js ou
  JavaScript simple).
- Images en WebP avec plusieurs tailles, chargement différé hors de l'écran.

## Déploiement et environnements

- Code sur GitHub (`syhard87/marketsport`).
- **Local** : PHP + MySQL (Laravel Herd, Sail ou Docker).
- **Préproduction** : sous-domaine (ex. `preprod.marque.fr`) pour montrer le site au client.
- **Production** : déploiement par SSH (`git pull`, `composer install --no-dev`,
  `php artisan migrate --force`, caches) ou GitHub Actions vers OVH.
- Secrets (clés Stripe, mot de passe MySQL) uniquement dans le `.env` du serveur, jamais
  dans le dépôt.

## Sécurité, RGPD, sauvegardes

- HTTPS partout, mots de passe d'administration forts, `APP_DEBUG=false` en production.
- Mises à jour régulières de Laravel et des dépendances (`composer update`, alertes GitHub).
- Sauvegarde de la base : sauvegardes OVH + export automatique planifié (cron).
- RGPD : mentions légales, politique de confidentialité, bandeau cookies si mesure
  d'audience (ou outil sans cookies), données de commande limitées au nécessaire.

## Phases

1. **Vitrine + catalogue** : pages de la maquette, catalogue géré par le client dans
   l'administration, contact, newsletter. Utilisable seul si le client choisit un site vitrine.
2. **Boutique** : panier, Stripe Checkout, webhooks, gestion des commandes et des stocks,
   e-mails de confirmation et d'expédition, CGV, frais de livraison.
3. **Plus tard, si besoin** : comptes clients, codes promo, avis, multi-langue.
