# docker-mern-app

is an minimal and easy way to deploy an development environment for building MERN apps.

docker-mern-app is designed in a way so that files can also be edited outside the conatiners - even if Containers are already running. And that with almost all common IDEs!

## Environment-Setup

The environment contains the following containers.

**Accessible via Browser:**

App: _127.0.0.1:3000_

Mongo web interface: _127.0.0.1:8081_

**Accessible with IP and Port**

Backend: _127.0.0.1:5000_

MongoDB: _127.0.0.1:27017_

**Frontend**
* mern_app: 
  * build on node-container
  * yarn already installed
  * mounts and stores data in app/
  * contains start.sh to control the start-up of the container
    * located inside at /home/start.sh 

**Backend**
* mern_backend: 
  * build on node-container
  * yarn already installed
  * mounts and stores data in backend/
  * contains start.sh to control the start-up of the container
    * located inside at /home/start.sh 

**MongoDB**
* mongo:
  * latest mongo container
  * mounts and stores data in database/
  * Credentials by default:
    * Username = root
    * Passwort = password

**Database Web-Interface**
* mongo-express:
  * latest mongo-express container
  * configured with default credentials

## Installation

### Prequisites
**None** (except docker)

### 1. Clone this repo
```git clone https://github.com/wipplingermax/docker-mern-app```

### 2. Change into mern-app dir
```cd docker-mern-app```

### 3. Install latest React version
Run app container

```./start-app-shell```

(If the startup scripts don't work, try: 
```chmod 755 start-app-shell``` and
```chmod 755 start-backend-shell```)

If you are now **inside of the app-container** (/home/app) run

```yarn create react-app .``` 

Exit Container

```exit```

### 4. Start 
```sudo docker-compose up --build```

### 5. Have fun with developing ;)
App is now accessible in browser on _127.0.0.1:3000_

## start / use / end  - development environment

**start**

* run the following command: ```docker-compose up --build```
  * this starts all 4 containers (app, backend, mongo, mongo web interface)
  * app container runs start.sh on start (editable: docker/app/start.sh) 
  * backend container runs start.sh on start (editable: docker/backend
  /start.sh)  

**use**
* Start shell inside the app container: ```./start-app-shell```
* Start shell inside the app container: ```./start-backend-shell```
* Mongodb is accessible inside the containers on _mongo:27017_

**end**
* run the following command: ```docker-compose down```

**Recommandations**
  * run app automatically on startup:
    * insert following line in /docker/app/start.sh ```yarn start```
  * automatically restart backend on file change with nodemon
    * install nodemon in backend:
      * ```./start-backend-shell```
      * inside backend ```yarn add nodemon```
    * insert following line in /docker/backend/start.sh ```nodemon server.js```

## Project Tree
The Folder tree was created in a way that the components (app, backend, database) can be managed separately.

By default the mapping and mounting is the following:

* /app 
  * is mounted in the mern-app container
  * path in container: /home/app

* /backend 
  * is mounted in the backend-app container
  * path in container: /home/backend

* /database
  * is mounted in the mongo container
  * path in container: /data/db

* /docker/app/start.sh
  * is copied while building process in the mern-app container
  * path in container: /home/start.sh

* /docker/app/start.sh
  * is copied while building process in the mern-backend container
  * path in container: /home/start.sh
```
.
├── app (frontend)
├── backend 
├── database (local mongo Database)
├── docker
│   ├── app
│   │   ├── Dockerfile (image for frontend)
│   │   ├── start.sh (startup script for frontend)
│   └── backend
│       ├── Dockerfile (image for backend)
│       ├── start.sh (startup script for backend)
├── docker-compose.yml (configure container start)
├── start-app-shell (start shell in app container)
└── start-backend-shell (start shell in backend container)
``` 

