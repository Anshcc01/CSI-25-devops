
# Azure DevOps Project Implementation

This guide outlines how to create a project in Azure DevOps, manage user groups, apply security policies, implement pull requests, CI/CD pipelines, and configure triggers and gates.

---

## 🔧 1. Create Azure DevOps Project and User Groups

### Steps:
1. Go to [Azure DevOps Portal](https://dev.azure.com).
2. Click on **"New Project"**.
3. Enter project name and visibility, then click **Create**.

### Add Users and Create Groups:
1. Navigate to **Project Settings** > **Permissions**.
2. Click **New Group** to create:
   - `Project Administrators`
   - `Contributors`
   - `Readers`
3. Assign users to respective groups.
4. Set permissions for each group accordingly.

📚 **Reference**:  
- [Add users and groups](https://learn.microsoft.com/en-us/azure/devops/organizations/security/add-users-team-project)

---

## 🔐 2. Apply Branch Policies: Only Admin Access to `master`

### Steps:
1. Go to **Repos** > **Branches**.
2. Click on the `...` next to `master`, then **Branch Policies**.
3. Set **Minimum number of reviewers**, enable **Check for linked work items**.
4. Uncheck **Allow users to approve their own changes**.

### Restrict Merge Permissions:
1. Go to **Project Settings** > **Repositories** > Select Repository.
2. Under `master` branch, remove "Contribute" permission for `Contributors`.
3. Allow only `Project Administrators`.

📚 **Reference**:  
- [Branch permissions](https://learn.microsoft.com/en-us/azure/devops/repos/git/branch-permissions)

---

## 🔒 3. Apply Branch Security and Locks

### Steps:
1. Go to **Repos** > **Branches** > Click `...` next to branch > **Lock**.
2. Under **Project Settings** > **Repositories**, manage branch permissions.
   - Deny "Force push" for all users.
   - Deny "Delete" for `Contributors`.

📚 **Reference**:  
- [Branch policies and security](https://learn.microsoft.com/en-us/azure/devops/repos/git/branch-policies)

---

## 📂 4. Apply Branch Filters and Path Filters

### Branch Filters in Policies:
1. While setting CI build validation, define specific branches using filters (e.g., `feature/*`).

### Path Filters:
1. In Branch Policies > **Build Validation** > **Path Filter**:
   - Include or exclude files/folders for triggering builds (e.g., `src/*`).

📚 **Reference**:  
- [Path filters](https://learn.microsoft.com/en-us/azure/devops/repos/git/branch-permissions)

---

## 🔁 5. Apply Pull Requests

### Steps:
1. Create a new branch: `feature/xyz`.
2. Make changes > commit > push branch.
3. Go to **Repos** > **Pull Requests** > **New Pull Request**.
4. Select base branch as `master`, compare with `feature/xyz`.
5. Add reviewers > Create.

📚 **Reference**:  
- [Pull Requests](https://learn.microsoft.com/en-us/azure/devops/repos/git/pull-requests)

---

## 🔐 6. Apply Branch Policy and Security

Repeat Steps 2 & 3 to:
- Enforce branch policy.
- Set permission levels per group.
- Prevent contributors from bypassing policies.

---

## 🚀 7. Apply Triggers in Build and Release

### CI Trigger:
1. Go to **Pipelines** > **Edit pipeline YAML**.
2. Add:
   ```yaml
   trigger:
     branches:
       include:
         - main
         - feature/*
   ```

### CD Trigger (Release Pipeline):
1. Go to **Releases** > Edit pipeline.
2. Enable continuous deployment trigger on artifact push.

📚 **Reference**:  
- [CI/CD Triggers](https://learn.microsoft.com/en-us/azure/devops/pipelines/build/triggers)

---

## 🛑 8. Apply Gates to Pipeline

### Steps:
1. In **Release Pipeline** > **Environments** > Pre-deployment conditions.
2. Enable **Gates**.
3. Add conditions like:
   - Azure Monitor Alerts
   - Work item queries
   - REST APIs

📚 **Reference**:  
- [Gates documentation](https://learn.microsoft.com/en-us/azure/devops/pipelines/release/approvals/gates)

---

## 🔐 9. Secure Branch: Allow PRs Only from Contributors

### Steps:
1. Go to **Project Settings** > **Repositories** > `master` branch.
2. Set:
   - Allow: Create branch, Create PR
   - Deny: Contribute, Bypass policies
3. Contributors can **create PRs** but **cannot merge** without approval.

📚 **Reference**:  
- [Secure branches](https://learn.microsoft.com/en-us/azure/devops/repos/git/branch-permissions)

---

## 📝 10. Use Work Items in Pipelines

### Steps:
1. Link commits to work items via `#WorkItemID` in commit messages.
2. In PR or commit view, verify work item link.
3. In YAML pipeline:
   ```yaml
   name: $(Build.BuildId)
   trigger:
     branches:
       include: [main]
   variables:
     system.debug: true
   steps:
     - script: echo "Associated Work Item ID: $(System.WorkItemId)"
   ```

📚 **Reference**:  
- [Work Items](https://learn.microsoft.com/en-us/azure/devops/boards/work-items/about-work-items)

---

## ✅ Final Checklist

- [x] Project created with groups and policies
- [x] Master branch access secured
- [x] Pull request flow enforced
- [x] CI/CD triggers and gates configured
- [x] Work items integrated into pipeline

---

## 🎥 References

- YouTube:  
  [Azure DevOps Boards & Repos Tutorial](https://www.youtube.com/watch?v=4ah5Tuj0i4s)  
  [Pull Requests & Pipelines](https://www.youtube.com/watch?v=qLhVWJvox7g)  
  [Pipelines & Security](https://www.youtube.com/watch?v=xH5EY7FCFQw)

- Docs:
  - [Azure DevOps Documentation](https://learn.microsoft.com/en-us/azure/devops/)
