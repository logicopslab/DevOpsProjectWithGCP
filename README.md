# DevOpsProjectWithGCP

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

Task 3. Define a Docker build

