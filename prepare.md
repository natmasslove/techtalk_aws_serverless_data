
## General

1. Create S3 bucket
```bash
aws cloudformation deploy --stack-name cf-techtalk-aws-serverless-data --template-file cloudformation/general.yaml
```

2. Copy NYC rides dataset into your bucket (it works for us-east-1 region)
```bash
aws s3 cp s3://nyc-tlc/opendata_repo/opendata_webconvert/yellow/ s3://s3-techtalk-aws-serverless-data/nyc_rides_2022_csv/ --recursive
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
