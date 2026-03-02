# kubernetes-minikube

Minikube is a tool that lets you run Kubernetes locally. 
minikube runs a single-node Kubernetes cluster on your personal computer (including Windows, macOS and Linux PCs) so that you can try out Kubernetes, or for daily development work.

## Docker installation

### installation for Mac, Windows 10 Pro, Enterprise, or Education

https://www.docker.com/get-started

Choose Docker Desktop

### installation for Windows home

https://docs.docker.com/docker-for-windows/install-windows-home/

## Kuberntes Minikube installation

https://minikube.sigs.k8s.io/docs/start/

Minikube provides a dashboard (web portal). Access the dashboard using the following command:

```
minikube dashboard
```

## Download this project

This project contains a web service coded in Java, but the language doesn't matter. This project has already been built and the binary version is there:

First of all, download and uncompress the project: https://github.com/charroux/kubernetes-minikube

You can also use git: `git clone https://github.com/charroux/kubernetes-minikube`

Then move to the sud directory with `cd kubernetes-minikube/myservice` where a DockerFile is.

## Test this project using Docker

Build the docker image:
```
docker build -t chaimaa .
```

Check the image:
```
docker images
```

Start the container:
```
docker run -p 4000:8080 -t chaimaa
```

8080 is the port of the web service, while 4000 is the port for accessing the container. Test the web service using a web browser: http://localhost:4000 It displays hello.

Ctrl-C to stop the Web Service.

Check the containerID:
```
docker ps
```

Stop the container:
```
docker stop 4a2b86290622
```

## Publish the image to the Docker Hub

Retreive the image ID:
```
docker images
```

Tag the docker image: 
```
docker tag d9d2d70c6bc7 chaimaaa/chaimaa:1
```

Example: `docker tag 1dsd512s0d myDockerID/myservice:1`

Login to docker hub: 
```
docker login
```
or
```
docker login http://hub.docker.com
```
or 
```
docker login -u username -p password
```

Push the image to the docker hub:
```
docker push chaimaaaa/chaimaa:1
```

Example: `docker push myDockerID/myservice:1`

## Create a kubernetes deployment from a Docker image

```
kubectl get nodes
```
```
>kubectl create deployment myservice --image=chaimaaaa/chaimaa:1
```

The image used comes from the Docker hub: https://hub.docker.com/r/efrei/myservice/tags

But you can use your own image instead.

Check the pod:
```
kubectl get pods
```

Check if the state is running.

Get complete logs for a pods: 
```
kubectl describe pods
```

Retreive the IP address but notice that this IP address is ephemeral since a pods can be deleted and replaced by a new one.

Then retrieve the deployment in the minikube dashboard. 
Actually the Docker container is runnung inside a Kubernetes pods (look at the pod in the dashboard).
  
You can also enter inside the container in a interactive mode with:
```
>kubectl exec -it myservice-69784d47b6-svr9h -- /bin/bash
```

where podname is the name of the pods obtained with:
```
kubectl get pods
```

List the containt of the container with:
```
ls
```

Don't forget to exit the container with:
```
exit
```

