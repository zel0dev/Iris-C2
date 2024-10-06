# 🔐 Enregistrement auprès du serveur C2 - Botnet Iris

L'enregistrement des bots auprès du serveur de commande et de contrôle (**C2**) dans **Iris** repose sur plusieurs protocoles et méthodes spécifiques.

## 1. 🌐 Connexion au Serveur C2

- **Telnet (TCP 23)** : Iris scanne et compromet des appareils via Telnet avec des identifiants par défaut (ex. `admin/admin`).
- **SSH (TCP 22)** : Connexion sécurisée, mais vulnérable si mal configurée.
- **HTTP/HTTPS (TCP 80/443)** : Utilisé pour télécharger des binaires malveillants ou envoyer des commandes. **HTTPS** chiffre le trafic, le rendant difficile à détecter.

## 2. 📡 Enregistrement du Bot

- **Telnet/SSH** : Après compromission, Iris envoie des **paquets TCP** pour établir la connexion C2 (souvent sur des ports comme **6667**).
- **TCP** : Utilisé pour transmettre l'adresse IP, type d'appareil, OS, etc.
- **HTTP/HTTPS** : Informations envoyées via des requêtes **GET/POST** avec chiffrement via **HTTPS**.

## 3. 🔄 Vérification du Bot et Réception des Commandes

- **ICMP (Ping)** : Vérification régulière via des requêtes **ICMP Echo Request**.
- **TCP (Heartbeats)** : Iris échange des **paquets heartbeat** pour maintenir une connexion active avec le C2.

## 4. 💥 Attaques DDoS

- **UDP Flood** : Iris envoie de nombreux paquets **UDP** pour surcharger la cible sans nécessiter de connexion.
- **TCP SYN Flood** : Inondation de paquets **SYN** pour bloquer des connexions TCP légitimes.
- **DNS Amplification** : Envoie des requêtes **DNS spoofées**, amplifiant le volume d'attaque via les serveurs DNS.
- **HTTP Flood** : Iris envoie des requêtes **HTTP GET/POST** massives pour épuiser les ressources d'un serveur web.

## 5. 🛡️ Techniques d'Obfuscation

- **Chiffrement SSL/TLS** : Utilisé pour chiffrer les communications et masquer le trafic entre les bots et le C2.
- **Rotation d'IP (Fast Flux)** : Changement fréquent des adresses IP ou domaines du C2 pour éviter la détection.

