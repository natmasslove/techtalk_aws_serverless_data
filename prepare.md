
## General

1. Create S3 bucket
```bash
aws cloudformation deploy --stack-name cf-techtalk-aws-serverless-data --template-file cloudformation/general.yaml
```

2. Copy NYC rides dataset into your bucket (it works for us-east-1 region)
```bash
aws s3 cp s3://nyc-tlc/opendata_repo/opendata_webconvert/yellow/ s3://s3-techtalk-aws-serverless-data/nyc_rides_2022_csv/ --recursive
```

## Redshift

1. Deploy all resources:

```bash
aws cloudformation deploy --stack-name cf-techtalk-aws-serverless-redshift --template-file cloudformation/redshift.yaml --capabilities CAPABILITY_NAMED_IAM
```

2. Go to UI Console -> Redshift Query Editor v2

3. Run SQL statements:

```sql
CREATE TABLE rstable1 (id int);

INSERT INTO rstable1 (id) VALUES (5);
```


## Glue 

1. Deploy all resources:

```bash
aws cloudformation deploy --stack-name cf-techtalk-aws-serverless-glue --template-file cloudformation/glue.yaml --capabilities CAPABILITY_NAMED_IAM
```

2. copy Glue script into S3
```
aws s3 cp source/glue/csv_to_parquet.py s3://s3-techtalk-aws-serverless-data/source/glue/
```

## EMR Serverless

1. Deploy all resources:

```bash
aws cloudformation deploy --stack-name cf-techtalk-aws-serverless-emrs --template-file cloudformation/emr_serverless.yaml --capabilities CAPABILITY_NAMED_IAM
```

2. copy EMR Serverless script into S3
```
aws s3 cp source/emrs/csv_to_parquet.py s3://s3-techtalk-aws-serverless-data/source/emrs/
```

## Athena

1. Deploy all resources:

```bash
aws cloudformation deploy --stack-name cf-techtalk-aws-serverless-athena --template-file cloudformation/athena.yaml --capabilities CAPABILITY_NAMED_IAM
```
