# How to build and deploy this application to Azure Kubernetes with Azure Container Registry.
## Prerequisites
- [ ] Prepare PowerShell environment
- [ ] Create an AKS Cluster in Azure
- [ ] Create an Azure Container Registry in Azure
- [ ] Connect PowerShell to Azure
- [ ] Download ratings_api_master to local pc
- [ ] Download ratings_web_master to local pc


## Setup MongoDB

### Configure the Helm client to use the stable repository 
`helm repo add bitnami https://charts.bitnami.com/bitnami`

### Install Mongo DB 
Latest Mongo DB is not working so for this project use the following command after making the necessary changes:

`helm install ratings bitnami/mongodb --namespace ratingsapp --set image.tag=5.0.14-debian-11-r9,auth.username=<username>,auth.password=<password>,auth.database=ratingsdb`

### Create a secret called mongosecret
kubectl create secret generic mongosecret \
    --namespace [namespace] \
    --from-literal=MONGOCONNECTION="mongodb://[username]:[password]@ratings-mongodb.[namespace]:27017/ratingsdb"

## Building and deploying middle-tier/front-end

### Build middle-tier/front-end to ACR
From within the api and web folder run the following command making changes as necessary

`az acr build --registry <acr> --image <imagename>:<version> <Source_Location>`

A finished example would look like the following:

`az acr build --registry marantoslab --image ratings-web:v1 .`

### Deploy middle-tier/front-end to AKS
Update the ratings-api-deployment.yaml file with proper ACR repo and then run the following command

`kubectl apply --namespace [namespace] -f ratings-api-deployment.yaml`

Update the ratings-api-service.yaml file with proper type (I chose ClusterIP) and then run the following command

`kubectl apply --namespace [namespace] -f ratings-api-service.yaml`

Update the ratings-web-deployment.yaml file with proper ACR web and then run the following command

`kubectl apply --namespace [namespace] -f ratings-web-deployment.yaml`
