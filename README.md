# Introduction
Around 3 months ago I was approached by a customer who was interested in building Ionic 2 Apps for Red Hat Mobile Application Platform (RHMAP). At the time I just limited to say "that shouldn't be a problem, the SDK is JS" but, as a devoted programmer I had to be sure. Below these lines you'll find the result of my findings and learn how to create your own Ionic 2 App for RHMAP.

Specifically you'll learn:

* How to import the template [here](https://github.com/feedhenry-staff/quickstart-ionic-v2-tabs) into a RHMAP environment
* How to use FH SDK as an Angular 2 JS Service
* How to run your Ionic v2 front-end app locally and push your changes to RHMAP

Prerequisites: 

* Node.js v6.10.0+ locally
* RHMAP SDK (fh-js-sdk) 2.14.+
* Cordova 5.0+
* Access to a RHMAP instance where you can create and run client and cloud apps

# Setting app the environment

In order to test the Ionic v2 app we're going to create, you need a Cloud App already running or create a new one. For the sake of completeness we're going to create a new one here, but it's optional, you could use an already created Cloud App in one of your projects.

## Creating an empty project with its Cloud App
Go to RHMAP Studio and then to 'Projects', we're going to create a new 'Empty Project'. You can search 'empty' at the search field to find 'Empty Project template'. Please, give your project a name and click 'Create'.
![](https://github.com/cvicens/rhmap-ionic-v2-project/raw/master/pictures/ionic_v2-03.png)
Now we're going to create a Cloud App, please go ahead and click on the '+' plus sign. You should see something like the next picture.
![](https://github.com/cvicens/rhmap-ionic-v2-project/raw/master/pictures/ionic_v2-05.png)
Click on 'Create New' and then choose 'Cloud App' as the app template, then choose a name for your cloud app.
![](https://github.com/cvicens/rhmap-ionic-v2-project/raw/master/pictures/ionic_v2-06.png)
Finally let's deploy the app and make sure it works as expected. In the next picture you can see the app is 'Stopped' (upper right dropdown).
![](https://github.com/cvicens/rhmap-ionic-v2-project/raw/master/pictures/ionic_v2-07.png)
Now please click on 'Deploy' (cloud icon on the left) and then click on 'Deploy Cloud App' (make sure the chosen run time is Node.js - 4.4.3)
![](https://github.com/cvicens/rhmap-ionic-v2-project/raw/master/pictures/ionic_v2-08.png)
After some seconds the app should be deployed and the upper right dropdown should be green. Now click on the 'Current Host' link (just one item up the Node js runtime dropdown) and add '/hello' to the url, the result should look like the image below.
![](https://github.com/cvicens/rhmap-ionic-v2-project/raw/master/pictures/ionic_v2-09.png)

## Creating an Ionic v2 App
Now that the Cloud App is up and running, let's create our Ionic v2 App. To do so, please go back to the project view. Or go to Projects, and look for your project, as in the next picture.
![](https://github.com/cvicens/rhmap-ionic-v2-project/raw/master/pictures/ionic_v2-10.png) 

Click on the '+' plus sign on the 'Apps' area and then on 'Create New App'.
![](https://github.com/cvicens/rhmap-ionic-v2-project/raw/master/pictures/ionic_v2-11.png)

Select 'Cordova' and give your app a name.
![](https://github.com/cvicens/rhmap-ionic-v2-project/raw/master/pictures/ionic_v2-14.png)
Choose git as the source of our template code and fill the fields with:

- Git URL: https://github.com/feedhenry-staff/quickstart-ionic-v2-tabs
- Git Branch: master

![](https://github.com/cvicens/rhmap-ionic-v2-project/raw/master/pictures/ionic_v2-17.png)

After clicking on 'Import and Move on to Integration' you should get to the 'Details' area of your new app where a wizzard will explain you some details about importing the SDK, here you just have to click 'Next' until done.
![](https://github.com/cvicens/rhmap-ionic-v2-project/raw/master/pictures/ionic_v2-18.png)
![](https://github.com/cvicens/rhmap-ionic-v2-project/raw/master/pictures/ionic_v2-19.png)

So far (hopefully) you have imported the template and can proceed to the next section.

## Working locally with our new App
Here we're going to clone the app, install npm packages and finally run the app locally.

**Cloning the app**
Clonig the your app requires that you have your SSH public key uploaded to your RHMAP enviroment, if not please follow [this](https://access.redhat.com/documentation/en-us/red_hat_mobile_application_platform_hosted/3/html/local_development_guide/ssh-key-setup) guide.
Assuming you have your SSH configuration set up, go back to Studio and to your new Ionic v2 App, at the 'Details' page find the 'Git Clone URL' item at the end. Copy the git url, open a terminal window and change dir to a folder of your choice.

```

$ mkdir ionic2-test
$ cd ionic2-test
$ git clone git@git.tom.redhatmobile.com:xyz/Ionic-v2-Test-Ionic-v2-Test-2.git
Cloning into 'Ionic-v2-Test-Ionic-v2-Test-2'...
...
Enter passphrase for key '/Users/cvicensa/Projects/rhmap/cvicensa_id_rsa': 
Warning: untrusted X11 forwarding setup failed: xauth key data not generated
remote: Counting objects: 139, done.
remote: Compressing objects: 100% (127/127), done.
remote: Total 139 (delta 5), reused 98 (delta 2)
Receiving objects: 100% (139/139), 4.34 MiB | 754.00 KiB/s, done.
Resolving deltas: 100% (5/5), done.

```

**Installing npm packages**
Now it's time to install the needed npm modules. First of all change to the folder created by git, then be sure you're running the required Node.js version then run 'npm install'.

```

$ cd  cd Ionic-v2-Test-Ionic-v2-Test-2
$ node -v
v6.10.0
$ npm install
├── @angular/common@2.4.8 
├── @angular/compiler@2.4.8 
...
├── typescript@2.0.9 
└── zone.js@0.7.2 

```

**Running the app locally**
We're going to use the command 'ionic serve' to run the app locally, this command starts up an http service (normally at port 8100) so that we can test the app in a browser (in this case we're not going to use any Cordova plugin so testing in a browser is enough).

Now please go back to the terminal window and change to the folder where you have prevously run 'npm install' and run 'ionic serve'

```

ionic serve

> ionic-app-base@ ionic:serve /Users/cvicensa/Projects/rhmap/borrar/ionic2-test/Ionic-v2-Test-Ionic-v2-Test-2
> ionic-app-scripts serve "--v2" "--address" "0.0.0.0" "--port" "8100" "--livereload-port" "35729"

[17:06:04]  ionic-app-scripts 1.1.4 
[17:06:04]  watch started ... 
...
[17:06:14]  build dev finished in 10.46 s 
[17:06:14]  watch ready in 10.48 s 
[17:06:14]  dev server running: http://localhost:8100/ 

```

Running 'ionic serve' usually  run your browser automatically pointing to the local http service, in this case running on http://localhost:8100/ .

To see if the test application works properly, please type in a name and click on 'Say Hello From The Cloud'.

![](https://github.com/cvicens/rhmap-ionic-v2-project/raw/master/pictures/ionic_v2-20.png)

You should get an answer like this.

![](https://github.com/cvicens/rhmap-ionic-v2-project/raw/master/pictures/ionic_v2-21.png)

**Relevant pieces of code**
Here are some pieces of code worth having a look:

* **src/services/fh.service.ts:** Angular service 'FHService' to call services/APIs in RHMAP, it uses the RHMAP Javascript SDK
* **src/pages/home.ts:** here you'll find the code that links the 'Say Hello From The Cloud' button with 'FHService'
* **src/app/app.module.ts:** here is where our Angular service 'FHService' is added as a provider so that it can be used in any page/component or our app

## Uploading the compiled version of the app
In general (take the Ionic v1 [template](https://github.com/feedhenry-templates/quickstart-ionic-app) for example) once you're satisfied with your local work you would commit and push your changes using git. In this case and because Ionic v2 tooling requires Node.js 6 the process is a bit different.

First, you should have noticed that 'ionic serve' compiles (or transpiles) your source code ('src' folder) and generates the usual 'www'. As a general rule you wouldn't need to commit/push the 'www' folder to RHMAP because it should be generated in the platform everytime you push your changes, but this is needed as of today(*) so let's be sure this folder is added, committed and pushed along with all the changes you had made to the code of our app.

(*) Note: This is an interim process and in next releases of RHMAP it could change so that it won't be necessary to commit/push the 'www' folder.

Now, please go to the terminal window and let's check if the 'www' folder is being tracked or not. You should see the following. If not, please check that 'www' is in your local folder and also if .gitignored contains 'www'.

```

$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	www/

nothing added to commit but untracked files present (use "git add" to track)

```

Now let's add 'www' by running 'git add www' as in the following excerpt.

```

$ git add www
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   www/assets/fonts/ionicons.eot
	new file:   www/assets/fonts/ionicons.scss
    ...
    new file:   www/manifest.json
	new file:   www/service-worker.js

```

Finally let's commit and push our changes.

```

$ git commit -a -m "First release"
[master b91c066] First release
 35 files changed, 183916 insertions(+)
 create mode 100644 www/assets/fonts/ionicons.eot
 ...
  create mode 100644 www/manifest.json
  create mode 100644 www/service-worker.js
$ git push origin master
Delta compression using up to 8 threads.
Compressing objects: 100% (35/35), done.
Writing objects: 100% (36/36), 3.30 MiB | 2.12 MiB/s, done.
Total 36 (delta 2), reused 0 (delta 0)
To git.tom.redhatmobile.com:techlab/Ionic-v2-Test-Borrar.git
   9fc2d64..b91c066  master -> master

```

Now it's time to go back to Studio to the 'Details' area and see if our app works on the simulator. Now that the 'www' folder in RHMAP constains the JS version of our Ionic 2 Typescript code, you should see the following.

![](https://github.com/cvicens/rhmap-ionic-v2-project/raw/master/pictures/ionic_v2-23.png)

Once your app is working properly in the simulator why not building the binary for Android or iOS? Go 'Build', choose your target OS, select your [credentials](https://access.redhat.com/documentation/en-us/red_hat_mobile_application_platform_hosted/3/html/product_features/projects-apps-and-services#credentials) bundle and click 'Build'.

![](https://github.com/cvicens/rhmap-ionic-v2-project/raw/master/pictures/ionic_v2-25.png)

After a while a modal window will pop up with a QR code and download url so that you'll be able to install your new Ionic v2 app in your device. Go scan that code!

# Recap
By following this tutorial you should have been able to quickly create an Ionic v2 App that works against your RHMAP enviroment, run it locally and finally build the binary for Android/iOS.
