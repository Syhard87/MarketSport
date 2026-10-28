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
   - ⏳ En parallèle : direction visuelle provisoire (nom de marque et images temporaires)
     → 2 directions proposées à Antoine, choix en attente
4. ⬜ Maquette Figma (accueil desktop + mobile, page produit, prototype cliquable)
5. ⬜ Validation de la maquette par le client
6. ⬜ Choix technique définitif et développement
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

## Choix technique envisagé

- Si **e-commerce** : Shopify (le client gère seul produits, stocks et commandes ;
  paiement intégré). Travail d'Antoine : thème, configuration, personnalisation.
  Alternative : WooCommerce.
- Si **vitrine** : site statique (Vite) ou Shopify en mode simple selon le besoin
  d'évolution vers la vente.
- Éviter de recoder paiement / gestion de stock en sur-mesure.

Décision à confirmer après les réponses du client.

## Outils

- **Figma** (espace d'équipe d'Antoine) pour la maquette.
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
  - Ce que le MCP permet : surtout **lire** une maquette (structure, styles, variables,
    captures, contexte pour générer le code) et créer des diagrammes FigJam. Il ne sert pas
    à dessiner des frames de maquette à la main → la maquette se fait dans Figma, ou on part
    d'un prototype HTML importé dans Figma (plugin html.to.design).

## Arborescence

```
CLAUDE.md               ← ce fichier
README.md               ← présentation rapide du repo
.mcp.json               ← déclaration du serveur MCP Figma pour Claude Code
docs/brief.md           ← brief client : besoins, réponses, décisions
docs/mail-client.md     ← mail envoyé au client (questions + éléments demandés)
docs/maquette.md        ← plan de la maquette Figma
assets/                 ← logo, photos, éléments fournis par le client
```

## Conventions

- Langue du projet et des échanges : **français**.
- Les éléments fournis par le client vont dans `assets/` (ne pas les modifier, travailler sur des copies).
- Toute décision prise avec le client est notée dans `docs/brief.md` (section « Décisions »).
