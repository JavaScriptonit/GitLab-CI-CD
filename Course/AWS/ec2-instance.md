## [AWS Configuration Cheat Sheet](https://github.com/JavaScriptonit/myselfRep/blob/main/Docker/Courses/Docker%20and%20Kubernetes:%20The%20Complete%20Guide/lesson-11.md)
### EC2 Connect steps: 
* In AWS, navigate to Services > EC2.
* Under Resources, select Running Instances.
* Highlight your instance and click Connect.
* In Terminal, cd into the directory containing your key and copy the command in step 3 under "To access your instance."
* In Terminal, run: ssh -vvv -i [MyEC2Key].pem ec2-user@xx.xx.xx.xx(xx.xx.xx.xx = your EC2 Public IP) OR run the command in the example under step 4.

### debugging steps to EC2 connection time out:
* Double-check the security group access for port 22
* Make sure you have your current IP on there and update to be sure it hasn't changed
* Make sure the key pair you're attempting to use corresponds to the one attached to your EC2
* Make sure your key pair on your local machine is chmod'ed correctly. I believe it's chmod 600 keypair.pem check this
  * `$ chmod 400 gitlab-runner-key.pem`
  * `$ ssh -i ~/Downloads/gitlab-runner-key.pem ubuntu@ec2-44-203-114-204.compute-1.amazonaws.com`
* Make sure you're in either your .ssh folder on your host OR correctly referencing it: HOME/.ssh/key.pem
* Last weird totally wishy-washy checks:
  * reboot instance
  * assign elastic IP and access that
  * switch from using the IP to Public DNS
  * add a : at the end of user@ip:
