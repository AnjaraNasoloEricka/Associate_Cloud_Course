# Cloud Run 

## What is Cloud Run ?
-  Managed compute platform that runs stateless containers via web requests or Pub/Sub events
- Cloud Run is serverless : it means it removes all infrastructure management tasks so you can focus on developing applications
- Built on Knative, an open API and runtime environment built on Kubernetes. It can be fully managed on Google Cloud, on Google Kubernetes Engine, or anywhere Knative runs.
- Can automatically scale up and down from zero almost instantaneously, and it charges only for the resources used, calculated down to the nearest 100 milliseconds, so you‘ll never pay for over-provisioned resources

## The Cloud Run developer workflow
1. Write your application using your favorite programming language : this application should start a server that listens for web requests
2. Build and package your application into a container image
3. The container image is pushed to Artifact Registry, where Cloud Run will deploy it.

Once you’ve deployed your container image, you’ll get a unique `HTTPS URL back`. Cloud Run then starts your container on demand to handle requests, and ensures that all incoming requests are handled by dynamically adding and removing containers.

## Why a a container-based workflow is great ?
1. It gives you a great amount of transparency and flexibility
2. Sometimes, you’re just looking for a way to turn source code into an HTTPS endpoint, and you want your vendor to make sure your container image is secure, well-configured and built in a consistent way.

> With Cloud Run you can do both : you can use a container-based workflow, as well as a source-based workflow.

## Source-based workflow
1. The source-based approach will deploy source code instead of a container image
2. Cloud Run then builds the source and packages the application into a container image. Cloud Run does this using `Buildpacks` - an open source project.

## Hands on Lab

### 1. Activate Google Cloud Shell

1. In Cloud console, on the top right toolbar, click the Open Cloud Shell button.
2. You can list the active account name with this command:
    ```bash
    gcloud auth list
    ```

3. You can list the project ID with this command:
    ```bash
    gcloud config list project
    ```

### 2. Enable the Cloud Run API and configure your Shell environment

1. From Cloud Shell, enable the Cloud Run API :
```bash
gcloud services enable run.googleapis.com
```
2. Set the compute region : 
```bash
gcloud config set compute/region "REGION"
```

3. Create a location environment variable : 
```bash
LOCATION="Region"
```

### 3. Write the sample application
- In Cloud Shell create a new directory named helloworld, then move your view into that directory. Just create your app in this folder.

### 4. Containerize your app and upload it to Artifact Registry
1. Create a DockerFile in your app folder.
```docker
# Use the official lightweight Node.js 12 image.
# https://hub.docker.com/_/node
FROM node:12-slim

# Create and change to the app directory.
WORKDIR /usr/src/app

# Copy application dependency manifests to the container image.
# A wildcard is used to ensure copying both package.json AND package-lock.json (when available).
# Copying this first prevents re-running npm install on every code change.
COPY package*.json ./

# Install production dependencies.
# If you add a package-lock.json, speed your build by switching to 'npm ci'.
# RUN npm ci --only=production
RUN npm install --only=production

# Copy local code to the container image.
COPY . ./

# Run the web service on container startup.
CMD [ "npm", "start" ]
```

2. Now, build your container image using Cloud Build by running the following command from the directory containing the Dockerfile. (Note the $GOOGLE_CLOUD_PROJECT environmental variable in the command, which contains your lab's Project ID)

```bash
gcloud builds submit --tag gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld
```

3. List all container images : 
```bash
gcloud container images list
```

4. Register gcloud as the credential helper for all Google-supported Docker registries
```bash
gcloud auth configure-docker
```

5. To run and test the application locally from Cloud Shell, start it using this standard docker command:
```bash
docker run -d -p 8080:8080 gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld
```

### 5. Deploy to Cloud Run
Deploying your containerized application to Cloud Run is done using the following command adding your Project-ID:
```bash
gcloud run deploy --image gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld --allow-unauthenticated --region=$LOCATION
```

### 6. Clean up images 
1. Delete your Google Cloud project to avoid incurring charges, which will stop billing for all the resources used within that project, or simply delete your helloworld image using this command
```bash
gcloud container images delete gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld
```

2. To delete the Cloud Run service, use this command : 
```bash
gcloud run services delete helloworld --region="REGION"
```