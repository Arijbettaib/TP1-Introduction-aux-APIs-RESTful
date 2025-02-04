# 🌦 Weather App

Une application Node.js qui récupère les données météorologiques d'une ville en utilisant l'API OpenWeatherMap.

## 📌 Fonctionnalités
- 🔄 Récupération des informations météorologiques en temps réel
- 🌡 Affichage de la température actuelle, minimale et maximale
- 💧 Affichage du taux d'humidité et de la pression atmosphérique
- 💨 Affichage de la vitesse et de la direction du vent
- 🌅 Affichage des heures de lever et coucher du soleil
- 🌎 Localisation précise avec le pays de la ville recherchée
- 🛠 Gestion avancée des erreurs (ville introuvable, problème de connexion, dépassement de quota API...)
- 🚀 Utilisation de `axios` et `async/await` pour un code plus performant
- 📏 Unités de mesure adaptées (Celsius, m/s, hPa...)

## 🛠️ Prérequis
- 📌 Node.js installé sur votre machine
- 🔑 Un compte OpenWeatherMap avec une clé API valide

## 🚀 Installation
1. **Clonez le dépôt GitHub** :
   ```sh
   git clone https://github.com/Arijbettaib/weather-app.git
   cd weather-app
   ```
2. **Installez les dépendances nécessaires** :
   ```sh
   npm install
   ```
3. **Ajoutez votre clé API dans le fichier `index.js`** :
   ```js
   const API_KEY = "VOTRE_CLE_API";
   ```

## 🎯 Utilisation
Exécutez le programme avec la commande suivante :
```sh
node index.js
```

Vous pouvez modifier la ville directement dans le fichier `index.js` :
```js
getWeatherData("Sousse");
```
Ou bien appeler la fonction avec une entrée utilisateur :
```js
const readline = require("readline");
const rl = readline.createInterface({ input: process.stdin, output: process.stdout });
rl.question("Entrez une ville : ", (ville) => {
    getWeatherData(ville);
    rl.close();
});
```

## 📜 Explication du code
### Importation des modules
```js
const axios = require("axios");
```
Nous utilisons `axios` pour effectuer les requêtes HTTP.

### Définition des constantes
```js
const API_KEY = "VOTRE_CLE_API";
const BASE_URL = "http://api.openweathermap.org/data/2.5/weather";
```
Nous définissons la clé API et l'URL de base de l'API OpenWeatherMap.

### Fonction pour récupérer les données météorologiques
```js
async function getWeatherData(city) {
    try {
        const url = `${BASE_URL}?q=${encodeURIComponent(city)}&appid=${API_KEY}&units=metric`;
        const response = await axios.get(url);
        const data = response.data;
```
- La fonction `getWeatherData(city)` est asynchrone.
- Nous construisons l'URL avec le nom de la ville et la clé API.
- `axios.get(url)` effectue une requête HTTP pour récupérer les données.

### Affichage des données
```js
        console.log(`📍 Ville: ${data.name}, ${data.sys.country}`);
        console.log(`🌦 Description: ${data.weather[0].description}`);
        console.log(`🌡 Température actuelle: ${data.main.temp}°C`);
        console.log(`🔺 Température max: ${data.main.temp_max}°C`);
        console.log(`🔻 Température min: ${data.main.temp_min}°C`);
        console.log(`💧 Humidité: ${data.main.humidity}%`);
        console.log(`🌬 Pression: ${data.main.pressure} hPa`);
        console.log(`💨 Vent: ${data.wind.speed} m/s, direction ${data.wind.deg}°`);
        console.log(`🌅 Lever du soleil: ${new Date(data.sys.sunrise * 1000).toLocaleTimeString()}`);
        console.log(`🌇 Coucher du soleil: ${new Date(data.sys.sunset * 1000).toLocaleTimeString()}`);
```
- `data.name` et `data.sys.country` affichent la ville et le pays.
- `data.weather[0].description` affiche la description du temps.
- `data.main.temp`, `data.main.temp_max` et `data.main.temp_min` affichent les températures en °C.
- `data.wind.speed` et `data.wind.deg` affichent la vitesse et la direction du vent.
- `new Date(data.sys.sunrise * 1000).toLocaleTimeString()` convertit le timestamp Unix en heure locale.

### Gestion des erreurs
```js
    } catch (error) {
        if (error.response) {
            console.error("❌ Erreur: ", error.response.data.message);
        } else {
            console.error("❌ Erreur de connexion: ", error.message);
        }
    }
}
```
- `error.response.data.message` affiche un message d'erreur si la ville n'est pas trouvée.
- `error.message` gère les erreurs de connexion.

## 📚 Dépendances
- [Axios](https://www.npmjs.com/package/axios) : pour effectuer des requêtes HTTP de manière efficace
- [Readline](https://nodejs.org/api/readline.html) : pour permettre l'entrée utilisateur en ligne de commande

## 🔥 Exemple de sortie
```
📍 Ville: Sousse, TN
🌦 Description: ciel dégagé
🌡 Température actuelle: 22°C
🔺 Température max: 25°C
🔻 Température min: 18°C
💧 Humidité: 65%
🌬 Pression: 1015 hPa
💨 Vent: 3.2 m/s, direction 180°
🌅 Lever du soleil: 06:30 AM
🌇 Coucher du soleil: 06:45 PM
```

## 🚀 Améliorations futures
- 📊 Ajout d'une fonctionnalité pour afficher la météo sur plusieurs jours
- 🌍 Ajout de la détection automatique de la localisation via l'adresse IP
- 📱 Création d'une interface web pour afficher les données plus visuellement

## 📝 Licence
Ce projet est sous licence MIT. Vous pouvez l'utiliser et le modifier librement.
