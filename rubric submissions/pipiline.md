# pipeline docs

1. inside app server-code add a deploy script using

```
b deploy udagram-api-dev --profile default
```

2. inside frontend code add a separate file for deploy script and add the following code

```
aws s3 cp --recursive --acl public-read ./www s3://udagram-frontend-361250016004/

```

3. refer the separate deploy file in the package.json scripts using

```

"deploy": "chmod +x ./bin/deploy.sh && ./bin/deploy.sh"

```

4. in the root folder add scripts to be used in the pipeline in the package.json file

```
"scripts": {
    "frontend:install": "cd udagram-frontend && npm install --force",
    "frontend:build": "cd udagram-frontend && npm run build",
    "frontend:deploy": "cd udagram-frontend && npm run deploy",
    "backend:install": "cd udagram-api && npm install",
    "backend:build": "cd udagram-api && npm run build",
    "backend:deploy": "cd udagram-api && npm run deploy"
  }
```

5. add a config.yml inside .circleci folder to intialize circleci setup

6. configure orbs to include nodejs, aws cli and eb cli

7. add a build job and configure to use a docker container image

8. add steps to build job which includes

- installing dependencies for frontend and backend
- building app for frontend and backend
- deploying app for frontend and backend
