- # Namespace


Namespace can work with only Name-spaced objects, and not cluster-wide objects

#### **To list Name-spaced Objects:**

**`kubectl api-resources --namespaced=true`**

<left><img src="./assets/image-20250918232008783.png" alt="image-20250918232008783" /></left>



#### To list Cluster-wide Objects:****

**`kubectl api-resources --namespaced=false`**

<left><img src="./assets/image-20250918232216391.png" alt="image-20250918232216391" /></left>



------

#### Default Namespaces

Total of 4 default namespace is present, to display namespaces: **`kubectl get namespace`**

<left><img src="./assets/image-20250918232355214.png" alt="image-20250918232355214" /></left>

- **kube-system:** The namespace for objects created by the Kubernetes system.
- **kube-public:** This namespace is readable by *all* clients (including those not  authenticated). This namespace is mostly reserved for cluster usage, in  case that some resources should be visible and readable publicly  throughout the whole cluster.
- **kube-node-lease:** Node leases allow the kubelet to send heartbeats so that the control plane can detect node failure.
- **default:** Kubernetes includes this namespace so that you can start using your new cluster without first creating a namespace.

---

#### Creating Namespaces

- using **kubectl** command
  - **`kubectl create namespace [NAMESPACE_NAME]`**

  - <left><img src="./assets/image-20250918232820316.png" alt="image-20250918232820316" /></left>

- using **config file**

  - <left><img src="./assets/image-20250918233832121.png" alt="image-20250918233832121" /></left>

  - <left><img src="./assets/image-20250918233755820.png" alt="image-20250918233755820" /></left>

---

#### Why Use Namespaces

- Without it

  - No Logical Grouping

    - Hard to manage resources, no overview

    - Everything in one Namespace

    - <left><img src="./assets/image-20250918234840159.png" alt="image-20250918234840159" /></left>

  - Conflicts: Many teams, same application

    - If a different team applies a config with same name, the first teams config will get overridden, which is an conflict 

    - <left><img src="./assets/image-20250918234429396.png" alt="image-20250918234429396" /></left>

- With it

  - Logical Grouping

    - Resources grouped in Namespaces

    - <left><img src="./assets/image-20250918234928365.png" alt="image-20250918234928365" /></left>

  - No Conflict

    - Since both the team is using different namespace, there wont be conflict

    - <left><img src="./assets/image-20250918234702001.png" alt="image-20250918234702001" /></left>

  - Resource Sharing

    - Can use a single deployed component for both application

    - <left><img src="./assets/image-20250918235123264.png" alt="image-20250918235123264" /></left>

  - Access and Resource Limits on Resource

    - Minimise risk of one team mistakenly interfering with other teams

    - <left><img src="./assets/image-20250918235328838.png" alt="image-20250918235328838" /></left>

---

#### Characteristics of Namespaces

- You cant access most resources from another namespaces

  - <left><img src="./assets/image-20250918235611776.png" alt="image-20250918235611776" /></left>

- You can access Service in another Namespace

  - <left><img src="./assets/image-20250918235754241.png" alt="image-20250918235754241" /></left>

- 
