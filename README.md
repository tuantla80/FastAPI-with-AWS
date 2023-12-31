## 1. Overview  
### Managers:  
- To handle the business logic
- To communicate with DB
- To tranform data and add it to DB and pass the result
### Models  
- To structure tables in DB
- To define schema for the objects
### Resources (Routes)  
- To create endpoints of the app
- To define behavior on GET, POST, PUT, DELETE for different routes
- To communiocate with managers to achieve its purpose
### Schemas  
- To validate data and structures of request and response objects using pydantic
### Services  
- To communicate with third party apps.
- In this project: AWS S3, AWS SES (Simple Email Service) and Wise payment service.
### Utils  
- To include helper functions used in the app.
## 2. Authentication and Authorization  
### JWT (JSON Web Token)  
- Transmiting client <--> server in a stateless and secure way.
- 3 parts seperately by a dot (*******.********.*********)
  - Header: algo (eg. HS256) and type
  - Payload: data
  - Signature: encode content of header and payload to a secret string
### Custom HTTPBearer  
### Add role to user model  
## 3. AWS S3 Service  
### Create a bucket on S3  
### Connect with AWS service using boto3 library  
- Get credentials: Access key ID and Secret access key
### Upload user's images to S3  
## 4. AWS SES (Simple Email Service)  
- Create ses.py to send email after approving or rejecting is completed.
- Modified managers.py to get email of approver and complainers.
## 5. Wise payment  
- Step 0: Get your profile
- Step 1: Create a quote
- Step 2: Create a recipient account
- Step 3: Create a transfer
- Step 4: Fund a transfer or cancel transfer 
## 6. Database Migration Tool
### Alembic  
### 7. Code Coverage and Quality  
#### Code Coverage  
```
- Install pytest-cov
- Configure the coverage reports in a .coveragerc file as below:
  [run]
  omit = tests/*
  branch = True
- Update the container:
  $ docker-compose up -d --build
- Run the tests with coverage
  $ docker-compose exec web python -m pytest --cov="."
  Want to view an HTML version
  $ docker-compose exec web python -m pytest --cov="." --cov-report html
```
#### Code Quality  
##### Flake8  
```
- Checking code for stylistic or programming errors
 Flake8 combines two popular linters -- pep8 and pyflakes
- Install flake8
- To configure Flake8, add a setup.cfg (or .flake.8) file to the "project" directory
  [flake8]
  max-line-length = 119
  exclude =
      migrations
      __pycache__
      manage.py
      settings.py
      env
      .env
- Update the containers
  $ docker-compose up -d --build
- Run Flake8:
  $ docker-compose exec web flake8 .
```
##### Black 
```
Black is a PEP 8 compliant opinionated formatter.
- Install black
- Update the containers:
  $ docker-compose up -d --build
- Run Black
  $ docker-compose exec web black . --check --exclude "env"
- Running it with the diff option
  $ docker-compose exec web black . --diff --exclude "env"
```
##### isort  
```
To quickly sort all imports alphabetically and automatically separate them into sections.
- Install isort
- Update the containers:
  $ docker-compose up -d --build
- Run isort
  $ docker-compose exec web isort . --check-only --skip "env"
  $ docker-compose exec web isort . --diff --skip "env"
  Apply changes
  $ docker-compose exec web isort .
```
##### Verify one last time that Flake8, Black, and isort all pass  
```
$ docker-compose exec web flake8 .
$ docker-compose exec web black . --check
$ docker-compose exec web isort . --check-only
```
### 8. Continuous Integration (CI) with GitHub Actions  
#### GitHub Packages  


