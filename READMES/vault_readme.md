# JustEnoughVCS Server Setup

This directory contains the server configuration and data for `JustEnoughVCS`.

## User Authentication
To allow users to connect to this server, place their public keys in the `./key/` directory.
Each public key file should be named `{member_id}.pem` (e.g., `juliet.pem`), and contain the user's public key in PEM format.

**ECDSA:**

```bash
openssl genpkey -algorithm ed25519 -out your_name_private.pem
openssl pkey -in your_name_private.pem -pubout -out your_name.pem
```

**RSA:**
```bash
openssl genpkey -algorithm RSA -out your_name_private.pem -pkeyopt rsa_keygen_bits:2048
openssl pkey -in your_name_private.pem -pubout -out your_name.pem
```

**DSA:**
```bash
openssl genpkey -algorithm DSA -out your_name_private.pem -pkeyopt dsa_paramgen_bits:2048
openssl pkey -in your_name_private.pem -pubout -out your_name.pem
```

Place only the `your_name.pem` file in the server's `./key/` directory, renamed to match the user's member ID.

## File Storage
All version-controlled files (Virtual File) are stored in the `./storage/` directory.

## License
This software is distributed under the MIT License. For complete license details, please see the main repository homepage.

## Support
Repository: `https://github.com/JustEnoughVCS/VersionControl`
Please report any issues or questions on the GitHub issue tracker.

## Thanks :)
Thank you for using `JustEnoughVCS!`