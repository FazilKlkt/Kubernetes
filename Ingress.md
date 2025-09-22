## Ingress

### What is Ingress?
- Routes external traffic to internal services using domain names.
- Replaces external IPs and ports with readable URLs.

### Ingress Controller
- Evaluates Ingress rules (e.g., Nginx Ingress Controller).
- Must be installed in the cluster.
- <left><img src="./assets/image-20250922203509656.png" alt="image-20250922203509656" /></left>

- In case of Cloud Provider LoadBalancer:

  - <left><img src="./assets/image-20250922203743015.png" alt="image-20250922203743015" /></left>

- In case of Bare Metal VM:

  - <left><img src="./assets/image-20250922203928757.png" alt="image-20250922203928757" /></left>

  - <left><img src="./assets/image-20250922204129607.png" alt="image-20250922204129607" /></left>

### Example Ingress Rule

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: dashboard-ingress
spec:
  rules:
  - host: dashboard.com
    http:
      paths:
        backend:
          serviceName: kubernetes-dashboard
          servicePort: 80
```

- In Above file:
  - **host**:
    -  should be a valid domain.
    - map domain name to Node's IP Address, which is entry-point.
  - **http**: means, take all the web requests.
  - **paths**: match the URL path, by default all.
  - **backend**: name & port of the service, which connects the application pod to the service.


---

### Different Use-case

- Multiple Path for same Host

  - <left><img src="./assets/image-20250922212719944.png" alt="image-20250922212719944" /></left>

- Multiple sub-domain for same host

  - <left><img src="./assets/image-20250922212924769.png" alt="image-20250922212924769" /></left>

---

### Configuring TLS certificate - https//

<left><img src="./assets/image-20250922213115964.png" alt="image-20250922213115964" /></left>

- Data keys need to be "**tls.crt**" and "**tls.key**".

- Values are **file content**, NOT file paths/locations.

- Secret component must be in the same namespace as the Ingress Component.

  
