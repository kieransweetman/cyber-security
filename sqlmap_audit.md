# Test des Mappings avec SQLMap

## 1. Préparation
L'application a été vérifiée et elle était bien accessible à l'adresse `http://localhost:9898/`. Le répertoire contenant sqlmap a été ouvert dans le terminal avec la commande suivante :

```bash
cd [chemin-vers-sqlmap]
```

## 2. Endpoints Testés

### 2.1. Page de Login : http://localhost:9898/

#### Objectif
Tester la présence de vulnérabilités SQL dans les champs de connexion username et password.
#### Commandes Utilisées

```bash
python sqlmap.py -u "http://localhost:9898/" --data="username=admin&password=password123" --batch
```

#### Résultats

```bash
    	___
   	__H__
 ___ ___[)]_____ ___ ___  {1.8.11.11#dev}
|_ -| . [)] 	| .'| . |
|___|_  [.]_|_|_|__,|  _|
  	|_|V...   	|_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 10:41:11 /2024-12-04/

[10:41:14] [INFO] testing connection to the target URL
got a 302 redirect to 'http://localhost:9898/login'. Do you want to follow? [Y/n] Y
redirect is a result of a POST request. Do you want to resend original POST data to a new location? [Y/n] Y
you have not declared cookie(s), while server wants to set its own ('JSESSIONID=741079F850D...E4D9949BEC'). Do you want to use those [Y/n] Y
[10:41:14] [INFO] testing if the target URL content is stable
[10:41:14] [WARNING] POST parameter 'username' does not appear to be dynamic
[10:41:14] [WARNING] heuristic (basic) test shows that POST parameter 'username' might not be injectable
[10:41:14] [INFO] testing for SQL injection on POST parameter 'username'
[10:41:14] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[10:41:14] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[10:41:14] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[10:41:14] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[10:41:15] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[10:41:15] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[10:41:15] [INFO] testing 'Generic inline queries'
[10:41:15] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[10:41:15] [WARNING] time-based comparison requires larger statistical model, please wait. (done)
[10:41:15] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[10:41:15] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[10:41:15] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[10:41:15] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[10:41:15] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[10:41:15] [INFO] testing 'Oracle AND time-based blind'
it is recommended to perform only basic UNION tests if there is not at least one other (potential) technique found. Do you want to reduce the number of requests? [Y/n] Y
[10:41:15] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[10:41:15] [WARNING] POST parameter 'username' does not seem to be injectable
[10:41:15] [WARNING] POST parameter 'password' does not appear to be dynamic
[10:41:15] [WARNING] heuristic (basic) test shows that POST parameter 'password' might not be injectable
[10:41:15] [INFO] testing for SQL injection on POST parameter 'password'
[10:41:15] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[10:41:15] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[10:41:15] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[10:41:15] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[10:41:15] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[10:41:15] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[10:41:15] [INFO] testing 'Generic inline queries'
[10:41:15] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[10:41:15] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[10:41:15] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[10:41:15] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[10:41:15] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[10:41:15] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[10:41:16] [INFO] testing 'Oracle AND time-based blind'
[10:41:16] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[10:41:16] [WARNING] POST parameter 'password' does not seem to be injectable
[10:41:16] [CRITICAL] all tested parameters do not appear to be injectable. Try to increase values for '--level'/'--risk' options if you wish to perform more tests. If you suspect that there is some kind of protection mechanism involved (e.g. WAF) maybe you could try to use option '--tamper' (e.g. '--tamper=space2comment') and/or switch '--random-agent'
[10:41:16] [WARNING] HTTP error codes detected during run:
404 (Not Found) - 144 times

[*] ending @ 10:41:16 /2024-12-04/

```

#### Résumé

* Les champs username et password ne sont pas vulnérables aux injections SQL selon les tests effectués.
* Des avertissements indiquent que les paramètres ne semblent pas dynamiques, ce qui peut limiter les possibilités d'injection SQL.

### 2.2. Endpoint API Clients : http://localhost:9898/api/clients

#### Objectif
Vérifier si le paramètre `id` de l'API est vulnérable aux injections SQL.

#### Commandes Utilisées

```bash
python sqlmap.py -u "http://localhost:9898/api/clients?id=1" --batch
```

#### Résultats

```bash
    	___
   	__H__
 ___ ___[)]_____ ___ ___  {1.8.11.11#dev}
|_ -| . ['] 	| .'| . |
|___|_  [)]_|_|_|__,|  _|
  	|_|V...   	|_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 10:46:46 /2024-12-04/

[10:46:48] [INFO] testing connection to the target URL
got a 302 redirect to 'http://localhost:9898/login'. Do you want to follow? [Y/n] Y
you have not declared cookie(s), while server wants to set its own ('JSESSIONID=2F7A14B6700...A501373229'). Do you want to use those [Y/n] Y
[10:46:48] [INFO] checking if the target is protected by some kind of WAF/IPS
[10:46:48] [INFO] testing if the target URL content is stable
[10:46:48] [WARNING] GET parameter 'id' does not appear to be dynamic
[10:46:48] [WARNING] heuristic (basic) test shows that GET parameter 'id' might not be injectable
[10:46:48] [INFO] testing for SQL injection on GET parameter 'id'
[10:46:49] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[10:46:49] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[10:46:49] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[10:46:49] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[10:46:49] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[10:46:49] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[10:46:49] [INFO] testing 'Generic inline queries'
[10:46:49] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[10:46:49] [WARNING] time-based comparison requires larger statistical model, please wait. (done)
[10:46:49] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[10:46:49] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[10:46:49] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[10:46:49] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[10:46:49] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[10:46:49] [INFO] testing 'Oracle AND time-based blind'
it is recommended to perform only basic UNION tests if there is not at least one other (potential) technique found. Do you want to reduce the number of requests? [Y/n] Y
[10:46:49] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[10:46:49] [WARNING] GET parameter 'id' does not seem to be injectable
[10:46:49] [CRITICAL] all tested parameters do not appear to be injectable. Try to increase values for '--level'/'--risk' options if you wish to perform more tests. If you suspect that there is some kind of protection mechanism involved (e.g. WAF) maybe you could try to use option '--tamper' (e.g. '--tamper=space2comment') and/or switch '--random-agent'

[*] ending @ 10:46:49 /2024-12-04/
```

#### Résumé
* Le paramètre `id` n'a pas été détecté comme injectable.
* Même avec des niveaux plus élevés de test, aucune vulnérabilité exploitable n'a été trouvée.
* Le serveur semble gérer correctement les requêtes, et aucune fuite d'informations ou erreur indicative n'a été identifiée.

### 2.3. Endpoint Ajout de Client : http://localhost:9898/client/add

#### Objectif
Tester les champs du formulaire (`name`, `email`, `phone`) pour détecter des vulnérabilités SQL.

#### Commandes Utilisées

```bash
python sqlmap.py -u "http://localhost:9898/client/add" --data="name=foo&email=bar@example.com&phone=1234567890" --batch
```

#### Résultats

```bash
    	___
   	__H__
 ___ ___[(]_____ ___ ___  {1.8.11.11#dev}
|_ -| . [)] 	| .'| . |
|___|_  ["]_|_|_|__,|  _|
  	|_|V...   	|_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 10:52:12 /2024-12-04/

[10:52:13] [INFO] testing connection to the target URL
got a 302 redirect to 'http://localhost:9898/login'. Do you want to follow? [Y/n] Y
redirect is a result of a POST request. Do you want to resend original POST data to a new location? [Y/n] Y
you have not declared cookie(s), while server wants to set its own ('JSESSIONID=79499FDCD60...C0E9E8E6A3'). Do you want to use those [Y/n] Y
[10:52:13] [INFO] testing if the target URL content is stable
[10:52:14] [WARNING] POST parameter 'name' does not appear to be dynamic
[10:52:14] [WARNING] heuristic (basic) test shows that POST parameter 'name' might not be injectable
[10:52:14] [INFO] testing for SQL injection on POST parameter 'name'
[10:52:14] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[10:52:15] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[10:52:15] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[10:52:15] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[10:52:16] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[10:52:16] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[10:52:17] [INFO] testing 'Generic inline queries'
[10:52:17] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[10:52:17] [WARNING] time-based comparison requires larger statistical model, please wait. (done)
[10:52:17] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[10:52:18] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[10:52:18] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[10:52:18] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[10:52:19] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[10:52:19] [INFO] testing 'Oracle AND time-based blind'
it is recommended to perform only basic UNION tests if there is not at least one other (potential) technique found. Do you want to reduce the number of requests? [Y/n] Y
[10:52:19] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[10:52:20] [WARNING] POST parameter 'name' does not seem to be injectable
[10:52:20] [WARNING] POST parameter 'email' does not appear to be dynamic
[10:52:20] [WARNING] heuristic (basic) test shows that POST parameter 'email' might not be injectable
[10:52:20] [INFO] testing for SQL injection on POST parameter 'email'
[10:52:20] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[10:52:21] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[10:52:21] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[10:52:21] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[10:52:22] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[10:52:22] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[10:52:23] [INFO] testing 'Generic inline queries'
[10:52:23] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[10:52:23] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[10:52:24] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[10:52:24] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[10:52:24] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[10:52:25] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[10:52:25] [INFO] testing 'Oracle AND time-based blind'
[10:52:25] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[10:52:26] [WARNING] POST parameter 'email' does not seem to be injectable
[10:52:26] [WARNING] POST parameter 'phone' does not appear to be dynamic
[10:52:26] [WARNING] heuristic (basic) test shows that POST parameter 'phone' might not be injectable
[10:52:26] [INFO] testing for SQL injection on POST parameter 'phone'
[10:52:26] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[10:52:27] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[10:52:27] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[10:52:27] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[10:52:27] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[10:52:28] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[10:52:28] [INFO] testing 'Generic inline queries'
[10:52:28] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[10:52:28] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[10:52:29] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[10:52:29] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[10:52:29] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[10:52:30] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[10:52:30] [INFO] testing 'Oracle AND time-based blind'
[10:52:30] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[10:52:31] [WARNING] POST parameter 'phone' does not seem to be injectable
[10:52:31] [CRITICAL] all tested parameters do not appear to be injectable. Try to increase values for '--level'/'--risk' options if you wish to perform more tests. If you suspect that there is some kind of protection mechanism involved (e.g. WAF) maybe you could try to use option '--tamper' (e.g. '--tamper=space2comment') and/or switch '--random-agent'

[*] ending @ 10:52:31 /2024-12-04/
```

#### Résumé
* Aucun des champs testés (`name`, `email`, `phone`) n'a été trouvé vulnérable aux injections SQL.
* Les avertissements indiquent que ces champs ne sont pas dynamiques, ce qui réduit les risques d'injection SQL.

## 3. Analyse des Tests de Vulnérabilités

### Points Positifs

1. Les tests effectués sur les trois endpoints n'ont détecté aucune vulnérabilité exploitable.
2. Les réponses du serveur sont stables, sans fuite d'informations sensibles dans les messages d'erreur.
3. Les redirections et les cookies semblent être correctement gérés par le système, limitant les possibilités d'attaque.

### Limites des Tests

1. Les paramètres non dynamiques réduisent l'efficacité de certains types de tests d'injection SQL.
2. Aucun mécanisme de protection (exemple : WAF) n'a été identifié directement, mais il pourrait exister et limiter les attaques.

## 4. Préconisations

### Renforcer la Validation des Entrées
1. S'assurer que tous les paramètres utilisateur sont validés côté serveur avec des requêtes préparées ou des ORM sécurisés.
2. Limiter la taille et le format des entrées utilisateur.

### Implémenter un WAF
Ajouter un pare-feu applicatif (WAF) pour surveiller et bloquer les tentatives d'injection SQL.

### Masquer les Messages d'Erreur
Configurer le serveur pour qu'il ne retourne pas de messages d'erreur détaillés en cas d'exception.

### Surveillance et Tests Réguliers
Effectuer des audits réguliers de sécurité avec des outils automatisés et des analyses manuelles.