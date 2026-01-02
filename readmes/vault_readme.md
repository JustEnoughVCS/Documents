# Setup an Upstream Vault

Thank you for using `JustEnoughVCS`.

This document guides you through setting up an **Upstream Vault** — a shared source of structure and content that other workspaces may depend on.

## Configuration File

Before starting the Vault service with `jvv listen`, you need to configure `vault.toml`.

This file defines the identity, connectivity, and responsibility boundaries of the Vault.

### Adding Hosts

Set the `hosts` parameter to specify which members are allowed to switch into the **Host** role for this Vault.

```toml
# Pan and Alice are allowed to operate this Vault as hosts
hosts = [ "pan", "alice" ]
```

Members listed here can switch their identity as follows:

```bash
jv as host/pan
```

> Becoming a Host means operating from a position that may affect other members.
> This role is not a permanent identity, but a responsibility-bearing context.

### Configuring Connection

Modify the `bind` parameter to `0.0.0.0` to allow access from other devices on the local network.

```toml
bind = "0.0.0.0"
```

> [!TIP]
> `JustEnoughVCS` uses port **25331** by default.
> You can change the listening port by modifying the `port` parameter if needed.

### Disabling Logger (Optional)

If you prefer a cleaner console output, you can disable logging:

```toml
logger = "no"
```

## Member Account Setup

Run the following command in the root directory of the **Vault** to register a member:

```bash
jvv member register pan
```

Registering a member only creates its identity record in the Vault.
It does **not** automatically make the member login-ready.

An authentication method must be registered separately.

> [!NOTE]
> Currently, `JustEnoughVCS` supports **key-based authentication** only.

Place the public key file provided by the member (`name.pem`) into the Vault’s `./key` directory.

For example, after registering a member named `pan`, the Vault directory structure should look like this:

```
.
├── key
│   └── pan.pem      <- Public key file
├── members
│   ├── pan.bcfg     <- Member registration info
│   └── host.bcfg
├── README.md
├── sheets
│   └── ref.bcfg
├── storage
└── vault.toml
```

## Completion

At this point, the Vault is fully configured:

* Member identities are registered
* Host roles are defined
* Authentication materials are in place

You can now start the Vault service using:

```bash
jvv listen
```

Other workspaces may connect to this Vault once it is listening.
