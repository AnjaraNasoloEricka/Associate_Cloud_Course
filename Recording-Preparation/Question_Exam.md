# Question Exam 

- Autorisation et permission (Cloud IAM) - IAM Policies
    - Que se passe t'il si j'ai cette autorisation ?
- Entrainement LAB
- A revoir : produits Google on Compute
- Type de disques (storage) surtout pour le cas du local persistent disk et local SSD
- Cloud storage
- Choix base de données
- Enoncé avec MySQL, PostgreSQL & SQL Server : penser à cloud SQL
- Mobile & Document database : penser à Firestore
- Identity Aware Proxy ??
- Analytics : think about BigQuery
- **Hadoop** : penser à datastore ou dataproc. **HBase** : Dataproc
- Pub/Sub -> Dataflow -> BigTable
- Toujours choisir les produits googles
- Best pratices on database
- Exam sample :
    - https://docs.google.com/forms/d/e/1FAIpQLSfexWKtXT2OSFJ-obA4iT3GmzgiOCGvjrT9OfxilWC1yPtmfQ/viewscore?viewscore=AE0zAgDFKj8HVyID67yOyLDg_0cFETXcIQBu9jiY4oDr-aFEmUfmzUf12DSq0eZIAwf1Ras
    - https://www.examtopics.com/exams/google/associate-cloud-engineer/view/

- Other documentations :
    - https://cloud.google.com/compute/docs/instances/adding-removing-ssh-keys
    - https://cloud.google.com/appengine/docs/standard/python/how-instances-are-managed
    - https://cloud.google.com/sdk/gcloud/reference/iam/roles/copy
    - https://cloud.google.com/compute/docs/instances/
    - https://cloud.google.com/bigquery/docs/estimate-costs
    - https://cloud.google.com/solutions/correlating-time-series-dataflow
    - https://cloud.google.com/storage/docs/lifecycle
    

- Learn more about Networking
    - Subnets range
    - VPC
    - Alias IP ranges

- Tag (all about network), label (for searching resources and billing)

- Shared VPC : communicate through internal IP address

- Cloud Load Balancing

- GKE (view the doc in certified-gcp-cloud-engineer)

- Cloud SQL does not support user-defined functions, which are
used in the database being migrated.

- Routing between pods in GKE can be accomplished using alias IPs
or Google Cloud Routes.

- `--trigger-event google.storage.object.finalize` : to analyze and act on files being
added to a Cloud Storage bucket

- Cloud storage Object Lifecycle Management :
    - https://storage.googleapis.com/cloud-training/gcpace/2.0/en/on-demand/Preparing_for_ACE_Module_4_v2.0.pdf : page 54

- gcloud command

- Load data in bigQuery :
    -  BigQuery Data Transfer Service in this [link](/Recording-Preparation/3-ACE%20Storage%20&%20Databases.md)

- Implementing resources via infrastructure as a code :
    - Building infrastructure via Cloud Foundation Toolkit (include Terraform for template deployment) templates and implementing best practices
    - Installing and configuring Config Connector in GKE to
create, update, delete, and secure resources

- Terraform lifecycle :
    1. terraform init : downloads latest version of Terraform provider
    2. terraform plan : verifies syntax, ensures supporting files exist, shows a
        preview of resources that will be created
    3. terraform apply : sets up requested resources output by the Terraform plan
    4. destroy all resources in the specified config file

- Upgrading manage instance group :
    - Command line :
        ```bash
            gcloud compute instance-groups managed
            rolling-action start_update cymball_supplychain_ig \
            --version=template=cymball_supplychain_ig_templat
            e_<yymmdd> \
            --type=proactive\
            --region=us-central1
        ```
    - Why upgrading ?
        - Updating the operating system of your instances.
        - Conducting A/B or canary testing of capability upgrades.
        - Changing the disk type or attached disks attached to your instances.

- Create a permanent table in BigQuery
    ```bash
        bq mk --external_table_definition=cymbal_trans_mngt_bt_def /
        cymbal_data_set.trans_mngt_ext_tbl
    ```

- Managed instance group :
    - Health check
    - Number of instances

- Steps for implementing an Instance group :
    - Create instance template for example identify machine type and boot disk
    - Configure your instance group for example number of instances and autoscaling settings

- In Cloud Monitoring you implement alerts by defining **alert policies**. An alerting policy specifies what you want to be alerted on and how you want to be notified. The “what”
is made of conditions that describe the state of a resource, or groups of resources,
that cause you to take action