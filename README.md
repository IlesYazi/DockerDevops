# 🚀 Stack DevSecOps – Déploiement d’Applications avec Docker & Nginx

## Sommaire

- [Présentation](#présentation)
- [Architecture](#architecture)
- [Applications déployées](#applications-déployées)
- [Technologies & choix](#technologies--choix)
- [Lancement rapide](#lancement-rapide)
- [Accès aux applications](#accès-aux-applications)
- [Publication des images Docker](#publication-des-images-docker)
- [Sécurité & bonnes pratiques](#sécurité--bonnes-pratiques)
- [Répartition des tâches](#répartition-des-tâches)
- [Contact](#contact)

---

## Présentation

Ce projet met en place une stack complète de 4 applications (dont une statique HTML) pour un client, avec gestion de la sécurité, reverse proxy, et intégration de la passerelle de paiement Stripe.  
L’ensemble est déployé via un unique fichier `docker-compose.yaml` (Infrastructure as Code), et toutes les images sont publiées sur Docker Hub.

---

## Architecture

![Schéma d’architecture](docs/architecture.png)

---

## Applications déployées

- **Frontend** : Application React (interface utilisateur)
- **Backend** : API Node.js (Express) – intègre Stripe pour les paiements
- **Rocket-ecommerce** : Microservice e-commerce (Node.js)
- **Task-API** : Microservice de gestion de tâches (Node.js) – accessible en direct
- **Application statique** : Dossier HTML/CSS/JS servi par Nginx

---

## Technologies & choix

- **React** : Rapidité de développement, SPA moderne
- **Node.js/Express** : API REST performante
- **Nginx** : Reverse proxy performant et sécurisé
- **Docker** : Portabilité, reproductibilité, optimisation des images
- **Stripe** : Solution de paiement sécurisée et facile à intégrer

---

## Lancement rapide

```bash
git clone <repo>
cd <repo>
docker-compose up -d
```

---

## Accès aux applications

| Service              | Via Nginx (reverse proxy)         | Accès direct (local)      |
|----------------------|-----------------------------------|---------------------------|
| Frontend             | http://localhost:5085/            | —                         |
| Backend API          | http://localhost:5085/api/        | —                         |
| Rocket-ecommerce     | http://localhost:5085/ecommerce/  | —                         |
| Task API             | http://localhost:5085/task-api/   | http://localhost:8080     |
| Application statique | http://localhost:5085/static/     | —                         |

---

## Publication des images Docker

Toutes les images sont disponibles sur Docker Hub :

- `lmessia93/pizzatech-front`
- `lmessia93/pizzatech-back`
- `lmessia93/rocket-ecommerce`
- `lmessia93/task-api`

---

## Sécurité & bonnes pratiques

- **Reverse proxy** : Toutes les applications sauf une sont derrière Nginx.
- **Pentest whitebox** : `task-api` est exposée en direct pour permettre des tests de sécurité approfondis.
- **Images Docker optimisées** : Multi-stage build, taille réduite, bonnes pratiques Docker.
- **Variables d’environnement** : Centralisées et sécurisées dans le docker-compose.
- **Open source** : Code source et images publiés pour la communauté.

---

## Répartition des tâches

| Membre                      | Rôle / Tâches principales                                                                 |
|-----------------------------|------------------------------------------------------------------------------------------|
| **MBARGA Philippe Ivan**    | Lead DevSecOps, coordination du projet, optimisation des images Docker, sécurité globale |
| **Yazi Iles**               | Configuration et sécurisation du reverse proxy Nginx, gestion des accès réseau           |
| **MESSIA DOLIVEUX Lucas**   | Développement et intégration du backend (API Node.js), intégration de Stripe             |
| **LEROGNON Grégoire**       | Développement du frontend (React), intégration avec l’API, gestion de l’application statique |
| **NTANTU Japhet**           | Développement du microservice e-commerce, gestion du service task-api, documentation     |

