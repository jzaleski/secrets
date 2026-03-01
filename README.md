# secrets

A simple CLI toolset for managing encrypted secrets using GPG

## Tools

All tools are located in the `bin/` directory:

- **bin/encrypt-secrets** - Encrypts the `secrets` directory and increments the version
- **bin/decrypt-secrets** - Decrypts and extracts the secrets archive
- **bin/check-secrets** - Verifies the secrets directory is up to date
- **scripts/build-release** - Bumps version and creates release tarball

## Requirements

- GPG (GNU Privacy Guard)
- macOS with Homebrew recommended: `brew install gpg`

## Environment Variables

- `SECRETS_PASSPHRASE` - Password used to encrypt/decrypt secrets
- `SECRETS_CIPHER_ALGO` - Optional, defaults to `AES256`

## Usage

### Setup

1. Create a `secrets` directory with your sensitive files
2. Run `SECRETS_PASSPHRASE="your-passphrase" bin/encrypt-secrets` to encrypt the directory

### Workflow

**To decrypt secrets:**
```bash
SECRETS_PASSPHRASE="your-passphrase" bin/decrypt-secrets
```

**To update and re-encrypt:**
```bash
SECRETS_PASSPHRASE="your-passphrase" bin/encrypt-secrets
```

**To verify secrets are current:**
```bash
bin/check-secrets
```

**To create a release:**
```bash
scripts/build-release
```

## How It Works

- Secrets are stored in a `secrets/` directory
- The directory is tarred, gzipped, and GPG-encrypted to `secrets.tar.gz.gpg`
- A version file (`secrets/secrets.version`) tracks changes
- The encrypted archive is locked with `secrets.lock` to prevent version conflicts
