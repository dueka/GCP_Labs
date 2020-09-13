# Google Cloud Fundamentals: Getting Started with Deployment Manager and Cloud Monitoring

Objectives

# Create a Deployment Manager deployment.

# Update a Deployment Manager deployment.

# View the load on a VM instance using Cloud Monitoring.

Step 1 : Confirm that needed APIs are enabled

1. Click APIs & services.

2. Scroll down the list and confirm that the necessary APIs are enabled.

   Cloud Deployment Manager v2 API

   Cloud Runtime Configuration API

   Cloud Monitoring API

Step 2 : Create a Deployment Manager deployment

1. Open Cloud shell.

2. Using Cloud Shell, download an editable Deployment Manager template:

   gsutil cp gs://cloud-training/gcpfcoreinfra/mydeploy.yaml mydeploy.yaml

3. use the sed command to replace the PROJECT_ID placeholder string with your Google Cloud Platform project ID

   sed -i -e "s/PROJECT_ID/\$DEVSHELL_PROJECT_ID/" mydeploy.yaml

4. use the sed command to replace the ZONE placeholder string with your Google Cloud Platform zone

   sed -i -e "s/ZONE/\$MY_ZONE/" mydeploy.yaml

5. Build a deployment from the template:

   gcloud deployment-manager deployments create my-first-depl --config mydeploy.yaml

Step 2 : Update a deployment manager deployment

1. edit the mydeploy.yaml file:

   nano mydeploy.yaml

2. Add more functions to the script;

   value: "apt-get update; apt-get install nginx-light -y"

3. deploy the new startup script:
   gcloud deployment-manager deployments update my-first-depl --config mydeploy.yaml

Step 3 : View the Load on a VM using Cloud Monitoring

1. Navigate to VM instances.

2. start the SSH.

3. create a CPU load:

   dd if=/dev/urandom | gzip -9 >> /dev/null &
