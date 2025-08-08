# Contributing

Thank you for your interest in contributing to this repository! I welcome pull requests and suggestions to help improve the Postman collections and environment for the HashiCorp HCP Terraform/Terraform Enterprise API v2.

## How to Contribute

1. **Fork the repository** and create your branch off of your default branch.
2. **Add or update Postman collections** in `postman/collections/` following the [repo conventions](README.md).
3. **Edit the shared environment** in `postman/environments/terraform.postman_environment.json` if needed. Use only UPPERCASE keys.
4. **Validate all JSON files** for correctness (Postman v2.1 schema).
5. **Update the README** to reflect any new or renamed collections. Keep the Collections list alphabetical.
6. **Open a pull request** with a clear description of your changes.

## Guidelines

- Use only environment variables; do not add collection-level variables.
- Filenames must be lowercase and hyphen-delimited.
- Collection `info.name` must end with "Collection".
- All request URLs use `https://{{BASE_URL}}` except for pre-signed upload URLs.
- Do not transform or prepend `UPLOAD_URL`.
- Ensure your changes import cleanly into Postman.

## Review Process

- PRs are reviewed for adherence to conventions, JSON validity, and documentation updates.
- Collections and environment files must remain valid and functional.
- All changes should maintain or improve coverage and consistency.

## Need Help?

If you have questions or need guidance, please open an issue or start a discussion in the repository.
