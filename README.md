# Enregistrement auprès du serveur de commande et de contrôle (C2) - Botnet Iris

L'enregistrement auprès du serveur de commande et de contrôle (C2) dans le botnet **Iris** repose sur plusieurs protocoles réseau courants et méthodes spécifiques. Ces protocoles et méthodes permettent aux dispositifs compromis de communiquer avec le serveur C2, de recevoir des instructions, et de lancer des attaques. Voici une description détaillée de ce processus en utilisant les noms de protocoles et les méthodes spécifiques impliqués.

## 1. Utilisation des Protocoles de Communication pour se Connecter au Serveur C2

### a. Protocole Telnet (TCP Port 23) :
- **Iris** utilise fréquemment **Telnet**, un protocole simple qui permet des connexions à distance via **TCP (Transmission Control Protocol)**.
- Le malware **Iris** scanne les appareils IoT en utilisant le **port 23 (Telnet)** pour trouver des dispositifs vulnérables qui acceptent des connexions Telnet, souvent avec des identifiants par défaut (comme « admin/admin » ou « root/1234 »).
- Une fois connecté via Telnet, **Iris** peut exécuter des commandes à distance sur l'appareil compromis.

### b. Protocole SSH (TCP Port 22) :
- Bien que moins courant que Telnet, **Iris** peut aussi essayer d'utiliser des connexions **SSH** sur le **port 22** pour compromettre des dispositifs qui utilisent ce protocole pour la gestion à distance.
- **SSH** est plus sécurisé que Telnet car il chiffre les communications, mais certains appareils mal configurés ou avec des identifiants par défaut peuvent encore être vulnérables.

### c. Protocole HTTP/HTTPS (TCP Ports 80/443) :
- **Iris** utilise également le **protocole HTTP (Hypertext Transfer Protocol)** sur le **port 80** et **HTTPS (HTTP sécurisé)** sur le **port 443** pour se connecter au serveur C2.
- Ces connexions **HTTP/HTTPS** sont souvent utilisées pour télécharger le code malveillant, envoyer des informations d’enregistrement, ou recevoir des commandes depuis le C2.
- HTTPS, étant chiffré, permet de masquer le trafic malveillant, rendant plus difficile sa détection par les systèmes de surveillance.

## 2. Envoi d'Informations d'Enregistrement au Serveur C2

Une fois qu'un appareil est compromis, il doit s'enregistrer auprès du serveur C2 pour signaler qu'il est prêt à recevoir des commandes. Ce processus inclut :

### a. Utilisation de Telnet/SSH :
- Après avoir compromis un appareil via **Telnet** ou **SSH**, **Iris** exécute des commandes pour télécharger son binaire malveillant sur l'appareil.
- **Iris** envoie ensuite des **paquets TCP** pour établir une connexion avec le serveur C2. Cette connexion est généralement établie sur un port particulier (souvent non standard), comme le **port 6667 (IRC)** ou **6666**, qui peuvent être configurés dans le code du malware.

### b. Paquets TCP :
- Le **protocole TCP (Transmission Control Protocol)** est utilisé pour la transmission des informations d'enregistrement. Ces paquets contiennent généralement :
  - L'**adresse IP** de l'appareil infecté.
  - Le **type d'appareil** (par exemple, routeur, caméra IP, DVR).
  - Des informations sur le **système d'exploitation** et le **firmware**.

### c. Protocole HTTP/HTTPS :
- Les informations peuvent également être envoyées via des requêtes **HTTP** ou **HTTPS** sous forme de **requêtes GET** ou **POST** vers le serveur C2. **HTTPS** est préféré pour le chiffrement des données, rendant le trafic malveillant plus difficile à analyser.

## 3. Vérification de l'État du Bot et Réception des Commandes

### a. Ping (ICMP) :
- Certains botnets utilisent des requêtes **ICMP Echo Request** (connues sous le nom de **ping**) pour vérifier si les bots sont toujours connectés et en état de fonctionner.
- Cela permet au serveur C2 de surveiller régulièrement l'état des bots en envoyant des messages de vérification et en attendant une réponse (**ICMP Echo Reply**).

### b. Protocole TCP (Heartbeats) :
- En plus des pings ICMP, **Iris** utilise des connexions **TCP** pour échanger régulièrement des **paquets heartbeat** avec le serveur C2. Les "heartbeats" sont de petites requêtes envoyées périodiquement pour maintenir une connexion active entre le bot et le serveur.
- Si le serveur C2 ne reçoit pas ces heartbeats, il peut marquer le bot comme inactif et cesser d'envoyer des commandes à cet appareil jusqu'à ce qu'il soit réenregistré.

## 4. Envoi des Commandes et Lancement des Attaques DDoS

Une fois qu'un bot est enregistré auprès du serveur C2, il peut recevoir des commandes pour exécuter des attaques DDoS. **Iris** utilise plusieurs types de méthodes pour submerger une cible, en fonction des protocoles réseau.

### a. Attaque par Flood UDP (User Datagram Protocol) :
- **Iris** peut lancer des **attaques UDP Flood** en envoyant de grands volumes de paquets **UDP (User Datagram Protocol)** à des ports aléatoires de la cible.
- UDP est un protocole sans connexion, ce qui signifie qu'il n'y a pas d'accusé de réception ou de handshake. Cela rend les attaques plus rapides mais plus difficiles à filtrer.
- L'attaque submerge les serveurs de la cible avec des paquets qui doivent être traités, ce qui épuise les ressources.

### b. Attaque TCP SYN Flood :
- **TCP SYN Flood** est une autre technique fréquemment utilisée par **Iris**. Dans cette attaque, les bots envoient une grande quantité de **paquets SYN** à une cible, initiant le processus de **handshake TCP** mais sans jamais le terminer.
- Cela laisse la cible avec une multitude de connexions TCP "incomplètes" ouvertes, consommant ses ressources et empêchant de nouvelles connexions légitimes.

### c. Attaque DNS Amplification :
- **Iris** peut également lancer des **attaques par amplification DNS**. Le bot envoie des requêtes **DNS falsifiées (spoofed)** à des serveurs DNS ouverts, en utilisant l'adresse IP de la cible comme adresse de retour.
- Les serveurs DNS renvoient alors des réponses beaucoup plus volumineuses à la cible, amplifiant ainsi le volume de l'attaque.

### d. Attaque HTTP Flood :
- Une **attaque HTTP Flood** consiste à envoyer de nombreuses requêtes **HTTP GET** ou **POST** à un serveur web pour saturer sa bande passante et ses ressources de traitement.
- **Iris** peut coordonner des milliers de bots pour envoyer simultanément des requêtes HTTP, sursaturant ainsi le serveur et le rendant indisponible pour les utilisateurs légitimes.

## 5. Techniques d'Obfuscation et de Redondance

### a. Utilisation du Chiffrement (SSL/TLS) :
- Pour masquer la communication entre les bots et le serveur C2, **Iris** peut utiliser des **protocoles de chiffrement** comme **SSL/TLS (Secure Sockets Layer/Transport Layer Security)**. Cela permet de chiffrer les données échangées, rendant plus difficile leur analyse par les systèmes de sécurité.

### b. Rotation des Adresses IP du Serveur C2 :
- Pour éviter d'être bloqué par les systèmes de sécurité, le serveur C2 change fréquemment ses adresses IP ou ses noms de domaine. Cela peut être automatisé par des techniques comme le **Fast Flux**, qui permet de faire tourner les adresses IP associées à un domaine pour compliquer la détection et le blocage.
