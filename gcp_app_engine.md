# Google Cloud Fundamentals: Getting Started with App Engine

# Objectives

# Initialize App Engine.

# Preview an App Engine application running locally in Cloud Shell.

# Deploy an App Engine application, so that others can reach it.

# Disable an App Engine application, when you no longer want it to be visible.

Step 1 : Initialize App Engine

1. Initialize your App Engine app with your project

   gcloud app create --project=\$DEVSHELL_PROJECT_ID

2. Clone the source code repositor

   git clone https://github.com/GoogleCloudPlatform/python-docs-samples

3. Navigate to the source directory:

   cd python-docs-samples/appengine/standard_python3/hello_world

Step 2 : Run Hello World Application locally

1. update the packages list.

   sudo apt-get update

2. Set up a virtual environment

   sudo apt-get install virtualenv

Type Y and Enter

    virtualenv -p python3 venv

4. Activate the virtual environment.

   source venv/bin/activate

5. pip install -r requirements.txt

6. python main.py

Step 3 : Deploy and run Hello World on App Engine

1. Navigate to the source directory:

   cd ~/python-docs-samples/appengine/standard_python3/hello_world

2. Deploy your Hello World application.

   gcloud app deploy

3. Launch your browser to view the app at

   gcloud app browse
