# Infrastructure Preview

# Objectives

# Use Marketplace to build a Jenkins Continuous Integration environment.

# Verify that you can manage the service from the Jenkins UI.

# Administer the service from the Virtual Machine host through SSH.

Step 1 : Use Marketplace to build a deployment

1. on the Navigation menu, click Marketplace.

2. Locate the Jenkins deployment by searching for Jenkins Certified by Bitnami.

3. Launch Jenkins

Step 2 : Examine the deployment

1. Copy the Admin user and Admin password

2. Click Visit the site

3. Click Install suggested plugins, and then click Restart after the installation is complete

Step 3 : Administer the service

1. on the Navigation menu, click Deployment Manager.

2. Click jenkins-1.

3. Click SSH to connect to the Jenkins server.

Step 4 : Shut down and restart the services

1. In the SSH window, shut down all the running services:

   sudo /opt/bitnami/ctlscript.sh stop

2. Restart the service

   sudo /opt/bitnami/ctlscript.sh restart
