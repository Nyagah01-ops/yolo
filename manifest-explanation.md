# client Deployment and Service Manifest

This manifest deploys a client application that depends on a backend service.

## Prerequisites

* A Kubernetes cluster (version 1.21 or later)
* A Docker image for the client application (e.g. `my-client-image:latest`)
* A backend service deployed in the same namespace (e.g. `backend`)

## Deployment

To deploy the client application, run the following commands:  

            kubectl apply -f client-deployment.yaml kubectl apply -f client-service.yaml 
 This will create a deployment named `client` with 3 replicas, and a service named `client` that exposes port 80.

## Configuration

The client deployment uses the following environment variable:

* `BACKEND_URL`: set to `http://backend.default.svc.cluster.local:80`, which points to the backend service.

You can update the `BACKEND_URL` environment variable by editing the `client-deployment.yaml` file.

## Accessing the Frontend

Once the deployment is complete, you can access the client application through the load balancer IP address. You can get the IP address by running:   
          kubectl get svc client -o jsonpath='{.status.loadBalancer.ingress[0].hostname}'

Then, open a web browser and navigate to `http://<load-balancer-ip>:80` to access the client application.

## Troubleshooting

If you encounter issues with the deployment, you can check the pod logs by running: 

kubectl logs -f deployment/client  

You can also check the service status by running:  

## Updating the Deployment

To update the client deployment, you can edit the `client-deployment.yaml` file and then re-apply the manifest: 

kubectl apply -f client-deployment.yaml


This will update the deployment with the new configuration.

## Deleting the Deployment

To delete the client deployment, run the following commands: 

kubectl delete deployment client kubectl delete svc client


This will remove the deployment and service from the Kubernetes cluster.
