**IAM Keys for Deployment**

You can use the same IAM User's access and secret keys from the single container app we created earlier, 
or, you can create a new IAM user for this application:

Search for the "IAM Security, Identity & Compliance Service"

Click "Create Individual IAM Users" and click "Manage Users"

Click "Add User"

Enter any name you’d like in the "User Name" field.

eg: docker-multi-travis-ci

Tick the "Programmatic Access" checkbox

Click "Next:Permissions"

Click "Attach Existing Policies Directly"

Search for "beanstalk"

Tick the box next to "AdministratorAccess-AWSElasticBeanstalk"

Click "Next:Tags"

Click "Next:Review"

Click "Create user"

Copy and / or download the Access Key ID and Secret Access Key to use in the Travis Variable Setup.