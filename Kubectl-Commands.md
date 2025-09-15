# Kubectl Commands

### Pods

#### To List running pods in node:  

##### command:  `kubectl get pods`

<left><img src="./assets/image-20250915230252926.png" alt="image-20250915230252926" /></left>



#### To Delete running pod in node:

#####  command: `kubectl delete pods [POD_NAME]`

<left><img src="./assets/image-20250915231256662.png" alt="image-20250915231256662" /></left>



------

### Deployments

#### To Create a deployment:

##### command:  `kubectl create deployment [DEPLOYEMNT_NAME] --image=[CONTAINER_IMAGE_NAME]`

<left><img src="./assets/image-20250915232219482.png" alt="image-20250915232219482" /></left>



#### To List deployments:

##### command:  `kubectl get deployments`

<left><img src="./assets/image-20250915232803297.png" alt="image-20250915232803297" /></left>



#### To Edit a deployment:

##### command:  `kubectl edit deployment [DEPLOYMENT_NAME]`

<left><img src="./assets/image-20250915234153369.png" alt="image-20250915234153369" /></left>

**Note**: When I edited the `spec->containers->image` from **nginx** to **nginx:1.16**

<left><img src="./assets/image-20250915234801470.png" alt="image-20250915234801470" /></left>

- The new container `nginx-depl-7d9b57bb64-znkn2` is being created
- Once the new container is active, old container will be deleted
- Above example is with respect to **Pods**, but the same will happen with **ReplicaSets**



#### To expose a Deployment to outside network:

##### command: `kubectl expose deployment [DEPLOYMENT_NAME] --type=NodePort --port=80`

<left><img src="./assets/image-20250915235929107.png" alt="image-20250915235929107" /></left>

###### after exposing the deployment, run `kubectl get services` to get external IP address

<left><img src="./assets/image-20250916000733367.png" alt="image-20250916000733367" /></left>





------

### Services

#### To Check running services in node:

##### command: `kubectl get services`

<left><img src="./assets/image-20250915230818435.png" alt="image-20250915230818435" /></left>





------

### ReplicaSet

#### To Check running replcaset in node:

##### command: `kubectl get replicaset`

<left><img src="./assets/image-20250915233122002.png" alt="image-20250915233122002" /></left>



------

### Useful Commands

#### To check logs of a Pod

##### command: `kubectl logs [POD_NAME]`

<left><img src="./assets/image-20250915235646257.png" alt="image-20250915235646257" /></left>



#### To get detailed info of a Pod

##### command: `kubectl describe pod [POD_NAME]`

<left><img src="./assets/image-20250916001154956.png" alt="image-20250916001154956" /></left>



#### To enter into interactivity mode(log in to the pod) of the Pod

##### command: `kubectl exec -it [POD_NAME] -- bin/bash`

above command will start the bash command of respective Pod

<left><img src="./assets/image-20250916001533007.png" alt="image-20250916001533007" /></left>



#### To generate a basic Deployment Config file

##### command: `kubectl create deployment [DEPLOYMENT_NAME] --image=[CONTAINER_IMAGE_NAME] --dry-run=client -o yaml`

- The **`--dry-run=client`** option simulates the action, without actually running it
- The **`-o yaml`** option prints the file in YAML format

<left><img src="./assets/image-20250916002249389.png" alt="image-20250916002249389" /></left>



#### To Create a Deployment using a Config file

##### command: `kubectl apply -f nginx-deployment.yaml`

<left><img src="./assets/image-20250916003023663.png" alt="image-20250916003023663" /></left>

- After creating the deployment using config file, when i update the **replicas to 2** in config file and apply the deployment again, observe in the below image. 

  - instead of **`deployment.apps/nginx created`** as shown in image above
  - it is showing **`deployment.apps/nginx configured`**
  - this is because, kubernetes is aware when to create new deployment, and when to update

- <left><img src="./assets/image-20250916003514203.png" alt="image-20250916003514203" /></left>



------

#### NOTE:

- <left><img src="./assets/image-20250915233359748.png" alt="image-20250915233359748" /></left>


  **ReplicaSet** is managing the replicas of **Pod**

  - **nginx-depl-5fcbf6fffd**  : ReplicaSet
  - **nginx-depl-5fcbf6fffd**-jwgtz : Pod

- Deployment manages a ReplicaSet  
- ReplicaSet manages Pod  
- Pod is a abstraction of a Container
- Everything below a Deployment will be managed by Kubernetes







