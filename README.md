# HCP Terraform / Terraform Enterprise API Postman Workspace

This repo now provides a modular set of Postman collections grouped by API metaphors (matching the official docs), plus a shared environment. All collections use Environment variables only; there are no collection-level variables.

## Import

Option A — import the folder (recommended):
1. In Postman, click Import.
2. Drag-and-drop the `postman/collections/` folder and `postman/environments/terraform.postman_environment.json`.
3. Select the `Terraform` environment after import.

Option B — import individual collections: Import one or more JSON files from `postman/collections/` alongside the shared environment.

## Configure

Enter values for the following Variables in Postman Environment (Environment-only model):

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

- Agents Collection (`postman/collections/agents.postman_collection.json`)
	- Agent Pools, Agents in Pool

- Configuration Versions Collection (`postman/collections/configuration-versions.postman_collection.json`)
	- List/Show/Create (upload URL) → Upload to Archivist; archive/download; TFE GC actions

- OAuth Clients Collection (`postman/collections/oauth-clients.postman_collection.json`)
	- OAuth Clients CRUD; attach/detach Projects; list OAuth Tokens by Client

- OAuth Tokens Collection (`postman/collections/oauth-tokens.postman_collection.json`)
	- List (by client), Show, Update (SSH key), Delete

- Organizations Collection (`postman/collections/organizations.postman_collection.json`)
	- Organizations and Entitlement Set; Terraform Enterprise-only: Data Retention Policy (show/create/update/delete) and Module Producers

- Policy Sets Collection (`postman/collections/policy-sets.postman_collection.json`)
	- Create/Show/List; Create Version → Upload to Archivist

- Private Registry Collection (`postman/collections/private-registry.postman_collection.json`)
	- Modules (list/create/show); Create Version → Upload to Archivist

- Projects Collection (`postman/collections/projects.postman_collection.json`)
	- Projects, Tag Bindings, Effective Tag Bindings, Move Workspaces

- Runs, Plans, Applies Collection (`postman/collections/runs-plans-applies.postman_collection.json`)
	- Runs (create/list/show; actions: apply/discard/cancel/force-cancel/force-execute)
	- Plans (show; JSON output; sanitized plan)
	- Applies (show; errored-state redirect)

- State Versions Collection (`postman/collections/state-versions.postman_collection.json`)
	- List/filter/show/current/create/upload/rollback; TFE GC actions

- Teams Collection (`postman/collections/teams.postman_collection.json`)
	- Teams, Team Tokens (modern + legacy); Team Memberships (add/remove users and org-memberships)

- Users Collection (`postman/collections/users.postman_collection.json`)
	- Show User

- Variable Sets Collection (`postman/collections/variable-sets.postman_collection.json`)
	- Org/Project/Workspace lists; create/show/update/delete; manage vars/workspaces/projects

- Workspaces Collection (`postman/collections/workspaces.postman_collection.json`)
	- Folders: Workspaces; Workspace Variables; Workspace Team Access; Workspace Resources (SSH key, tags, remote state consumers); Terraform Enterprise-only: Workspace Data Retention Policy (show/create/update/delete)

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
