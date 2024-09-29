# Setting up a google cloud environment

**Case study :** Cymbal Superstore's cloud solution

## What do u need to do ?
1. Setting up cloud projects and accounts 
    - Start with a planning meeting 
    - **About :**
        - How the project will be structured or organized ? 
            - Resource hierarchy 
            - Managing projects, quotas 
            - Managing users and groups 
            - Apply Access Management 

2. Setting up billing and monitoring (use of cloud resources)

3. Choosing how u interact with Google 
    - GUI 
    - CLI 
    - Software development tools

### Resource hierarchy 

3. Project Level (Env of the project) : 
    - B2B Dev
    - B2B Staging
    - B2B Production 

2. Folder Level 
    - About operations 
        - **Folder name** : B2B Supply Chain
        - **Runtime environment and tools** : `virtual machines`
    - About sales and marketing 
        - **Folder name** :ECommerce App
        - **Runtime environment and tools** : 
            - Containerize App
            - Use `Google Kubernetes Engine`
    - About Logistics 
        - **Folder name** : Transportation App
        - **Runtime environment and tools** : 
            - Use `Cloud Functions` to track location
    - **Multiple project in each folder**
        - Each environment should  : 
            - contains CICD for developing, staging and production
            - Grant organizational policies : 
                - Data access in other folder
                    - Give viewer permission 
                - Enabling APIs, with projects during setup
            - Setup member IM (information management) role 
                - Right access depending on the needs of their job and role on symbal superstore
    
1. Organization Level (the customer's final project) 
    - Cymbal Superstore in our case

### Exemple of use case 
**UC** : Data analysts in the Marketing Department will need access to historic sales data in the Ecommerce system.

This is a great use case for BigQuery, Google's cloud-based data warehouse solution.

1. How would we go about giving the proper access 
    - Data analyst added to a group 
    - Now, you manage it in a group level
    - What they need : 
        - View data and run queries with BigQuery, dataviewer role 
        - Permissions : 
            - **BigQuery.jobs.create permission**

    - On which resource : **BigQuery**

### Setting up products in Google Cloud's operations suite (or stack driver)
- Usage : 
    - Provides metrics and logging services
- How ? 
    - Setup projet scoping (staging)
    - Monitored project (#scoping) (dev and production)

### Migrate to Google Cloud 
For that, u'll need to : 
    - Create a different billing account for each group and link each project to the appropriate account.

## Interacting with Google Cloud 
- **Web user interface :** Google Cloud Console
- **Cloud SDK and Cloud Shell** : CLI 
    - Use `gcloud`
- **Cloud Mobile App**
- **REST-based API**
