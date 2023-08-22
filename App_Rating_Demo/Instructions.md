# AKS_Projects
This is a place to store any projects I worked on that targeted AKS.

# Configure the Helm client to use the stable repository 
helm repo add bitnami https://charts.bitnami.com/bitnami

# Install Mongo DB 
helm install ratings bitnami/mongodb \
    --namespace <namespace> \
    --set mongodbUsername=<username>,mongodbPassword=<password>,mongodbDatabase=ratingsdb

# Create a secret called mongosecret
kubectl create secret generic mongosecret \
    --namespace <namespace> \
    --from-literal=MONGOCONNECTION="mongodb://<username>:<password>@ratings-mongodb.ratingsapp:27017/ratingsdb"