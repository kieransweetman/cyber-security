---
CreatedAt: 2024-12-05:1412
LastUpdated: 2024-12-05:1449
---
# Rapport d'Analyse de Vulnérabilités et Recommandations

## Table des Matières
1. [Introduction](#introduction)
2. [Application SpringBoot](#application-springboot)
   - [Résultats](#résultats)
   - [Recommandations](#recommandations)
3. [Application Laravel](#application-laravel)
   - [Résultats](#résultats-1)
   - [Recommandations](#recommandations-1)
4. [Node Hidora](#node-hidora)
   - [Résultats](#résultats-2)
   - [Recommandations](#recommandations-2)
5. [Conclusion](#conclusion)

---

## Introduction
Ce document présente les résultats d'une analyse approfondie des vulnérabilités réalisée sur les cibles suivantes :
- Un projet local basé sur SpringBoot.
- Une application Laravel déployée sur une IP publique.
- Un nœud Big Data hébergé à `node179686-env-1839015-etudiant-d02-01.sh1.hidora.com`.

---

## Application SpringBoot
### Methodologie

#### Analyse du systeme
Un application web de SpringBoot qui accede a un base de donnee MySQL. L'application web emploie aussi des routes d'un `API`. 

L'application  possede 1 route lorsqu'un utilsateur n'est pas autentiqué, `/login`. Cette page contient un form html avec deux inputs `username` & `password`. Ceci ensuit envoie une methode `POST` au meme route.  

Sinon, lorsque l'utilisateur est autentiqué il serra aussi autorisé a accedé les routes suivantes : 
- `/api/clients`
- `/client/add`



#### Attaque sur l'infrastructure

- black box & white box testing
##### Black box testing

###### Identification des faiblesse 

1. Services de l'application
```bash
Host is up (0.00100s latency).
Not shown: 65528 closed tcp ports (reset)
PORT      STATE SERVICE    VERSION
3306/tcp  open  mysql? 
5000/tcp  open  rtsp
7000/tcp  open  rtsp
9898/tcp  open  monkeycom?
35729/tcp open  tcpwrapped
63693/tcp open  unknown
```

 Plusieurs PORT ouvert dont :
- `3306/tcp mysql` -> mysql database port
- `5000/tcp` & `7000/tcp rtsp` -> streaming protocl
- `9898/tcp monkeycom` -> serveur web

2. HTTP/HTTPS

3. Manipulation d'un utilisateur

####
- brute force on user form for weak credentials
- sql injection
- brute force on MySQL database instance
- CRSF attack




### Résultats
- Plusieurs ports ouverts détectés (53, 3306, 5000, etc.).
- Des tests de force brute sur les mots de passe ont révélé plusieurs identifiants faibles.
- Vulnérabilité possible de type CSRF détectée lors des tentatives de connexion.

### Recommandations
- Appliquer une politique stricte de mots de passe forts voir 2FA.
- Valider les cookies côté serveur pour empêcher les attaques CSRF.
- Limiter les ports ouverts et configurer des règles de pare-feu adéquates.

---

## Application Laravel
### Methodologie
### Résultats
- Le scan Nmap a révélé des ports exposés SSH (22) et HTTP (80).
- Le scan des répertoires a identifié des fichiers sensibles mais pas accessible (403 lorsque on essaye d'accèder e.g., `.bash_history`, `.htpasswd`).

### Recommandations
- Sécuriser les fichiers sensibles avec des mécanismes de contrôle d'accès appropriés.

---

## Node Hidora
### Methodologie
### Résultats
- Le scan Nmap a détecté des services SSH et HTTP actifs fonctionnant sur Jetty.
- Des vulnérabilités potentielles liées aux versions obsolètes de Jetty.

### Recommandations
- Mettre à jour Jetty vers la dernière version pour corriger les vulnérabilités connues.

---

## Conclusion

