# My Docker Assignment Report

Name: lujain al hallak
Repository URL:https://github.com/lujainalhallak2006-del/docker-assignment-starter.git

Use short sentences. Add the answers requested in the assignment PDF.
Keep passwords, tokens, and private keys out of this report.

## Mission 1 - First Container

Commands used:

____________________

What happened:

____________________

What I learned:

____________________

Problem I faced:

____________________

How I fixed it:

____________________
What does 8080:80 mean? Mapping my device's port 8080 to port 80 that the container is listening on
____
Is this container a full Virtual Machine? Explain in one or two sentences. No, the difference is that a virtual machine contains all the application files along with a suitable operating system, whereas a container shares the host machine's operating system.
_____
Which command showed you the container logs? docker logs web-server


## Mission 2 - Build Your Own Image

Commands used:

____________________

What happened:

When I edited the message.txt file, nothing changed because Docker still relies on the image it took during the build, so to apply the changes we need to build a new image.

What I learned:

____________________

Problem I faced:

____________________

How I fixed it:

____________________

## Mission 3 - Broken Port

Commands used:

chmode +x start_brokrn.sh
./start-broken.sh
docker stop a90cec62ccb2
sudo nano start-broken.sh

What happened:

When I tried to run the script that includes the command to create a container, I got an error message saying that the container can't be created because port 8080 is already taken by another container

What I learned:

That no specific port on my device can be used by more than one container

Problem I faced:

unable to create the container 

How I fixed it:

I stopped the old container that was using port 8080 and modified the script to make it listen on port 3000 instead of 5000.

short Questions:
What was wrong?When I tried to run the script that includes the command to create a container, I got an error message saying that the container can't be created because port 8080 is already taken by another container

Which command helped you find the problem? sudo ./start-broken.sh

In your fixed command, what is the host port and what is the container port? host port:8080 , container port :it was 5000,then he changed it to 3000 because the application
utilizes port 3000s

## Mission 4 - Environment Variables

Commands used:
 sudo docker run -d --name env-app -p 8082:3000 -e APP_MESSAGE="Hello from the docker assignment"  devops-node-app:v1 

sudo docker exec -it env-app sh
# printenv APP_MESSAGE

sudo docker stop env-app

sudo docker rm env-app

sudo docker run -d --name env-app -p 8082:3000 -e APP_MESSAGE="new messaget"  devops-node-app:v1



____________________

What happened:

No problem occurred, I ran a new container from an image I had created earlier, set the port and environment variables, then displayed the variable's value, and after that I stopped the container and deleted it, then created a new container from the same image and the same port but with a different variable value.
____________________

What I learned:
To define a variable, the definition must be done when running the container, and it is possible to create more than one container with a different name for the same image.

____________________

Problem I faced:

____________________

How I fixed it:

____________________

Short Question:
 
Why could you change the application message without building a new image?
Because setting the variable isn’t something that has to be done when creating the image, which means you can run multiple containers with different variables for the same image

## Mission 5 - Docker Hub

Commands used:
sudo docker login -u lujainalh
sudo docker tag devops-node-app:v1 lujainal/devops-node-app:v1
sudo docker push lujainal/devops-node-app:v1
____________________

What happened:
I created an account on Docker Hub, then created a repo, then logged in from the terminal, and then pushed the image to the repo.
____________________

What I learned:
How to upload a picture to Docker Hub
____________________

Problem I faced:
When I was uploading the image, I kept getting an error saying 'repository does not exist' and 'unauthorized'.
____________________

How I fixed it:
I wrote the upload command in the folder 02-node-app that contains the Dockerfile
____________________

## Mission 6 - Remote Deployment

Commands used:
docker login 
sudo docker pull lujainal/devops-node-app:v1
sudo docker run -d --name remote-app -p 8080:3000 lujainal/devops-node-app:v1
sudo docker ps
curl http://localhost:8080

____________________

What happened:
I pulled an image from Docker Hub to my device to build a container
____________________

What I learned:

____________________

Problem I faced:
non
____________________

How I fixed it:

____________________
Short Question: Why is a registry useful when developers and servers are different machines?
Because the Registry works as a secure platform that makes it easy to store and share container images, it allows the developer to build and test the image on their machine and upload it once, so any server or other machine can pull it directly (docker pull) and run it right away without needing to rebuild the image from scratch on each machine.


## Mission 7 - Volumes

Commands used:
sudo docker run -d --name mongo-lap mongo:7
sudo docker run -d --name mongo-lap -v mongo-Data:/data/db mongo:7
sudo docker exec mongo-lap mongosh --quiet --eval 'db.getSiblingDB("devops").messages.insertOne({text:"keep-me"})'
{
sudo docker exec mongo-lap mongosh --quiet --eval 'db.getSiblingDB("devops").messages.find().toArray()'
sudo docker rm -fv mongo-lap


____________________

What happened:

____________________

What I learned:
If you want to save important data, you should link the folder with the volume.
____________________

Problem I faced:

____________________

How I fixed it:

____________________

Why was the old record missing after you created a fresh container?
Because the data is not saved and the folder is not linked to persistent storage, when the container is deleted, everything inside it is deleted.

Why did the data survive after you attached mongo-data?  It is a permanent storage space and remains even if the delete command is applied to  container

What is the difference between deleting a container and deleting a volume?
When you delete the container, the permanent storage stays, but when you delete the volume, the permanent files are deleted too.

## Mission 8 - Docker Networking

Commands used:
sudo docker compose up --build -d

sudo docker compose logs app


____________________

What happened:
When trying to run the app, it couldn't connect
____________________

What I learned:
The word localhost means the same container and not another container, so to connect to another container, I must write the service name.
____________________

Problem I faced:
Failed to connect to PostgreSQL
____________________

How I fixed it:
I changed the DB-HOST value from localhost to postgres
____________________
● What did localhost point to inside the app container? It was pointing to the container itself
● Which hostname fixed the connection? postgres
● Why is using the service name better than hard-coding a container IP address?  Because the container's IP changes every time the container is created or started, so when we use the name, it gets linked immediately to the current IP and connects.

## Mission 9 - Docker Compose
Commands used:
cd  09-compose-final folder
touch compose.yaml
nano compose.yaml
touch .env
nano .env
 touch gitignore
 nano gitignore
 docker compose up -d 
docker compose ps 
docker compose logs
docker compose down 
docker volume ls

____________________

What happened:
I put two services inside the compose.yaml file, then ran the compose. It pulled the images for the services and then started the containers.
____________________

What I learned:
Create a compose.yaml file and run the containers
____________________

Problem I faced:
non
____________________

How I fixed it:

____________________
Why does pgAdmin connect to PostgreSQL using the service name instead of localhost? Because localhost refers to the container itself and not to Postgres.

Which service needs a host port for the browser? pgadmin


What happens to the named volume after docker compose down? It stays as it is
## Bonus Mission

Commands used:
cd 02-node-app
touch compose.yaml
nano compose.yaml
sudo docker compose up -d
sudo docker compose ps
____________________

What happened:

____________________

What I learned:

____________________

Problem I faced:
I wrote the compose.yaml file and when I tried to run the compose, I got an error: validating /home/lujain/docker-assignment-starter/02-node-app/compose.yaml: volumes must be a mapping
____________________

How I fixed it:
I edited the file and redefined the volumes
____________________

