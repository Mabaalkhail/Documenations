# Kubernetes

This file will walk you through the steps on how to install and deploy your first project on kubernetes.

# Download
download the version that matches your system(windows,linux,mac)
 [Kubernetes](https://kubernetes.io/docs/setup/)
[Docker](https://www.docker.com/products/docker-desktop/)
[Node.js](https://nodejs.org/en) 
Any text editor or IDE 
I recommend [Visual Studio Code](https://code.visualstudio.com/download)   


## getting-started

To check which version you have 
use this command in cmd 
`minikube version`
![enter image description here](https://i.postimg.cc/05ShR8sr/Screenshot-2023-05-15-132159.png)

For Node use this Command in cmd

    node
![enter image description here](https://i.postimg.cc/FRr1tPfH/node.png)

installing express using Command prompt

    npm install express

Creating js file using VSC
First step is create index.js file using any editor I used VSC 
write a code to test whether it's working or not 
![enter image description here](https://i.postimg.cc/kM6GD4XD/Screenshot-2023-05-16-085309.png)
 
 Then to test js file use this Command 
 

    node index.js 
the expected response should be 

    > Server listening on port 8080
 now we can see the response using the browser 
 

    localhost:8080



## Creating docker image

First step is to create a file named Dockerfile in the same directory of our previous step
inside the Dockerfile write these commands 

   ```Dockerfile
   FROM node:14-alpine 
   # node is the image and alpine is the lighter version 
    WORKDIR /app
    # where the directory inside the image
    COPY package.json .
    # it takes the json containing express dependency
    RUN npm install --production 
    COPY . .
    EXPOSE 8080
    # makes the port accesible outside the container 
    CMD ["npm", "start"]
    
```
Now build an image using the docker build command "note: you must be in the same directory"

    docker build -t my-api .


To run it use this command 

    docker run my-api
After running it you should be able to see the result through the browser

    localhost:8080



## deployemnt through kubernetes


We will use minikube to deploy our work. 
to start minikube use the following command 

    minikube start

you should see the following output 

    * Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default

The command `minikube docker-env` outputs a list of environment variables that can be used to configure a local Docker client to use the Docker daemon running in Minikube. The command `Invoke-Expression` is a PowerShell cmdlet that executes a string as a command.

    minikube docker-env | Invoke-Expression
    

now you should build your docker image while you're inside minikube 

    docker build -t my-api .


you can check the running containers by using this command 

    docker ps

create a yaml file

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-api
  labels:
    app: my-api
spec:
  selector:
    matchLabels:
      app: my-api
  replicas: 2
  template:
    metadata:
      labels: # labels to select/identify the deployment
        app: my-api 
    spec:     # pod spec                  
      containers: 
      - name: my-api
        image: apiv1
        imagePullPolicy: Never
        ports:
        - containerPort: 8080
       

---
apiVersion: v1
kind: Service
metadata:
  name: my-api
spec:
  type: NodePort
  selector:
    app: my-api
  ports:
  - port: 80
    targetPort: 8080

```

apply the yaml file using the command 
```
kubectl apply -f deployment.yaml
```

to display the exsiting nodes

    kubectl get nodes


The `kubectl get svc` command can be used to list the services in a Kubernetes cluster.


The command `minikube service my-api` exposes the service named `my-api or whatever you named it` on the host machine. This allows you to access the service from outside of the Kubernetes cluster.

**now your api is running in a deployment** 


