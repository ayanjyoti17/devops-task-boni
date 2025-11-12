# DevOps Engineer - Kubernetes Deployment Task



This repository contains the configuration files for a technical assessment. The task was to take an open-source web application, containerize it, and deploy it on a Kubernetes cluster, providing a live, accessible link.



This project was deployed using **k3s** (a lightweight Kubernetes distribution) running on an **AWS EC2 (t2.micro)** instance.



---



## 🚀 Live Deployed Application



You can access the live "Hello World" application at the following link:



**`http://50.19.71.72:30155/`**


---



## 🛠️ Technology Stack Used



* **Cloud Provider:** AWS (using a `t2.micro` EC2 instance on the free tier)

* **Containerization:** Docker

* **Orchestration:** k3s (Lightweight Kubernetes)

* **Application:** A simple Python Flask "Hello World" web app

* **Operating System:** Ubuntu Server 22.04 LTS



---



## 📂 File Explanations



This repository contains the core files used to build and deploy the application:



* **`Dockerfile`**

    This file contains the instructions to build a Docker image for the Python Flask application. It uses a slim Python base image, installs dependencies from `requirements.txt`, and serves the app using `gunicorn`.



* **`deployment.yaml`**

    This Kubernetes manifest defines a `Deployment`. It tells the cluster to run two replicas of the application, using the Docker image and ensuring the app is restarted if it fails.



* **`service.yaml`**

    This manifest defines a `Service` of type **`NodePort`**. This is what exposes the application to the internet. It maps a public port on the EC2 host machine (in the range 30000-32767) to the application's internal port (5000), allowing it to be accessed via the EC2 instance's public IP.



---



## Reproducing This Deployment



1.  **Launch AWS EC2 Instance:**

    * Instance Type: `t2.micro` (Free tier eligible)

    * AMI: Ubuntu Server 22.04 LTS

    * Security Group: Allow inbound traffic for SSH (port `22`) and the NodePort range (Custom TCP `30000-32767`).



2.  **Install k3s:**

    * SSH into the EC2 instance.

    * Run: `curl -sfL https://get.k3s.io | sh -`



3.  **Deploy Application:**

    * Create the `deployment.yaml` and `service.yaml` files on the server (or clone this repository).

    * Apply the manifests:

        ```bash

        sudo k3s kubectl apply -f deployment.yaml

        sudo k3s kubectl apply -f service.yaml

        ```



4.  **Find the Deployed Link:**

    * Get the allocated `NodePort` by running: `sudo k3s kubectl get service hello-app-service`

    * Construct the public URL: `http://50.19.71.72:30155/`