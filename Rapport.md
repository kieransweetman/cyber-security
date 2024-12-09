---
CreatedAt: 2024-12-05:1412
LastUpdated: 2024-12-09:0945
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

### Méthodologie

#### Analyse du système
Une application web développée avec SpringBoot accède à une base de données MySQL. Cette application expose plusieurs routes via une API.

L'application possède une seule route accessible sans authentification : `/login`. Cette page contient un formulaire HTML avec deux champs `username` et `password`, et envoie une requête `POST` à la même URL.

Une fois l'utilisateur authentifié, il peut accéder aux routes suivantes :
- `/api/clients`
- `/client/add`

---

### Attaque sur l'infrastructure

#### Tests effectués

##### Scanning des ports ouverts
```bash
Host is up (0.00100s latency).
Not shown: 65528 closed tcp ports (reset)
PORT      STATE SERVICE    VERSION
3306/tcp  open  mysql
5000/tcp  open  rtsp
7000/tcp  open  rtsp
9898/tcp  open  monkeycom?
35729/tcp open  tcpwrapped
63693/tcp open  unknown
````

- **Port 3306**: Exposition possible de la base de données MySQL.
- **Ports 5000 et 7000**: Protocoles RTSP identifiés, potentiellement liés à des outils de streaming locaux.
- **Port 9898**: Serveur web accessible sur `/login`, vulnérable à des attaques par force brute.

##### Tests de vulnérabilités spécifiques

- **Brute force**:
    - Attaque sur `/login` révélant des identifiants faibles.
    - Tentative de connexion à la base de données MySQL par Brute force et avec des mots de passe par défaut.
- **Injection SQL**:
    - Mapping `/client/add` 
```bash
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.64.1:9898/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /home/kali/Downloads/api-endpoints.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/api/clients          (Status: 200) [Size: 60332]
Progress: 269 / 270 (99.63%)
===============================================================
Finished
===============================================================

```

- **CSRF**:
    - Analyse des requêtes POST montrant l'absence de protection contre les attaques CSRF.

---

### Résultats

#### Failles détectées

- Plusieurs ports ouverts, notamment des services non sécurisés (RTSP, MySQL).
- Absence de mécanismes de sécurité sur `/login` (e.g., protections anti-CSRF, captcha, 2FA).


---

### Recommandations

#### Sécurisation des ports

2. Restreindre l’accès à MySQL en le liant uniquement à `127.0.0.1` pour éviter les connexions externes. 

#### Protection des utilisateurs

1. Implémenter une politique stricte de mots de passe forts (longueur minimale, complexité).
2. Activer l'authentification à deux facteurs (2FA) pour toutes les connexions.

#### Protection des endpoints

1. Implémenter des jetons CSRF pour toutes les requêtes POST.
2. Protéger les routes sensibles avec des validations d’entrée robustes pour éviter les injections SQL.
3. Ajouter des mécanismes comme Captcha pour empêcher les attaques par force brute sur les formulaires de connexion. 
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

