 steps for setting up Kubernetes using Minikube and K9s locally, along with deploying an application on Amazon EKS:

---

### **How to Set Up and Deploy Your Application on Kubernetes: Local and AWS EKS**

---

### **Part 1: Setting Up Kubernetes Locally with Minikube and K9s**

#### **1. Install Minikube**

- **Install Minikube:**
   - Follow the official guide to install Minikube, which allows you to run Kubernetes locally: [Install Minikube](https://minikube.sigs.k8s.io/docs/start/).

#### **2. Start Minikube**

- **Start the Minikube Cluster:**
   - Start a local Kubernetes cluster using Minikube.
     ```bash
     minikube start
     ```

#### **3. Deploy Your Application on Minikube**

- **Apply Kubernetes Manifests:**
   - Deploy your application using the Kubernetes manifest files (e.g., `deployment.yml` and `service.yml`).
     ```bash
     kubectl apply -f deployment.yml
     kubectl apply -f service.yml
     ```

- **Expose the Service:**
   - Get the URL to access your service.
     ```bash
     minikube service <service-name> --url
     ```

#### **4. Manage Kubernetes with K9s**

- **Install K9s:**
   - Install K9s, a terminal UI to manage your Kubernetes clusters: [Install K9s](https://k9scli.io/topics/install/).

- **Use K9s:**
   - Run `k9s` to interact with your local Kubernetes cluster and manage resources like pods, services, and deployments.

#### **5. Access Your Application**

- **Access the Application:**
   - Use the URL provided by `minikube service` to access your application in a web browser.

#### **6. Stop Minikube**

- **Stop the Minikube Cluster:**
   - When you're done, stop the Minikube cluster.
     ```bash
     minikube stop
     ```

---

### **Part 2: Creating and Deploying Your Application on Amazon EKS**

#### **1. Connect to Your AWS User Account**

- **Configure AWS CLI:**
   - Configure your AWS CLI with your access key and secret key.
     ```bash
     aws configure
     ```

#### **2. Install AWS CLI**

- **Install AWS CLI:**
   - Install the AWS CLI using the guide provided by AWS: [Install AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

#### **3. Install eksctl**

- **Install eksctl:**
   - Follow the guide to install `eksctl`: [Install eksctl](https://docs.aws.amazon.com/emr/latest/EMR-on-EKS-DevelopmentGuide/setting-up-eksctl.html).

#### **4. Create a Cluster on AWS**

- **Create EKS Cluster:**
   - Use `eksctl` to create a Kubernetes cluster on AWS.
     ```bash
     eksctl create cluster --name <cluster-name> --nodes-min=2
     ```

#### **5. Ensure Namespace Consistency**

- **Verify Namespace:**
   - Make sure the namespace in your manifest files matches the one on your EKS cluster.

#### **6. Update Service Type to LoadBalancer**

- **Modify service.yaml:**
   - Change the service type from `NodePort` to `LoadBalancer` in your manifest file.
   ```yaml
   spec:
     type: LoadBalancer
   ```

#### **7. Deploy Your Application on EKS**

- **Apply Kubernetes Manifests:**
   - Deploy the application using `kubectl`.
     ```bash
     kubectl -n <namespace-name> apply -f deployment.yml
     kubectl -n <namespace-name> apply -f service.yml
     ```

#### **8. Access Your Application**

- **Access via K9s:**
   - Use K9s to get the external IP of your service.
   - Copy the external IP and access your application via a web browser.

#### **9. Delete Your Cluster**

- **Clean Up:**
   - Delete your EKS cluster when you're done.
     ```bash
     eksctl delete cluster --name <cluster-name>
     ```

---

This documentation provides a comprehensive guide for deploying your application using Kubernetes, both locally with Minikube and on AWS with EKS. It covers everything from setup and deployment to accessing and managing your application.
