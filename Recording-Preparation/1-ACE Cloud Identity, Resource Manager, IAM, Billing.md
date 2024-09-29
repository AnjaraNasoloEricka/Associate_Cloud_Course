# 1- ACE Cloud Identity, Resource Manager, IAM, Billing

## Controlling Access

### 1- Authentification (Cloud Identity)

#### What is Cloud Identity ?

- Cloud Identity is an identity as a service (IDaaS) solution that allows you to centrally manage users,groups and authentification settings who can access GCP `resources`
- Manage identity by LDAP connexion (often)

#### Difference between users and groups

- Users are the individual people who access your GCP resources
- Groups are collections of users that you can manage as a single entity (for example 'dev/admin'). This group has policy.

#### Types of User accounts

1. Consumer users : connect via personal mail. Not recommended by google
2. Organization-managed users :
    - Users with creation and authentification options managed by an organization

#### What Cloud Identity provides ?

- User lifecycle management
- Account security
- Single sign-on
- Cloud directory
- Device management
- Reporting and analytics
- App management
- Extensible through APIs

### 2- Authorization (Cloud IAM)

- IAM : Identity and Access Management
- Lets you manage access control by defining `who (identity)` has `what access (role)` on `which organization node`
- Cloud IAM lets you adopt the security principle of least privilege, so you grant only the necessary access to your resources

#### Cloud Identity members

In Cloud IAM, you grant access to `Cloud Identity members` which can be of following types :

- Google Account
- Service Account : accounts that represent an application or a virtual machine (VM) instead of an individual end user. Created in project and by users or services (GCE, GAE (Google App Engine))
- Google Group
- Google Workspace domain or Cloud Identity Domain

#### IAM Policies

- Check IAM Doc

#### Roles

- Primitive roles (à éviter car donne trop de liberté à l'utilisateur), Custom Roles (créer à partir d'interface ou d'un fichier .yaml), Predifined roles (check IAM and roles doc)

## Resource Manager

- Voir doc (Structure GCP : Resources - Project - Folder - Organization)

## Billing Account

- Used to define `who pays for a given set of resources`
- Many project can owned `one billing account`
- Billing account includes a `payment instrument` to which costs are charged and `access control` that is established by Cloud IAM roles
- There are **2 types** of billing account :
    - `Self-serve` : created online, credit or debit card or ACH direct debit
    - `Invoiced` : offline, check or wire transfer
- Resource consumption is measured on :
    - Rate of use/time
    - Number of items
    - Feature use

## Administrative tools

- Google Cloud SDK
- Cloud Console & Shell
- Restful APIs
- Mobile App