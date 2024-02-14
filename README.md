# Grupo3Capstone

## Capstone documentation

Based on https://github.com/alfreluna12/Europe-Travel-Website-html-css-js

Update libraries

Download docker using command sudo apt-get install docker
curl -sSL https://get.docker.com/ | sudo sh

Check docker version using command docker --version

Current version 25.0.3, build 4debf41

Clone the repository to a local computer

Run docker using command 
$ docker run -it --rm -d -p 8080:80 --name web nginx
Docker will be usable in the port 80

This command will run the website locally

sudo docker run -it --rm -d -p 8080:80 --name web -v /home/juanluna/Capstone/Europe-Travel-Website-html-css-js/Europe\ Travel:/usr/share/nginx/html nginx

Create a Docker file with the following content without extension

FROM nginx:latest

COPY . /usr/share/nginx/html

Docker build -t web-image-finales .

This creates the image on Docker we have to execute this command on the directory that has the Docker file

The next step is to install the Google Cloud CLI

Install the dependencies of Google Cloud

sudo apt-get install apt-transport-https ca-certificates gnupg curl sudo

This download the Google Cloud Authentication keys and add the Google Cloud SK repository

curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo gpg --dearmor -o /usr/share/keyrings/cloud.google.gpg
echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list

This command install the Google Cloud CLI

sudo apt-get update && sudo apt-get install google-cloud-cli

The following commands were used to Authentication:

gcloud init

Gcloud oauthlogin

gcloud config set project elsalgroup3 <- this is the project name

gcloud services enable artifactregistry.googleapis.com

docker tag web-image-finales gcr.io/elsalgroup3/myartifactrepo/web-image-finales:v1

gcloud auth configure-docker

Create an artifact repository on Artifact Registry using Google Cloud Console: with a name and tag.

docker push gcr.io/elsalgroup3/myartifactrepo/web-images-finales:v1

gcloud artifacts repositories list --project elsalgroup3

This command was used to list the repositories 
gcloud artifacts repositories list

And then we moved to the Google Cloud Console UI

We first access the Container Registry searching for it in the search bar.

Then we check for the list of containers and click on our repository

Click on our docker image name 

Once we enter the docker image page, we click the 3 dots menu, and select deploy GKE

We configure a GKE using default settings and we set the port 80, or the one used by Nginx on our load balancer configuration.

To check our service, we use the load balancer IP address. 
