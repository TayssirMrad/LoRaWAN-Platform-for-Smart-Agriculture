# LoRaWAN-Platform-for-Smart-Agriculture
# AWS-Config-for-Smart-Agriculture
![smart-farming-agriculture-du-futur-iot](https://github.com/LoRaWAN-Platform-for-Smart-Agriculture/AWS-Grafana-for-Smart-Agriculture-/assets/60198040/6437a22c-ec94-47b1-a758-5443a39beda7)

### 1) AWS IoT Core et de son rôle
AWS IoT Core est un service géré par Amazon Web Services. C’est une PaaS (Platform en tant que Service) qui occupe une place centrale dans notre architecture IoT car il assure une gestion sécurisée de la connectivité de nos dispositifs, du traitement des messages MQTT reçus et envoyés, et prend en charge des fonctionnalités de routage de données entre les dispositifs et les autres services d’AWS dont nous allons parler par la suite. 
![Picture1](https://github.com/LoRaWAN-Platform-for-Smart-Agriculture/AWS-Grafana-for-Smart-Agriculture-/assets/60198040/92cb7458-508e-4627-bff6-2c52ba27fe97)

### 2) Configuration de la Gateway
La plateforme cloud AWS IoT Core permet aux appareils connectés d'interagir facilement et en toute sécurité avec les applications cloud et d'autres dispositifs. 
Elle peut prendre en charge des milliards de transactions par jour provenant de milliers d'appareils, rationalisant la communication entre le nombre croissant d'objets connectés à Internet (y compris les capteurs, actionneurs, dispositifs embarqués, serveurs périphériques, passerelles, appareils mobiles et dispositifs portables) et le cloud.
![Picture1](https://github.com/LoRaWAN-Platform-for-Smart-Agriculture/AWS-Grafana-for-Smart-Agriculture-/assets/60198040/05308c25-b3df-4698-9a24-c50f70f291ed)

#### Étape 1 : Création d’un compte AWS
#### Étape 2: Création d’utilisateur et accordez des autorisations (Add an IAM role)
#### Étape 3 : Prendre le identificateur unique du gateway 
#### Étape 4 : Configurer le gateway et la création des certificats 
#### Étape 5 : Ajout des configuration au UI Web du gateway
#### Étape 6 : Vérification du dernier upLink reçu 
![78645312](https://github.com/LoRaWAN-Platform-for-Smart-Agriculture/AWS-Config-for-Smart-Agriculture-/assets/60198040/03ca05cf-eb35-44a3-b114-86686bda696f)


### 3) Configuration du device
Lorsque on connecte la passerelle à AWS IoT Core pour LoRaWAN, il suffit d'ajouter le périphérique final à AWS IoT Core pour LoRaWAN, de le démarrer, et le périphérique final commencera à communiquer avec la passerelle.
![Picture4](https://github.com/LoRaWAN-Platform-for-Smart-Agriculture/AWS-Grafana-for-Smart-Agriculture-/assets/60198040/8fce2745-9045-4293-b0e4-1ed584c1c725)

#### Etape 1 : Créer un profil de device
Lorsque nous connectons votre passerelle à AWS IoT Core pour LoRaWAN, la première étape est de créer un profil de device. Ce profil définit les caractéristiques et les paramètres de configuration spécifiques :

- Frequence (RFRegion) : EU868

- Version MAC : 1.0.3

- Protocole : OTAA

![789465139846513](https://github.com/LoRaWAN-Platform-for-Smart-Agriculture/AWS-Config-for-Smart-Agriculture-/assets/60198040/68c4de1a-041b-4336-bc41-008ca74395a7)


#### Etape 2 : Créer un profil de service
En plus, nous avons créer un profil de service pour définir les services et les fonctionnalités disponibles pour le périphérique final. Cela peut inclure des services tels que la gestion des données, la sécurité, les mises à jour logicielles, et d'autres fonctionnalités essentielles.

#### Etape 3 :  Créer des rôles IAM pour les destinations

#### Etape 4 : Créer une destination pour la date de charge utile du nœud final

#### Etape 5 : Vérifier la connectivité du périphérique

#### NB : pour Configurer Arduino nous avons utiliser la bibliotheque : "arduino-lmic" 

source : https://github.com/matthijskooijman/arduino-lmic/blob/master/examples/ttn-otaa/ttn-otaa.ino 

![Picture9](https://github.com/LoRaWAN-Platform-for-Smart-Agriculture/AWS-Config-for-Smart-Agriculture-/assets/60198040/915bd237-f9b1-4048-9c8d-08f624e7c5df)

NB: Le code Arduino "Code_Connectivity_Arduino_LoraWAN_AWS" peut être utilisé pour tester la connéctivité de la carte avec AWS IoT.

![image](https://github.com/LoRaWAN-Platform-for-Smart-Agriculture/AWS-Config-for-Smart-Agriculture-/assets/60198040/7b964f79-40fb-41b1-9bca-8da8fb5b1da9)


### 4) Routage des Données via une Rule
En effet, au niveau des devices, on spécifie le nom de  la règle qui va traiter les données de notre device afin que les services AWS IoT puissent utiliser les données.
Nous avons nommée la règle que nous voulons utilisé, “parse_io_data” de manière à refléter clairement l'action qu'elle accomplit.

![Picture7](https://github.com/LoRaWAN-Platform-for-Smart-Agriculture/AWS-Config-for-Smart-Agriculture-/assets/60198040/0ed7643c-8058-4d70-bb4f-09f078b0ad9a)

  
lors de la création d’une règles, nous pouvons aussi définir une ou plusieurs actions que cette règle va invoquer lorsqu’elle est évaluée comme vraie/que ses conditions sont remplies.
Nous avons choisis l’action de règle nommée “Lambda” sur AWS qui va diriger les messages lu sur le topic MQTT “lorawan” vers une fonction AWS lambda. Une fonction qui va nous permettre d’automatiser davantage le processus.


![Picture6](https://github.com/LoRaWAN-Platform-for-Smart-Agriculture/AWS-Config-for-Smart-Agriculture-/assets/60198040/8487f572-acbc-4b10-9df2-20b8957b7bd5)
![Picture8](https://github.com/LoRaWAN-Platform-for-Smart-Agriculture/AWS-Config-for-Smart-Agriculture-/assets/60198040/21f1d035-bddd-401a-af45-cc9d3a83189e)

![Picture1](https://github.com/user-attachments/assets/94c6bfcc-a19f-4b56-8052-6fee38ad957e)


