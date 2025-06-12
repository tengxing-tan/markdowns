
[Preparing for AZ-204 - Develop Azure compute solutions (Part 1 of 5) | Microsoft Learn](https://learn.microsoft.com/en-us/shows/exam-readiness-zone/preparing-for-az-204-develop-azure-compute-solutions)

Azure developer certification roadmap
- Azure Fundamental
- Azure Developer Exam Prep
- Azure Associate
# Azure Developer CLI
To streamline **provisioning & deploying** workflows
- provisioning
	- hardware, database, resources, network, security are properly configured
- deploying
	- ensure software is installed, configured, running in production. 

```powershell
winget install microsoft.azd
azd version
azd template list
```

**Quick start**
```powershell
azd init --template todo-nodejs-mongo
# enter env name

azd auth login

azd up
# choose your subscription 
# (get from https://portal.azure.com/#view/Microsoft_Azure_Billing/SubscriptionsBlade)

# To open live metrics dashboard in browser
azd monitor --live
azd monitor --overview
azd monitor --logs
```

`azd up`
- Update app by provision, package & deploy source code
- Or specifically:
- `azd provision`
	- To create and update Azure resources to the subscription
- `azd deploy`
	- To package & deploy your source code changes

**CI/CD**
- Create new GitHub repo, set origin & run:
```powershell
azd pipeline config
# Select GitHub
```
- On GitHub, navigate to the **Actions** tab to find the workflows as created from Azure template.
- By doing so, `azd auth login, azd provision, azd deploy` will be run by GitHub Actions on every git push.  

**Delete Azure resources**



---

# Docker image in Azure

What
- You can **deploy a web app** by using an image from **Azure Container Registry** 

Why
- Less administrative work
- Docker image is compatible on not only Azure, so it is easy to deploy to other place.

Why not Docker Hub
- More control on hand
- Secure, private Docker images
- 500GB sku, span a couple of nodes concurrently. 

How: [Deploy a web app by using an image from an Azure Container Registry repository - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/deploy-run-container-app-service/4-deploy-web-app)

How to continuous deployment (CD):
- Use Container Registry **webhook** to restart site and update images
- [Exercise - Modify the image and redeploy the web app - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/deploy-run-container-app-service/7-exercise-update-web-app?pivots=csharp)

---

# Azure serverless function

- Explain functional differences between Azure Functions, Azure Logic Apps, and WebJobs
	- Azure Functions: code-first (imperative)
	- Azure Logic Apps: designer-first (declarative)
	- WebJobs: Same to Azure Functions but no pay-as-you-go, no serverless model
- Describe Azure Functions hosting plan options
	- Consumption plan: pay-as-you-go, max 200 instances
	- Premium: virtual network
	- Dedicated: predictable billing
- Describe how Azure Functions scale to meet business needs

