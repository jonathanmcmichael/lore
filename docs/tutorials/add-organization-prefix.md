# Add an organization prefix

This tutorial walks you through grouping your Lore repositories under an organization prefix (e.g., `/MyOrg/MyProject`). Using prefixes is a common requirement for Lore Servers that use a shared authentication service to manage access.

## Prerequisites

- The `lore` CLI installed.
- A running Lore Server (see [Deploy a local Lore Server](../how-to/deploy-local-lore-server.md)).

## Steps

1. **Understand organization prefixes.**

   When you create or clone a repository on a server, Lore uses a path-based naming convention: `ucs://<server>:<port>/<Organization>/<Repository>`.

   If you omit the organization (e.g., `ucs://localhost:41337/MyProject`), the server might reject the request or default to an internal organization (typically `Epic`).

2. **Create a repository with a custom organization.**

   To group your project under your own organization, include it in the URL when running `repository create`.

   ```bash
   lore repository create ucs://localhost:41337/MyOrg/MyProject
   ```

3. **Clone a repository using its full path.**

   When cloning, ensure you specify the full path including the organization.

   ```bash
   lore repository clone ucs://localhost:41337/MyOrg/MyProject ./MyProject
   ```

4. **Verify the remote configuration.**

   Check that the local repository is correctly linked to the organization.

   ```bash
   lore repository config remote_url
   ```

## Deep nesting (Optional)

Lore supports deep directory-style nesting for larger organizations. You can group repositories by department, team, or project phase.

```bash
# Example of deep nesting
lore repository create ucs://localhost:41337/MyOrg/Games/Mobile/InternalTest
```

> [!NOTE]
> The total length of the path (including all prefixes and the repository name) must be under **1,000 characters**.

## Verify

Run `lore repository info` to see the full repository name including the prefix.

```bash
lore repository info
```

Expected output includes the organization in the name:

```text
Name: MyOrg/MyProject
ID: ...
```

## Next steps

- [Set up your Lore identity](./setup-identity.md)
- [Add an existing Unreal Engine project](./add-unreal-project.md)
