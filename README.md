<h1 align="center">🕊️ Iris C2 - Created By Zekrom X Zel0dev 🕊️</h1>

![image](https://github.com/user-attachments/assets/968c5340-6b6b-474b-ac2b-ec740248e0c9)

<h1 align="center">🔐 Enregistrement auprès du serveur C2 - Botnet Iris 🔐</h1>

<p align="center">
L'enregistrement des bots auprès du serveur de commande et de contrôle (C2) dans Iris s'effectue selon des protocoles et méthodes avancés, garantissant une efficacité optimale dans la gestion et le contrôle des appareils compromis.
</p>

<h1 align="center">🌐 Connexion au Serveur C2 🌐</h1>

- **Telnet (TCP 23)** : Iris identifie et prend le contrôle d'appareils via Telnet en exploitant des identifiants par défaut (par ex. `admin/admin`), démontrant sa capacité à détecter les failles les plus basiques.
- **SSH (TCP 22)** : Malgré sa sécurisation, **SSH** peut être vulnérable si mal configuré, et Iris exploite cette opportunité pour établir une connexion solide.
- **HTTP/HTTPS (TCP 80/443)** : Iris utilise ces protocoles pour télécharger des binaires malveillants ou transmettre des commandes, et **HTTPS** assure un chiffrement qui rend les activités difficiles à détecter.

<h1 align="center">📡 Enregistrement du Bot 📡</h1>

- **Telnet/SSH** : Une fois le contrôle pris, Iris envoie des **paquets TCP** pour inscrire le bot auprès du C2, généralement sur des ports comme **6667**, garantissant une liaison stable.
- **TCP** : Ce protocole assure la transmission d’informations cruciales, telles que l’adresse IP, le type d’appareil, ou encore le système d'exploitation.
- **HTTP/HTTPS** : L'enregistrement passe aussi par des requêtes **GET/POST**, sécurisées grâce au chiffrement **HTTPS**, renforçant la confidentialité.

<h1 align="center">🔄 Vérification du Bot et Réception des Commandes 🔄</h1>

- **ICMP (Ping)** : Iris assure la disponibilité des bots via des requêtes **ICMP Echo Request**, garantissant un suivi constant.
- **TCP (Heartbeats)** : L’échange de **paquets heartbeat** permet à Iris de maintenir une connexion active et stable avec le C2.

<h1 align="center">💥 Attaques DDoS 💥</h1>

- **UDP Flood** : Iris inonde les cibles de paquets **UDP**, les surchargent efficacement sans besoin de connexion.
- **TCP SYN Flood** : L’envoi massif de paquets **SYN** paralyse les connexions TCP légitimes.
- **DNS Amplification** : Iris exploite les serveurs **DNS** pour amplifier ses attaques en inondant les cibles de trafic.
- **HTTP Flood** : En envoyant des requêtes **HTTP GET/POST** en masse, Iris épuise rapidement les ressources des serveurs web ciblés.

<h1 align="center">🛡️ Techniques d'Obfuscation 🛡️</h1>

- **Chiffrement SSL/TLS** : Iris chiffre les communications entre les bots et le C2, masquant ses activités.
- **Rotation d'IP (Fast Flux)** : Le changement rapide d’adresses IP ou de domaines C2 rend la détection quasi impossible, garantissant une discrétion totale.
