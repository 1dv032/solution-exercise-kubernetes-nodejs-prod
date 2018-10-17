# solution-exercise-kubernetes-nodejs-prod

## Getting application images to registry
Create application image
`docker build ./web/ -t cscloud414.lnu.se:5000/hello-template:1.0`
Push images to registry
`docker push cscloud414.lnu.se:5000/hello-template:1.0`
Create a pull secret
`kubectl create secret docker-registry cscloud414cred --docker-server=cscloud414.lnu.se:5000 --docker-username=<your-name> --docker-password=<your-pword> --docker-email=<your-email>`
Apply the app deployment
`kubectl apply -f kubernetes/app-deployment.yaml`