# Introduction to containers and docker

    Objectives

# Build a Docker image.

# Push a Docker image to Google Cloud Registry.

# Run a Docker container.

Step 1 : Confirm the directory containing the pre-provisioned VM is available.

1. Navigate to VM Instances in compute engine to access the pre-provisioned VM running Ubuntu Xenial and necessary tools pre-installed.

2. On the VM instance, click the SSH drop-down arrow and select open in browser window.

3. Use the "ls /" command to check the filesystem for the "desired directory"

Step 2 : Run the web server

1. Check the "kickstart" directory to confirm the contents of py file.

2. List all the contents with the below command.

   ls - lh

Step 3. Install Dependencies

1. Install latest version of Python and PIP.

   sudo apt-get install -y python3 python3-pip

   Install Tornado library

   pip3 install tornado

2. Run the Python application in the background.

   python3 web-server.py &

3. Ensure that the web server is accessible.

   curl http://localhost:8888

4. Terminate the web server.

   kill %

Step 4 : Package using Docker

1. View the dockerfile

   cat Dockerfile

2. Build a Docker image with the web server.

   sudo docker build -t py-web-server:v1 .

3. Run the web server using Docker.

   sudo docker run -d -p 8888:8888 --name py-web-server -h my-web-server py-web-server:v1

4. stop the container.

   sudo docker rm -f py-web-server

Step 5 : Upload the Image to a Registry

1. Add the signed in user to the Docker group so you can run docker commands without sudo and push the image to the repository as an authenticated user using the Container Registry credential helper.

   sudo usermod -aG docker \$USER

2. Exit the current SSH session .

   exit

3. Create a new SSH session and return to the kickstart directory

   cd /kickstart

4. Store the GCP project name in an environment variable.

   export GCP_PROJECT=`gcloud config list core/project --format='value(core.project)'`

5. Rebuild the Docker image with a tag that includes the registry name gcr.io and the project ID as a prefix.

   docker build -t "gcr.io/\${GCP_PROJECT}/py-web-server:v1" .

Step 6 : Make the Image Publicly Accessible

1. Configure Docker to use gcloud as a Container Registry credential helper

PATH=/usr/lib/google-cloud-sdk/bin:\$PATH
gcloud auth configure-docker

2. Push the image to gcr.io.

   docker push gcr.io/\${GCP_PROJECT}/py-web-server:v1

3. Update ther permissions on Google Cloud Storage to make the image repository publicly accessible.

   gsutil defacl ch -u AllUsers:R gs://artifacts.\${GCP_PROJECT}.appspot.com

   gsutil acl ch -r -u AllUsers:R gs://artifacts.\${GCP_PROJECT}.appspot.com

   gsutil acl ch -u AllUsers:R gs://artifacts.\${GCP_PROJECT}.appspot.com

#

#

#
