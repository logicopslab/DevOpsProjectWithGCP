# DevOpsProjectWithGCP

In this project, you will build a continuous integration pipeline using Cloud Source Repositories, Cloud Build, build triggers, and Container Registry.

![0hYrmLCtV96fbLY7rct7Ue94xgf6OUG+O930FbxOeuA=](https://github.com/logicopslab/DevOpsProjectWithGCP/assets/82759985/c1dcc6c3-abb7-4925-8a71-b00b60ddbf80)

**Prerequisites**

1) Google Cloud tools Cloud Source Repositories.
2) Cloud Build.
3) Build triggers. 
4) Container Registry.

And, a bit of familiarity with GCP. 

**Objectives - In this lab, you will learn how to perform the following tasks:**

1) Create a Git repository
2) Create a simple Python application
3) Test Your web application in Cloud Shell
4) Define a Docker build
5) Manage Docker images with Cloud Build and Container Registry
6) Automate builds with triggers
7) Test your build changes
8) You have done a great job! Pat ya back!

**Task Distribution**

**Task 1. Create a Git repository**

First, you will create a Git repository using the Cloud Source Repositories service in Google Cloud. This Git repository will be used to store your source code. Eventually, you will create a build trigger that starts a continuous integration pipeline when code is pushed to it.

1) In the Cloud Console, on the Navigation menu, click Source Repositories. A new tab will open.
2) Click Add repository.
3) Select Create new repository and click Continue.
4) Name the repository devops-repo.
5) Select your current project ID from the list.
6) Click Create.
7) Return to the Cloud Console, and click Activate Cloud Shell (Cloud Shell icon).
8) If prompted, click Continue.
9) Enter the following command in Cloud Shell to create a folder called gcp-course:
mkdir gcp-course
10) Change to the folder you just created:
cd gcp-course
11) Now clone the empty repository you just created:
gcloud source repos clone devops-repo
12) The previous command created an empty folder called devops-repo. Change to that folder:
cd devops-repo

**Task 2. Create a simple Python application**

You need some source code to manage. So, you will create a simple Python Flask web application. The application will be only slightly better than "hello world", but it will be good enough to test the pipeline you will build.

1) In Cloud Shell, click Open Editor (Editor icon) to open the code editor. If prompted click Open in a new window.
2) Select the gcp-course > devops-repo folder in the explorer tree on the left.
3) Click on devops-repo
4) On the File menu, click New File
5) Paste the following code into the file you just created:
https://github.com/logicopslab/DevOpsProjectWithGCP/blob/main/main.py
6) To save your changes. Press CTRL + S, and name the file as main.py.
7) Click on SAVE
8) Click on the devops-repo folder.
9) Click on the File menu, click New Folder, Enter folder name as templates.
10) Click OK
11) Right-click on the templates folder and create a new file called layout.html.
12) Add the following code and save the file as you did before:
https://github.com/logicopslab/DevOpsProjectWithGCP/blob/main/layout.html
13) Also in the templates folder, add another new file called index.html. Add the following code and save the file as you did before:
https://github.com/logicopslab/DevOpsProjectWithGCP/blob/main/index.html
14) In Python, application prerequisites are managed using pip. Now you will add a file that lists the requirements for this application.
15) In the devops-repo folder (not the templates folder), create a New File and add the following to that file and save it as requirements.txt:
https://github.com/logicopslab/DevOpsProjectWithGCP/blob/main/requirements.txt
16) You have some files now, so save them to the repository. First, you need to add all the files you created to your local Git repo. In Cloud Shell, enter the following code:
cd ~/gcp-course/devops-repo
git add --all
17) To commit changes to the repository, you have to identify yourself. Enter the following commands, but with your information (you can just use your Gmail address or any other email address):
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
18) Now, commit the changes locally:
git commit -a -m "Initial Commit"
19) You committed the changes locally, but have not updated the Git repository you created in Cloud Source Repositories. Enter the following command to push your changes to the cloud:
git push origin master
20) Refresh the Source Repositories web page. You should see the files you just created.

**Task 3. Define a Docker build**

The first step to using Docker is to create a file called Dockerfile. This file defines how a Docker container is constructed. You will do that now.

1) In the Cloud Shell Code Editor, expand the gcp-course/devops-repo folder. With the devops-repo folder selected, on the File menu, click New File and name the new file Dockerfile.
The file Dockerfile is used to define how the container is built.
https://github.com/logicopslab/DevOpsProjectWithGCP/blob/main/Dockerfile

**Task 4. Manage Docker images with Cloud Build and Container Registry**

The Docker image has to be built and then stored somewhere. You will use Cloud Build and Container Registry.

1) Return to Cloud Shell. Make sure you are in the right folder:
cd ~/gcp-course/devops-repo
2) The Cloud Shell environment variable DEVSHELL_PROJECT_ID automatically has your current project ID stored. The project ID is required to store images in Container Registry. Enter the following command to view your project ID:
echo $DEVSHELL_PROJECT_ID
3) Enter the following command to use Cloud Build to build your image:
gcloud builds submit --tag gcr.io/$DEVSHELL_PROJECT_ID/devops-image:v0.1 .
Notice the environment variable in the command. The image will be stored in Container Registry.
4) If asked to enable Cloud Build in your project, type Yes. Wait for the build to complete successfully.
**Note #1**: If you receive the error "INVALID_ARGUMENT: unable to resolve source", wait a few minutes and try again.
**Note**: In Container Registry, the image name always begins with gcr.io/, followed by the project ID of the project you are working in, followed by the image name and version.

The period at the end of the command represents the path to the Dockerfile: in this case, the current directory.

5) Return to the Cloud Console and on the Navigation menu ( Navigation menu icon), click Container Registry. Your image should be on the list.
6) Now navigate to the Cloud Build service, and your build should be listed in the history.

You will now try running this image from a Compute Engine virtual machine.

7) Navigate to the Compute Engine service.
8) Click Create Instance to create a VM.
9) On the Create an instance page, specify the following, and leave the remaining settings as their defaults:
<img width="438" alt="image" src="https://github.com/logicopslab/DevOpsProjectWithGCP/assets/82759985/5cbedb42-bfdf-42fb-a7da-ca7298a69caf">

10) Click Create.
11) Once the VM starts, create a browser tab and make a request to this new VM's external IP address. The program should work as before.
**Note**: You might have to wait a minute or so after the VM is created for the Docker container to start.
12) You will now save your changes to your Git repository. In Cloud Shell, enter the following to make sure you are in the right folder and add your new Dockerfile to Git:
cd ~/gcp-course/devops-repo
git add --all
13) Commit your changes locally:
git commit -am "Added Docker Support"
14) Push your changes to Cloud Source Repositories:
git push origin master
15) Return to Cloud Source Repositories and verify that your changes were added to source control.

**Task 5. Automate builds with triggers**

1) On the Navigation menu (Navigation menu icon), click Container Registry. At this point, you should have a folder named devops-image with at least one container in it.
2) On the Navigation menu, click Cloud Build. The Build history page should open, and one or more builds should be in your history.
3) Click the Triggers link on the left.
4) Click Create trigger.
5) Name the trigger devops-trigger.
6) Select your devops-repo Git repository under repository dropdown.
7) Select .*(any branch) for the branch.
8) Choose Dockerfile for Configuration and select the default image.
9) Accept the rest of the defaults, and click Create.
10) To test the trigger, click Run and then Run trigger.
11) Click the History link and you should see a build running. Wait for the build to finish, and then click the link to it to see its details.
12) Scroll down and look at the logs. The output of the build here is what you would have seen if you were running it on your machine.
13) Return to the Container Registry service. You should see a new folder, devops-repo, with a new image in it.
14) Return to the Cloud Shell Code Editor. Find the file main.py in the gcp-course/devops-repo folder.
15) In the main() function, change the title property to "Hello Build Trigger." as shown below:

@app.route("/")
def main():
    model = {"title":  "Hello Build Trigger."}
    return render_template(`index.html`, model=model)

16) Commit the change with the following command:
cd ~/gcp-course/devops-repo
git commit -a -m "Testing Build Trigger"

17) Enter the following to push your changes to Cloud Source Repositories:
git push origin master
18) Return to the Cloud Console and the Cloud Build service. You should see another build running.

**Task 6. Test your build changes**

1) When the build completes, click on it to see its details. Under Execution Details, copy the Image link, format should be gcr.io/qwiklabs-gcp-00-f23112/devops-repoxx34345xx.
2) Go to the Compute Engine service. As you did earlier, create a new virtual machine to test this image. Click DEPLOY CONTAINER and paste the image you just copied.
3) Select Allow HTTP traffic.
4) When the machine is created, test your change by making a request to the VM's external IP address in your browser. Your new message should be displayed.
**Note**: You might have to wait a few minutes after the VM is created for the Docker container to start.

**Congratulations!**
In this lab, you built a continuous integration pipeline using the Google Cloud tools Cloud Source Repositories, Cloud Build, build triggers, and Container Registry.

**Credits:-**

Lab link - https://partner.cloudskillsboost.google/course_templates/41
Disclaimer - I do not own the code/process/tech material used in this project. This code/process is taken from QuickLabs for studying/information purposes.
Website - https://go.qwiklabs.com/
