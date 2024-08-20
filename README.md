
# **Steps to Push a Docker Image to Docker Hub and Configure GitHub Actions**

#### **1. Build and Push Docker Image to Docker Hub**

1. **Build your Docker Image:**
   - Use Docker to build your image locally.
     ```bash
     docker build -t <your-dockerhub-username>/<image-name>:<tag> .
     ```

2. **Login to Docker Hub:**
   - Authenticate your Docker CLI with Docker Hub.
     ```bash
     docker login
     ```

3. **Push the Docker Image to Docker Hub:**
   - Push the image to your Docker Hub repository.
     ```bash
     docker push <your-dockerhub-username>/<image-name>:<tag>
     ```

#### **2. Create an Access Token in Docker Hub**

1. **Generate an Access Token:**
   - Go to Docker Hub, navigate to your account settings, and create a new Access Token.
   - Save the token securely, as you will need it for GitHub.

#### **3. Configure GitHub Repository for GitHub Actions**

1. **Access GitHub Repository Settings:**
   - Go to your GitHub repository.
   - Navigate to `Settings` > `Secrets and variables` > `Actions`.

2. **Add GitHub Action Variables:**
   - **DOCKERHUB_USERNAME**:
     - Add a new repository secret named `DOCKERHUB_USERNAME` and set it to your Docker Hub username.
   - **DOCKERHUB_TOKEN**:
     - Add another secret named `DOCKERHUB_TOKEN` and paste the Docker Hub Access Token you created earlier.

#### **4. Set Up GitHub Actions Workflow**

1. **Create a GitHub Actions YAML File:**
   - In your repository, navigate to `.github/workflows/`.
   - Create a new YAML file (e.g., `docker-publish.yml`) with the following content:

     ```yaml
     name: Build and Push Docker Image  # The name of the workflow that appears in the GitHub Actions UI

     on:
       push:
         branches: [dev]  # Triggers the workflow when there is a push to the 'dev' branch
       pull_request:
         branches: [dev]  # Also triggers the workflow when a pull request targets the 'dev' branch

     jobs:
       build-and-push:  # Defines a job named 'build-and-push'
         runs-on: ubuntu-latest  # Specifies the operating system used by the runner (latest Ubuntu version)

         steps:
           - name: Checkout code  # Step 1: Check out the repository code
             uses: actions/checkout@v2  # Uses the GitHub-provided action to check out the latest code

           - name: Log in to Docker Hub  # Step 2: Log in to Docker Hub
             uses: docker/login-action@v1  # Uses the Docker login action provided by Docker
             with:
               username: ${{ secrets.DOCKERHUB_USERNAME }}  # Fetches the Docker Hub username from GitHub Secrets
               password: ${{ secrets.DOCKERHUB_TOKEN }}  # Fetches the Docker Hub access token from GitHub Secrets

           - name: Build and push Docker image  # Step 3: Build and push the Docker image
             env:
               REPOSITORY: taskmanagement  # Sets an environment variable for the Docker repository name
               IMAGE_TAG: latest  # Sets an environment variable for the Docker image tag
             run: |
               docker build -t ${{ secrets.DOCKERHUB_USERNAME }}/$REPOSITORY:$IMAGE_TAG .  # Builds the Docker image and tags it with the repository name and 'latest' tag
               docker push ${{ secrets.DOCKERHUB_USERNAME }}/$REPOSITORY:$IMAGE_TAG  # Pushes the tagged image to Docker Hub
     ```

2. **Commit and Push the Workflow File:**
   - Commit the workflow file to your repository and push it to GitHub.
   - GitHub Actions will automatically trigger based on the configuration.

---

### **Summary of the Workflow:**

- **Building and Pushing Docker Image:**
  - The process starts by building a Docker image locally using `docker build`, then pushing the image to Docker Hub using `docker push`.

- **Generating Docker Hub Access Token:**
  - An Access Token is generated from Docker Hub, which is required to authenticate the GitHub Actions workflow.

- **Configuring GitHub Secrets:**
  - In the GitHub repository, secrets are configured for `DOCKERHUB_USERNAME` and `DOCKERHUB_TOKEN`, which are securely stored and used in the workflow.

- **Setting Up GitHub Actions Workflow:**
  - A YAML file is created in `.github/workflows/` to define the steps that should be executed when a push or pull request is made to the `dev` branch. This workflow checks out the code, logs into Docker Hub, builds the Docker image, and pushes it to Docker Hub.

This updated documentation should provide a clear and concise guide to setting up the Docker image build and push process using GitHub Actions.
