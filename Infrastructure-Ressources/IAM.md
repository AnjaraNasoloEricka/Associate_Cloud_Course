# Identity and Access Management or IAM

## Goals 

- Administrators can apply policies that define who can do what and on which resources.

## The "Who" part of an IAM Policy

### Definition 
- Also called `principal`.Each principal has its own identifier, usually an email address.

### Types 

It can be a :

- Google Account
- Google Group
- Service Account
- Cloud Identity or Google Workspace domain

## The "Can do what" part of an IAM Policy
### Definition
This part is defined by a `role`. An IAM role is a collection of permissions.

### Example 
To manage virtual machine instances in a project, you must be able `to create, delete, start, stop and change virtual machines.`
So these permissions are grouped into a `role` to make them `easier to understand and easier to manage`.

### Kind of Roles in IAM 
1. **Basic roles** : quite broad in scope (large scope)
    - When applied to a Google Cloud Projet, they affect all resources in that project 
    - Include those roles : 
        - *Owner*: can make changes, access, manage the associated roles and permission, set up billing
        - *Editor* : can access and make changes to a resources
        - *Viewer* : can access resources but can't make any change
        - *Billing administrator* : can access resources and set up billing
2. **Predifined roles** : 
    - Not like Basic Roles, it defines where those roles can be applied (collection of permissions)
    - Example : 
        - **Subject:  Compute Engine (virtual machines as a service)**
        - **Example of predifined roles:**
            - `instanceAdmin` : to compute engine resources in a given project, folder or an entire organization
                - Predifined actions : 
                    - compute.instances.delete
                    - compute.instances.get
                    - compute.instances.list
                    - compute.instances.setMachineType
                    - compute.instances.start
                    - compute.instances.stop
3.  **Custom roles** :     
    - A role that has more specific permissions
    - It uses a `least-privilege` model in which each person in your organization is given the minimal amount of privilege needed to do their job.
    - Example : 
        - To define an `instanceOperator`, you'll need to : 
            - to `allow some users to stop and start Compute Engine virtual machines`, but not reconfigure them.
    - *Note that*: 
        - You’ll need to manage the permissions that define the custom role you’ve created
        - Custom roles can only be applied to either the project level or organization level but not in the Folder Level

## Service account 

> Goal : give permissions to a Compute Engine virtual machine, rather than to a person

### Concept 
- You have an application running in a virtual machine that needs to store data in Cloud Storage, but you don’t want anyone on the internet to have access to that data–just that particular virtual machine.

> You can create a service account to authenticate that VM to Cloud Storage.

### Specification
- Named with an `email adress`
- Instead of passwords they use `cryptographic keys` to access resources.
- So, if a service account has been granted `Compute Engine’s Instance Admin role`, this would allow an application running in a VM with that service account to create, modify, and delete other VMs.
- Service account is like resources, so it can have IAM policies of its own attached to it.
    - Example : 
        - For example, maybe Alice needs to manage which Google accounts can act as service accounts, while Bob just needs to be able to view a list of service accounts.
            - This means that Alice can have the editor role on a service account, and Bob can have the viewer role.

## Cloud Identity 
**Goal** : With a tool called Cloud Identity, organizations can define policies and manage their users and groups using the Google Admin Console.

- Admins can log in and manage Google Cloud resources using the same usernames and passwords they already use in existing Active Directory or LDAP systems.

- Using Cloud Identity also means that when someone leaves an organization, an administrator can use the Google Admin Console to disable their account and remove them from groups.

> Note : access to resources can be limited by folder

## Example of Compute Engine IAM Roles

- **Compute Admin :** Full control of all compute engine resources (compute)

- **Network Admin :** Permissions to create, delete, modify resources except for firewall rules and SSL certificates

- **Storage Admin :** Permissions to create, delete and modify images, snapshots and disks

