

# AWS Redshift

## Cluster Overview

- Show Redshift Serverless console
- Namespace vs Workgroup

## Running query via AWS Console

- Open Query Editor v2
- Run SQLs
```sql
CREATE TABLE rstable1 (id int);

INSERT INTO rstable1 (id) VALUES (5);

SELECT * FROM rstable1
```
## Connecting via DBeaver

- Open Up a DBeaver to show connection

## Notebooks

- facepalm: they are SQL only
- for Data Analysts, I guess
```sql
select table_schema, count(*) from svv_tables group by table_schema order by table_schema
```

## Cloudwatch

- How to check consumption