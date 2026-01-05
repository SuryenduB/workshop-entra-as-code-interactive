# Stage 0: Prerequisites

## Goals
- create the Service Principal with secret in portal to be used in the next stage.
- start with simple permissions and add more in the next stages.
- ask for your Entra ID account: username and password.

## ⏱️ Estimated Time: 15-20 minutes

## Prerequisites Checklist
Before starting, ensure you have:
- [ ] Access to an Entra ID tenant with **Global Administrator** role
- [ ] **Entra ID P1 license** (for Stage 4) or **P2 license** (for Stages 5-6)
- [ ] VS Code installed
- [ ] Terraform installed
- [ ] Git installed (to clone the repository)

## Tools
- VS Code
```
winget install Microsoft.VisualStudioCode
```
- REST Client for VS Code https://marketplace.visualstudio.com/items?itemName=humao.rest-client
- Terraform
```
winget install HashiCorp.Terraform
```
- Git (if not installed)
```
winget install Git.Git
```

### Verify Installation
```powershell
terraform --version
code --version
git --version
```

## Steps to Create Service Principal in Azure Portal

1. **Navigate to Entra ID Portal**
   - Go to [Azure Portal](https://portal.azure.com) → Microsoft Entra ID → App registrations

2. **Register a New Application**
   - Click "New registration"
   - Name: `Workshop-Terraform-SP`
   - Supported account types: "Accounts in this organizational directory only"
   - Click "Register"

3. **Create Client Secret**
   - Go to "Certificates & secrets" → "New client secret"
   - Description: `workshop-secret`
   - Expiry: 90 days (for workshop)
   - Copy the secret value immediately (you won't see it again!)

4. **Assign API Permissions**
   - Go to "API permissions" → "Add a permission"
   - Select "Microsoft Graph" → "Application permissions"
   - Add the following permissions (add more as you progress through stages):
   
   | Permission | Required For | Assing Now with Stage 0 | 
   |------------|--------------|---------|
   | `Application.ReadWrite.All` | Stages 1-3 | ⚠️ YES |
   | `Policy.ReadWrite.ConditionalAccess` | Stage 4 | NO |
   | `Policy.Read.All` | Stage 4 | NO |
   | `EntitlementManagement.ReadWrite.All` | Stage 5 | NO |
   | `Group.ReadWrite.All` | Stage 5 | NO |
   | `Directory.ReadWrite.All` | Stage 5 | NO |
   | `PrivilegedEligibilitySchedule.ReadWrite.AzureADGroup` | Stage 6 | NO |
   
   - Click **"Grant admin consent for [Your Tenant]"**

5. **Note Down Values**
   - Application (client) ID: Copy from Overview
   - Directory (tenant) ID: Copy from Overview
   - Client Secret: Already copied in step 3

6. **(Stage 4 only) Disable Security Defaults**
   - Go to Entra ID → Properties → Manage Security defaults
   - Set to "Disabled"
   - This is required for Conditional Access policies

## Code
Update the **Basic** section of the [main.tf](../../main.tf) file. Use a prefix with your name or initials for the value of `deployment_unique_name`.
``` hcl
# Set deployment unique name
variable "deployment_unique_name" {
  default = "MJ"
}
```

Update the [provider.tf](../../provider.tf) file with your Service Principal credentials:
``` hcl
provider "azuread" {
  client_id     = "YOUR_CLIENT_ID_HERE"
  client_secret = "YOUR_CLIENT_SECRET_HERE"
  tenant_id     = "YOUR_TENANT_ID_HERE"
}
```

## Verification
- [ ] client_id and client_secret are stored in [provider.tf](../../provider.tf) file.
- [ ] permissions 'Application.ReadWrite.All' assigned and consented: https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/guides/service_principal_configuration
- [ ] Each module should have a unique name `deployment_unique_name` to avoid conflicts (optional).
- [ ] Run `terraform init` to verify provider configuration works.

## Troubleshooting
| Issue | Solution |
|-------|----------|
| "Insufficient privileges" error | Ensure admin consent is granted for all permissions |
| "Invalid client secret" | Secret may have expired or was copied incorrectly |
| Cannot find App registrations | Ensure you're in the correct tenant |

---

## Stage Completion Checklist
- [ ] I have access to an Entra ID tenant with the Global Administrator role
- [ ] I have installed VS Code, Terraform, and Git
- [ ] I have created the Service Principal in the Azure Portal
- [ ] I have copied client_id, client_secret, and tenant_id
- [ ] I have assigned and consented to API permissions: `Application.ReadWrite.All`
- [ ] I have updated provider.tf with credentials
- [ ] I have run `terraform init` successfully
- [ ] Ready to move to the next stage

> **Tip:** Check all boxes above and close this issue when completed!

> **Report Issues:** Found a bug or have a question? [Report it here](https://github.com/mjendza/workshop-entra-as-code-interactive/issues)

---
**Navigation:** [Next Stage → Stage 1: SSO Application](../stage-1/SSO-application.md)
