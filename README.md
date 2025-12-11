# eikon parcel starter

## Prérequis

- Git installé
- NPM installé

## Installation

Cloner le repository git

```
git clone git@github.com:eikon-frontend/starterkit.git <nom du projet>
```

Se rendre dans le dossier du projet, puis installer les dépendances avec NPM

```
cd <nom-du-projet>
npm install
```

## Commandes

Compiler la SCSS, aggréger le JS, lancer le serveur et écouter les changements

```
npm run dev
```

Compiler pour la production

```
npm run build
```

## Utilisation

### Système de traduction bilingue

Ce projet intègre un système de traduction qui permet de basculer entre le français et l'anglais. La langue choisie est sauvegardée dans le navigateur et persiste lors de la navigation entre les pages.

#### Structure des fichiers de traduction

Les traductions sont stockées dans des fichiers JSON à la racine du projet :

- `fr.json` : contient toutes les traductions en français
- `en.json` : contient toutes les traductions en anglais

Exemple de structure :

```json
{
  "home.title": "Bienvenue",
  "home.description": "Description de la page",
  "page2.title": "Page 2"
}
```

#### Ajouter un élément traduisible dans le HTML

Pour qu'un élément soit automatiquement traduit, ajoutez l'attribut `data-translation` avec une clé correspondant à celle dans les fichiers JSON :

```html
<h1 data-translation="home.title">Texte par défaut</h1>
<p data-translation="home.description">Description par défaut</p>
```

#### Boutons de changement de langue

Les boutons de langue doivent avoir :

- La classe `lang-switch` pour être détectés par le script
- L'attribut `data-lang` avec le code de la langue (ex: "fr" ou "en")

```html
<button class="lang-switch" data-lang="fr">FR</button>
<button class="lang-switch" data-lang="en">EN</button>
```

#### Fonctionnement technique

1. **Au chargement de la page** : Le script vérifie si une langue a été sauvegardée dans le localStorage. Si oui, il l'applique, sinon il utilise le français par défaut.

2. **Lors du clic sur un bouton de langue** :

   - La nouvelle langue est sauvegardée dans le localStorage
   - Tous les éléments avec `data-translation` sont mis à jour
   - La préférence est conservée lors de la navigation

3. **Persistance** : Le choix de langue reste enregistré même après fermeture du navigateur grâce au localStorage.

#### Ajouter une nouvelle langue

1. Créer un nouveau fichier JSON (ex: `de.json` pour l'allemand)
2. Dans `main.js`, ajouter l'import et l'entrée dans `translations_map` :

```js
import deTranslations from "../de.json";

const translations_map = {
  en: enTranslations,
  fr: frTranslations,
  de: deTranslations,
};
```

3. Ajouter un bouton dans le HTML :

```html
<button class="lang-switch" data-lang="de">DE</button>
```
