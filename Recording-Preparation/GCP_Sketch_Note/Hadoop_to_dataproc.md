# Migrating Apache Hadoop to Dataproc

## Key Dataproc features 
Dataproc features include : 
- customizable machines that scale up and down as needed 
- on-demand ephemeral clusters to save cost 
- tight integration with Google Cloud Analytics or other security services 
- support for open source tools in the Hadoop and Spark ecosystem including 30+ OSS tools

## Migration scenario to consider 
1. Are you trying to migrate NoSQL workloads?
    - If you are using **HBase** then check if you need to use co-processors or **SQL with Phoenix**. 
        - **Dataproc** is the best option
    - But if you don’t require a co-processor or SQL
        - **Bigtable** is a good choice.
2. Are you processing streaming data? 
    - If you use **Apache Beam**
        - **Dataflow** is the best option because it's based on Beam SDK 
    - If you use **Spark** or **Kafka**
        - **Dataproc** is a good option
3. Are you doing interactive data analysis or ad hoc querying ?
    - If you are doing interactive data analysis in Spark with interactive notebooks
        - **Dataproc** is great in combination with Jupyter Notebook or Zeppelin. 
    - If instead you are doing data analysis with SQL in Hive or Presto AND want to keep it that way
        - **Dataproc** is a good fit.
    - If you are interested in a managed solution for your interactive data analysis
        - BigQuery is a fully managed data analysis and warehousing solution.

4. Are you doing ETL or batch processing ?
- If you are running ETL or batch processes using MapReduce, Pig, Spark, or Hive.
    - Use **Dataproc**
- If you’re using a workflow orchestration tool such as Apache Airflow or Oozie and want to keep the jobs as they are
    - **Dataproc** is great. However
- If you prefer a managed solution
    - **Cloud Composer**, which is managed by Apache Airflow