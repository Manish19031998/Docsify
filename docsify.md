# Docsify setup 
**Requirement of docsify setup:**

Docsify is a lightweight, flexible, and easy-to-set-up documentation generator that can turn your Markdown documentation into a website.

- Distributor ID: Ubuntu <br>
- Description: Ubuntu 22.04.3 LTS <br>
- Codename: jammy<br>

**Prerequisites tools:**
 
 - Podman <br>
 - Github <br>
   

**Podman**

- Podman is a tool that helps you run and manage software packages called containers on your computer.

**Github**

- GitHub is an online software development platform. It's used for storing, tracking, and collaborating on software projects.
 
<br>  
Now start a setup by following these steps:
<br>


## Steps:- Install podman 

First update and upgrade by using this command :
```
sudo apt update 
sudo apt upgrade
  ```

Then use podman installation command:

**Step 1: Update and Upgrade Your System**

sudo apt update 


output


Hit:1 https://brave-browser-apt-release.s3.brave.com stable InRelease                                            
Hit:2 https://dl.google.com/linux/chrome/deb stable InRelease                                                    
Hit:2 https://dl.google.com/linux/chrome/deb stable 
InRelease                 
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 4EB27DB2A3B88B8B
Hit:3 https://packages.microsoft.com/repos/vscode stable InRelease
Get:4 https://deb.torproject.org/torproject.org jammy InRelease [2,812 B] 

sudo apt upgrade output:

Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Calculating upgrade... Done
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.

**Step 2: Install Podman**
```bash
sudo apt-get install -y podman
```
output:

Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
podman is already the newest version (3.4.4+ds1-1ubuntu1.22.04.2).
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.


- sudo : Superuser do

- apt : This stands for "Advanced Package Tool. apt is used to install, update, and manage software packages on your sysytem.

- -y : Automatically confirms the installation without asking for user input.

- podman : It is the name of the package you want to install.

**Step 3: Check Podman Version**

```bash
podman --version
```
podman version 3.4.4


**Step 4: Create a Directory**

```bash
mkdir docsify1
```
- mkdir : This command use for making a new directory
- docs : Name of new directory.
  

**Step-5:- Create Dockerfile**

Add details in Dockerfile:


```bash
vim Dockerfile
```
- vim : Use for create and edit a file.

- Dockerfile : Name of file.

Add details in Dockerfile:

``` bash 
FROM node:latest
LABEL description="A demo Dockerfile for build Docsify."
WORKDIR /docs
RUN npm install -g docsify-cli@latest
EXPOSE 3000/tcp
ENTRYPOINT docsify serve .
  ```

**Step-4:-Create index.html**

```bash
vim index.html
```

``` bash 

<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
    <meta name="viewport" content="width=device-width,initial-scale=1" />
    <meta charset="UTF-8" />
    <link
      rel="stylesheet"
      href="//cdn.jsdelivr.net/npm/docsify@4/themes/vue.css"
    />
    <style>
    
      
    </style>
  </head>
  <body>
    <div id="app"></div>
    <script>
      window.$docsify = {
        //...
      };
    </script>
    <script src="//cdn.jsdelivr.net/npm/docsify@4"></script>
  </body>
</html>
  ```

Add details in html file:

**Step-5:- Create new fil
e in md format**

```bash
touch README.md
```

```bash
OUTPUT:

Hii i am manish Chaudhary
```
- touch : Use for creating new file.
- touch README.md : you can add your project here whatever you want to write.
  
Here we can check all files by using this command:

- ls : It is a Linux shell command that lists directory contents of files and directories.
  
**Step-6:- Build docker image**
```bash 
 podman build -f Dockerfile -t docsify/demo .
 ```

output:

STEP 1/6: FROM node:latest
STEP 2/6: LABEL description="A demo Dockerfile for build Docsify."
--> Using cache 4f1a40115e84d7131a68d48778baf0ceb758834369192148fb75b62daffc231e
--> 4f1a40115e8
STEP 3/6: WORKDIR /docs
--> Using cache be1b47bf1443bcc2ff9cf0d175607e67fa0f7b1ba62b2d3b62823f615af94deb
--> be1b47bf144
STEP 4/6: RUN npm install -g docsify-cli@latest
--> Using cache ed8794539611fec3efe1c5d76fedbe590db72c436742da0b20acf8fd33281796
--> ed879453961
STEP 5/6: EXPOSE 3000/tcp
--> Using cache 32f0b6fc4e0cb33ad46d15903cdb1b170682992acfba53e2e8582dabab2c84d8
--> 32f0b6fc4e0
STEP 6/6: ENTRYPOINT docsify serve .
--> Using cache b987f431bf106d4778a43f112c324d147733cc386d1b7aaa70998056f7f718a9
COMMIT docsify/demo
--> b987f431bf1
Successfully tagged localhost/docsify/demo:latest
b987f431bf106d4778a43f112c324d147733cc386d1b7aaa70998056f7f718a9



- podman build : Initiating the container image building process means starting the procedure to create a new container image.

- -f : It stands for file.

- Dockerfile : It specifies the name of the Dockerfile that should be used for the container image build.

- -t : It stands for tag.

- docsify : This is the name for the image.

- / : It uses for path separator in file and directory path.

- demo : This is the tag for the image.

This command is used to manage container images in Podman.

**Step-7:-Run podman**

Create a podman container for docsify.

```bash
 podman run -d -p 3000:3000 -v /home/manish/docsify1:/docs localhost/docsify/demo
```
output

82aaaa05c48a630dbeb3ef916306a48c328c1bdae9d353ce7bbdd1ea0e6073f5


This command will run a container based on the docsify/demo image.

- Podman run : It is used to run a container from the docsify/demo image.

- -d (detach mode): It allows the container to run in the background. It's useful for users who don't want to see the container's output in the terminal.

- -p (port forwarding): It enables port forwarding between the container and the host system.

- -v : It indicates volume mounted from your host's into the container

```bash
podman ps -a
```

**Step-8:- Preview Output**

CONTAINER ID  IMAGE                          COMMAND     CREATED             STATUS                     PORTS                                           NAMES
1b6429040279  k8s.gcr.io/pause:3.5                       2 weeks ago         Exited (0) 2 weeks ago     0.0.0.0:3000->3000/tcp, 0.0.0.0:5432->5432/tcp  fcbdb7043d19-infra
c7fba40c27d8  k8s.gcr.io/pause:3.5                       2 weeks ago         Created                    0.0.0.0:3000->3000/tcp, 0.0.0.0:5432->5432/tcp  f237ffd86892-infra
8f22a58b5b3a  localhost/docsify/demo:latest              42 hours ago        Exited (130) 41 hours ago  0.0.0.0:3000->3000/tcp                          podman-itp
82aaaa05c48a  localhost/docsify/demo:latest              About a minute ago  Up About a minute ago      0.0.0.0:3000->3000/tcp                          compassionate_davinci


## GitHub

**GitHub Integration Steps:**

**Step-1:-Create repository**

Make a new repository with public account.<br>
Give a name to new repository.<br>



**Step-2:-Clone the repository**

Go to [GitHub] , click on "Sign up," and follow the prompts to create your GitHub account. Then, log in to GitHub.


**Step 2: Create a GitHub Repository**
- Click on the "+" icon in the top-right corner and select "New Repository."
- Choose a name for your repository.
- Write a short description of your project or documentation.
- Choose whether the repository should be public or private.
- Click "Create repository."

**Step 3: Set Up Your Local Git Repository**
```bash
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin 
https://github.com/your-username/your-repository.git
```

**Step 4: Generate a Personal Access Token**
- Go to your GitHub account settings.
- Select "Developer settings."
- Choose "Personal access token (Classic version)."
- Click "Generate new token" and follow the prompts to generate a token.

**Step 5: Clone the Repository and Push Changes**
```bash
git push -u origin main
```

Your Docsify documentation should now be hosted on GitHub and accessible through your repository's URL. You can continue to edit your documentation locally and push changes to GitHub as needed.
