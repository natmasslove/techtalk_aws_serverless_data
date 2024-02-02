

# EMR Serverless

## About NYC Taxi Ride data set
 - Show in AWS Data Exchange -> Marketplace -> Product catalog -> Taxi
 - 40 Mln rows, 12 files - for each month

## Running EMR Serverless Job
 - Browse to EMR Studio
 - Browse to Application (app id - in cloudformation output)
 - Submit Job Run:
   - Name: csv_to_parquet_20230127
   - Role: role-techtalk-emr-serverless
   - Script location: s3://s3-techtalk-aws-serverless-data/source/emrs/csv_to_parquet.py
   - Arguments: ["s3-techtalk-aws-serverless-data", "nyc_rides_2022_csv/yellow_tripdata_2022-01.csv", "output/emrs/"]
   - Application logs -> upload to s3
     - s3://s3-techtalk-aws-serverless-data/logs

Additional arguments (Job configuration) can be used when needed:            
```json
{
        "sparkSubmitParameters": {
            "spark.hadoop.hive.metastore.client.factory.class": "com.amazonaws.glue.catalog.metastore.AWSGlueDataCatalogHiveClientFactory",
            "spark.executor.instances" : "6",
            "spark.dynamicAllocation.enabled" : "false",
            "spark.executor.cores" : "4",
            "spark.executor.memory" : "16G"
        }
}        
```          

 - Show pySpark script

2. Note state transition and logs (while Job is running):

   PENDING -> SCHEDULED -> RUNNING -> SUCCESS

```log
2023-12-28 16:42:43 - INFO - Processing test item: {
    "type": "emr_serverless",
    "run_name": "emrs_convert_to_parquet_fullyear_2w",
    "script_name": "emrserverless_scripts/csv_to_parquet.py",
    "arguments": [
        "s3-glue-vs-emr-serverless-405389362913",
        "nyc_rides_2022_csv/",
        "output/emrs_convert_to_parquet_fullyear/2w/"
    ],
    "sparkSubmitParameters": {
        "spark.hadoop.hive.metastore.client.factory.class": "com.amazonaws.glue.catalog.metastore.AWSGlueDataCatalogHiveClientFactory",
        "spark.executor.instances": "2",
        "spark.dynamicAllocation.enabled": "false",
        "spark.executor.cores": "4",
        "spark.executor.memory": "16G"
    }
}
2023-12-28 16:42:44 - INFO - PENDING
...
2023-12-28 16:44:07 - INFO - PENDING
2023-12-28 16:44:09 - INFO - State PENDING: 85.247129 seconds
2023-12-28 16:44:09 - INFO - SCHEDULED
...
2023-12-28 16:44:47 - INFO - SCHEDULED
2023-12-28 16:44:50 - INFO - State SCHEDULED: 40.723861 seconds
2023-12-28 16:44:50 - INFO - RUNNING
...
2023-12-28 16:48:05 - INFO - RUNNING
2023-12-28 16:48:07 - INFO - RUNNING
2023-12-28 16:48:09 - INFO - State RUNNING: 199.927597 seconds
2023-12-28 16:48:09 - INFO - SUCCESS
2023-12-28 16:48:14 - INFO - Waiting for totalResourceUtilization to be populated.
2023-12-28 16:48:14 - INFO - Total Running Time: 330.7110 seconds
2023-12-28 16:48:14 - INFO - Output:
{
    "state_durations": {
        "PENDING": 85.247129,
        "SCHEDULED": 40.723861,
        "RUNNING": 199.927597,
        "SUCCESS": 2.002423
    },
    "totalResourceUtilization": {
        "vCPUHour": 0.647,
        "memoryGBHour": 2.799,
        "storageGBHour": 3.233
    },
    "billedResourceUtilization": {},
    "totalExecutionDurationSeconds": 199,
    "dashboard_url": "https://..."
}
``````

3. Result of Job Execution:

  3.1 View logs
  3.2 Resource utilization: consumed and billed.  
    How it's priced
  3.3 Spark UI
