## Google Cloud Fundamentals: Getting Started with Compute Engine

Labs Objectives :

1.  Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console

2.  Create a Compute Engine virtual machine using the gcloud command-line interface.

3.  Connect between the two instances.

# Step 1

1.  Click Compute Engine > VM instances.

2.  Click Create.

3.  Specify desired name

4.  For Region and Zone, select the region and zone specified.

5.  Accept the default machine type.

6.  Select the boot disk

7.  Choose desired parameters for identity and API access.

8.  Specify the nature of the traffic allowed. HTTP or HTTPS.

9.  In the search bar, type LAMP, click LAMP Certified by Bitnami.

10. On the LAMP page, click Launch.

11. Zone, select the deployment zone, leave defaults.

12. Click Deploy.

# Step 2 Creating a virtual machine using the gcloud command line

1.  In the toolbar, click the cloud shell button.

2.  To display a list of all zones in the regions.

gcloud compute zones list | grep region

gcloud compute zones list | grep us-central1

3. To change the previous zone :

gcloud config set compute/zone zone

gcloud config set compute/zone us-centra1-b

4. To create a new instance from the command line

gcloud compute instances create "name" \ -- machine-type "machine_type" \ --image-project "image_project" \ --image "image_specified" \ --subnet "default"

gcloud compute instances create "my-vm-2" \
--machine-type "n1-standard-1" \
--image-project "debian-cloud" \
--image "debian-9-stretch-v20190213" \
--subnet "default"

# Step 3 : Connect between VM instances

1. open a command prompt on the newly created instance, click SSH in its row in the VM instances list.

2. se the ping command to confirm that my-vm-2 can reach my-vm-1 over the network:

ping my-vm-1

3. Use the ssh command to open a command prompt on my-vm-1:

ssh my-vm-1

4. use the command prompt on my-vm-1, install an Nginx web server:

sudo apt-get install [package] -y

sudo apt-get install nginx-light -y

5. Use the nano text editor to add a custom message to the home page of the web server:

sudo nano /var/path/filename.html

sudo nano /var/www/html/index.nginx-debian.html

6. Press Ctrl+O and then press Enter to save your edited file, and then press Ctrl+X to exit the nano text editor.

7. Confirm that the web server is serving a new page.

curl http://localhost/

8. click exit on the command line to exit the my-vm-1

exit

9. confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2,

curl http://instance_name/

curl http://my-vm-1/

2.  On the GCP Console, under Get started with LAMP Certified by Bitnami, click SSH

3.  In the SSH window, change the current working directory to /opt/bitnami

# cd /opt/bitnami

4.  copy the phpinfo.php script from the installation directory to a publicly accessible location under the web server document root

# sudo sh -c 'echo "<?php phpinfo(); ?>" > apache2/htdocs/phpinfo.php'

5. close the SSH window

# exit
