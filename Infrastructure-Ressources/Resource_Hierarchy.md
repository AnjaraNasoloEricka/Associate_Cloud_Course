# Functional Structure of Google Cloud 

## Resource Hierarchy

Google Cloud's hierarchy contains `4 level` : 

1. **Resources** : represent virtual machines, Cloud Storage buckets, tables in BigQuery, or anything else in Google Cloud.
    - Resources are organized into project
2. **Project** : 
    - Projects can be organized into folders, or even subfolders.
3. **Folder** 
4. **Organization node**: encompasses all the projects, folders, and resources in your organization.

### Hierarchy Policies 
- Policies are `inherited downward`.
    - This means that if you apply a policy to a folder, it will also apply to all of the projects within that folder.

### More about Project Level
- Each project is a separate entity under the organization node, and each resource belongs to exactly one project.
- Projects can have different owners and users because they’re billed and managed separately.
- Each Google Cloud project has three identifying attributes: `a project ID, a project name, and a project number`: 
    - Project ID : used in different contexts to inform Google Cloud of the exact project to work with.
    - Project names : don’t have to be unique and they can be changed at any time, so they are not immutable.
    - Projet number : an unique value that Google Cloud assigns that is mainly used internally by Google Cloud to keep track of resources.
- Each project has a unique project ID, which is used to identify the project in the Google Cloud Console and in the API.

### More about Folder Level
- **Goal** : let you assign policies to resources at a level of granularity you choose.
- You can use folders to group projects under an organization in a hierarchy.
- Give teams the ability to delegate administrative rights so that they can work independently.
- **Special roles associated with this top-level organization node :**
    - *Organization policy administrator* : people with privilege can change policies
    - *Project creator role* : control who can create projects and, therefore, who can spend money.

### Google Cloud’s Resource Manager tool
- **Goal :** designed to programmatically help you manage projects.
- **Definition :**
    - API that can gather a list of all the projects associated with an account, create new projects, update existing projects, and delete projects.
    - It can even recover projects that were previously deleted,and can be accessed through the RPC API and the REST API.