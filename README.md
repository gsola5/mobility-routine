# Mobilité

Petite PWA de routine mobilité/muscu, un jour par groupe musculaire.

## Structure

```
mobility-routine/
├── index.html       ← toute l'app (HTML + CSS + JS inline)
├── manifest.json    ← config PWA
├── sw.js            ← service worker (offline)
├── icon.svg         ← icône vectorielle
├── icon-192.png     ← icône iOS
├── icon-512.png     ← icône iOS grande
└── images/          ← photos des exercices (à ajouter)
    ├── hanche-01.jpg
    ├── hanche-02.jpg
    └── ...
```

## Déployer sur GitHub Pages

1. Crée un repo public sur GitHub, par ex. `mobility-routine`
2. Pousse ces fichiers :
   ```bash
   cd mobility-routine
   git init
   git add .
   git commit -m "init"
   git branch -M main
   git remote add origin https://github.com/TON_USER/mobility-routine.git
   git push -u origin main
   ```
3. Sur GitHub : **Settings → Pages → Source: `main` branch, folder `/root`** → Save
4. Attends 1–2 min, ton URL sera `https://TON_USER.github.io/mobility-routine/`

## Installer sur iPhone

1. Ouvre l'URL dans **Safari** (pas Chrome — iOS ne permet l'install PWA que depuis Safari)
2. Appuie sur le bouton Partager
3. **Ajouter à l'écran d'accueil**
4. L'app s'ouvre en plein écran, sans barre Safari, avec icône dédiée

## Ajouter des jours

Ouvre `index.html`, cherche `const routine = {`, ajoute :

```js
2: { // Mardi
  name: "Ischios",
  exercises: [
    {
      name: "Nom de l'exercice",
      description: "Description courte.",
      sets: 3,
      reps: 12,           // OU duration: 30 pour un exo au temps
      perSide: true,      // true si unilatéral (chaque côté)
      rest: 30,           // secondes de repos entre séries
      image: "images/ischios-01.jpg"  // optionnel
    }
  ]
},
```

Numéros de jours : `1` = Lundi, `2` = Mardi, ..., `6` = Samedi, `0` = Dimanche.

## Ajouter les photos

- Prends tes photos, mets-les dans `images/`
- Nomme-les selon le chemin dans la data (par ex. `images/hanche-01.jpg`)
- Format conseillé : JPG, ratio 4:3, ~800×600px, compressé

Si une image n'existe pas, l'app affiche un placeholder — pas de bug.

## Cache et mises à jour

Le service worker met en cache les fichiers. Pour forcer un refresh après un push :
- Incrémente `CACHE = 'mobilite-v1'` → `'mobilite-v2'` dans `sw.js`
- Ou depuis l'iPhone : ferme l'app, la relance
