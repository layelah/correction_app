Remote Control Pro - Système de Contrôle à Distance
Version : 1.0.0

Développé par :

Abdoulaye Lah (GitHub)
Ousmane Mbaye (GitHub)
Moustapha Diagne (GitHub)
Bienvenue dans Remote Control Pro, une application client-serveur avancée conçue dans le cadre du cours de Java Avancé à l’École Supérieure Polytechnique de Dakar (Master 1 GLSI). Ce projet, réalisé par une équipe de trois développeurs talentueux, propose une solution moderne pour contrôler à distance des ordinateurs via une interface graphique intuitive et sécurisée. Que vous soyez un utilisateur technique ou non, ce document vous guidera pas à pas pour déployer et utiliser cette application en local sur votre machine, quel que soit votre système d’exploitation.

Description de l’Application
Aperçu Général
Remote Control Pro est un logiciel de contrôle à distance qui permet à un utilisateur (le client) de se connecter à une machine distante (le serveur) pour exécuter des commandes système, transférer des fichiers et surveiller les activités en temps réel. Inspiré par des outils comme SSH, ce projet combine une architecture réseau robuste avec une interface utilisateur conviviale, offrant une expérience fluide et sécurisée.

Fonctionnalités Principales
Exécution de Commandes à Distance : Envoyez des commandes système (par exemple, dir sous Windows ou ls sous Linux/macOS) depuis le client et recevez les résultats instantanément.
Gestion Multi-Clients : Le serveur peut gérer simultanément jusqu’à 10 clients grâce à une gestion multitâche basée sur un pool de threads.
Interface Graphique Intuitive : Développée avec JavaFX, l’interface offre une expérience utilisateur moderne pour le client (saisie de commandes, historique, sortie) et le serveur (liste des clients connectés, logs).
Sécurité :
Authentification par login/mot de passe (actuellement codée en dur pour la démonstration : admin / password123).
Communication sécurisée via SSL/TLS pour protéger les échanges entre le client et le serveur.
Transfert de Fichiers : Téléversez des fichiers du client vers le serveur ou téléchargez des fichiers du serveur vers le client.
Journalisation Avancée : Les événements du serveur (connexions, commandes, erreurs) sont enregistrés dans une interface graphique et dans des fichiers logs pour un suivi détaillé.
Historique des Commandes : Le client conserve un historique consultable des commandes exécutées.
Connexion/Déconnexion Dynamique : Connectez ou déconnectez le client du serveur en un clic.
Architecture Technique
Langage : Java (version 21).
Bibliothèques : JavaFX pour l’interface graphique, SLF4J/Logback pour la journalisation, et les API standard Java (Sockets, Threads, ProcessBuilder).
Communication : Basée sur le protocole TCP avec des sockets sécurisés (SSL).
Modularité : Le code est organisé en packages (client, server, core) pour une lisibilité et une maintenance optimales.
Cas d’Utilisation
Administrateurs Système : Exécuter des commandes à distance sans accès physique à la machine.
Éducation : Démontrer des concepts avancés de programmation réseau et multitâche.
Entreprises : Transférer des fichiers ou surveiller des serveurs à distance de manière sécurisée.
Prérequis pour le Déploiement
Pour déployer Remote Control Pro sur votre ordinateur, vous aurez besoin des outils suivants. Ne vous inquiétez pas : nous vous expliquerons comment les installer facilement, même si vous n’avez jamais utilisé de logiciel de développement auparavant.

Java Development Kit (JDK) 21
Le JDK est un ensemble d’outils qui permet d’exécuter des applications Java. Nous utilisons la version 21 pour garantir une compatibilité maximale avec les fonctionnalités modernes.
Maven
Maven est un outil qui simplifie la gestion et l’exécution du projet. Il télécharge automatiquement tout ce dont vous avez besoin pour lancer l’application.
Git (optionnel)
Git permet de télécharger le projet depuis GitHub. Si vous préférez, vous pouvez aussi télécharger une archive ZIP.
Guide d’Installation et de Déploiement
Suivez ces étapes attentivement pour installer et exécuter Remote Control Pro sur votre ordinateur. Ce guide est conçu pour fonctionner sur Windows, macOS et Linux.

Étape 1 : Vérification et Installation des Prérequis
1.1. Installer le JDK 21
Ouvrez votre navigateur (par exemple, Chrome ou Firefox).
Rendez-vous sur le site officiel d’Adoptium : https://adoptium.net/.
Sélectionnez la version JDK 21 (la dernière version stable au moment de la rédaction).
Choisissez votre système d’exploitation :
Windows : Téléchargez le fichier .msi et double-cliquez dessus pour l’installer.
macOS : Téléchargez le fichier .pkg et suivez les instructions à l’écran.
Linux : Téléchargez le fichier .tar.gz, extrayez-le, et suivez les instructions du site.
Une fois installé, ouvrez une fenêtre de commande :
Windows : Appuyez sur Windows + R, tapez cmd, et appuyez sur Entrée.
macOS/Linux : Ouvrez l’application « Terminal ».
Tapez java -version et appuyez sur Entrée. Vous devriez voir une sortie indiquant 21 (par exemple, openjdk 21.0.1). Si ce n’est pas le cas, contactez un administrateur.
1.2. Installer Maven
Allez sur le site officiel de Maven : https://maven.apache.org/download.cgi.
Téléchargez le fichier Binary zip archive (par exemple, apache-maven-3.9.6-bin.zip).
Extrayez le fichier dans un dossier facile à trouver (par exemple, C:\Maven sur Windows ou /home/user/maven sur Linux/macOS).
Ajoutez Maven à votre système :
Windows :
Faites un clic droit sur « Ce PC » > « Propriétés » > « Paramètres système avancés » > « Variables d’environnement ».
Dans « Variables système », trouvez Path, cliquez sur « Modifier », puis « Nouveau », et ajoutez le chemin vers le dossier bin de Maven (ex. : C:\Maven\apache-maven-3.9.6\bin).
macOS/Linux :
Ouvre le Terminal.
Tapez nano ~/.zshrc (ou nano ~/.bashrc selon votre système) et ajoutez cette ligne :
export PATH=$PATH:/chemin/vers/maven/apache-maven-3.9.6/bin.
Sauvegardez (Ctrl+O, Entrée, Ctrl+X) et tapez source ~/.zshrc (ou source ~/.bashrc).
Vérifiez l’installation en tapant mvn -version dans une fenêtre de commande. Vous devriez voir une version comme Apache Maven 3.9.6.
1.3. Télécharger le Projet
Ouvrez votre navigateur et allez sur : https://github.com/noreyni03/remote-control-project.
Cliquez sur le bouton vert « Code » et sélectionnez « Download ZIP ».
Extrayez l’archive dans un dossier de votre choix (par exemple, C:\Projets\remote-control-project ou /home/user/remote-control-project).
Étape 2 : Lancer le Serveur
Ouvrez une fenêtre de commande :
Windows : Windows + R, tapez cmd, Entrée.
macOS/Linux : Ouvrez « Terminal ».
Naviguez vers le dossier du projet :
Tapez cd chemin/vers/remote-control-project (ex. : cd C:\Projets\remote-control-project ou cd /home/user/remote-control-project) et appuyez sur Entrée.
Compilez le projet :
Tapez mvn clean install et appuyez sur Entrée. Cela peut prendre quelques minutes la première fois (Maven télécharge les dépendances). Vous verrez des messages dans la fenêtre ; assurez-vous que la dernière ligne indique BUILD SUCCESS.
Lancez le serveur :
Tapez mvn exec:java -pl :server -Dexec.mainClass="fr.uvsq.server.gui.ServerGUI" et appuyez sur Entrée.
Une fenêtre graphique s’ouvrira avec le titre « Remote Control Server - v1.0 ». Cliquez sur « Start Server » pour démarrer le serveur. Vous verrez un message indiquant « Server listening on port 5001 with SSL ».
Étape 3 : Lancer le Client
Ouvrez une deuxième fenêtre de commande (ne fermez pas celle du serveur).
Naviguez à nouveau vers le dossier du projet (répétez la commande cd de l’étape 2).
Lancez le client :
Tapez mvn exec:java -pl :client -Dexec.mainClass="fr.uvsq.client.gui.ClientGUI" et appuyez sur Entrée.
Une fenêtre graphique s’ouvrira avec le titre « Remote Control Pro - v1.0 ».
Connectez-vous au serveur :
Dans les champs « Login » et « Mot de passe », entrez respectivement admin et password123.
Cliquez sur « Connect ». Si tout fonctionne, vous verrez « ✅ Connecté au serveur » dans la zone de sortie.
Étape 4 : Utiliser l’Application
Depuis le Client :
Exécuter une commande : Tapez une commande dans le champ en bas (ex. : dir sur Windows ou ls sur Linux/macOS), puis cliquez sur « Execute ». La sortie s’affichera dans la zone centrale, et la commande sera ajoutée à l’historique à gauche.
Envoyer un fichier : Cliquez sur « Upload File », choisissez un fichier, et il sera envoyé au serveur.
Télécharger un fichier : Cliquez sur « Download File », entrez le nom du fichier (ex. : test.txt), choisissez où le sauvegarder, et il sera téléchargé depuis le serveur.
Effacer la sortie : Cliquez sur « Clear » pour vider la zone de sortie.
Déconnexion : Cliquez sur « Disconnect » pour fermer la connexion.
Depuis le Serveur :
La liste des clients connectés apparaît à gauche (ex. : 127.0.0.1:XXXX).
Les logs (connexions, commandes, erreurs) sont affichés à droite.
Cliquez sur « Stop Server » pour arrêter le serveur.
Remarques Importantes
Localhost : Par défaut, le client se connecte à 127.0.0.1 (votre propre ordinateur). Si le serveur est sur une autre machine, contactez un administrateur pour ajuster l’adresse IP dans le code.
Port : Le serveur utilise le port 5001. Assurez-vous qu’il n’est pas bloqué par un pare-feu.
Erreurs : Si une erreur apparaît (ex. : « Connexion refusée »), vérifiez que le serveur est bien lancé avant le client.
Contributions des Développeurs
Ce projet est le fruit d’une collaboration étroite entre trois étudiants passionnés :

Abdoulaye Lah : Conception de l’interface graphique (JavaFX), intégration SSL pour la sécurité, et gestion des transferts de fichiers.
Ousmane Mbaye : Développement de l’architecture client-serveur (sockets TCP, threads), authentification, et journalisation.
Moustapha Diagne : Implémentation de l’exécution des commandes système (ProcessBuilder), optimisation multitâche, et tests.
Contact
Pour toute question ou assistance, veuillez contacter l’équipe via GitHub :

Abdoulaye Lah : layelah
Ousmane Mbaye : noreyni03
Moustapha Diagne : moustaph18
Merci d’utiliser Remote Control Pro ! Nous espérons que cette application répondra à vos attentes et impressionnera par sa robustesse et son élégance.
