# HCP Terraform / Terraform Enterprise API Postman Workspace

This repo now provides a modular set of Postman collections grouped by API metaphors (matching the official docs), plus a shared environment.

## Import

Option A — import the folder (recommended):
1. In Postman, click Import.
2. Drag-and-drop the `postman/collections/` folder and `postman/environments/hcp-terraform.postman_environment.json`.
3. Select the `hcp-terraform` environment after import.

Option B — import individual collections: Import one or more JSON files from `postman/collections/` alongside the shared environment.

## Configure

Enter values for the following Variables in Postman Environment:

- BASE_URL: app.terraform.io (no protocol) or your TFE hostname
- API_TOKEN: your user/team/org token
- ORG_NAME, ORG_ID
- WORKSPACE_ID, WORKSPACE_NAME
- PROJECT_ID
- TEAM_ID, TEAM_WORKSPACE_ID
- TOKEN_ID (for team tokens)
- OAUTH_CLIENT_ID, OAUTH_TOKEN_ID, AGENT_POOL_ID, SSH_KEY_ID
- POLICY_SET_ID
- REGISTRY_NAMESPACE, MODULE_NAME, MODULE_PROVIDER
- UPLOAD_URL (set dynamically from create-version responses)
- VARIABLE_ID, VARSET_ID, VAR_ID, USER_ID, ORG_MEMBERSHIP_ID
- CONFIG_VERSION_ID, RUN_ID, PLAN_ID, APPLY_ID, STATE_VERSION_ID

Notes:
- The collection explicitly uses https://{{BASE_URL}} in request URLs. Keep BASE_URL as a hostname only.
- Pre-signed uploads use {{UPLOAD_URL}} and remain fully qualified; do not prefix with BASE_URL.

## Auth

- Collection-level Bearer Token auth uses {{API_TOKEN}} from the environment.

## Collections

The collections mirror the Terraform Cloud API documentation structure: https://developer.hashicorp.com/terraform/cloud-docs/api-docs

- HCP Terraform - Organizations (`postman/collections/HCP-Terraform-Organizations.postman_collection.json`)
	- Organizations and Entitlement Set; Terraform Enterprise-only: Data Retention Policy (show/create/update/delete) and Module Producers

- HCP Terraform - Teams (`postman/collections/HCP-Terraform-Teams.postman_collection.json`)
	- Teams, Team Tokens (modern + legacy); Team Memberships (add/remove users and org-memberships)

- HCP Terraform - Projects (`postman/collections/HCP-Terraform-Projects.postman_collection.json`)
	- Projects, Tag Bindings, Effective Tag Bindings, Move Workspaces

- HCP Terraform - Workspaces (`postman/collections/HCP-Terraform-Workspaces.postman_collection.json`)
	- Folders: Workspaces; Workspace Variables; Workspace Team Access; Workspace Resources (SSH key, tags, remote state consumers); Terraform Enterprise-only: Workspace Data Retention Policy (show/create/update/delete)

- HCP Terraform - OAuth Clients (`postman/collections/HCP-Terraform-OAuth-Clients.postman_collection.json`)
	- OAuth Clients CRUD; attach/detach Projects; list OAuth Tokens by Client

- HCP Terraform - OAuth Tokens (`postman/collections/HCP-Terraform-OAuth-Tokens.postman_collection.json`)
	- List (by client), Show, Update (SSH key), Delete

- HCP Terraform - Users (`postman/collections/HCP-Terraform-Users.postman_collection.json`)
	- Show User

- HCP Terraform - Agents (`postman/collections/HCP-Terraform-Agents.postman_collection.json`)
	- Agent Pools, Agents in Pool

- HCP Terraform - Policy Sets (`postman/collections/HCP-Terraform-Policy-Sets.postman_collection.json`)
	- Create/Show/List; Create Version → Upload to Archivist

- HCP Terraform - Private Registry (`postman/collections/HCP-Terraform-Private-Registry.postman_collection.json`)
	- Modules (list/create/show); Create Version → Upload to Archivist

- HCP Terraform - Variable Sets (`postman/collections/HCP-Terraform-Variable-Sets.postman_collection.json`)
	- Org/Project/Workspace lists; create/show/update/delete; manage vars/workspaces/projects

- HCP Terraform - Configuration Versions (`postman/collections/HCP-Terraform-Configuration-Versions.postman_collection.json`)
	- List/Show/Create (upload URL) → Upload to Archivist; archive/download; TFE GC actions

- HCP Terraform - Runs, Plans, Applies (`postman/collections/HCP-Terraform-Runs-Plans-Applies.postman_collection.json`)
	- Runs (create/list/show; actions: apply/discard/cancel/force-cancel/force-execute)
	- Plans (show; JSON output; sanitized plan)
	- Applies (show; errored-state redirect)

- HCP Terraform - State Versions (`postman/collections/HCP-Terraform-State-Versions.postman_collection.json`)
	- List/filter/show/current/create/upload/rollback; TFE GC actions

Legacy (all-in-one): If present, `postman/collections/HCP-Terraform-API.postman_collection.json` remains for convenience; prefer the modular collections above.

### Common Flows

- Create Config Version → Upload to Archivist (UPLOAD_URL) → Create Run → Apply
- Create Policy Set Version → Upload to Archivist (UPLOAD_URL)
- Create Module Version → Upload to Archivist (UPLOAD_URL)

### Pagination

- Query params like page[number], page[size] are included in many list endpoints.
- include=current_version example included for Policy Sets.

### Variable Reference Examples

- URLs: https://{{BASE_URL}}/api/v2/...
- Org/workspace: {{ORG_NAME}}, {{WORKSPACE_ID}}, {{WORKSPACE_NAME}}
- IDs: {{PROJECT_ID}}, {{TEAM_ID}}, {{TEAM_WORKSPACE_ID}}, {{TOKEN_ID}}, {{OAUTH_CLIENT_ID}}, {{AGENT_POOL_ID}}, {{SSH_KEY_ID}}, {{POLICY_SET_ID}}
- Registry: {{REGISTRY_NAMESPACE}}, {{MODULE_NAME}}, {{MODULE_PROVIDER}}
- Uploads: {{UPLOAD_URL}}
- Variables/Varsets: {{VARIABLE_ID}}, {{VARSET_ID}}, {{VAR_ID}}
- Run workflow: {{CONFIG_VERSION_ID}}, {{RUN_ID}}, {{PLAN_ID}}, {{APPLY_ID}}
- State: {{STATE_VERSION_ID}}
