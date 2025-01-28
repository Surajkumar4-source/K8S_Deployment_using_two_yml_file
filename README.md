# Deploying and Exposing an Application in Kubernetes Using two *yml* files


## Introduction

*In this implementation, I learned how to deploy and expose an application in a Kubernetes environment using Deployment and Service resources. The main focus was to understand how Kubernetes manages the lifecycle of pods, including scaling, and how to expose an application to the external world via a Service. By working with YAML files, I was able to define both the desired state of the application and the network access configuration, giving me deeper insights into Kubernetes architecture and its powerful features for managing containerized applications.*

---


## Follow the below steps to Implement.
<br>

### 1. Deployment YAML

- A Deployment manages multiple replicas of your application pods and handles rolling updates and rollbacks.

#### Example: `deployment.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-deployment
  labels:
    app: my-app
spec:
  replicas: 3  # Number of desired pods
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: nginx-container
        image: nginx:latest  # Replace with your application's Docker image
        ports:
        - containerPort: 80

```



- *apiVersion: Specifies the API version for the Deployment.*
  
- *replicas: Sets the number of pod replicas (in this case, 3).*
  
- *image: Defines the Docker image for the container (e.g., nginx:latest).*
  
- *containerPort: Exposes port 80 on the container inside each pod.*


### 2. Service YAML
- A Service provides a stable network interface to a set of pods, allowing external access if needed.


#### Example: `service.yaml`



```yml

apiVersion: v1
kind: Service
metadata:
  name: my-app-service
spec:
  selector:
    app: my-app  # Matches the Deployment's label
  ports:
  - protocol: TCP
    port: 80  # Exposed port on the Service
    targetPort: 80  # Port on the container
  type: LoadBalancer  # Exposes Service externally; use NodePort if not on a cloud provider


```


- *type: Sets the type of Service. Options:*
  - *LoadBalancer: Exposes externally (suitable for cloud providers like AWS, GCP, Azure).*
  - *NodePort: Exposes a specific port on each Node.*
  - *ClusterIP: Restricts access to within the cluster (default).*
    
- *port: Exposed Service port (80 in this example).*
- *targetPort: Port on the container receiving the traffic.*
- *selector: Matches the label defined in the Deployment to ensure the Service routes to the correct pods.*



### 3. Applying the YAML Files
1. Create YAML Files

- Save the Deployment configuration to a file named deployment.yaml.
- Save the Service configuration to a file named service.yaml.

2. Apply the Configurations

  - *Run the following commands to create the Deployment and Service in your Kubernetes cluster:*

```yml
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

3. Verify Resources

- To confirm that the resources are running, use:


```yml

kubectl get deployments
kubectl get services

```






<br>
<br>


## Conclusion
---
*Through this exercise, I gained valuable hands-on experience with Kubernetes, specifically in managing deployments and exposing services. I learned how to scale applications, configure network access, and apply YAML files to deploy resources efficiently. This implementation reinforced my understanding of Kubernetes concepts like Deployment, Service, and pod scaling, which are crucial for maintaining high availability and seamless updates in production environments. The knowledge gained from this task will be highly beneficial in managing real-world applications and infrastructure in a Kubernetes cluster.*














<br>
<br>
<br>
<br>



**👨‍💻 𝓒𝓻𝓪𝓯𝓽𝓮𝓭 𝓫𝔂**: [Suraj Kumar Choudhary](https://github.com/Surajkumar4-source) | 📩 **𝓕𝓮𝓮𝓵 𝓯𝓻𝓮𝓮 𝓽𝓸 𝓓𝓜 𝓯𝓸𝓻 𝓪𝓷𝔂 𝓱𝓮𝓵𝓹**: [csuraj982@gmail.com](mailto:csuraj982@gmail.com)





<br>






