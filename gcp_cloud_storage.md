## Google Cloud Fundamentals: Getting Started with Cloud Storage and Cloud SQL

Objectives

Create a Cloud Storage bucket and place an image into it.

Create a Cloud SQL instance and configure it.

Connect to the Cloud SQL instance from a web server.

Use the image in the Cloud Storage bucket on a web page.

# Step 1: Deploy a web server VM instance

1. Navigation menu (Navigation menu), click Compute Engine > VM instances

2. Click Create.

3. Create an Instance page, specify a name

4. Specify region and zone.

5. Select machine type.

6. Select boot disk

7. Select the Identity and API access.

8. Click Management, security, disks, networking, sole tenancy to open that section of the dialog.

9. Specify a startup script

apt-get update
apt-get install apache2 php php-mysql -y
service apache2 restart

10. Click create

11. Copy the internal ip and external ip of the bloghost instance.

# Step 2 : Create a Cloud Storage bucket using the gsutil command line

1. click Activate Cloud Shell

2. Use environment variables to store Location.

export LOCATION=US

3.  the DEVSHELL_PROJECT_ID environment variable contains the project ID. The below command contains a bucket named after the project id, as the bucket name must be globally unique.

gsutil mb -l $LOCATION gs://$DEVSHELL_PROJECT_ID

4. To retrieve a banner image from a publicly accessible Cloud Storage location:

gsutil cp image_link image_name

gsutil cp gs://cloud-training/gcpfci/my-excellent-blog.png my-excellent-blog.png

5. Copy the banner image to the newly created Cloud Storage bucket:

gsutil cp my-excellent-blog.png gs://\$DEVSHELL_PROJECT_ID/my-excellent-blog.png

6. Modify the Access Control List of the object

gsutil acl ch -u allUsers:R gs://\$DEVSHELL_PROJECT_ID/my-excellent-blog.png

# Step 3 : Create the Cloud SQL instance

1. on the Navigation menu, click SQL.

2. Click Create instance.

3. Choose a database engine, select MySQL.

4. Select an instance id and enter a root password.

5. Select the specified region and zone.

6. Click create

7. Click the newly created instance, to open it's details page.

8. copy the Public IP address for the SQL instance.

9. Click on Users menu on the left-hand side, and then click ADD USER ACCOUNT.

10. User name, specify username

11. specify a password

12. Click create, this would create the user account in the database.

13. On the connections tab, click Add network.

14. Specify a name

15. The network, should be the external IP address of the bloghost VM instance, followed by /32

35.192.208.2/32

16. Click Done

17. Click save, this would save the configuration change.

# Step 4 : Configure an application in a Compute Engine instance to use Cloud SQL

1. click Compute Engine > VM instances.

2. click SSH in the row for your VM instance

3. change the working directory to the document root of the web server:

4. Use the nano text editor to edit a file:

sudo nano filename

sudo nano index.php

5. In the nano text editor, replace CLOUDSQLIP with the Cloud SQL instance Public IP address and the specified DBPASSWORD.

6. Restart the server :

sudo service apache2 restart

# Step 5 : Configure an application in a Compute Engine instance to use a Cloud Storage object

1. click Storage > Browser.

2. Click on the bucket that is named after the GCP project, copy the public ip.

3. on the ssh session, set the working directory to the document root of the web server.

cd /var/www/html

4. Use the nano editor to edit index.php

sudo nano filename

sudo nano index.php

4. paste the public ip into an image src.

<img src='https://storage.googleapis.com/qwiklabs-gcp-0005e186fa559a09/my-excellent-blog.png'>

5. Exit the editor with ctrl-0 to save, and ctrl-x to exit.

6. restart the web server to see your changes

sudo service apache2 restart
