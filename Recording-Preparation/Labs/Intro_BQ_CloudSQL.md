# Intro to BigQuery and CloudSQL 

## BigQuery 
- You can access to BigQuery via Navigation Menu > BigQuery 
- You can run SQL Query via the Query editor 
- projects -> datasets -> tables

## Cloud SQL 
### Create a database via CloudSQL 
1. export PROJECT_ID=$(gcloud config get-value project)
gcloud config set project $PROJECT_ID

2. gcloud auth login --no-launch-browser

3. gcloud sql connect my-demo(db name) --user=root --quiet
