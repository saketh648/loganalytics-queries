


# loganalytics-queries


Every morning at 6 AM the pipeline logs in to HashiCorp Vault and lists the secrets under one path. For each secret it compares the Vault version number with the vault_version tag on the matching Key Vault secret. If the secret is missing in AKV (new) or Vault's version is higher (rotated), it writes the value to AKV as a new version with the updated tag. If the versions match, it skips the secret.

At the end, one email goes out listing the new and rotated secret names and versions (never values), and a separate alert is sent if the run fails.

In one line: Vault is the source of truth, the version tag in AKV is the memory, and only a new or higher version triggers a write and an email.