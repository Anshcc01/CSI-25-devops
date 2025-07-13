# Azure DevOps – CI/CD, Pipelines, Dashboards, and Infrastructure Setup

This project demonstrates how to configure and manage complete DevOps workflows using Azure DevOps. It includes work item tracking, pipeline variables, CI/CD with Docker, AKS, ACI, App Service, React deployment to VM, and other best practices.

---

## 🧩 1. Configure Dashboard and Queries for Work Items

**Steps**:
1. Go to **Azure DevOps > Boards > Queries**.
2. Click `+ New Query` → set `Work Item Type` to `Bug`, `Task`, or `User Story`.
3. Save the query and click on `Pin to dashboard`.
4. Go to **Boards > Dashboards** → create or select a dashboard.
5. Use the `Query Tile`, `Chart for Queries`, or `Work Item Widgets` to visualize.

📚 [Learn More](https://learn.microsoft.com/en-us/azure/devops/boards/queries/using-queries)

---

## ⚙️ 2. Use Pipeline Variables

**Steps**:
1. In YAML, define variables at the top:
   ```yaml
   variables:
     buildConfig: 'Release'
     dockerImage: 'myapp'
   ```
2. Use the variables:
   ```yaml
   - script: echo "Building in $(buildConfig) mode"
   ```

📚 [Learn More](https://learn.microsoft.com/en-us/azure/devops/pipelines/process/variables)

---

## 📦 3. Use Variable and Task Groups in Pipelines

**Steps**:
1. Navigate to **Pipelines > Library** → `+ Variable Group`.
2. Add key-value pairs and set stage-specific scopes.
3. Link in YAML:
   ```yaml
   variables:
   - group: my-variable-group
   ```

📚 [Learn More](https://learn.microsoft.com/en-us/azure/devops/pipelines/library/variable-groups)

---

## 🔐 4. Create a Service Connection

**Steps**:
1. Go to **Project Settings > Service connections > New**.
2. Choose Azure Resource Manager → Automatic or Manual service principal.
3. Assign proper roles (`Contributor` or `Owner`).

📚 [Learn More](https://learn.microsoft.com/en-us/azure/devops/pipelines/library/service-endpoints)

---

## 🖥️ 5. Create a Linux/Windows Self-Hosted Agent

**Steps**:
1. Go to **Project Settings > Agent Pools** → Add Agent.
2. Download the agent package and run:
   ```bash
   ./config.sh --url https://dev.azure.com/<org> --auth pat
   ./svc.sh install
   ./svc.sh start
   ```
3. Ensure agent shows up as “Online”.

📚 [Learn More](https://learn.microsoft.com/en-us/azure/devops/pipelines/agents/linux-agent)

---

## ✅ 6. Apply Pre and Post-Deployment Approvers

**Steps**:
1. Go to **Pipelines > Releases > Edit** your release pipeline.
2. Click on the stage → `Pre-deployment conditions`.
3. Add `Approvers` (users or groups).
4. Do the same for `Post-deployment`.

📚 [Learn More](https://learn.microsoft.com/en-us/azure/devops/pipelines/release/approvals)

---

## 🐳 7. CI/CD: Docker to ACR → AKS

**Steps**:
1. In YAML:
   ```yaml
   - task: Docker@2
     inputs:
       command: 'buildAndPush'
       repository: '$(dockerImage)'
       dockerfile: 'Dockerfile'
       containerRegistry: 'ACR-Service-Connection'
   - task: Kubernetes@1
     inputs:
       command: apply
       connectionType: Azure Resource Manager
   ```
2. Use `kubectl apply` for deployment manifests.

📚 [Docs](https://learn.microsoft.com/en-us/azure/devops/pipelines)

---

## 🐳 8. CI/CD: Docker to ACR → ACI

**Steps**:
1. Build and push Docker image as above.
2. Add an Azure CLI task:
   ```yaml
   - task: AzureCLI@2
     inputs:
       scriptType: bash
       scriptLocation: inlineScript
       inlineScript: |
         az container create --name mycontainer          --image myacr.azurecr.io/myapp          --resource-group my-rg          --registry-login-server myacr.azurecr.io
   ```

📚 [Docs](https://learn.microsoft.com/en-us/azure/devops/pipelines)

---

## 🌐 9. CI/CD: .NET to Azure App Service

**Steps**:
1. Define YAML pipeline:
   ```yaml
   - task: DotNetCoreCLI@2
     inputs:
       command: 'build'
       projects: '**/*.csproj'
   - task: AzureWebApp@1
     inputs:
       azureSubscription: 'App-Service-Connection'
       appName: 'dotnet-webapp'
       package: '$(System.DefaultWorkingDirectory)/**/*.zip'
   ```

📚 [Medium Guide](https://ougabriel.medium.com/deploy-a-net-application-using-azure-ci-cd-pipeline-and-0eea18aedbb5)

---

## ⚛️ 10. CI/CD: React to Azure VM

**Steps**:
1. Build React app:
   ```yaml
   - script: |
       npm install
       npm run build
   ```
2. Use SCP to copy files to VM:
   ```yaml
   - task: CopyFilesOverSSH@0
     inputs:
       sshEndpoint: 'my-azure-vm'
       sourceFolder: 'build'
       targetFolder: '/var/www/html'
   ```

📚 [Medium Guide](https://medium.com/@isuruariyarathna2k00/create-a-ci-cd-pipeline-for-your-react-js-app-using-azure-devops-06e3fb153b10)

---

## 🧾 Summary

| Task | Status |
|------|--------|
| Work Items Dashboard | ✅ |
| Pipeline Variables | ✅ |
| Variable/Task Groups | ✅ |
| Service Connection | ✅ |
| Self-hosted Agent | ✅ |
| Approvers in Release | ✅ |
| CI/CD: ACR → AKS | ✅ |
| CI/CD: ACR → ACI | ✅ |
| CI/CD: .NET → App Service | ✅ |
| CI/CD: React → Azure VM | ✅ |

---

## 📎 Resources

- [Azure DevOps Docs](https://learn.microsoft.com/en-us/azure/devops/)
- [DevOps YouTube Tutorials](https://www.youtube.com/watch?v=xH5EY7FCFQw)
- [CI/CD Practical YouTube](https://www.youtube.com/watch?v=o9OpFMQMSHw)

---

## 👨‍💻 Author

**Ansh Jaiswal**  
Azure DevOps Practitioner | React & .NET CI/CD Enthusiast  
GitHub: [@Anshcc01](https://github.com/Anshcc01)