---
description: BONUS - React from 0 to 1
---

# React

Cette est un bonus, elle est dédiée à React. Une des libraries les plus utilisées pour faire des interfaces web. Elle s'intègre très bien avec Symfony. Mais avant de commencer, il faut comprendre comment fonctionne React et comment l'utiliser. Alors, nous allons réaliser 2 projets.

- Countrix : un projet pour apprendre les bases de React
- Cinemax : un projet pour continuer sur les bases de React
- Symfony ❤ React : un projet pour intégrer React dans Symfony

## Projet Countrix

C'est un projet pour apprendre les bases de React. Nous allons utiliser l'API RestCountries pour récupérer des données sur les pays du monde par région. Une sélection des régions permettra d'afficher les pays de la région sélectionnée.

Commençons créer le projet Countrix avec Vite.

```bash
$ npm create vite@latest
```

Nommer le projet `countrix`, choisir `react` et `js` comme langage puis suivez les instructions `cd countrix`, `npm install` et `npm run dev`.

### Architecture du projet

Voici l'architecture du projet Countrix.

```bash
├── node_modules/       # Ce dossier contient les dépendances du projet
├── public/             # Ce dossier contient les fichiers statiques du projet
├── src/                # Ce dossier contient les fichiers sources du projet
│   ├── App.css         # Ce fichier contient le style du composant App
│   ├── App.jsx         # Ce fichier contient le composant App
│   ├── index.css       # Ce fichier contient le style de l'application
│   └── main.jsx        # Ce fichier contient le chargement de l'application
├── .eslintrc.cjs       # Ce fichier contient la configuration d'ESLint
├── .gitignore          # Ce fichier contient la liste des fichiers à ignorer par Git
├── package-lock.json   # Ce fichier contient la liste des dépendances du projet
├── package.json        # Ce fichier contient la configuration du projet utilisée par npm
├── index.html          # Ce fichier contient le point d'entrée de l'application
├── README.md           # Ce fichier contient la documentation du projet
└── vite.config.js      # Ce fichier contient la configuration de Vite
```

Il est temps de faire votre premier commit.

### Composant App

Le composant App est le composant principal de l'application. Il est défini dans le fichier `src/App.jsx`. Commençons par y ajouter le code dont nous avons besoin.

Une constante `region` qui contiendra la région sélectionnée et ajoutée au point de sortie (endpoint) de l'API RestCountries. On mettre l'Europe par défaut :

```jsx
const [region, setRegion] = useState('europe');
```

Maintenant, nous allons aussi définir une constante `countries` qui contiendra les pays de la région sélectionnée. Nous allons utiliser le hook `useEffect` pour faire une requête à l'API RestCountries et mettre à jour la constante `countries` :

```jsx
const [countries, setCountries] = useState([]);
```

Voilà nos deux constantes sont définies. Nous allons maintenant les utiliser pour afficher les pays de la région sélectionnée. Nous allons utiliser le hook `useEffect` pour mettre à jour la constante `countries` avec `setCoutries` à chaque fois que la région sélectionnée change.

```jsx
useEffect(() => {
  fetch(`https://restcountries.com/v3.1/region/${region}`)
    .then((response) => response.json())
    .then((data) => setCountries(data));
}, [region]);
```

Maintenant, on passe à l'affichage des pays. On utilise la méthode `map` pour parcourir le tableau `countries` et afficher les pays. Pour cela nous avons besoin de créer plusieurs composants `RegionSelector` et `CountryCard`. Saisissez le code suivant dans `return` du composant `App` :

```jsx
  return (
    <div className="App">
        <header>
            <h1>Countrix</h1>
            <RegionSelector onChange={setRegion} />
        </header>
        <div className="countries">
            {countries.map((country) => (
                <CountryCard key={country.cca2} country={country} />
            ))}
        </div>
    </div>
  )
```

### Composant RegionSelector

Ce composant permet de sélectionner une région. Commencez par créer un fichier `src/RegionSelector.jsx`. À présent il faut y ajouter le code suivant :

```jsx
import React from 'react'

function RegionSelector({ onChange }) {
    const regions = [
        { value: 'africa', label: 'Africa' },
        { value: 'america', label: 'Americas' },
        { value: 'asia', label: 'Asia' },
        { value: 'europe', label: 'Europe' },
        { value: 'oceania', label: 'Oceania' },
    ]

    return (
        <div className="regions">
            <select onChange={e => onChange(e.target.value)}>
                {regions.map(region => (
                    <option key={region.value} value={region.value}>
                        {region.label}
                    </option>
                ))}
            </select>
        </div>
    )
}

export default RegionSelector
```

### Composant CountryCard

Ce composant permet d'afficher les informations d'un pays. Commencez par créer un fichier `src/CountryCard.jsx`. À présent il faut y ajouter le code suivant :

```jsx
import React from 'react';

function CountryCard({ country }) {
    return (
        <div className="card">
            <div className="card-body">
                <h5 className="card-title">
                    {country.name.common} {country.flag ? country.flag : ''}
                </h5>
                <p className="card-text">Capitale: {
                    country.capital ? country.capital : 'N/A'
                    }</p>
                <p className="card-text">Population: {country.population.toLocaleString('fr-FR')}</p>
            </div>
        </div>
    );
}

export default CountryCard;
```

### CSS et conclusion

Libre à vous de styliser l'application comme vous le souhaitez. Nous avons fait le nécesssaire que l'application réponde aux besoins. Il suffit désormais de lancer la commande `npm run build` pour générer les fichiers statiques de l'application dans le dossier `dist`. Vous pouvez les déployer sur un serveur web.

---

Références :

- [React](https://react.dev/)
- [Vite](https://vitejs.dev/)
- [RestCountries](https://restcountries.com/)

