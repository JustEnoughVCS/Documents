# Setup a Workspace

You have created an empty local **Workspace** using `jv create` or `jv init`.

At this point, the workspace exists only as a local structure.
It is **not yet associated with any identity or upstream Vault**.

Follow the steps below to complete the initial setup.

## Account Setup

> [!TIP]
> If you have already registered an account on this machine, you can skip this section.

An account represents **this machine acting on your behalf**.
You can create an account and generate a private key using the following commands.

```bash
# Make sure OpenSSL is installed on your system.
# Create an account and automatically generate a private key using OpenSSL.
jv account add pan --keygen

# If you already have a private key, you can associate it with an account.
jv account movekey pan ./your_private_key.pem
```

After creating the private key, generate the corresponding public key.
This also requires `OpenSSL` support.

```bash
# Generate the public key in the current directory.
jv account genpub pan ./
```

**Send the generated public key file to a Host of the upstream Vault.**
Only after the key is registered by the Vault can this workspace authenticate.

## Login

> In the following example, we assume:
>
> * the account name is `pan`
> * the upstream Vault address is `127.0.0.1`

Navigate to the workspace directory (the directory containing this file), then run:

```bash
# Log in as pan to the upstream Vault at 127.0.0.1
# -C skips confirmation prompts
jv login pan 127.0.0.1 -C
```

This command performs the following steps internally:

```bash
jv account as pan        # Bind the workspace to account pan
jv direct 127.0.0.1 -C   # Set the upstream Vault address
jv update                # Fetch initial structure and metadata from upstream
rm SETUP.md              # Remove this setup document
```

After login, the workspace becomes a **live participant** connected to the upstream Vault.

## Completion

At this point, the workspace is fully set up:

* An account identity is bound locally
* An upstream Vault is configured
* Initial data has been synchronized

Normally, `jv login` removes this file automatically.
If the file still exists due to a deletion failure, please remove it manually to keep the workspace clean.

Once this file is gone, the workspace is considered **ready for daily use**.

## Why does this file delete itself?

A freshly created JVCS workspace is considered **clean** only when no sheets are in use and no unexplained files exist.

During the initial setup phase, this `SETUP.md` file is the only allowed exception.
It exists solely to guide the workspace into a connected and explainable state.

Once the workspace is connected to an upstream Vault and enters normal operation,
every file in the workspace is expected to be **explainable by structure**.

If this setup file remains:

* it becomes an unexplained local file
* `JustEnoughVCS` cannot determine which sheet it belongs to
* and any subsequent `jv use` operation would be ambiguous

To prevent this ambiguity, JVCS enforces a strict rule:

**A workspace with unexplained files is not allowed to enter active use.**

Deleting `SETUP.md` marks the end of the setup phase and confirms that:

* all remaining files are intentional
* their placement can be explained
* and the workspace is ready to participate in structure-driven operations

This is why the setup document removes itself.
It is not cleanup — it is a boundary.
