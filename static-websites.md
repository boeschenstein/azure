# Create free Azure Static Website (pure HTML, from Portal)

- Create GitHub login, create new repository, add file `index.html` and enter 'Hello World'
- Create free Azure Subscription, Login to Azure Portal
  - Azure Portal: Create Static Web App
  - select free tier
  - connect to GitHub (free storage), select created repository
  - Create Website, wait until created, go to Resource, click URL to open website: you should see 'Hello World'
- anytime `index.html` is changed, an Github action is running (check 'Actions')

<https://docs.microsoft.com/en-us/azure/static-web-apps/get-started-portal?tabs=vanilla-javascript&pivots=github>
