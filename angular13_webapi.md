# New Frontend/Backend Project with Angular 13

(no DevOps: source locally handled)

Ideas from <https://www.c-sharpcorner.com/article/easily-create-spa-with-net-6-0-and-angular-13-and-deploy-to-azure/>

## Create new Angular App

- open Vs2022, create new Project, select template 'ASP.NET Core with Angular'
- run it to test the app, you should see a page with header (Home, Counter, Fetch data) and a title 'Hello, world!'

## Deploy it to Azure

### Azure Portal: create Web App

- in `pp Service`: Create `Web App`
- select subscription, select or create Resource Group
- enter name: `angular13webapi`
- Runtime stack: `.NET 6 (LTS)`
- Region: close to your place
- Optional: disable Application Insights

### Publish

- in VS 2022, right-click on project, click on `Publish...`
- select `Azure`, next
- select `Azure App Service (Windows)`, next
- select the Web Api you created (I created `angular13webapi`)
- Press `Finish`
- Check config
- Press `Publish`
