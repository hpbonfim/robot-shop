# Stan's Robot Shop App Deployment Guide
![04_LAB01_deploying_a_microservice_application_to_kubernetes](https://github.com/hpbonfim/robot-shop/assets/40275173/750be3ec-b82d-41b4-b105-e9181dbcf3c0)

This guide provides step-by-step instructions on how to deploy the Stan's Robot Shop app to a Kubernetes cluster and scale up the MongoDB deployment to two replicas.

## Deployment Steps

1. Clone the Git repo that contains the pre-made descriptors by running the following command in your terminal:
```
cd ~/
git clone https://github.com/linuxacademy/robot-shop.git
```

2. Create a separate namespace for the app by executing the following command:
```
kubectl create namespace robot-shop
```

3. Deploy the app to the cluster using the following command:
```
kubectl -n robot-shop create -f ~/robot-shop/K8s/descriptors/
```

4. Check the status of the application's pods by running the command:
```
kubectl get pods -n robot-shop
```
This will display the status of the pods and ensure they are running successfully.

5. Once the pods are running, you should be able to access the Stan's Robot Shop app from your browser. Use the Kube master node's public IP and port 30080 in the following format:
```
http://$kube_master_public_ip:30080
```
Replace `$kube_master_public_ip` with the actual public IP address of your Kubernetes master node.

## Scaling Up MongoDB Deployment

1. Edit the deployment descriptor for MongoDB by executing the following command:
```
kubectl edit deployment mongodb -n robot-shop
```
This will open the descriptor in your default text editor.

2. Within the YAML file, locate the line that specifies the number of replicas and change it from `replicas: 1` to `replicas: 2`.

3. Save the changes and exit the text editor.

4. Check the status of the deployment to ensure it reflects the desired replica count:
```
kubectl get deployment mongodb -n robot-shop
```
After a few moments, you should see the number of available replicas as 2.

Congratulations! You have successfully deployed the Stan's Robot Shop app to your Kubernetes cluster and scaled up the MongoDB deployment to two replicas.
