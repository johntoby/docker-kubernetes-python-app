# docker-kubernetes-python-app
This project is a simple Python flask application, that is containerized by docker and deployed using Kubernetes. 

The Architecture of the project will flow like this: 
![johntoby python app drawio](https://github.com/user-attachments/assets/a78bb019-4f31-4e3c-a44b-0b44dc5eca84)


## Prerequisites 
To successfully build, package and deploy the application, the following needs to be installed on your machine - either local machine or virtual machine: 

 - Docker: the containerization engine. Click [HERE](https://docs.docker.com/engine/install/ ) to install docker. 
 - Minikube: a local kubernetes installation which makes it easy to learn and develop applications on kubernetes easily. Click [HERE](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fwindows%2Fx86-64%2Fstable%2F.exe+download") to install minikube.    
 - Kubectl: a command line utility to interact with kubernetes clusters. Install kubectl from [HERE](https://kubernetes.io/docs/tasks/tools/) 
 - VS code: code editor to build your code and configuration files. Install VS Code from [HERE](https://code.visualstudio.com/download) 

## Write your python code

Create an app.py file on your vscode and write a simple python code using flask framework to return Hello JT...Welcome to Kodecamp to the screen 

![app py](https://github.com/user-attachments/assets/88ad6d0b-bf4a-4fbc-abe2-49b1ca06507e)

Then create another file called reuirements.txt to store your major application requirement. Here, we have just one requirement which is flask:

![requirements txt](https://github.com/user-attachments/assets/19146d61-86e1-47c0-b68b-eacaa8cab99b)

## Dockerize the application 
After creating the application source code, and the requirements file, we will write a Dockerfile to containerize the application using a python slim image

![dockerfile1](https://github.com/user-attachments/assets/65bdf43f-0fd1-46c5-bb04-2afaf3274b86)

![dockerfile2](https://github.com/user-attachments/assets/a8c8b989-eb53-4749-9c27-3c66f1536887)


to build the docker image, run this command 
```
docker build -t johntoby/python-app .
```
This will build the application image named johntoby/python-app 

![docker-images-list](https://github.com/user-attachments/assets/1f4f515d-5e14-48d9-8ac7-271e9924011a)

To run the application locally using docker and expose it on port 5000, we will run the following command: 
```
docker run -it -p 5000:5000 johntoby/python-app
```
![docker run working](https://github.com/user-attachments/assets/63a8ee13-b220-4a68-b437-a3afb63b1c81)

Since the application is running on an ec2 instance, I will browse the public ip of my ec2 instance on port 5000 i.e. 54.89.171.65:5000 

![finalapp-port-5000](https://github.com/user-attachments/assets/bdfe899a-6ffd-40c1-8ab3-4ec27d20e34a)

This confirms the application is successfully dockerized and running on port 5000. 


## Push the image to dockerhub 
Login to dockerhub and authenticate to your CLI. Then run this command to push the local image to dockerhub 
```
docker push johntoby/python-app
```
![docker hub image](https://github.com/user-attachments/assets/1f92c16d-a63d-44ae-a3e1-75d647bd6c89)



## Deply the application to kubernetes 
We will use minikube to deploy the application on kubernetes. 

Run this command to start minikube 
```
minikube start
```
Create deployment.yaml file to deploy the image

![deployment yaml](https://github.com/user-attachments/assets/a3eab172-ff5b-4aec-b1a7-e67d32824284)

run this command to check if your deployment is created successfully 
```
kubectl get deployment
```


![deployment-created](https://github.com/user-attachments/assets/f3d89356-38f3-4b7d-98b9-e7d5b3d56eb7)


Create your service.yaml file to expose the application on port 5000 
![service yaml](https://github.com/user-attachments/assets/b528686c-b822-440b-9482-1b5785e7c825)

Run this command to check if your service is successfully created 
```
kubectl get service
```

![service-created](https://github.com/user-attachments/assets/3991997e-1394-474e-ac8e-8f0dae5b1ae3)

To check the service, run this command
```
minikube service
```
![service-running](https://github.com/user-attachments/assets/b3bf6072-9d27-4e80-9d1f-458b79c5d83a)

Finally, to port-forward the service to be able to view it on the browser, run this command:
```
kubectl port-forward service/kodecamp-service 5000:5000
```
The application should be available on the browser at localhost:5000 

![finalapp-port-5000](https://github.com/user-attachments/assets/7fa8c251-f4c5-40e7-8cd8-597d3e961757)

Thanks. 


