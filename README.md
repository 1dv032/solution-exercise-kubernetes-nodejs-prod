# solution-exercise-kubernetes-nodejs-prod

## Creating app deployment
Create application image
`docker build ./web/ -t cscloud389.lnu.se:5000/hello-template:1.0`
Push images to registry
`docker push cscloud389.lnu.se:5000/hello-template:1.0`
Create a pull secret
`kubectl create secret docker-registry cscloud389cred --docker-server=cscloud389.lnu.se:5000 --docker-username=<your-name> --docker-password=<your-pword> --docker-email=<your-email>`
Apply the app deployment
`kubectl apply -f kubernetes/app-deployment.yaml -f kubernetes/app-service.yaml`
