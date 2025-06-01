# Jenkins, Sonarqube and Nexus setup and integration with java project

## Instalation

- Clone the repo

```bash
git clone https://github.com/Prabhueswaran/java_sample_webapp.git
```

```bash
cd java_sample_webapp
```

```bash
docker-compose up -d 
```

## Access the applications: 

**Jenkins:** 
  - URL: http://localhost:8080

  - Admin Password: 

    ```docker exec -it jenkins cat /var/jenkins_home/secrets/initialAdminPassword```

**SonarQube:** 
  - URL: http://localhost:9000

  - Default login: admin / admin

**Nexus:** 
  - URL: http://localhost:8081

  - Default login:
  
    ```docker exec -it nexus cat /nexus-data/admin.password```

## Project setup on Jenkins

#### Credentials for Jenkins

- Add SonarQube and Nexus credentials under:

```Jenkins → Manage Jenkins → Credentials → Global → Add Credentials```

### Prerequisites

- SonarQube server running (locally or remote)

- SonarQube token created for authentication

##### Jenkins plugins:

- SonarQube Scanner for Jenkins and Pipeline plugin

- SonarQube Scanner and Java installed on Jenkins agents


#### Configure SonarQube in Jenkins

1. Go to Jenkins → Manage Jenkins → Configure System

2. Scroll to SonarQube servers

3. Click Add SonarQube

    - Name: MySonarQube

    - Server URL: http://sonarqube:9000 (adjust as needed)

    - Add credentials (choose Secret Text and paste your SonarQube token)

4. Under Global Tool Configuration:

   - Find SonarQube Scanner

   - Click Add SonarQube Scanner

   - Name it (e.g., SonarScanner) and install automatically

#### Add Nexus Credentials to Jenkins

1. Go to Jenkins Dashboard → Manage Jenkins → Credentials

   - Add Username/Password credentials for your Nexus login

   - ID: nexus-creds (you’ll use this in Jenkinsfile)


## Create a Pipeline Project

1. Open Jenkins Dashboard (e.g., http://localhost:8080)

2. Click “New Item”

3. Enter a name (e.g., sample-webapp)

4. Select “Pipeline” and click OK

5. Under General:

   - (Optional) Check “GitHub project” and add the repo URL

6. Scroll down to Pipeline section:

   - Definition: Choose Pipeline script from SCM if your Jenkinsfile is in GitHub or Git.
      - Select Git, add your repository URL, and credentials if needed
      - Set Script Path to Jenkinsfile (default)
   - OR choose Pipeline script and paste the Jenkinsfile content directly

7. Click Save

8. Click Build Now to test it