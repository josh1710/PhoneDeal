# 📊 PhoneDeal Dashboard – Documentation Technique

## Présentation

**PhoneDeal Dashboard** est une application de bureau réalisée avec Electron permettant de visualiser en temps réel :
- Les dernières commandes passées sur la boutique
- Les demandes d’assistance des clients

L’application se connecte à une API Node.js qui interroge une base de données PostgreSQL (hébergée sur Neon ou autre).

---

## Sommaire
- [Fonctionnalités](#fonctionnalités)
- [Architecture](#architecture)
- [Installation et lancement](#installation-et-lancement)
- [Structure des fichiers](#structure-des-fichiers)
- [Connexion à l’API](#connexion-à-lapi)
- [Création de l’exécutable Windows](#création-de-lexécutable-windows)
- [Technologies utilisées](#technologies-utilisées)
- [Sécurité et bonnes pratiques](#sécurité-et-bonnes-pratiques)
- [Auteurs](#auteurs)

---

## Fonctionnalités
- Affichage des dernières commandes (date, articles, total)
- Affichage des demandes d’aide clients (date, email, message)
- Interface responsive et moderne
- Application de bureau multiplateforme (Windows, Mac, Linux)
- Génération d’un exécutable `.exe` pour Windows

---

## Architecture

- **Electron** : Affiche l’interface et interroge l’API via `fetch`.
- **API Node.js** : Fournit les routes `/api/orders` et `/api/help`.
- **PostgreSQL** : Stocke les commandes (`orders`) et les demandes d’aide (`help_requests`).

---

## Installation et lancement

### 1. Cloner le projet
```bash
git clone <url-du-repo>
cd dashboard-app
```

### 2. Installer les dépendances
```bash
npm install
```

### 3. Lancer l’application en mode développement
```bash
npm start
```

### 4. Générer un exécutable Windows
```bash
npm run package-win
```
Le dossier `PhoneDealDashboard-win32-x64` contiendra le `.exe`.

---

## Structure des fichiers

```
/dashboard-app/
  ├─ main.js           # Point d’entrée Electron
  ├─ dashboard.html    # Interface utilisateur
  ├─ package.json      # Dépendances et scripts
  └─ ...
```

---

## Connexion à l’API

L’application interroge l’API Node.js sur :
- `GET http://localhost:3001/api/orders` (commandes)
- `GET http://localhost:3001/api/help` (demandes d’aide)

**Exemple de réponse attendue pour /api/orders** :
```json
[
  {
    "created_at": "2024-06-27T10:00:00.000Z",
    "articles": [ { "nom": "iPhone 15" }, { "nom": "AirPods 4" } ],
    "total": 1299.99
  },
  ...
]
```

**Exemple de réponse attendue pour /api/help** :
```json
[
  {
    "created_at": "2024-06-27T11:00:00.000Z",
    "email": "client@mail.com",
    "message": "Je souhaite modifier ma commande."
  },
  ...
]
```

---

## Création de l’exécutable Windows

1. Installer les dépendances de build :
   ```bash
   npm install --save-dev electron-packager
   ```
2. Générer l’exécutable :
   ```bash
   npm run package-win
   ```
3. L’exécutable se trouve dans le dossier `PhoneDealDashboard-win32-x64`.

---

## Technologies utilisées
- **Electron** (interface de bureau)
- **HTML5/CSS3/JavaScript** (frontend)
- **Node.js/Express** (API backend)
- **PostgreSQL** (base de données)
- **Neon** (hébergement PostgreSQL cloud)

---

## Sécurité et bonnes pratiques
- Les accès à la base de données sont sécurisés côté serveur (jamais exposés dans Electron).
- L’API doit être protégée (authentification recommandée en production).
- Les fichiers sensibles (`.env`, `node_modules/`, etc.) sont exclus du dépôt via `.gitignore`.

---


