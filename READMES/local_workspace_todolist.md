# Get Started - Local Workspace

This directory is a **Local Workspace** managed by `JustEnoughVCS`. All files and subdirectories within this scope can be version-controlled using the `JustEnoughVCS` CLI or GUI tools, with the following exceptions:

- The `.jv` directory
- Any files or directories excluded via `IGNORE_RULES.toml`

> [!NOTE]
>
> Files in this workspace will be uploaded to the upstream server. Please ensure you fully trust this server before proceeding.



## TODO LIST

We've prepared a checklist to help you set up your local workspace in order:

> [!TIP]
>
> The following assumes you're using the command line. If you're using the GUI, you can skip these setup steps.

- [ ] **Set up account**

  First, register your account on your local machine:

  ```bash
  # Register your account
  # Use `--keygen` to generate private key
  jv account + YOUR_NAME --keygen
  
  # Set current workspace to use your account
  jv as YOUR_NAME
  ```

- [ ] **Register keys** (Manual)

  To connect to the server, you'll need to generate asymmetric keys for your account.

  You can use `openssl` to create keys, for example an ED25519 key:

  ```bash
  # Generate private key
  openssl genpkey -algorithm ed25519 -out YOUR_NAME_PRIVATE.pem
  
  # Generate public key from private key
  openssl pkey -in YOUR_NAME_PRIVATE.pem -pubout -out YOUR_NAME_PUBLIC.pem
  # If you registered private key, you can
  # jv account genpub YOUR_NAME ./ # Generate public key here
  ```

  After generating the key files, register them to your account:

  ```bash
  # Move private key to key registry
  jv account mvkey YOUR_NAME YOUR_NAME_PRIVATE.pem
  
  # (Optional) List all accounts to verify private key registration
  # jv accounts
  ```

  You should still have a public key file (called `YOUR_NAME_PUBLIC.pem` in this example) - provide this to the upstream repository administrator.

- [ ] **Provide public key to upstream repository administrator**

- [ ] **Connect to server**

  Once the administrator registers your public key, you can connect to the server:

  ```bash
  # Connect workspace to upstream repository (no confirmation)
  # jv direct <UPSTREAM_ADDR> -C
  ```

  > ![TIP]
  >
  > You can use the following command to login to the upstream more easily.

  ```bash
  jv login <YOUR_ACCOUNT> <UPSTREAM_ADDR> -C
  # =
  # jv as <YOUR_ACCOUNT>
  # jv direct <UPSTREAM_ADDR> -C
  # jv update
  # rm SETUP.md # Delete this document to keep workspace clean
  ```

  

- [ ] **Create or use a sheet**

  First, update your local information:

  ```bash
  jv u # Update local information
  ```

  If you've worked in this upstream repository before, you should see your sheets:

  ```bash
  jv sheets # View all sheets
  ```

  If you don't have a sheet, create one:

  ```bash
  jv make your_sheet # Create sheet
  jv u # Sync after upstream changes
  ```

- [ ] **Final steps**

  After completing the above steps, your workspace is connected to the upstream repository.

  Now delete this document to keep your workspace clean, and use this command to start working:

  ```bash
  jv use your_sheet # Use the sheet you just created to begin work
  ```



## Support

- **Permission or access issues?** → Contact your server administrator
- **Tooling problems or bugs?** → Reach out to the development team via [GitHub Issues](https://github.com/JustEnoughVCS/VersionControl/issues)
- **Documentation**: Visit our repository for full documentation

------

*Thank you for using JustEnoughVCS!*
