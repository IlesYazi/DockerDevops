# 🚀 Stack DevSecOps – Déploiement d’Applications avec Traefik & Docker

---

## 🧭 Démarche & solutions choisies

Dans le cadre de ce projet, nous avons opté pour une architecture moderne et modulaire, facilitant le développement, la sécurité et la maintenance :

- 🛡️ **Reverse proxy Traefik** : Simplicité de configuration, gestion dynamique des routes via labels Docker, dashboard intégré. Chaque service est exposé sur un sous-domaine local dédié.
- 🧩 **Découplage des services** : Chaque application (frontend, backend, e-commerce, task-api) est packagée dans un conteneur Docker indépendant, facilitant le déploiement et la scalabilité.
- 🌐 **Sous-domaines locaux** : Accès à chaque service via un sous-domaine personnalisé (ex : frontend.localhost, api.localhost, etc.) pour une expérience de développement proche de la production.
- 🚪 **Task-API hors proxy** : Le microservice task-api est exposé en dehors de Traefik pour permettre des tests directs, des audits de sécurité ou des accès spécifiques sans reverse proxy.
- 🔒 **Sécurité & bonnes pratiques** : Centralisation des variables d’environnement, images Docker optimisées, documentation claire et schéma d’architecture à jour.

L’ensemble de ces choix vise à garantir une stack DevSecOps robuste, évolutive et facilement maintenable.

---

## 🗂️ Sommaire
- [Présentation](#-présentation)
- [Architecture](#-architecture)
- [Applications déployées](#-applications-déployées)
- [Technologies & choix](#-technologies--choix)
- [Lancement rapide](#-lancement-rapide)
- [Accès aux applications](#-accès-aux-applications)
- [Publication des images Docker](#-publication-des-images-docker)
- [Sécurité & bonnes pratiques](#-sécurité--bonnes-pratiques)
- [Répartition des tâches](#-répartition-des-tâches)
- [Commandes utiles](#-commandes-utiles-du-début-à-larrêt)
- [Endpoints Task API](#-endpoints-de-lapi-task-api)

---

## 📖 Présentation

Ce projet met en place une stack complète de 4 applications pour un client, avec gestion de la sécurité, reverse proxy Traefik, et intégration de la passerelle de paiement Stripe.  
L’ensemble est déployé via un unique fichier `docker-compose.yaml` (Infrastructure as Code), et toutes les images sont publiées sur Docker Hub.

---

## 🏗️ Architecture

![Schéma d’architecture](docs/architecture.png)

---

## 🧩 Applications déployées

- ⚛️ **Frontend** : Application React (interface utilisateur)
- 🟩 **Backend** : API Node.js (Express) – intègre Stripe pour les paiements
- 🛒 **Rocket-ecommerce** : Microservice e-commerce (Node.js)
- 📝 **Task-API** : Microservice de gestion de tâches (Go)
- 🚦 **Traefik** : Reverse proxy moderne, dashboard intégré

---

## 🛠️ Technologies & choix

- ⚛️ **React** : Rapidité de développement, SPA moderne
- 🟩 **Node.js/Express** : API REST performante
- 🐹 **Go** : Microservice léger et rapide
- 🚦 **Traefik** : Reverse proxy dynamique, gestion des routes par labels, dashboard
- 🐳 **Docker** : Portabilité, reproductibilité, optimisation des images
- 💳 **Stripe** : Solution de paiement sécurisée et facile à intégrer

---

## ⚡ Lancement rapide

```bash
# 1. Cloner le dépôt
git clone <repo>
cd <repo>

# 2. (Optionnel) Vérifier/éditer le fichier hosts pour les sous-domaines locaux
# Ajouter dans /etc/hosts (Linux/Mac) ou C:\Windows\System32\drivers\etc\hosts (Windows) :
# 127.0.0.1 frontend.localhost api.localhost ecommerce.localhost

# 3. Lancer la stack en arrière-plan
docker-compose up -d
```

---

## 🌍 Accès aux applications

| 🧩 Service           | 🌐 URL d’accès                  |
|----------------------|---------------------------------|
| ⚛️ Frontend          | http://frontend.localhost       |
| 🟩 Backend API       | http://api.localhost/api        |
| 🛒 Rocket-ecommerce  | http://ecommerce.localhost      |
| 📝 Task API (Go)     | http://localhost:8080           |
| 🚦 Traefik Dashboard | http://localhost:8081           |

---

## 📦 Publication des images Docker

Toutes les images sont disponibles sur Docker Hub :
- `lmessia93/pizzatech-front`
- `lmessia93/pizzatech-back`
- `lmessia93/rocket-ecommerce`
- `lmessia93/task-api`

---

## 🔒 Sécurité & bonnes pratiques

- 🚦 **Reverse proxy Traefik** : Toutes les applications sont accessibles via des sous-domaines locaux.
- 🛡️ **Dashboard sécurisé** : Accès au dashboard Traefik sur un port dédié.
- 🐳 **Images Docker optimisées** : Multi-stage build, taille réduite, bonnes pratiques Docker.
- 🗝️ **Variables d’environnement** : Centralisées et sécurisées dans le docker-compose.
- 🌍 **Open source** : Code source et images publiés pour la communauté.

---

## 👥 Répartition des tâches

| 👤 Membre                   | 📝 Rôle / Tâches principales                                                      |
|----------------------------|----------------------------------------------------------------------------------|
| **MBARGA Philippe Ivan**    | DevSecOps, coordination du projet, optimisation des images Docker                  |
| **MESSIA DOLIVEUX Lucas**   | DevSecOps, propriétaire du Docker Hub, développement et intégration du backend (API Node.js) |
| **Yazi Iles**               | Configuration réseau, documentation, intégration de Stripe                        |
| **LEROGNON Grégoire**       | Développement du frontend (React), intégration avec l’API                         |
| **NTANTU Japhet**           | Développement du microservice e-commerce, gestion du service task-api, documentation |

---

## 🧰 Commandes utiles du début à l’arrêt

```bash
# 1. Cloner le dépôt
git clone <repo>
cd <repo>

# 2. (Optionnel) Vérifier/éditer le fichier hosts pour les sous-domaines locaux
# Ajouter dans /etc/hosts (Linux/Mac) ou C:\Windows\System32\drivers\etc\hosts (Windows) :
# 127.0.0.1 frontend.localhost api.localhost ecommerce.localhost

# 3. Lancer la stack en arrière-plan
docker-compose up -d

# 4. Voir les logs d’un service (exemple : backend)
docker-compose logs -f pizzatech-backend

# 5. Lister les conteneurs actifs
docker ps

# 6. Arrêter tous les services
docker-compose down

# 7. (Optionnel) Nettoyer les volumes (supprime les données persistantes)
docker-compose down -v
```

---

## 🔗 Endpoints de l'API Task API

### 📌 Obtenir toutes les tâches
- **Méthode :** GET
- **URL :** `/tasks`
- **Exemple de réponse JSON :**
```json
[
  {
    "id": 1,
    "title": "Faire les courses"
  },
  {
    "id": 2,
    "title": "Apprendre Go"
  }
]
```

### 📌 Ajouter une nouvelle tâche
- **Méthode :** POST
- **URL :** `/tasks`
- **Exemple de requête JSON :**
```json
{
  "title": "Acheter du pain"
}
```
- **Exemple de réponse JSON :**
```json
{
  "id": 3,
  "title": "Acheter du pain"
}
```

### 📌 Modifier une tâche existante
- **Méthode :** PUT
- **URL :** `/tasks/:id`
- **Exemple de requête JSON :**
```json
{
  "title": "Faire du sport"
}
```
- **Exemple de réponse JSON :**
```json
{
  "id": 1,
  "title": "Faire du sport"
}
```

### 📌 Supprimer une tâche
- **Méthode :** DELETE
- **URL :** `/tasks/:id`
- **Exemple de réponse JSON en cas de succès :**
```json
{
  "message": "Tâche supprimée"
}
```
- **Exemple de réponse JSON si la tâche n'existe pas :**
```json
{
  "error": "Tâche non trouvée"
}
```

---

