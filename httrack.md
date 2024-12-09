# Analyse des Sites avec HTTrack

Dans le cadre de ce projet de pentesting, l’outil **HTTrack** sera utilisé pour effectuer un clonage des sites cibles et récupérer leurs ressources accessibles. HTTrack est un outil de téléchargement de sites web permettant de récupérer l’intégralité du contenu d’un site pour une analyse hors ligne. Cette méthode est particulièrement utile pour explorer les éléments statiques d’un site, tels que les pages HTML, les fichiers JavaScript, CSS, ainsi que les images et autres ressources associées.

L’objectif est de cloner chaque site cible, y compris les applications web comme Laravel, Symfony ou WordPress, ainsi que la VM Big Data hébergée sur Hidora, afin d’analyser leur structure interne et d’identifier d’éventuelles vulnérabilités. 

Les sites suivants seront analysés dans ce projet :

1. **Application Laravel** : Le site web basé sur Laravel accessible à l’URL `http://45.86.36.184/public/`.
2. **VM Big Data à scanner** : La machine virtuelle (VM) Big Data avec les services Hadoop lancés sur Hidora.
3. **Symfony 7 et PHP 8** : Un site Symfony utilisant PHP 8.
4. **WordPress Standalone Protégé et Non Protégé** : Des installations WordPress, l’une protégée par des mesures de sécurité, et l’autre non protégée.

Cette étape de clonage nous permettra de recueillir des informations sur les ressources accessibles publiquement, et de préparer des analyses plus approfondies à l’aide d’autres outils de pentesting, comme **Nmap** et **Foremost**. L’objectif est de réaliser une évaluation complète de la sécurité des sites, en identifiant des vulnérabilités potentielles, telles que des failles de configuration, des erreurs de permissions ou des problèmes dans la gestion des ressources.

---

## Analyse de l'Application Laravel

L'application Laravel accessible à l'URL `http://45.86.36.184/public/` constitue un site web basé sur le framework PHP Laravel. Pour cette section, nous allons procéder à une analyse détaillée en utilisant **HTTrack** pour cloner les ressources accessibles publiquement et en évaluer la structure ainsi que les éventuelles vulnérabilités.

### 1. Clonage du Site Laravel avec HTTrack

La première étape consiste à récupérer l'intégralité du site à l'aide de l'outil HTTrack. Grâce à cet outil, nous clonons le site à l'URL mentionnée afin de sauvegarder localement toutes les ressources disponibles. Cela inclut les pages HTML, les fichiers CSS et JavaScript, ainsi que d'autres éléments comme les images ou les fichiers de configuration accessibles.

#### Commande exécutée :
```bash
httrack "http://45.86.36.184/public/" -O "laravel_scan" "+*.45.86.36.184/*"
```

#### Résultat de l'exécution :
![Capture d'écran](Image1.png)
Le site a été cloné avec succès et les ressources sont disponibles localement dans le répertoire laravel_scan.

### 2. Analyse des Ressources Clonées


#### Exploration du Répertoire Cloné

Après avoir cloné le site, nous accédons au répertoire contenant les ressources téléchargées pour examiner les fichiers récupérés.

**Commandes exécutées :**

```bash
cd laravel_scan
ls
```

**Résultat de l'exécution**
![Capture d'écran](Image2.png)

### Détails des fichiers récupérés

- **45.86.36.184** : Ce dossier contient les fichiers spécifiques au site web cloné.
- **backblue.gif** et **fade.gif** : Des fichiers image, potentiellement utilisés pour le design du site.
- **cookies.txt** : Un fichier contenant des informations sur les cookies récupérés lors du clonage.
- **hts-cache** : Répertoire contenant des informations de cache utilisées par HTTrack.
- **hts-log.txt** : Fichier journal généré par HTTrack, détaillant le processus de clonage.
- **index.html** : Une copie locale de la page d'accueil du site.

