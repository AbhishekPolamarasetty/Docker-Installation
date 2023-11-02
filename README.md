## AWS Docker Instalation in Ubuntu

1. **Docker Installation**

   Follow the Docker installation instructions from the [official documentation](https://docs.docker.com/engine/install/ubuntu/).

   ```bash
   sudo apt-get update
   sudo apt-get install ca-certificates curl gnupg
   sudo install -m 0755 -d /etc/apt/keyrings
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
   sudo chmod a+r /etc/apt/keyrings/docker.gpg
   echo "deb [arch=\$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \$(. /etc/os-release && echo \"\$VERSION_CODENAME\") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   sudo apt-get update
   sudo apt-get install docker-ce docker-ce-cli containerd.io
   ```



2. **Minikube Installation**

   Follow the Minikube installation instructions from the [official documentation](https://minikube.sigs.k8s.io/docs/start/).

   ```bash
   curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
   sudo install minikube-linux-amd64 /usr/local/bin/minikube
   ```

3. **Kubectl Installation**

   Follow the Kubectl installation instructions from the [official documentation](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/).

   ```bash
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
   echo "$(cat kubectl.sha256) kubectl" | sha256sum --check
   snap install kubectl --classic
   ```

4. **Apache2 Installation**

   Install Apache2:

   ```bash
   sudo apt-get update
   sudo apt-get install apache2
   ```

5. **Set Up Docker and Minikube**

   Add your user to the Docker group:

   ```bash
   sudo usermod -aG docker $USER
   newgrp docker
   ```

   Start Minikube:

   ```bash
   minikube start --driver=docker
   ```

## Usage

1. Create a directory for your project and navigate to it:

   ```bash
   mkdir your_project_directory
   cd your_project_directory
   ```

2. Create a `deployment.yaml` file to define your Kubernetes deployment. Be sure to specify the image from your Docker repository.

3. Create a `service.yaml` file to define your Kubernetes service.

4. Apply the deployment and service configurations:

   ```bash
   kubectl apply -f deployment.yaml
   kubectl apply -f service.yaml
   ```

5. Check the status of your services, pods, and nodes:

   ```bash
   kubectl get svc
   kubectl get all
   kubectl get pods
   kubectl get node
   kubectl get node -o wide
   ```

6. Access your service using Minikube:

   ```bash
   minikube service service_name
   ```

7. Obtain the Minikube internal IP:

   ```bash
   minikube ip
   ```

8. Use `curl` to access your service using the internal IP and port obtained from `kubectl get svc`.

   ```bash
   curl internal_ip:port
   ```


