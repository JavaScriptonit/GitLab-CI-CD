## Build a real life CI/CD Pipeline for a Node.js application

### Final Pipeline for Node.js Git Project:
* Run Unit Tests
* Run SAST
* Build Docker Image
* Push to Docker Registry
* Deploy to DEV
* Promote to STAGING
* Promote to PROD

### Show reports in GitLab UI (.gitlab-ci.yml):
* use `artifacts:reports:` - to add reports to the Job
* use `junit: app/junit.xml` - to use xml created by jest library
* use `paths: - app/junit.xml` - additional artifact of reports to **DOWNLOAD**
