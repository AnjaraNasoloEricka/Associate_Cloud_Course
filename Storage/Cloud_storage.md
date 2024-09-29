# Cloud Storage

## What is Cloud Storage ? 
A service that offers developers and IT organizations durable and highly available `object storage`.

- Google’s object storage product
- It allows customers to store any amount of data, and to retrieve it as often as needed.
- It’s a fully managed scalable service that has a wide variety of uses
- The storage objects offered by Cloud Storage are immutable, which means that you do not edit them, but instead a new version is created with every change made. Administrators have the option to either allow each new version to completely overwrite the older one, or to keep track of each change made to a particular object by enabling “versioning” within a bucket

### What is object storage ? 
Object storage is a computer data storage architecture that manages data as “objects” and not as a file and folder hierarchy (file storage), or as chunks of a disk (block storage).

These objects are stored in a packaged format which contains the binary form of the actual data itself, as well as relevant associated meta-data (such as date created, author, resource type, and permissions), and a globally `unique identifier`.

These unique keys are in the `form of URLs`, which means `object storage interacts well with web technologies`.

## Why do we need Cloud Storage ? 
- Cloud Storage’s primary use is whenever `binary large-object storage` (also known as a “BLOB”) is needed for :
    - Online content
    - Backup and archiving
    - Storage and immediate result

## Cloud storage file organization 
- Organized into buckets 
    - A bucket needs a globally unique name and a specific geographic location for where it should be stored, and an ideal location for a bucket is where latency is minimized.

## How to control user access to objects and buckets?
1. For most purposes, `IAM is sufficient` : Roles are inherited from project to bucket to object.
2. If you need finer control, you can create `access control lists`
    - Each access control list consists of `two pieces of information`: 
        1. **scope :** defines who can access and perform an action
        2. **permission :**  defines what actions can be performed, like read or write.

> NB : Cloud storage has also `Lifecycle policies` for example to delete objects older than 365 days; or to delete objects created before January, 1, 2013; or to keep only the 3 most recent versions of each object in a bucket that has versioning enabled.

## Storage classes 

### Type of storage classes
There are 4 types of storage classes : 

#### 1. Standard Storage
- considered best for `frequently accessed`, or `hot data`
-  data that’s stored for only brief periods of time

#### 2. Nearline Storage
- best for storing infrequently accessed data, like reading or modifying data on average `once a month or less`
- **Examples :** data backups, long-tail multimedia content, or data archiving

#### 3. Coldline Storage
- low-cost option for storing infrequently accessed data
- is meant for reading or modifying data, at most, `once every 90 days`

#### 4. Archive Storage
- lowest-cost option, used ideally for data archiving, online backup, and disaster recovery
- data access and operations and a `365-day minimum storage duration`

### Features
- unlimited storage with no minimum object size requirement
- worldwide accessibility and locations
- low latency and high durability
- uniform experience which extends to security, tools, and APIs
- geo-redundancy if data is stored in a multi-region or dual-region
- **Autoclass**
    - which automatically `transitions objects to appropriate storage classes `based on each object's access pattern
    -  moves data that is not accessed to colder storage classes to reduce storage cost 
    - moves data that is accessed to Standard storage to optimize future accesses
- security perspective : Cloud Storage always encrypts data on the server side, before it’s written to disk, at no additional charge and Data traveling between a customer’s device and Google is encrypted by default using HTTPS/TLS, which is Transport Layer Security.

### Billing 
- Pay for what you use
- No prior provisioning of capacity

### Ways to bring data into Cloud Storage
- **Online Transfer**
    - gcloud storage
    - Cloud Console
- **Storage Transfer Service** 
    - use **Storage Transfer Service** which enables you to import large amounts of online data into Cloud Storage quickly and cost-effectively
    -  Storage Transfer Service lets you schedule and manage batch transfers to Cloud Storage from another cloud provider, from a different Cloud Storage region, or from an HTTP(S) endpoint.
- **Transfer Appliance**
    -  is a rackable, high-capacity storage server that you lease from Google Cloud
    - You connect it to your network, load it with data, and then ship it to an upload facility where the data is uploaded to Cloud Storage
    - You can transfer up to a petabyte of data on a single appliance

## ACL (Access Control List)
An ACL is a mechanism you use to define who has access to your buckets and objects, as well as what the level of access is they have.

Each ACL consists of one or more entries, and these entries consist of two pieces of information :

- **Scope :** which defines who can perform the specified actions (for example, a specific user or group of users)
- **Permission :**  which defines what actions can be performed (for example, read or write)

### ACL Setup
- To set the access list to private and verify the results, run the following commands:

```bash
gsutil acl set private gs://$BUCKET_NAME_1/setup.html
gsutil acl get gs://$BUCKET_NAME_1/setup.html  > acl2.txt
cat acl2.txt
```

- To update the access list to make the file publicly readable, run the following commands

```bash
gsutil acl ch -u AllUsers:R gs://$BUCKET_NAME_1/setup.html
gsutil acl get gs://$BUCKET_NAME_1/setup.html  > acl3.txt
cat acl3.txt
```


## Other features

### Object versioning :

Once enabled, Cloud Storage creates an archived version of an object each time the live version of the object is overwritten or deleted (using soft delete).

#### How to enable versioning :
- `gsutil versioning get gs://$BUCKET_NAME_1`
- To enable versioning feature, you can run : `gsutil versioning set on gs://$BUCKET_NAME_1`
- To list all versions of one file in cloud storage : `gcloud storage ls -a gs://$BUCKET_NAME_1/setup.html`

### Object Lifecycle Management :

- Assign a lifecycle management configuration to a bucket
- Object inspection occurs in asynchronous batches, so rules may not be applied immediately
- Change can take 24 hours to apply
- Example of use cases :
    - Downgrade the storage class of objects older than a year to Coldline Storage
    - Delete objects created before a specific date
    - Keep only the 3 most recent versions of each object in a bucket with versioning enabled

#### How to enable lifecycle management
- `gsutil lifecycle get gs://$BUCKET_NAME_1`
- create a `life.json` file :
    ```json
    {
        "rule":
            [
                {
                    "action": {"type": "Delete"},
                    "condition": {"age": 31}
                }
            ]
    }
    ```

- `gsutil lifecycle set life.json gs://$BUCKET_NAME_1`

### Object Retention Lock :

- Lets you set retention configuration on objects within Cloud Storage buckets that have enabled the feature
- Retention configuration governs how long the object must be retained
- Helps you meet data retention regulatory and compliance requirements, such as those associated with FINRA, SEC, and CFTC

### Data import services :

- **Data transfer Appliance :**  a hardware appliance you can use to securely migrate large volumes of data (from hundreds of terabytes up to 1 petabyte) to Google Cloud without disrupting business operations
- **Storage Transfer Service :**  enables high-performance imports of online data. That data source can be another Cloud Storage bucket, an Amazon S3 bucket, or an HTTP/HTTPS location
- **Offline Media Import :** a third party service where physical media (such as storage arrays, hard disk drives, tapes, and USB flash drives) is sent to a provider who uploads the data

