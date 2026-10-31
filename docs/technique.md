# Options techniques et plan de développement

**C'est le client qui choisit.** Ce document liste les options à lui proposer, de la moins
chère à la plus chère, puis détaille le plan technique de l'option « boutique développée
sur mesure, hébergée chez OVH », que préfère Antoine.

## Options à proposer au client (coûts relevés en octobre 2026)

Coûts annuels en ordre de grandeur, TTC, hors création du site. Le **prix de création**
dépend du temps de travail d'Antoine : plus il y a de sur-mesure, plus il est élevé.

| Option | Ce que ça permet | Coût annuel fixe | Frais par vente | Temps de création | Gestion par le client |
|---|---|---|---|---|---|
| 1. Vitrine codée, hébergement statique | Présenter la marque et les collections, pas de vente | Domaine seul (~10 €/an) avec un hébergement statique gratuit, ou ~50 à 90 €/an chez OVH (offre Perso) | Aucun | Court | Via un petit CMS gratuit, ou modifications faites par Antoine |
| 2. Vitrine + boutons d'achat Stripe (liens de paiement) | Vendre quelques produits sans panier : un bouton « Acheter » par produit ouvre la page de paiement Stripe | Comme l'option 1 | Environ 1,5 % + 0,25 € par paiement (carte européenne) | Court | Commandes dans le tableau de bord Stripe, stocks suivis à la main |
| 3. Boutique WooCommerce chez OVH | Boutique complète (panier, stocks, commandes) | ~100 à 145 €/an (offre Pro) + domaine | Frais du moyen de paiement (Stripe ou PayPal) | Moyen (thème WordPress adapté à la maquette) | Interface WordPress, mises à jour à suivre |
| 4. Boutique développée sur mesure chez OVH | Boutique complète, entièrement codée par Antoine | ~100 à 145 €/an (offre Pro) + domaine | Environ 1,5 % + 0,25 € par paiement (Stripe) | Long | Interface d'administration Filament, maintenance par Antoine |
| 5. Boutique Shopify | Boutique complète clé en main | ~324 €/an (paiement annuel) à ~432 €/an + domaine | Environ 1,5 % + 0,25 € par paiement | Court à moyen | Interface Shopify et application mobile |

Les plus économiques :

- **Pour démarrer sans vendre en ligne** : option 1, le domaine est presque le seul coût.
- **Pour vendre un petit nombre de produits** (lancement, une collection) : option 2. Il n'y a
  pas d'abonnement, seulement les frais Stripe sur les ventes, et on peut passer aux options 3
  ou 4 plus tard en gardant le design.
- **Pour une boutique complète** : options 3 et 4, au même coût annuel (l'hébergement OVH).
  L'option 3 coûte moins cher à créer, l'option 4 donne plus de liberté mais demande plus de
  temps de développement et de maintenance. Shopify (option 5) coûte moins cher à créer mais
  environ trois fois plus cher par an.

Sources des tarifs (blogs et comparatifs, à revérifier avant le devis) : OVH (grille revue en
mai 2026, prix d'appel puis renouvellement plus cher), Shopify France, Stripe, domaine .fr
chez OVH. Les frais spécifiques aux liens de paiement Stripe restent à vérifier sur stripe.com.

---

# Plan technique — boutique développée sur mesure, hébergée chez OVH (option 4)

Option préférée d'Antoine si le client choisit le sur-mesure. Le type de site (vitrine ou
boutique) reste à décider avec le client : l'architecture ci-dessous permet de commencer en
vitrine et d'ajouter la vente ensuite, sans tout refaire.

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
