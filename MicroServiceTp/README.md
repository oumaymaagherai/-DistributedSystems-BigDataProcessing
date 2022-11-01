# Compte rendu 
Dans ce TP, nous somme amené à mettre en oeuvre une application distribuée basée sur deux micro-services ;Customer-service et Billing-service.
## Customer-service : 
c'est un micro-service qui permet de gérer les clients,

![image](https://user-images.githubusercontent.com/79479398/198992968-95574566-57ee-4a8a-88bc-83017b24f5f9.png)

test de la couche web avec swagger-ui: 

![image](https://user-images.githubusercontent.com/79479398/198996287-2df69c31-8942-4e4a-93a4-493cf3978e33.png)

List des customers :  Get  

![image](https://user-images.githubusercontent.com/79479398/198996526-aac10267-7f6c-425c-922b-b7392516e7b0.png)

Ajouter un customer : POST 

![image](https://user-images.githubusercontent.com/79479398/198996795-33cb860f-6432-42ae-b17f-a7e95fabe8a1.png)

![image](https://user-images.githubusercontent.com/79479398/198996817-8fe45af6-b574-494e-82da-2a761658332c.png)

retourner un customer par son id : 

![image](https://user-images.githubusercontent.com/79479398/198997202-e2473053-0f50-4935-8e33-bb4a47038313.png)

![image](https://user-images.githubusercontent.com/79479398/198997235-e8db0c87-f8e1-480a-bf6a-94b47c0a8a1a.png)


## Billing-service: 
c'est un micro-service qui gére la factures
la communication entre Billing-service et customer-service est fait à partir OpenFeign

![image](https://user-images.githubusercontent.com/79479398/198993484-454cc341-9ea8-4832-8add-a861b485df66.png)

test de la couche web avec swagger-ui:

![image](https://user-images.githubusercontent.com/79479398/199217796-f816b350-1077-49e4-ba24-462e689c5c78.png)

List des factures : Get

![image](https://user-images.githubusercontent.com/79479398/199187599-0bc4f526-206f-4f83-becf-6aca37a6a91b.png)

Ajouter une facteur : Post

![image](https://user-images.githubusercontent.com/79479398/199187739-9449422e-8b39-4ea4-8f01-d7e72880b8ac.png)

![image](https://user-images.githubusercontent.com/79479398/199187822-521e4a31-3265-4698-b4b3-16f1a4bbff7c.png)

List des facteurs d'un customer : GetByCustomer

![image](https://user-images.githubusercontent.com/79479398/199187997-aa944dd1-7e02-4589-82c5-e53a8a5df2b3.png)

![image](https://user-images.githubusercontent.com/79479398/199188187-455bcc2e-94cd-4815-be75-3882e22f1182.png)

Obtenir un facteur par son id : getById

![image](https://user-images.githubusercontent.com/79479398/199188300-24c1332e-b4b1-4a06-be4b-95af680e361c.png)

![image](https://user-images.githubusercontent.com/79479398/199188360-e0f0f808-a001-4ee6-afa1-08c65ede723d.png)

## Eureka-Server :
Eureka Server contient les informations sur toutes les micro-services client . Chaque micro service s'enregistrera sur le serveur Eureka et le serveur Eureka connaît toutes les applications client exécutées sur chaque port et adresse IP. 

![image](https://user-images.githubusercontent.com/79479398/199212172-3d35c66d-280d-47fe-b8c4-55b691dc5631.png)

lancement de sereveur eureka sur le port 8761 : 

![image](https://user-images.githubusercontent.com/79479398/199188579-af597ffa-535d-464f-b002-858c1b37ca9e.png)

## Gateway-Service
Gateway-service est un point d'accès unique et agit comme un proxy pour les micro-service customer et billing.
  
![image](https://user-images.githubusercontent.com/79479398/199213455-16a3a548-f116-4688-8315-8d3de74f4daa.png)

accéder à customer-service à partir de la gateway

![image](https://user-images.githubusercontent.com/79479398/199188697-6ae28b79-4bee-451e-9aa8-1c1dc7490615.png)

![image](https://user-images.githubusercontent.com/79479398/199188795-fec75ffc-b77f-4988-af01-3d147169bbd1.png)

accéder à billing-service à partir de la gateway

![image](https://user-images.githubusercontent.com/79479398/199189039-a3b96fec-8283-4966-ab79-1ba444d9a5fa.png)

![image](https://user-images.githubusercontent.com/79479398/199189573-ebfe74d8-ef64-4188-aac2-36882b607424.png)

![image](https://user-images.githubusercontent.com/79479398/199189753-022e1596-d010-4002-beda-ac89ebfdd567.png)


## Docker-compose : 
![image](https://user-images.githubusercontent.com/79479398/199224492-b4339ae5-565d-480a-92d3-3d94e76f8a02.png)

pour chaque  micro-service: 

  -Premiérement, Générer un jar par la commande -mvn clean install
  -ensuite, Créer un fichier Dockerfile qui contient la configuration suivante de création d'une image, ce qui différe le nom de Jar-file pour chaque micro-service : 
  
![image](https://user-images.githubusercontent.com/79479398/199223702-f7a7951a-2ae5-4a96-9ac7-e17693187ad2.png)

- après , Créer un répertoire dans laquelle on va rassmbler le jar et DockerFile 
- puis, Créer un fichier docker-compose dans laquelle on va appeler les quatres images en même temps et exécuter également leurs conteneurs 

![image](https://user-images.githubusercontent.com/79479398/199223860-77107b9f-72c0-4ce4-a28b-42244f1ae94f.png)

![image](https://user-images.githubusercontent.com/79479398/199224000-0b8b8297-00c6-4fdb-8b14-cb4627e99331.png)

-enfin, démarrer les conteneurs à l'aide de la commande  docker-compose up --build

![image](https://user-images.githubusercontent.com/79479398/199223658-e82bff4f-e429-44e8-88d8-c9076756650d.png)

Accéder au serveur eureka à partir de contneur eureka-service1 dans l'image docker-root-eureka-service : 

![image](https://user-images.githubusercontent.com/79479398/199319689-cec2d0d9-21f0-4fef-b5dd-b0cac5331879.png)

![image](https://user-images.githubusercontent.com/79479398/199320329-dd1a16f8-c280-4e29-a6cb-3bf05a3c4d83.png)





