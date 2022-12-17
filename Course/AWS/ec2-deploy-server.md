1. Create UBUNTU instance on AWS
    * [dev-server example i-04b8f1ad800cca49e](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#Instances:)
2. `$ chmod 400 microservice-deployment-server-key.pem`
3. `$ ssh -i ~/Downloads/microservice-deployment-server-key.pem ubuntu@ec2-54-205-13-165.compute-1.amazonaws.com`
4. `$ sudo apt update` - to update the package before installing the tools
5. `$ sudo apt install docker.io` - install Docker on EC2
6. `$ sudo apt  install docker-compose` - install Docker-compose on EC2
7. `$ sudo usermod -aG docker ubuntu` - [Add your user to the docker group](https://docs.docker.com/engine/install/linux-postinstall/)
8. `$ exit` - logout and login again to complete
