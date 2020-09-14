## REACT WITH AKS

### About
This repository define a simple React app which is able to run in Azure Kubernetes Service. Any changes made to the master branch is automatically pushed to ACR and AKS using Github Actions.

### Implementation
The React code is from running `npx create-react-app`. 

To build and serve the React app in an image we create a Dockerfile. The Dockerfile creates an optimized production build running `npm run build` and then serves the build using nginx. For further configuration of ports and paths we define a nginx confgiration file in `nginx/nginx.conf` and include this in the image. The container thus exposes port `8080` and serves the react app on request. 

To push changes to Azure we utilize GitHub Actions. The workflow configuration is provided in `.github/workflows/main.yaml`. The workflow runs on push- and pull-requests to master. The workflow pipeline is as follows:
1.  login to ACR
2.  build the image using the new code and push the image to ACR
3.  install kubectl
4.  login to AKS and set the correct Kubernetes cluster context
5.  update the previously created deployment image


### Prerequisites
The code in this repository does not create or initiate the Azure resources needed to run AKS. [This workshop](https://docs.microsoft.com/en-us/learn/modules/aks-workshop/02-deploy-aks) describes the steps needed to deploy Kubernetes with AKS. Using the relevant pieces of the workshop should enable you to create and deploy your own AKS.

### Glossary
ACR = Azure Container Registry

AKS = Azure Kubernetes Service

kubectl = Kubernetes command line tool
