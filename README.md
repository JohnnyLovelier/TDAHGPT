# DIVA 2.0 FR, assistant d'entretien React prêt pour Vercel

Mini application React + Vite pensée pour être déployée telle quelle sur Vercel.

## Ce que fait le site

- structure l'entretien en 5 étapes
- sépare les exemples et la validation finale de chaque symptôme
- compte automatiquement les critères A et H/I
- vérifie les seuils du formulaire DIVA 2.0 FR
- documente la persistance, le retentissement dans au moins 2 domaines, et le critère E
- calcule le sous-type probable
- sauvegarde automatiquement dans le navigateur via localStorage
- permet de copier un résumé prêt à partager

## Lancer en local

```bash
npm install
npm run dev
```

## Build de production

```bash
npm install
npm run build
```

## Déploiement sur Vercel

1. pousse ce dossier sur GitHub
2. crée un nouveau projet sur Vercel
3. importe le repository
4. Vercel détectera automatiquement Vite
5. build command: `npm run build`
6. output directory: `dist`

Le fichier `vercel.json` est déjà inclus.

## Fichiers principaux

- `src/App.jsx` : logique de l'application et données du questionnaire
- `src/styles.css` : UI
- `src/main.jsx` : point d'entrée React
- `package.json` : dépendances et scripts

## Note importante

Ce projet structure un entretien et un résumé, mais ne remplace pas une évaluation médicale ou psychiatrique.
