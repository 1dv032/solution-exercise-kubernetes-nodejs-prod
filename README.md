# solution-exercise-kubernetes-nodejs-prod

## Creating app deployment
**Create application image**
`docker build ./web/ -t cscloud389.lnu.se:5000/hello-template:1.0`

**Push images to registry**
`docker push cscloud389.lnu.se:5000/hello-template:1.0`

**Create a pull secret**
`kubectl create secret docker-registry cscloud389cred --docker-server=cscloud389.lnu.se:5000 --docker-username=<your-name> --docker-password=<your-pword> --docker-email=<your-email>`

**Apply the app deployment and service**
`kubectl apply -f kubernetes/app-deployment.yaml -f kubernetes/app-service.yaml`

## Reverse proxy with self-sign cert
**Create cert**
`./proxy/certificates.sh`

**Adding cert to kubernetes**
`kubectl create secret tls nginxsecret --key sslcerts/key.pem --cert sslcerts/cert.pem`
When you are using a tls secret the cert and key file name will change to tls.crt and tls.key.
You need to change this in the nginx config file before addling the config to kubernetes.

**Adding nginx config to kubernetes**
`kubectl create configmap nginxconfigmap --from-file=proxy/nginx-sites.conf`

**Apply the proxy deployment and service**
`kubectl apply -f kubernetes/proxy-deployment.yaml -f kubernetes/proxy-service.yaml`