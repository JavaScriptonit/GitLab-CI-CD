1. Create UBUNTU instance on AWS
   * [dev-server example i-04b8f1ad800cca49e](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#Instances:)
2. `$ chmod 400 dev-server-key.pem`
3. `$ ssh -i ~/Downloads/dev-server-key.pem ubuntu@ec2-54-91-111-16.compute-1.amazonaws.com`
4. `$ sudo apt update` - to update the package before installing the tools
5. `$ sudo apt install docker.io` - install Docker on EC2
6. `$ sudo usermod -aG docker ubuntu` - [Add your user to the docker group](https://docs.docker.com/engine/install/linux-postinstall/)
7. `$ exit` - logout and login again to complete
8. `$ cat ~/Downloads/dev-server-key.pem` - print the value of the SSH_KEY
9. add variable in "Settings -> CI/CD -> Variables -> Add variable":
   * `SSH_PRIVATE_KEY`
   * `$ cat ~/Downloads/dev-server-key.pem`
   * Type: `File`
   * Flags: `Protect variable`
10. Add deploy stage in Pipeline
11. Create new job
12. Add script in that job, script: `- ssh -o StrictHostKeyChecking=no -i $SSH_PRIVATE_KEY ubuntu@$DEV_SERVER_HOST "
    docker login -u $CI_REGISTRY_USER -p $CI_REGISTRY_PASSWORD $CI_REGISTRY &&
    docker run -d -p 3000:3000 $IMAGE_NAME:$IMAGE_TAG"`
    * StrictHostKeyChecking=no is a skip for a Check: "YES/NO"
13. Add security groups new rule with port 3000 to access this instance
14. Open Public IPv4 address:3000 or Public IPv4 DNS:3000
    * `http://54.91.111.16:3000/`
    * `http://ec2-54-91-111-16.compute-1.amazonaws.com:3000/`
15. Add environment to deploy stage
    * `name: development` - name of environment
    * `url: $DEV_ENDPOINT` - http://ec2-54-165-186-129.compute-1.amazonaws.com:3000
    * GitLab provides a full history of deployments of each env
    * You always know what is deployed on servers
    * [GitLab environments URL](https://gitlab.com/JavaScriptonit/mynodeapp-cicd-project/-/environments)
16. Create docker-compose.yaml:
    * `version: "3.3"` - latest version of docker-compose
    * `services: app:` - list of services
    * `image: registry.gitlab.com/javascriptonit/mynodeapp-cicd-project:1.2` - latest image
    * `ports: - 3000:3000` - host port and container port
17. Update .gitlab-ci.yaml:
    * add script commands for using dc file and running it:
      * `- scp -o StrictHostKeyChecking=no -i $SSH_PRIVATE_KEY ./docker-compose.yaml ubuntu@$DEV_SERVER_HOST:/home/ubuntu` - to copy docker-compose file from gitlab runner to dev-server
      * `docker-compose -f docker-compose.yaml down` - stop running images
      * `docker-compose -f docker-compose.yaml up -d"` - run new image after commit
    * add script command for versioning:
      * `cat app/package.json | jq -r .version` - get version value from package.json object
      * `- export PACKAGE_JSON_VERSION=$(cat app/package.json | jq -r .version)` - full command with saving version variable
      * `- export VERSION=$PACKAGE_JSON_VERSION.$CI_PIPELINE_IID` - change 3 patch numbers to variable every build
    * install jq on gitlab runner (to get value from object):
      * `ssh -i ~/Downloads/gitlab-runner-key.pem ubuntu@ec2-54-208-34-176.compute-1.amazonaws.com` - login
      * `sudo apt-get install jq` - install

