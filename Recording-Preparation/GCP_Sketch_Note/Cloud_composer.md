# Cloud Composer 

## What is Cloud Composer ? 
- A fully managed workflow orchestration built on **Apache Airflow** that helps you author,schedule, monitor pipelines spanning hybrid and multi-cloud environments.

## Apache Airflow  ? 
### What is Apache Airflow ?
- An open-source platform for developing, scheduling, and monitoring batch-oriented workflows
- If your workflows have a clear start and end, and run at regular intervals, they can be programmed as an `Airflow DAG`.

> Note : a DAG represents a workflow, a collection of tasks 

### Difference between ETL (Extract, transform, and load) and ELT (Extract, load, and transform)
- **ETL approach :** uses a set of business rules to process data from several sources before centralized integration
- **ELT approach :** loads data as it is and transforms it at a later stage, depending on the use case and analytics requirements

## Security features 
- **Private IP**
- **Private IP + Web server ACLs**
- **VPC Native Mode** 
- **VPC Service Controls**
- **Custom Managed Encryption Keys**
- **Restricting Identities By Domain**
- **Integration with secret manager**
