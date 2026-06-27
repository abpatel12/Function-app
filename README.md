<<<<<<< HEAD
# Azure Function App – CI/CD with Azure DevOps

A .NET-based Azure Function App deployed end-to-end using Azure DevOps Pipelines (CI) and Azure DevOps Releases (CD), with two live functions: an **HTTP Trigger** and a **Timer Trigger**.

---

## Project Structure

```
function-app/
├── .vscode/
├── Properties/
├── .gitignore
├── Fapp.csproj
├── host.json
├── HttpTrigger1.cs
├── TimerTriggerCSharp1.cs
└── README.md
```

---

## What Was Built

### 1. Azure Function App (C# / .NET)
- Created a .NET Azure Function App hosted on **Azure (Consumption Plan – Windows)**.
- Runtime stack: **.NET 8 (LTS), Isolated Worker Model**.
- Two functions are deployed and enabled:
  - **HttpTrigger1** – triggered via HTTP requests.
  - **TimerTriggerCSharp1** – triggered on a scheduled timer.

---

### 2. CI Pipeline – Azure DevOps (Build)

A classic build pipeline named **`funcation app-CI (1)`** was configured with the following stages under **Agent Job 1** (runs on `windows-latest`):

| Step | Task | Description |
|------|------|-------------|
| 1 | **Use .NET Core SDK** | Installs the required .NET SDK version |
| 2 | **dotnet build** | Builds the project (`**/*.csproj`) in Release configuration with output to `publish_output` |
| 3 | **Copy Files** | Copies compiled output to `$(build.artifactstagingdirectory)` |
| 4 | **Publish Artifact: drop** | Publishes the build artifact named `drop` for use in release |

**Build settings:**
- Azure Subscription: `Azure subscription 1`
- Command: `build`
- Path: `**/*.csproj`
- Arguments: `--output publish_output --configuration Release`
- Timeout: `300000`

The pipeline ran successfully (Run **#110**), producing **1 artifact** in approximately **1 minute 39 seconds**.

---

### 3. CD Pipeline – Azure DevOps (Release)

A release pipeline named **`New release pipeline (1)`** was set up to deploy the build artifact directly to Azure Functions.

**Artifact source:**
- Source type: **Build**
- Project: `funcation app`
- Source pipeline: `funcation app-CI (1)`
- Default version: **Latest**
- Source alias: `_funcation app-CI (1)`

**Stage 1 – Deployment:**
- Task: **Azure Functions Deploy** (Task version 2.x)
- Display name: `Azure Function App Deploy: fuction124565`
- Azure Resource Manager connection: `Azure subscription 1`
- App type: **Function App on Windows**
- Azure Functions App name: `fuction124565`
- Package or folder: `$(System.DefaultWorkingDirectory)/_funcation app-CI (1)/drop`

**Result:** Release-1 → Stage 1 → **Succeeded** ✅

---

### 4. Azure Function App – Live

After a successful release, the Function App `fuction124565` was confirmed **Running** in the Azure Portal:

- **Resource Group:** fuction12_group  
- **Location:** Korea South  
- **App Service Plan:** ASP-fuction12group-a3ae  
- **Runtime version:** 4.1048.200.26180  
- **Operating System:** Windows  
- **Default domain:** `fuction124565-fhhqefbafbdbf5g9.koreassouth-01.azurewebsites.net`

Both functions are live and enabled:

| Function | Trigger | Status |
|----------|---------|--------|
| HttpTrigger1 | HTTP | ✅ Enabled |
| TimerTriggerCSharp1 | Timer | ✅ Enabled |

The **Function URL** for `HttpTrigger1` can be retrieved from the Azure Portal under **Code + Test → Get Function URL**, with keys available at the `_master (Host key)`, `default (Host key)`, and `default (Function key)` levels.

---

## Tech Stack

- **Language:** C# / .NET 8
- **Platform:** Azure Functions (Consumption Plan, Windows, Isolated Worker)
- **Source Control:** Azure DevOps Repos
- **CI/CD:** Azure DevOps Pipelines (Build + Release)
- **Cloud:** Microsoft Azure

---

## Getting Started

### Prerequisites
- .NET 8 SDK
- Azure CLI or Azure Portal access
- Azure DevOps account with an active subscription

### Installation
1. Clone the repo from Azure DevOps:
   ```bash
   git clone <your-azure-devops-repo-url>
   cd function-app
   ```
2. Restore and build locally:
   ```bash
   dotnet build --configuration Release
   ```
3. Run locally with Azure Functions Core Tools:
   ```bash
   func start
   ```

### Deployment
Deployment is fully automated via the Azure DevOps CI/CD pipeline. Push to the `main` branch to trigger a build, which then flows into the release pipeline and deploys to Azure automatically.

---

## License
This project is provided for learning and demonstration purposes.
=======
# Introduction 
TODO: Give a short introduction of your project. Let this section explain the objectives or the motivation behind this project. 

# Getting Started
TODO: Guide users through getting your code up and running on their own system. In this section you can talk about:
1.	Installation process
2.	Software dependencies
3.	Latest releases
4.	API references

# Build and Test
TODO: Describe and show how to build your code and run the tests. 

# Contribute
TODO: Explain how other users and developers can contribute to make your code better. 

If you want to learn more about creating good readme files then refer the following [guidelines](https://docs.microsoft.com/en-us/azure/devops/repos/git/create-a-readme?view=azure-devops). You can also seek inspiration from the below readme files:
- [ASP.NET Core](https://github.com/aspnet/Home)
- [Visual Studio Code](https://github.com/Microsoft/vscode)
- [Chakra Core](https://github.com/Microsoft/ChakraCore)
>>>>>>> 92c38b344eb3eeab56f71625b03f908560246f5f
