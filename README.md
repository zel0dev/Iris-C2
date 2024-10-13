<h1 align="center">🪐 Iris C2 - Created By Zekrom X Zel0dev</h1>

![image](https://github.com/user-attachments/assets/968c5340-6b6b-474b-ac2b-ec740248e0c9)

<h1 align="center">🔐 Enregistrement auprès du serveur C2 - Botnet Iris</h1>

L'enregistrement des bots auprès du serveur de commande et de contrôle (**C2**) dans **Iris** repose sur plusieurs protocoles et méthodes spécifiques.

<h1 align="center">🌐 Connexion au Serveur C2</h1>

- **Telnet (TCP 23)** : Iris scanne et compromet des appareils via Telnet avec des identifiants par défaut (ex. `admin/admin`).
- **SSH (TCP 22)** : Connexion sécurisée, mais vulnérable si mal configurée.
- **HTTP/HTTPS (TCP 80/443)** : Utilisé pour télécharger des binaires malveillants ou envoyer des commandes. **HTTPS** chiffre le trafic, le rendant difficile à détecter.

<h1 align="center">📡 Enregistrement du Bot</h1>

- **Telnet/SSH** : Après compromission, Iris envoie des **paquets TCP** pour établir la connexion C2 (souvent sur des ports comme **6667**).
- **TCP** : Utilisé pour transmettre l'adresse IP, type d'appareil, OS, etc.
- **HTTP/HTTPS** : Informations envoyées via des requêtes **GET/POST** avec chiffrement via **HTTPS**.

<h1 align="center">🔄 Vérification du Bot et Réception des Commandes</h1>

- **ICMP (Ping)** : Vérification régulière via des requêtes **ICMP Echo Request**.
- **TCP (Heartbeats)** : Iris échange des **paquets heartbeat** pour maintenir une connexion active avec le C2.

<h1 align="center">💥 Attaques DDoS</h1>

- **UDP Flood** : Iris envoie de nombreux paquets **UDP** pour surcharger la cible sans nécessiter de connexion.
- **TCP SYN Flood** : Inondation de paquets **SYN** pour bloquer des connexions TCP légitimes.
- **DNS Amplification** : Envoie des requêtes **DNS spoofées**, amplifiant le volume d'attaque via les serveurs DNS.
- **HTTP Flood** : Iris envoie des requêtes **HTTP GET/POST** massives pour épuiser les ressources d'un serveur web.

<h1 align="center">🛡️ Techniques d'Obfuscation</h1>

- **Chiffrement SSL/TLS** : Utilisé pour chiffrer les communications et masquer le trafic entre les bots et le C2.
- **Rotation d'IP (Fast Flux)** : Changement fréquent des adresses IP ou domaines du C2 pour éviter la détection.

