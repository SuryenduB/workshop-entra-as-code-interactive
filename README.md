# 🚀 Entra as a Code Workshop 🚀
Manage your Tenant with Infrastructure as Code: it works for Workforce and Customer instances

## 🎯 Interactive Workshop Mode

This workshop supports **interactive tracking via GitHub Issues**! Each stage creates a dedicated issue with:
- Full documentation and instructions
- Progress checkboxes to track your completion
- Labels for easy filtering

### How to Start Interactive Mode

1. **Fork the repository:**
   - Go to **Issues** tab

2. **Track Your Progress:**
   - Each stage has its own GitHub Issue with checkboxes
   - Check the boxes as you complete each step
   - Close the issue when you finish the stage

3. **Recommended Workflow:**
   | Step | Action |
   |------|--------|
   | 1 | Open the stage issue |
   | 2 | Read the documentation |
   | 3 | Complete all tasks |
   | 4 | Check all checkboxes |
   | 5 | Close the issue |
   | 6 | Move to next stage |

> **Pro Tip:** Use the issue comments to note any problems or learnings during each stage!

## 📚 Changelog 
| Version | Date       | Description                                        |
|---------|------------|----------------------------------------------------|
| v0.8    | 2025.04.28 | Alpha                                              |
| v0.9    | 2025.05.07 | Beta - dryrun                                      |
| v0.9.1  | 2025.05.16 | For Self-Workshop: more pictures and description   |
| v0.10  | 2026.01.03 | Typos and doc improvment & update provider version |
| v1.0  | 2026.01.05 | 🎆 Public repository version |
## ❔Q&A
| Question                                           | Answer                                                                       |
|----------------------------------------------------|------------------------------------------------------------------------------|
| Do I need an Entra ID Tenant?                      | Yes, when you run a workshop on your own; no, during an online or onsite workshop. |
| Do I need an Azure Subscription?                   | No, we will use Entra ID only.                                               |
| Do I need to have a Workforce or an External ID tenant? | All steps are for Workforce, 1-4 will work with the External ID tenant.          |
| Do I need the Global Admin role?                       | Yes.                                                                         |
| Is the workshop to learn Terraform?                | No, the workshop is to manage Entra ID as code with Terraform.               |

## 🛠️ Prerequisites
### Technical
- ✅ [Entra ID Tenant](https://www.microsoft.com/en-gb/security/business/identity-access/microsoft-entra-id)
- ✅ A global administrator or the authentication policy administrator permission is required.
- ✅ **Entra ID P1 or P2 license** (required for Stages 4-6: Conditional Access, Access Packages, PIM)
- ✅ **Security Defaults disabled** in tenant (required for Stage 4: Conditional Access)

- ✅ VSCode
- ✅ Terraform (v1.0+)
- ✅ Git (to clone the repository)
- ✅ Windows Workstation (all flows I tested on Windows - but you can use any OS)
  
### Entra ID Permissions (cumulative per stage)
| Stage | Required Graph API Permissions |
|-------|-------------------------------|
| 0-3 | `Application.ReadWrite.All` |
| 4   | + `Policy.ReadWrite.ConditionalAccess`, `Policy.Read.All` |
| 5   | + `EntitlementManagement.ReadWrite.All`, `Group.ReadWrite.All`, `Directory.ReadWrite.All` |
| 6   | + `PrivilegedEligibilitySchedule.ReadWrite.AzureADGroup` |

### Skills (Basic)
- ✅ Basic knowledge of scripting and the command line
- ✅ Basic understanding of Service Principal Authentication
- ✅ Familiarity with Azure Portal navigation


## 🥇 Achievements
- Authenticate with service access (Service Principal)
- Set up basic Entra ID elements with Terraform.
- Understand limitations.

## ⏱️ Total Workshop Duration: ~90-120 minutes

## 🗝️ Workshop key points
1. Set up the workstation environment
2. Create a Service Principal
3. Prepare the Terraform file structure
4. First Terraform resource and module 
5. Init&Plan&Apply
6. Create a couple of Entra ID resources
7. Spacelift.io for integration

## Workshop
### Prerequisites installation
VS Code
```
winget install Microsoft.VisualStudioCode
```
Terraform
```
winget install HashiCorp.Terraform
```

#### VS Code extensions
- [Terraform](https://marketplace.visualstudio.com/items/?itemName=HashiCorp.terraform)
- [REST Client](https://marketplace.visualstudio.com/items/?itemName=humao.rest-client)

 
### Terraform basic command
init
```
terraform init
```
plan
```
terraform plan
```
apply
``` 
terraform apply
```
destroy
``` 
terraform destroy
```

## Structure of the project - code organisation
1. Recommended: The interactive version of the workshop is prepared to work as a fork - the pipeline will create GitHub Issues for each stage.
   - Mark the process with checkboxes in the issues and close finished steps.
   - Back to the workshop after a while - based on the marked progress. 
1. A Workshop is a list of steps in the `doc` folder (same as copy in the GitHub Issues). 
   - [Stage 0](doc/stage-0/prerequisits.md)
   - [Stage 1](doc/stage-1/SSO-application.md)
   - [Stage 2](doc/stage-2/service-principal.md)
   - [Stage 3](doc/stage-3/workload-federation.md)
   - [Stage 4](doc/stage-4/conditional-access.md)
   - [Stage 5](doc/stage-5/access-package.md)
   - [Stage 6](doc/stage-6/pim.md)
   - [Stage 7](doc/stage-7/end.md)
   - [Final Solution](doc/stage-final/main.tf)
   - [Stage Next](doc/stage-next/what-next.md)
1. The steps are instructions and requirements for creating module instances (`modules` folder) in the `main.tf` file to create simple Entra ID resources.
1. To verify the configuration, please use `test` folder.

## 📋 Workshop Stages Overview (Interactive)

| Stage | Topic | Duration | License Required | Issue Label |
|-------|-------|----------|------------------|-------------|
| 0 | [Prerequisites](doc/stage-0/prerequisits.md) | 15-20 min | - | `stage-0` |
| 1 | [SSO Application](doc/stage-1/SSO-application.md) | 10-15 min | - | `stage-1` |
| 2 | [Service Principal](doc/stage-2/service-principal.md) | 10 min | - | `stage-2` |
| 3 | [Workload Federation](doc/stage-3/workload-federation.md) | 15 min | - | `stage-3` |
| 4 | [Conditional Access](doc/stage-4/conditional-access.md) | 15 min | P1 | `stage-4` |
| 5 | [Access Package](doc/stage-5/access-package.md) | 10 min | P2 | `stage-5` |
| 6 | [PIM](doc/stage-6/pim.md) | 15 min | P2 | `stage-6` |
| 7 | [End & Cleanup](doc/stage-7/end.md) | 5 min | - | `stage-7` |
| Bonus | [What's Next](doc/stage-next/what-next.md) | - | - | `bonus` |

> **Interactive Mode:** Run the GitHub Action to create trackable issues for each stage!

## 📊 Plan
- Pull the repository to the workstation.
- Follow the steps in the doc folder from zero to the end.
- Destroy the resources created in the Entra ID tenant with the command `terraform destroy`.

## ⚠️ Excluded and not covered in this workshop
- Cost of the Terraform license (if any).
- Manage the Terraform state file.
- Secret management (client_id and client_secret) access to Entra ID tenant and Azure subscription (not covered at all).

## 🔍 Troubleshooting

| Issue                                | Solution                                                                    |
|--------------------------------------|-----------------------------------------------------------------------------|
| No changes in the Terraform plan.    | Always be sure to save the changes in the `main.tf`.                        |
| Can't remove(destroy) the resources. | Check Access Package assignments. Remove all assignments to your package.   |
| `Error: Module not installed`        | Run "terraform init" to install all modules required by this configuration. |

## Report Issues

Found a bug, have a question, or want to suggest an improvement? Please report any issues with the workshop at:

**[https://github.com/mjendza/workshop-entra-as-code-interactive/issues](https://github.com/mjendza/workshop-entra-as-code-interactive/issues)**
