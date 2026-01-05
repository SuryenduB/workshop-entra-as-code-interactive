# Stage 2: Service Principal

## Goals
- Create the Service Principal in Entra ID with terraform
- Manual creation of the secret

## ⏱️ Estimated Time: 10 minutes

## Documentation
- https://learn.microsoft.com/en-us/entra/identity-platform/v2-oauth2-client-creds-grant-flow#get-a-token

## Steps & code
To create the Service Principal we will use module `./modules/service_principal`.

> **Note:** Please use unique business name for each service principal to avoid conflicts with the shared sandbox workshop tenant.

Find needed Application.Read.All permission on the page: https://learn.microsoft.com/en-us/graph/permissions-reference

use the code below to create the Service Principal:

``` hcl
module "Demo_ServicePrincipal" {
  source = "./modules/service_principal"
  business_name = "${var.deployment_unique_name}-Demo"
  graph_permissions = ["PASTE_YOUR_GRAPH_PERMISSION_GUID_HERE"]
}
```

## Verification
- Review AppRegistration and Enterprise Application in Entra ID: check the name and permissions.
- Check if Global Admin consent is required for the selected permissions.
- Generate the secret for the Service Principal and update `test/sso.http` file with the secret.
- Fill `test/sso.http` with `clientId` and `tenantId` from the Azure Portal App Registration blade.
- Manual test: access token + Graph API call.

---

## Stage Completion Checklist
- [ ] I have read and understood this stage
- [ ] I have added the Service Principal module to main.tf
- [ ] I have found the correct Graph API permission GUID
- [ ] I have run `terraform plan`
- [ ] I have run `terraform apply`
- [ ] I have verified the Service Principal in Entra ID
- [ ] I have generated a secret for the Service Principal
- [ ] I have tested with the REST client
- [ ] Ready to move to the next stage

> **Tip:** Check all boxes above and close this issue when completed!

> **Report Issues:** Found a bug or have a question? [Report it here](https://github.com/mjendza/workshop-entra-as-code-interactive/issues)

---
**Navigation:** [← Previous: Stage 1](../stage-1/SSO-application.md) | [Next → Stage 3: Workload Federation](../stage-3/workload-federation.md)
