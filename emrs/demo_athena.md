

# AWS Athena - SQL Query

## Running SQL Query

- Browse to AWS Athena -> Query Editor
- Choose Workgroup: athenawg-techtalk
- Run SQL + Collect "Data Scanned Info"
```sql
SELECT trip_month, count(*) 
  FROM (
        SELECT date_trunc('month', date_parse(tpep_pickup_datetime,'%Y-%m-%d %k:%i:%s')) as trip_month
          FROM "db-techtalk"."techtalk-nyc-taxi-csv" 
       ) 
 GROUP BY  trip_month 
 ORDER BY  trip_month; 
```
## Running Spark Code

- Browse to AWS Athena -> Notebook Editor
- Choose Workgroup: athenawg-techtalk-spark
- Create Notebook **showing Options**
- Cell 1
```python
s3_bucket_name = "s3-techtalk-aws-serverless-data"
input_path = "nyc_rides_2022_csv/yellow_tripdata_2022-01.csv"
output_path = "output/athena_spark/"
```
- Cell 2
```python
from pyspark.sql.types import StructType, StructField, StringType, IntegerType, DoubleType, TimestampType

schema = StructType([
    StructField("VendorID", IntegerType()),
    StructField("tpep_pickup_datetime", TimestampType()),
    StructField("tpep_dropoff_datetime", TimestampType()),
    StructField("passenger_count", IntegerType()),
    StructField("trip_distance", DoubleType()),
    StructField("RatecodeID", IntegerType()),
    StructField("store_and_fwd_flag", StringType()),
    StructField("PULocationID", IntegerType()),
    StructField("DOLocationID", IntegerType()),
    StructField("payment_type", IntegerType()),
    StructField("fare_amount", DoubleType())
])

# Input and output paths
full_input_path = f"s3://{s3_bucket_name}/{input_path}"
full_output_path = f"s3://{s3_bucket_name}/{output_path}"
```
- Cell 3 (we already have spark session initialized)
```python
print(f'Reading CSV file from {full_input_path}')
df = spark.read.csv(full_input_path, header=True, schema=schema)

print(f'Writing data to {full_output_path}')
df.write.mode("overwrite").parquet(full_output_path)

print('Done')
```
- Show output
- Terminate session