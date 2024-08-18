[README.md](https://github.com/user-attachments/files/16648582/README.md)
# [AWS] Highly available & Scalable Containerized Application using Docker, Kubernetes

![cluster architecture](https://github.com/user-attachments/assets/f7c52670-49d8-47bd-af77-61d532684a9d)


## Documentation

[Super Cloud Man - [AWS] Highly available & Scalable Containerized Application using Docker, Kubernetes 💯 ](https://supercloudman.com/post3)

### This Doc contains some installation and configuration files for the project.


## Authors

- [@supertonkaman](https://www.github.com/supertonka)

In this project we are going to build a scalable web application using Docker and Kubernetes, deploy it on AWS, and integrate monitoring services. The web application will be developed in Python and deployed in Docker containers. Use AWS's EC2 instances for virtualization and leverage AWS's managed Kubernetes service, EKS.

## Dockerizing Python application

```Dockerfile
# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install flask

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME=World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

## Kubernetes Deployment Configuration
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: flask-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: flask-app
  template:
    metadata:
      labels:
        app: flask-app
    spec:
      containers:
      - name: flask-app
        image: supertonka/flask-app:latest
        ports:
        - containerPort: 5000
```

## Kubernetes Service Configuration
```yaml
apiVersion: v1
kind: Service
metadata:
  name: flask-app-service
spec:
  type: LoadBalancer
  selector:
    app: flask-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 5000
```Uploading README.md…]()
