# YAML Configurations

- 3 parts of configuration files
- Connecting  Deployments to Services to Pods

------

####  3 parts of configuration files

- Metadata

  - <left><img src="./assets/image-20250916202339407.png" alt="image-20250916202339407" /></left>

- Specification

  - <left><img src="./assets/image-20250916202420690.png" alt="image-20250916202420690" /></left>


- Status(Desired/Actual, basis of self healing feature)

  - **etcd** holds the status data




**Note**: Attributes of Specification are specific to the Kind! 

<div style='display: flex;
  justify-content: space-evenly;'><img src="./assets/image-20250916200941115.png" alt="image-20250916200941115" />
<img src="./assets/image-20250916201528864.png" alt="image-20250916201528864" /></div>



------

#### Blueprint for Pods

- Template
  - this template applies to the **Pod** of Deployment, basically a blueprint for the pod
  - this decides
    - on which which port it should open
    - what will be the name of container
    - which image it should be based on


<left><img src="./assets/image-20250916202854301.png" alt="image-20250916202854301" /></left>






------

#### Connecting  Deployments to Services to Pods

- Labels, Selectors & Ports

- The connection is established through Label & Selector

  - **Metadata contains Labels**

  - **Specification contains Selector**

  - Pods gets the Label though template blueprint

    - <left><img src="./assets/image-20250916210928330.png" alt="image-20250916210928330" /></left>

  - The label is matched by selector, to indicate that the Pod belong to that Deployment

    - <left><img src="./assets/image-20250916211202556.png" alt="image-20250916211202556" /></left>

  - Deployment has it's own label, which is used by Service to connect to deployment

    - <div style='display:flex; justify-content:space-evenly; align-items:center;'><left><img src="./assets/image-20250916212136432.png" alt="image-20250916212136432" /></left>  <left><img src="./assets/image-20250916212358963.png" alt="image-20250916212358963" /></left></div>

  - Port Setting
  
     <div style="text-align: center; background-color: #e0f7fa; padding: 20px; border-radius: 10px;">
        <div style="border: 1px solid black; padding: 10px; display: inline-block;">
          <strong>DB Service</strong><br>
          port: 80
        </div>
        <div style="margin: 10px 0;">&#8595;</div>
        <div style="border: 1px solid black; padding: 10px; display: inline-block;">
          <strong>nginx Service</strong><br>
          targetPort: 8080
        </div>
        <div style="margin: 10px 0;">&#8595;</div>
        <div style="border: 1px solid black; padding: 10px; display: inline-block;">
          <strong>Pod</strong>
        </div>
      </div>
  
<div style='display: flex;
    justify-content: space-evenly;'><left><img src="./assets/image-20250916213329711.png" alt="image-20250916213329711" /></left><left><img src="./assets/image-20250916213416982.png" alt="image-20250916213416982" /></left></div>
- Container runs on port 8080. Service make others access the network at port 80 on TCP protocol, and forwards the connection to port 8080 

  -   <left><img src="./assets/image-20250916214214619.png" alt="image-20250916214214619" /></left>

  -   When we describe the service, we can see that two endpoints are present(since 2 replicas were configured in deployment)

      -   Pods are running at IP:  **10.244.0.16**, **10.244.0.17**

      -   and having the Port:  **8080**

      -   <left><img src="./assets/image-20250916214619363.png" alt="image-20250916214619363" /></left>

      -   in above command, **`-o wide`** option is used to get more details of pods

  -   
