# Kubernetes Workshop

## Requirements

1. Ubuntu 16.04 with sudo access

## Installation

### Package Update

```bash
sudo apt update
```

### Docker

1. Uninstall old versions

    ```bash
    sudo apt remove docker docker-engine docker.io containerd runc
    ```

2. Set up the repository

    ```bash
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    sudo apt update
    ```

3. Install Docker

    ```bash
    sudo apt install docker-ce docker-ce-cli containerd.io
    ```

### Kubectl

1. Install Kubectl

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
    chmod +x ./kubectl
    sudo mv ./kubectl /usr/local/bin/kubectl
    kubectl version
    ```

### Minikube

1. Install Minikube

    ```bash
    curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    chmod +x ./minikube
    sudo mv ./minikube /usr/local/bin/
    minikube version
    ```

## Setup

1. Setup minikube vm-driver to `none`

    ```bash
    sudo minikube config set vm-driver none
    ```

2. Start minikube

    ```bash
    sudo minikube start
    ```

3. Setup permissions

    ```bash
    sudo chown -R $USER $HOME/.kube $HOME/.minikube
    ```

## Using Minikube

1. Get all pods details

    ```bash
    kubectl get pods -A
    sudo docker ps
    ```

2. Run Google Echo server

    ```bash
    kubectl create deployment --image gcr.io/google_containers/echoserver:1.3 hello-minikube
    ```

3. List the pods

    ```bash
    kubectl get pods
    kubectl describe pods
    ```

4. List the deployment

    ```bash
    kubectl get deployment
    kubectl describe deployment
    ```

5. Scale up application

    ```bash
    kubectl scale deployment --replicas 2 hello-minikube
    kubectl get pods
    ```

6. Expose the deployment

    ```bash
    kubectl expose deployment hello-minikube --type=NodePort --port=8080
    kubectl get service
    ```

7. View the service

    ```bash
    minikube service hello-minikube
    ```

8. Upgrade the application

    ```bash
    kubectl set image deployment hello-minikube echoserver=gcr.io/google_containers/echoserver:1.4
    kubectl get pods
    ```

9. Cleanup

    ```bash
    kubectl delete service hello-minikube
    kubectl delete deployments hello-minikube
    ```

## Stop minikube

1. Stop Minikube

    ```bash
    sudo minikube stop
    ```

2. Cleanup Setup

    ```bash
    sudo minikube delete
    ```
