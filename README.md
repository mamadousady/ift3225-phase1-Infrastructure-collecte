# Bibliothèque API- Phase 1
## Description
Api rest pour la collecte et l'analyse de l'ambiance sonore en bibliothéque 
.Ce système permet de collecter des données de niveau sonore depuis phyphox,interroger l'ambiance via des endpoints sémantiques,stocker les données dans MONGODB Atlas et authentifier les sources de données par clé API.

## Prérequis
|outils|Version|Lien|
|------|-------|----|
|Node.js|v26.0.0|https://nodejs.org/en|
|MongoDB Atlas||https://www.mongodb.com/products/platform/atlas-database|
|Phyphox|v1.2.0|Apple Store ou PlayStore|

```bash
git clone https://github.com/mamadousady/ift3225-phase1-Infrastructure-collecte.git
cd bibliotech api
npm install
cp .env.example .env
npm run seed
npm start
npm run dev


# Table des endpoints
|Méthode|Endpoint|Description
"Endpoints public"
| GET   |   /    |"Verification de l'état du serveur"|
| GET   |measurements/|"Dernieres mesures"|
| GET|observations|"Dernieres observations"|
| GET   |/ambiance/:location/history|"Historique d'ambiance sur une periode"|
| GET   |/ambiance/:location/quiet-hours|"Créneaux typiquement calme"|
| GET   |/ambiance/:location|"liste tous les lieux actifs"|

"Endpoints protégées"
Methdodes|Endpoint|"Corps requis"|Description
| POST  |/measurements|" {type,value,location,timestamp?}"|"envoyer une mesure capteur"|
| POST  |/observations|"{location,proximity,vibe,perceived_noise,occupants,disturbance_event?,notes?}|Envoyer une observation manuelle|

Endpoints admin
| POST|/devices|{name,locations,device-type?}|créer un nouveau device|
|GET|/devices|"dernieres"devices""|


# Test avec Postman

1-Tester un endpoint public
|Method|URL|

|GET|http://localhost:3000/|

2- Tester un endpoint protégé
|Method|URL|headers|Body|
|POST|http://localhost:3000/measurements|Content-type:application-json,x-api-key: demo-key-1234567890abcdef|{"type":"ambiance,"value":42.5,"location":"salle-412"|

3-Tester `un` endpoint `admin`
|Method|URL|
|GET|http://localhost:3000/devices|

4-Tester `un` endpoint `sémantique`
|Method|URL|

|GET|http://localhost:3000/ambiance/salle-412/history|

# fichier .env.example

```env 
#===========================================================================================================
# -Serveur
#==========================================================================================================

PORT=3000
SERVER_URL="http://localhost:3000"
#===========================================================================================================
#-MONGODB
#===========================================================================================================
MONGODB_URL=mongodb+srv://mamadousady_db_user:g18Pbr5GoqfVgMDu@cluster0.tpf7d6y.mongodb.net/?appName=Cluster0
retryWrites=true&w=majority

#===========================================================================================================
#-CLÉ API
#===========================================================================================================

apiKey=demo-key-1234567890abcdef




