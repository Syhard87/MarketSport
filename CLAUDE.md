# CLAUDE.md — Site marque de vêtements de sport

Ce fichier donne le contexte du projet à Claude Code. À lire en début de session.

## Le projet

Un client possède une marque de vêtements de sport et veut un site internet.
Antoine (développeur) réalise le projet : maquette Figma, puis développement.

- Nom de la marque : **à compléter** (remplacer `[MARQUE]` partout une fois connu)
- Références citées par le client : **Nike** (https://www.nike.com/fr/) et **Macron** (https://www.macron.com/fr/)
- Type de site : **pas encore décidé** — site vitrine ou e-commerce (voir `docs/brief.md`)

## Statut actuel

1. ✅ Premier appel avec le client
2. ✅ Mail envoyé avec les questions et la demande d'éléments (`docs/mail-client.md`)
3. ⏳ En attente des réponses : logo, couleurs, photos, réseaux, type de site, budget, délai
   - ✅ En parallèle : direction visuelle provisoire → direction A « Impact » choisie
4. ⏳ Maquette Figma v1 construite directement dans Figma (voir `docs/maquette.md`) :
   accueil et page produit en desktop + mobile, guide des tailles, prototype cliquable,
   photos Unsplash provisoires posées (30/10/2026).
   Reste à faire : relecture par Antoine, puis partage du lien du prototype au client.
   - ✅ Dossier Google Drive partagé préparé pour le client (30/10/2026) : liens utiles,
     présentation de la maquette, suite du projet (options techniques et coûts).
     À partager avec le client par Antoine.
5. ⬜ Validation de la maquette par le client
6. ⏳ Choix technique : développement sur mesure hébergé chez OVH (décidé par Antoine le
   31/10/2026, stack à confirmer), puis développement
7. ⬜ Mise en ligne

Mettre à jour cette liste au fil du projet.

## Références de style (ce qu'on retient, sans copier)

- **Nike** : page d'accueil construite autour de grandes campagnes visuelles plein écran,
  chacune avec un titre très court, une phrase d'accroche et un bouton « Acheter ».
  Ambiance très photo / vidéo, typographie forte.
- **Macron** : navigation organisée par univers (lifestyle, athleisure, sports de raquette,
  merchandising, sports d'équipe) et collections saisonnières (Automne-Hiver / Printemps-Été).
  Plus « catalogue ».

Règle : s'inspirer de la structure et de l'ambiance, **jamais** reprendre leurs logos,
visuels, slogans ou textes. Le site doit rester celui de la marque du client.

## Direction visuelle provisoire

Choisie par Antoine le 28/10/2026, en attendant le logo et les photos du client.
**Rien n'est encore validé par le client** : c'est une base de discussion.

- Direction **A « Impact »** (sombre, esprit campagne) :
  - Couleurs : noir profond `#0E0E0E` (fond), blanc cassé `#F5F3EE` (texte),
    gris acier `#8A8A8A` (texte secondaire), orange signal `#FF4D1F` (boutons, accent).
    Texte des boutons orange en noir (contraste suffisant, le blanc ne l'est pas).
  - Typo (Google Fonts) : **Anton** pour les titres (capitales condensées), **Inter** pour le texte.
  - Ambiance : campagnes photo plein écran, slogans de 2-3 mots, univers en grandes tuiles photo.
- Direction écartée pour l'instant : B « Club » (fonds clairs crème, vert terrain `#1F4D3A`,
  jaune `#F2B632`, Barlow Condensed / Barlow, plus catalogue). À ressortir si le client
  préfère une ambiance claire.
- Nom de marque provisoire : **ESSOR** (à remplacer partout par le vrai nom, comme `[MARQUE]`).
- Photos temporaires : Unsplash (licence gratuite), choisies sans logo de marque visible.
  Crédits dans `docs/maquette.md` et dans la « Photothèque » de la page Styles & composants.
  Dans Figma, chaque emplacement photo est un calque nommé `Photo / …` ; le calque
  « Indication photo » (masqué) décrit la photo attendue, utile pour les remplacer par
  celles du client.
- Ton des textes : tutoiement, phrases courtes (à valider avec le client).

## Choix technique

Décision d'Antoine (31/10/2026) : le site est **développé sur mesure par Antoine** et
**hébergé chez OVH** (pas de Shopify ni de WooCommerce). Plan détaillé : `docs/technique.md`.

- Stack proposée, **à confirmer** : PHP + Laravel + MySQL sur un hébergement mutualisé
  OVH (offre Pro minimum, pour l'accès SSH). Back-office du client avec Filament.
  Alternative : Symfony + EasyAdmin.
- Paiement (si boutique) : **Stripe Checkout**, le site ne traite jamais de carte bancaire ;
  le stock est décrémenté à la confirmation du paiement (webhook).
- Phase 1 vitrine + catalogue, phase 2 boutique : le client peut encore choisir un site
  vitrine sans que l'architecture change.
- Le document client « 3. La suite du projet » (Google Drive) présente encore Shopify comme
  solution recommandée : à mettre à jour avec cette option.

## Outils

- **Figma** (espace d'équipe d'Antoine, plan Starter) pour la maquette :
  fichier « ESSOR — Maquette v1 (direction Impact) »
  https://www.figma.com/design/eJajkcdg88JyZTawINA73P
- **Google Drive** (compte d'Antoine) : dossier « Projet site internet — dossier partagé »,
  destiné à être partagé avec le client.
  https://drive.google.com/drive/folders/1tv0zkGr2m3gSYV_bDNdnYYTmROzryLvf
  - `1. Liens utiles` : maquette, documents, sites de référence, contacts (à compléter).
  - `2. Présentation de la maquette v1` : contenu, direction visuelle, provisoire, retours.
  - `3. La suite du projet` : étapes, vitrine / Shopify / WooCommerce, hébergement, base
    de données, coûts (relevés en octobre 2026), points à décider.
  - Sous-dossier `Éléments de la marque` : dépôt du logo, des photos et des textes du client
    (à copier ensuite dans `assets/`).
  - Le connecteur Google Drive de claude.ai crée des fichiers ; pour modifier un Google Doc
    existant, il faut aussi le connecteur Google Docs.
- **MCP Figma** : `https://mcp.figma.com/mcp` — à connecter dans Claude Code pour lire
  la maquette et s'en servir pour générer le code.
  ```
  claude mcp add --transport http figma https://mcp.figma.com/mcp
  ```
  - Déjà déclaré dans `.mcp.json` (portée projet) : en local, lancer `claude` dans le repo,
    approuver le serveur, puis `/mcp` → figma → *Authenticate* (connexion au compte Figma).
  - Sessions Claude Code dans le cloud (claude.ai/code) : `.mcp.json` ne suffit pas
    (domaine bloqué par le réseau, pas d'authentification possible). Brancher plutôt le
    connecteur **Figma** sur https://claude.ai/customize/connectors, puis ouvrir une nouvelle session.
  - Ce que le MCP permet : **lire** une maquette (structure, styles, variables, captures,
    contexte pour générer le code) **et écrire** dedans : créer un fichier, des variables,
    des styles, des composants, des frames, des liens de prototype (outil `use_figma`).
    La maquette v1 a été construite ainsi, sans passer par un prototype HTML.
  - Limites constatées : le MCP ne peut pas télécharger d'images depuis Internet ; pour
    poser une photo il faut envoyer le fichier depuis la session (domaine `mcp.figma.com`)
    ou passer par le plugin Figma « Unsplash ». Sur un plan Starter / siège View, les outils
    de **lecture** du MCP sont limités à quelques appels par mois (à garder pour la phase
    de développement, ou prendre un siège Dev/Full sur un plan payant).
- **Connecteur Unsplash** (claude.ai, compte d'Antoine) : recherche et enregistrement des
  téléchargements. Il ne renvoie que des descriptions : télécharger les photos pour les
  vérifier avant de les utiliser (logos de marque fréquents sur les vêtements).
- **Réseau de l'environnement cloud** : domaines `images.unsplash.com` et `mcp.figma.com`
  autorisés (nécessaires pour télécharger les photos et les envoyer dans Figma).

## Arborescence

```
CLAUDE.md               ← ce fichier
README.md               ← présentation rapide du repo
.mcp.json               ← déclaration du serveur MCP Figma pour Claude Code
docs/brief.md           ← brief client : besoins, réponses, décisions
docs/mail-client.md     ← mail envoyé au client (questions + éléments demandés)
docs/maquette.md        ← plan de la maquette Figma
docs/technique.md       ← plan technique : stack, hébergement OVH, base de données, pages
assets/                 ← logo, photos, éléments fournis par le client
```

## Conventions

- Langue du projet et des échanges : **français**.
- Les éléments fournis par le client vont dans `assets/` (ne pas les modifier, travailler sur des copies).
- Toute décision prise avec le client est notée dans `docs/brief.md` (section « Décisions »).
