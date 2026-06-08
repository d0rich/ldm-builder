# LDM Builder

Générateur de lettres de motivation personnalisées en PDF. Remplissez le poste et l'entreprise, cliquez sur "Imprimer" et exportez en PDF — c'est tout.

**Demo live :** https://ldm.d0rich.me

## Comment ça marche

Le projet est une application **frontend-only** (Vue 3 + Vite) qui :

1. Charge un template Markdown depuis `src/assets/template.md`
2. Remplace les placeholders `{{POSTE}}` et `{{ENTREPRISE}}` avec les valeurs saisies dans le formulaire
3. Convertit le Markdown en HTML via `remark`
4. Affiche la lettre avec un style typographique propre (Tailwind Typography)
5. Utilise le **dialogue d'impression du navigateur** (`window.print()`) pour exporter en PDF

Les données sont persistées dans le `localStorage` du navigateur : rien n'est envoyé à un serveur.

```
src/
├── assets/
│   └── template.md          # Le texte de la lettre avec {{POSTE}} et {{ENTREPRISE}}
├── components/
│   ├── ReplacementsForm.vue # Formulaire + bouton "Imprimer"
│   └── MotivationLetter.vue # Rendu de la lettre en HTML
└── App.vue                  # État global, titre de page dynamique
```

## Commandes

```bash
# Installer les dépendances
npm install

# Démarrer en développement (hot-reload)
npm run dev

# Build de production
npm run build

# Prévisualiser le build localement
npm run preview
```

## Forker et adapter pour vous

Ce projet est conçu pour être forké et personnalisé. Voici les étapes pour l'adapter à votre propre lettre :

### 1. Forker le repo

Cliquez sur le bouton **Fork** en haut à droite de la page GitHub pour créer votre propre copie du repo, puis clonez-la :

```bash
git clone https://github.com/VOTRE_USERNAME/ldm-builder.git
cd ldm-builder
npm install
```

### 2. Éditer le template

Ouvrez `src/assets/template.md` et remplacez le contenu par votre propre lettre de motivation.

Les seules règles à respecter :
- Utilisez `{{POSTE}}` là où le nom du poste doit apparaître
- Utilisez `{{ENTREPRISE}}` là où le nom de l'entreprise doit apparaître

```markdown
Madame, Monsieur,

Je vous écris pour postuler au poste de **{{POSTE}}** au sein de **{{ENTREPRISE}}**...

Cordialement,
Votre Nom
```

### 3. Mettre à jour les métadonnées SEO

Dans `index.html`, ajustez les balises `<meta>` (titre, description, auteur, URL canonique, image Open Graph) pour les faire correspondre à votre identité.

### 4. Déployer gratuitement

Le projet génère un simple dossier `dist/` — des fichiers statiques sans serveur. Vous pouvez le déployer gratuitement sur :

| Plateforme | Commande / méthode |
|---|---|
| **GitHub Pages** | `gh-pages` branch ou GitHub Actions |
| **Vercel** | Connecter le repo, build command `npm run build` |
| **Netlify** | Glisser-déposer le dossier `dist/` ou connecter le repo |
| **Cloudflare Pages** | Connecter le repo, build command `npm run build` |

---

## Contribuer

Ce projet est actuellement une lettre **personnelle et hard-codée**. L'objectif à long terme serait d'en faire un outil générique utilisable par n'importe qui sans avoir à forker.

**Contrainte absolue : frontend-only.** Pas de backend, pas de serveur, pas de base de données — le projet doit rester déployable gratuitement sur un hébergement statique.

### Pistes d'amélioration

- **Plusieurs placeholders configurables** : permettre à l'utilisateur de définir ses propres variables (ex. `{{NOM}}`, `{{VILLE}}`, `{{DIPLOME}}`) au lieu de `{{POSTE}}` et `{{ENTREPRISE}}` en dur.

- **Éditeur de template intégré** : un éditeur Markdown in-app (avec prévisualisation en temps réel) pour que l'utilisateur puisse écrire et modifier son template directement dans le navigateur, sans avoir à cloner le repo.

- **Import / export de template** : permettre de charger un fichier `.md` local comme template et de sauvegarder les modifications (via l'API File System Access ou un simple téléchargement).

- **Plusieurs templates** : gérer une liste de templates (stage, CDI, freelance…) et basculer de l'un à l'autre.

- **Styles d'impression configurables** : proposer différentes mises en page / polices pour le PDF généré.

- **Internationalisation** : rendre l'interface disponible en plusieurs langues.

### Comment contribuer

1. Forker le repo et créer une branche (`git checkout -b feature/ma-feature`)
2. Tester votre changement avec `npm run dev`
3. Ouvrir une Pull Request en décrivant le problème résolu et en confirmant que ça reste **frontend-only**
