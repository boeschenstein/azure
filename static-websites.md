# Create free Azure Static Website (pure HTML, from Portal)

- Create GitHub login, create new repository, add file `index.html` and enter 'Hello World'
- Create free Azure Subscription, Login to Azure Portal
  - Azure Portal: Create Static Web App
  - select free tier
  - connect to GitHub (free storage), select created repository
  - Create Website, wait until created, go to Resource, click URL to open website: you should see 'Hello World'
- anytime `index.html` is changed, an Github action is running (check 'Actions')

<https://docs.microsoft.com/en-us/azure/static-web-apps/get-started-portal?tabs=vanilla-javascript&pivots=github>

# Create free Azure Static Website (Angular, from CLI)

- Create free Azure Subscription, Login to Azure Portal
- Create new Angular Website in new Github repository 'my-first-static-web-app' (<https://github.com/staticwebdev/angular-basic/generate>)
- open CLI, enter `az login`
- create new Ressource Group
  - `az group create --name my-swa-group --location "westEurope"`
- Create Environment variable:
  - `GITHUB_USER_NAME=<YOUR_GITHUB_USER_NAME>`
- Create static Website

```bash
az staticwebapp create \
    --name my-first-static-web-app \
    --resource-group my-swa-group \
    --source https://github.com/$GITHUB_USER_NAME/my-first-static-web-app \
    --location "westEurope" \
    --branch main \
    --app-location "/" \
    --output-location "dist/angular-basic" \
    --login-with-github
```

- Get Repository URL: `az staticwebapp show --name  my-first-static-web-app --query "repositoryUrl"`
- Get Website URL: `az staticwebapp show --name my-first-static-web-app --query "defaultHostname"`

- Cleanup `az group delete --name my-swa-group`

<https://docs.microsoft.com/en-us/azure/static-web-apps/get-started-cli?tabs=angular>
