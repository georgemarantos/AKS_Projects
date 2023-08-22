# Setup MongoDB

## Configure the Helm client to use the stable repository 
helm repo add bitnami https://charts.bitnami.com/bitnami

## Install Mongo DB 
helm install ratings bitnami/mongodb \
    --namespace ratingsapp \
    --set mongodbUsername=<username>,mongodbPassword=<password>,mongodbDatabase=ratingsdb

## Create a secret called mongosecret
kubectl create secret generic mongosecret \
    --namespace ratingsapp \
    --from-literal=MONGOCONNECTION="mongodb://<username>:<password>@ratings-mongodb.ratingsapp:27017/ratingsdb"

# Building and deploying back/front-end

## Build back/front-end to ACR
From within the api and web folder run the following command making changes as necessary

'az acr build --registry <acr> --image <imagename>:<version> <Source_Location>'

An exampple would be:

'az acr build --registry marantoslab --image ratings-web:v1 .'