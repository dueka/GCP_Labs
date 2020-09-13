# Console and Cloud Shell

Objectives

# Get access to Google Cloud.

# Create a Cloud Storage bucket using the Cloud Console.

# Create a Cloud Storage bucket using Cloud Shell.

# Become familiar with Cloud Shell features.

Step 1 : Create a bucket using the Cloud Console

1. In the Cloud Console. click Storage > Browser.

2. Click Create bucket.

3. type a globally unique bucket name

4. Click Create.

Step 2 : Access Cloud Shell

1. In the cloud menu, activate Cloud Shell, on the prompt, click Continue.

Step 3 : Create a bucket using Cloud Shell

1. In Cloud shell, Create a bucket.
   gsutil mb gs://<BUCKET_NAME>

Step 4 : Upload a file to Cloud shell

1. Copy the file into one of the buckets

   gsutil cp [MY_FILE] gs://[BUCKET_NAME]

   gsutil cp cloudbank gs://storage*bucket*!

Step 5 : Create a persistent state in Cloud Shell

1. Open Cloud Shell from the Cloud Console.

2. list available regions

   gcloud compute regions list

3. Create an environment variable and replace [YOUR_REGION]

   INFRACLASS_REGION=[YOUR_REGION]

   INFRACLASS_REGION=us-central-1

4. Verify it with echo:

   echo \$INFRACLASS_REGION

5. Append the environment variable to a file

# Create a subdirectory for materials

    mkdir directory

    mkdir infraclass

# Create a file called config

    touch infraclass/config

# Append the value of the Region environment variable to the config file:

    echo INFRACLASS_REGION=$INFRACLASS_REGION >> ~/infraclass/config

# Create a second environment variable for the Project ID

    INFRACLASS_PROJECT_ID=[YOUR_PROJECT_ID]

# Append the value of your Project ID environment variable to the config file:

    echo INFRACLASS_PROJECT_ID=$INFRACLASS_PROJECT_ID >> ~/infraclass/config

# Use the source command to set the environment variables

    source infraclass/config

echo \$INFRACLASS_PROJECT_ID

Step 6 : Modify the bash profile and create persistence

1. Edit the shell profile

   nano .profile

2. Add the following line

# source infraclass/config
