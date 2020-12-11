# Udagram

Udagram is a simple cloud application developed alongside the Udacity Cloud Developer Nanodegree. It allows users to register and log into a web client and post photos to the feed.

----

## Deployment Model

The project is split into two parts:
1. Frontend - Angular web application built with Ionic Framework
2. Backend RESTful API - Node-Express application

![DeploymentModel](/screenshots/Deployment_model.png)

[Image Courtesy](https://blog.juadel.com/2020/05/15/create-a-kubernetes-cluster-in-amazon-eks-using-a-reverse-proxy/)

## Containers and Microservices

1. `/feed` and `/user` backends are separated into independent microservices.
2. The project includes Dockerfiles for each project to successfully create Docker images for /feed, /user (backend), frontend and reverse-proxy

## Independent Releases and Deployments

The project includes Travis CI pipeline to automatically push the Docker images of the microservices into Dockerhub

## Service Orchestration with Kubernetes

1. The Microservices are deployed using Kubernetes cluster on AWS.
2. Uses the NGINX reverse proxy to redirect the request to the correct microservice (/feed or /users) based on path based load-balancing.
3. The Kubernetes pods are replicted for self-healing.
4. The Kubernetes deployments are autoscaled with CPU metrics threshold. 

## Debugging, Monitoring, and Logging

The backend API logging is improved using request IDs.

### How to use this project

### Database
Create a PostgreSQL database either locally or on AWS RDS. Set the config values for environment variables prefixed with `POSTGRES_`.

### S3
Create an AWS S3 bucket. Set the config values for environment variables prefixed with `AWS_`

### Backend API
* To download all the package dependencies, run the command from the directory `udagram-api/`:
    ```bash
    npm install .
    ```
* To run the application locally, run:
    ```bash
    npm run dev
    ```
* You can visit `http://localhost:8080/api/v0/feed` in your web browser to verify that the application is running. You should see a JSON payload.

### Frontend App
* To download all the package dependencies, run the command from the directory `udagram-frontend/`:
    ```bash
    npm install .
    ```
* Install Ionic Framework's Command Line tools for us to build and run the application:
    ```bash
    npm install -g ionic
    ```
* Prepare your application by compiling them into static files.
    ```bash
    ionic build
    ```
* Run the application locally using files created from the `ionic build` command.
    ```bash
    ionic serve
    ```
* You can visit `http://localhost:8100` in your web browser to verify that the application is running. You should see a web interface.

### Kubernetes Deployment

The deployment files for pods and services are available [here](https://github.com/realnitinworks/udagram/tree/master/udagram-deployment).
These files can be applied on the K8S cluster using

```bash
kubectl -f <file.yml>
```

