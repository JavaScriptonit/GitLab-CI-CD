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

