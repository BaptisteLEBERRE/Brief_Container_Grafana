# Brief_Container_Grafana

## Ubuntu - Connexion au serveur Linux :

``# ssh user@10.10.51.151``

-Première connexion,

-Changement du mot de passe,

-Déconnexion automatique,

-Deuxième connexion.

## FileZilla - Création du dossier et transfert des fichiers :

-Insertion de l'hôte (``sftp://10.10.51.151``), de l'identifiant (``user1``) et du mot de passe.

-Insertion du chemin du dossier originel dans ``Site Local`` (``C:\Users\utilisateur\Desktop\Briefs\Brief_Container_Grafana\``),

-Création dossier de réception sur le serveur (``/home/user1/docker/country_vaccinations``),

-Transfert des fichiers ``docker-compose.yaml`` et ``country_vaccinations.sql``.

## Ubuntu - Montage du docker :

-Déplacement sur le dossier de réception (``cd /home/user1/docker/country_vaccinations``),

-Connexion à docker (``sudo docker`` suivi du mot de passe docker),

-Optionel : Installation de docker-compose sur le serveur (``sudo apt install docker-compose``),

-Montage du docker-compose.yaml (``docker-compose up -d``) qui contient :

``version: "2"

services:
  grafana:
    image: grafana/grafana:latest
    ports:
      - 3000:3000
    user: "root"

  mysql:
    image: mysql:5.7
    ports:
    - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: country_vaccinations
    volumes:
    - ./country_vaccinations.sql:/docker-entrypoint-initdb.d/init.sql``
    
Avec les deus services Grafana et MySQL. ``image`` correspond au type de service et à sa version, ``port`` au port utilisé, ``user`` et ``environment`` les renseignements supplémentaires.
    
L'instruction dans ``volumes`` récupère les données du fichier ``country_vaccinations.sql`` et les monte dans le docker MySQL.


    
    
