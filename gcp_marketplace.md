## Google Cloud Fundamentals: Getting Started with Cloud Marketplace

Labs Objectives : how to launch a solution using Cloud Marketplace.

# Step 1

1.  GCP Console, on the Navigation menu (Navigation menu), click Marketplace.

2.  In the search bar, type LAMP, click LAMP Certified by Bitnami.

3.  On the LAMP page, click Launch.

4.  Zone, select the deployment zone, leave defaults.

5.  Click Deploy.

# Step 2

1.  When the deployment is complete, click the Site address link in the right pane.

2.  On the GCP Console, under Get started with LAMP Certified by Bitnami, click SSH

3.  In the SSH window, change the current working directory to /opt/bitnami

# cd /opt/bitnami

4.  copy the phpinfo.php script from the installation directory to a publicly accessible location under the web server document root

# sudo sh -c 'echo "<?php phpinfo(); ?>" > apache2/htdocs/phpinfo.php'

5. close the SSH window

# exit
