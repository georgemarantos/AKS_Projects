# AKS_Projects
This is a place to store any projects I worked on that targeted AKS.

## Preparing powershell environment
Make sure [AZ CLI](https://aka.ms/installazurecliwindowsx64) is installed.

Make sure [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/#install-kubectl-binary-with-curl-on-windows) is installed.

Make sure [Helm](https://github.com/helm/helm/releases) is installed.

## Preparing powershell environment
Usefull commands

##Verify Secret Exist
'kubectl describe secret mongosecret --namespace [namespace]'

##Get Realtime Status of Pods
'kubectl get pods --namespace [namespace] --watch'
