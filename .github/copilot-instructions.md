# AI agent guide for this repo

Purpose
- This repo provides importable Postman collections and a shared environment for the HashiCorp HCP Terraform/Terraform Enterprise API v2.
- Goal: keep collections modular by API domain, with a single shared Environment and consistent variable strategy.

Architecture & layout
- postman/collections/: one Postman v2.1 collection per API area. Filenames are lowercase, hyphen-delimited (e.g., organizations.postman_collection.json).
- postman/environments/terraform.postman_environment.json: the only environment. Its Postman name is "Terraform".
- README.md: canonical usage docs, import instructions, and conventions. Keep it in sync when adding or renaming files.

Key conventions (must follow)
- Variables live only in the Environment. Do not add collection-level variables.
- Environment variable keys are UPPERCASE (e.g., BASE_URL, API_TOKEN, ORG_NAME, WORKSPACE_ID, UPLOAD_URL, etc.).
- BASE_URL is host-only (no protocol). All requests specify https:// explicitly in URLs.
- Pre-signed uploads (Archivist) use fully-qualified UPLOAD_URL returned by create-version endpoints; do not prepend BASE_URL.
- Collections' info.name follow "<Name> Collection" (e.g., "Workspaces Collection").
- Coverage includes Cloud and Enterprise-only endpoints; align endpoints and folder structure with official docs.

Typical developer tasks
- Add or update a collection:
  1) Follow filename style (e.g., policy-sets.postman_collection.json).
  2) Set info.name to "<Name> Collection" and inherit Bearer Token auth from environment using {{API_TOKEN}}.
  3) Ensure all request URLs use https://{{BASE_URL}} except pre-signed upload URLs.
  4) Use only Environment variables; no collection variables.
  5) Validate JSON (v2.1 schema) and import into Postman to sanity-check.
  6) Update README.md: add the collection entry under Collections (alphabetical by display name).
- Update environment variables: edit postman/environments/terraform.postman_environment.json. Keep variable names UPPERCASE; maintain existing keys used in collections.

Integration points
- Terraform Cloud/Enterprise API v2 (JSON:API) with Bearer tokens (user/team/org). Pagination params (page[number], page[size]) and includes are used where applicable.
- Archivist pre-signed uploads for: configuration versions, policy set versions, module versions.

Quality gates for changes
- JSON validity: all .postman_collection.json and .postman_environment.json must be valid JSON.
- Naming: filenames must be lowercase-hyphen; info.name ends with "Collection"; environment name remains "Terraform".
- Links: README paths must match filenames; Collections list is alphabetical.

Examples in repo
- Collections: organizations, workspaces, teams, projects, oauth-clients, oauth-tokens, users, agents, policy-sets, private-registry, variable-sets, configuration-versions, runs-plans-applies, state-versions.
- Environment: postman/environments/terraform.postman_environment.json defines BASE_URL, API_TOKEN, and IDs used across flows.

Gotchas
- Postman variable resolution: avoid nested/indirect variable lookups; keep values directly in the environment.
- Do not transform UPLOAD_URL; treat it as an absolute URL.
- Enterprise-only actions (e.g., data retention, GC endpoints) should be clearly labeled and remain included.

PR checklist for AI agents
- [ ] Updated/added collection respects conventions and imports cleanly
- [ ] README updated (alphabetical Collections, paths accurate)
- [ ] Environment-only variables used; no collection-level variables introduced
- [ ] JSON validated; no stray references to removed/old filenames
