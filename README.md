# HCP Terraform / Terraform Enterprise API Postman Workspace

This repo contains an importable Postman collection and environment for the full HCP Terraform / Terraform Enterprise API v2 plus Private Registry endpoints.

## Import

1. In Postman, click Import.
2. Select `postman/collections/HCP-Terraform-API.postman_collection.json` and `postman/environments/hcp-terraform.postman_environment.json`.
3. Select the environment after import.

## Configure

- In the environment, set:
  - baseUrl: https://app.terraform.io (or your TFE hostname)
  - apiToken: your user/team/org token
  - orgName, orgId
  - workspaceId, workspaceName
  - projectId
  - teamId, teamWorkspaceId
  - tokenId (for team tokens)
  - oauthClientId, agentPoolId, sshKeyId
  - policySetId, uploadUrl (set dynamically from create-version responses)
  - registryNamespace, moduleName, moduleProvider

## Auth
## Coverage

- Organizations, Teams, Team Access, Team Tokens (modern + legacy)
- Projects, Workspaces (locks, delete, SSH keys, tags, state consumers)
- OAuth Clients, Agents/Agent Pools/Agents
- Policy Sets (upload via Archivist), Private Registry Modules (upload via Archivist)
- Workspace Variables (list/create/update/delete)
- Variable Sets (org/project/workspace lists; create/show/update/delete; manage vars/workspaces/projects)
- Configuration Versions (list/show/create upload-url/upload/archive/download; TFE GC actions)
- Runs (create/list/show; actions: apply/discard/cancel/force-cancel/force-execute)
- Plans (show; JSON output; sanitized plan)
- Applies (show; errored-state redirect)
- State Versions (list/filter/show/current/create/upload/rollback; TFE GC actions)

  - POST /runs
  - POST /workspaces/:id/configuration-versions
- Workspace Data Retention Policy endpoints are Terraform Enterprise-only.
### Pagination and include examples
- Uploads/flows: `{{uploadUrl}}`
- Variables/Varsets: `{{variableId}}`, `{{varsetId}}`, `{{varId}}`
- Run workflow: `{{configVersionId}}`, `{{runId}}`, `{{planId}}`, `{{applyId}}`
- State: `{{stateVersionId}}`

- Team Tokens (modern multi-token + legacy single-token)
- Projects (list/create/show/update/delete; tag-bindings; move workspaces)
- Workspaces (list/show/create/update; safe/force delete; lock/unlock/force-unlock; SSH key assign/unassign; remote state consumers; flat tags; tag-bindings)
- OAuth Clients
- Agents and Agent Pools
- Policy Sets and Policy Set Versions (upload flow)
- Private Registry Modules (list/create/versions/upload/get)

Planned next:
- Users, Team Memberships, Project Team Access
- Variables, Variable Sets
- Runs, Plans, Applies, Config Versions, State Versions, Outputs
- Run Tasks, Cost Estimates, Notifications, Explorer, Billing/Invoices

Contributions welcome.
