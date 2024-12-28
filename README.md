# Sports Event Platform

*SportEvent* est une application web complète conçue pour simplifier la gestion des événements sportifs, allant de l'inscription des participants au suivi des résultats. Avec une architecture robuste et moderne, elle vise à offrir une expérience optimale aux organisateurs et aux participants.

---

## 📚 *Table des Matières*

- [🛠 Architecture Logicielle](#-architecture-logicielle)  
- [🐳 Docker](#-docker)
- [🎯 Fonctionnalités](#-fonctionnalités)
- [🎨 Frontend](#-frontend)  
- [💻 Backend](#-backend)  
- [🎥 Vidéo démonstrative](#-vidéo-demonstrative)  
 
---

## 🛠 *Architecture Logicielle*

L'application est composée de :
- **Backend** : Spring Boot  
- **Frontend** : React.js  
- **Base de données** : MySQL  

## 🛠 *Prérequis*

- Git : Assurez-vous que Git est installé. Sinon, téléchargez-le depuis git-scm.com.

- XAMPP : Installez XAMPP depuis apachefriends.org. Démarrez les serveurs Apache et MySQL. Assurez-vous que MySQL utilise le port 3306.

- Node Version Manager (NVM) : Installez NVM depuis github.com/nvm-sh/nvm. Utilisez NVM pour installer Node.js version 14.11.0 :

---
## *Docker*
```sh
version: '3.8'

services:
  mysql:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: eventsport
      MYSQL_USER: user
      MYSQL_PASSWORD: userpassword
    ports:
      - "3306:3306"
    volumes:
      - mysql_data:/var/lib/mysql
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost", "-u", "root", "-p$$MYSQL_ROOT_PASSWORD"]
      interval: 10s
      timeout: 5s
      retries: 5

  backend:
    build:
      context: ./PFM/event-sports-back/event-sports-back
    ports:
      - "8085:8085"
    depends_on:
      mysql:
        condition: service_healthy
    environment:
      SPRING_DATASOURCE_URL: jdbc:mysql://mysql:3306/eventsport
      SPRING_DATASOURCE_USERNAME: user
      SPRING_DATASOURCE_PASSWORD: userpassword
    healthcheck:
      test: ["CMD-SHELL", "curl -f http://localhost:8085/actuator/health || exit 1"]
      interval: 30s
      timeout: 10s
      retries: 5
      start_period: 40s

  frontend:
    build:
      context: ./PFM/event-sports-front/event-sports-front
    ports:
      - "80:80"
    depends_on:
      backend:
        condition: service_healthy

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    environment:
      PMA_HOST: mysql
      PMA_PORT: 3306
      MYSQL_ROOT_PASSWORD: rootpassword
    ports:
      - "8081:80"
    depends_on:
      mysql:
        condition: service_healthy

volumes:
  mysql_data:

networks:
  default:
    name: app-network

```

![image](https://github.com/user-attachments/assets/4a640298-0c5a-4aa3-8af2-abc5301c100f)


## 🎯 *Fonctionnalités*:
- Module d’Authentification Utilisateur : Authentification et Autorisation des utilisateurs avec Spring Boot et React. Le système d’inscription et de connexion a été ajouté pour que seuls les utilisateurs authentifiés (Administrateur ou Client) puissent effectuer leurs fonctionnalités.

- Module de Catégorie d’Événements : Ajouter une Catégorie, Modifier une Catégorie, Supprimer une Catégorie, Voir les Catégories.

- Module d’Événements : Ajouter un Événement, Modifier un Événement, Supprimer un Événement, Voir les Événements.

- Module de Réservation d’Événements : Ajouter une Réservation d’Événement, Paiement & Réservation, Voir les Réservations d’Événements.


### 🧩 Technologies utilisées

## 🛠 *Backend*
- Spring Boot
- Spring Security
- MySQL
- Java
## 🛠 *Frontend*
- React.js

Dépendances:
```sh
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <scope>runtime</scope>
</dependency>
```

### ⚙️ *Installation du Frontend*
```bash
cd frontend
npm install
npm start
```

## *Accès à l'application*
Frontend : http://localhost:3000

## *Vidéo démonstrative*

https://github.com/user-attachments/assets/cbccdd0e-db66-4802-9a20-a2524dad3406

## *Contributeurs*
- [Khouribech imane](https://github.com/HindEnnahir)
- [HindEnnahir](https://github.com/khouribechimane)

























