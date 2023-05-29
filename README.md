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

**Task distribution**

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

