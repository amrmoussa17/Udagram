# Aws configuration

## setting up a database using RDS service

1. use rds service to configure a database using postgres database
2. ensure you select a free tier option
3. ensure to make it has public access
4. set up database name and enter your database username and password

## setting up server environment using elasticbeanstalk

- in the project starter code change path to : udagram-api

1. Change main entry in the package.json to be equal server.js
2. in command prompt type `npm run build` to build server code
3. in command prompt type `eb init` and in the prompt specify application name: udagram-api and platform branch NODE.js16
4. after finishing eb configuration .elasticbeanstalk folder is created
5. inside elasticbeanstalk folder, in the config.yml file add artifact which is the deployed source code path using

```
deploy:
  artifact: www/archive
```

6. type `aws configure` and enter your aws credentials
7. in command prompt type `eb create –sample udagram-api-dev` to create a sample app server

## setting up frontend app using s3

- in the project starter code change path to : udagram-frontend

1. in command prompt type `aws s3api create-bucket --bucket udagram-frontend--361250016004 --region us-east-1` to create an s3 bucket for hosting your app
2. in aws console , configure created s3 bucket for web hosting
3. in aws console, configure permissions policy using

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::udagram-frontend-361250016004/*"
        }
    ]
}
```

4. in starter code in path udagram-frontend/src/environments modify code to link your server api to your s3 bucket

```
export const environment = {
  production: true,
  appName: "udagram-api",
  apiHost: "http://udagram-api-dev.eba-wwn4ufd4.us-east-1.elasticbeanstalk.com/api/v0",
};
```
