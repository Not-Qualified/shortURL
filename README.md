
## Implementation of URL Shortner with AWS Serverless Architecture

This repository contains code for creating short url generator with AWS Lambda and PostgresQL as database

[Live Code ](https://quwsootxp7c2yorf4ft6v3wpte0kjbsj.lambda-url.ap-south-1.on.aws) - `https://quwsootxp7c2yorf4ft6v3wpte0kjbsj.lambda-url.ap-south-1.on.aws/`


#### Deployment Steps:

1: Create AWS Lambda Function with `python 3.9` runtime with function url enabled

2: Download [lambdaZip](https://d32r8fal0p61y.cloudfront.net/shortURL.zip) and import code into your lambda function

3: Create environment variable in lambda as follows:
```
DB_HOST = <db_host>
DB_NAME = <db_name>
DB_PASSWORD = <db_password>
DB_PORT = <db_port>
DB_USER = <db_user>
LAMBDA_URL = <lambda_url>
```

4: Attach Lambda Layer using below ARN: ( This will only work for ap-south-1 region ) - refer - [KLayers](https://github.com/keithrozario/Klayers/tree/master/deployments/python3.9) for your region's layer ARN
```
jinja2 - arn:aws:lambda:ap-south-1:770693421928:layer:Klayers-p39-jinja2:4
psycopg2-binary - arn:aws:lambda:ap-south-1:770693421928:layer:Klayers-p39-psycopg2-binary:1
```
`Jinja for template render`

`psycopg2 for PostgresQL Connection`

5: In your database, create `kLinks` table as follows with SQL:
```
CREATE TABLE kLinks (
    original text NOT NULL,
    short text NOT NULL,
    PRIMARY KEY (original, short)
);
```

6: Make sure that your database is reachable using lambda and make sure your lambda function url is also public with no authenticaion, unless you are intention is doing so with authenticaion
