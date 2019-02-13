### Link For Discussion/Doubts: [Discuss any doubts on this page](https://gdgnd.org/gdg-new-delhi/events/web-developer-days-1/session-discussions?speaker_resource=30)

## Steps for this CodeLab

### Pre-requisites
- Sign up on Google Cloud Platform(if you've not already)
- Activate the [GCP free trial](https://console.cloud.google.com/freetrial/signup/tos?_ga=2.84344729.-1032321293.1549865094)
- Install the [Cloud SDK](https://cloud.google.com/sdk/)
- Working NodeJS and Angular app from previous codelab
- A little familiarity with the Terminal/Powershell/Command Prompt

### Install the following (use google!)
- Node.js (version > 10)


### Build your Angular App
1. Go to your Angular App directory and run the following command to make your app production ready
`ng build --prod`

This will create a dist folder in your project directory.

2. Now check the structure of the dist folder. You have to look where the `index.html` is located.


### Create Config file

Now you have to create a config file for your project that will be used by Google Cloud App Engine to deploy the project.
1. Create a new file and name it as `app.yaml`.
2. Add the following code in it.
```
runtime: nodejs
env: flex

api_version: 1
threadsafe: true
handlers:
- url: /
  static_files: dist/web-dev-day-angular/index.html
  upload: dist/web-dev-day-angular/index.html
- url: /
  static_dir: dist/web-dev-day-angular
```
3. Now, your app is ready to be deployed.

### Setting up Google Cloud
1. Assuming that you already have a Google account. Go to the [Google Cloud Console](https://console.cloud.google.com/) and login with your Google account.
2. Create a new project for your angular app deployment e.g. angular-app-gcp.
3. In that project, create a `Google Storage Bucket`. You can search for it in the Search bar provided or just the follow this link.
4. Name your bucket something e.g. angular-app-bucket and leave the rest of things as default and click on create.

### Deploying the Application using Cloud Shell

1. Go to the bucket you just created (angular-app-bucket) on the cloud console
2. Select the Upload Files option there and upload your `dist` folder as well your `app.yaml` file. The folder structure inside your bucket should be as follows:

```
app.yaml
web_dev_day_angular/
```
3. Now, open the Google Cloud Interactive Shell. It is an in-browser terminal window provided by Google for your project.
4. Once you are connected to the Cloud Shell, Create a directory there for your app e.g. angular-app-gcp.
5. Now you need to sync your data from your bucket into this directory. Use the following command for that:
```
gsutil rsync -r gs://angular-app-bucket ./angular-app-gcp
```
6. You’re almost done. Now simply deploy your application using the following command:
```
gcloud app deploy
```
7. You will be asked for the zone/region where you’d like the App Engine to host your application. Select any zone.

8. It will take a couple of minutes and your app will be deplyed on `https://<project-id>/appspot.com`





### Setting up a new project
As we are all set with the code changes, our app is now ready to get deployed. Follow the next steps in order to create a project on Google cloud console:
1. Log into the [GCP console](https://cloud.google.com/)
2. Create a new project. Make sure you give it a relevant name.

### Preparing for Deployment
1. There is a cloud shell icon on the navigation bar. Click on the icon to activate the in-browser shell. This is going to provide you a Virtual Machine to work on.
2. Now, clone your repository into the VM.
3. Make sure that the package.json contains "start" script.
4. Click on the hamburger icon and GOTO `Source Repositories`. 
5. Click on `Add repository` in front of the project name.
6. Choose the `Connect external repository` option and click on Continue button.
7. Add GitHub as the Git provider.
8. Check the checkbox giving consent to Gcloud to source your repositories from Github and Click on `Connect to GitHub` button.
9. Select the repo to be connected and click on `Connect Selected repository`.
10. After the repository is sourced in the Google Cloud, click on `Cloud Console` on the navbar.


### Deploying using Cloud Shell
1. Once you are onto the cloud console page, activate the Cloud Shell Machine by clicking on the 
`Activate Cloud Shell` icon on the right of the navbar.
2. Once the cloud shell is up and running, clone the repository using `https`.
`git clone <https://github.com/---->`
3. `cd` into the directory which was created as a result of the above step.
4. Here comes the final step: `gcloud app deploy`.
5. You will be provided the URL of the deployed app: `https://<project-id>.appspot.com/`
6. Hit it up in the browser and there you have your node application live!

    
### You can now find [ASSIGNMENT] tags in every file, try them on your own
 - Some links (look out for documentation in each)
    - Mongoose: https://mongoosejs.com/
    - Express.js: https://expressjs.com/
    - Node.js: https://nodejs.org/en/
    - MongoDB: https://www.mongodb.com/
