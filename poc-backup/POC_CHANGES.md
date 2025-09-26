# POC Work - File Changes Documentation

This directory contains backup copies of files that were modified/created for the POC work but are ignored by Git.

## Files Backed Up:

### Configuration Files:
- **`librechat.yaml.poc`** - Main LibreChat configuration file
  - Contains POC-specific settings and configurations
  - Original file: `librechat.yaml` (ignored by Git)

- **`docker-compose.override.yml.poc`** - Docker Compose overrides
  - Contains POC-specific Docker configuration
  - Original file: `docker-compose.override.yml` (ignored by Git)

### Environment Files:
- **`.env.poc`** - Environment variables
  - Contains POC-specific environment settings
  - Original file: `.env` (ignored by Git)

- **`.env.production.poc`** - Production environment variables
  - Contains POC-specific production settings
  - Original file: `.env.production` (ignored by Git)

### Data Files:
- **`violations.json.poc`** - Violations data
  - Contains data generated during POC work
  - Original file: `data/violations.json` (ignored by Git)

## Why These Files Are Ignored:

These files are listed in `.gitignore` because they typically contain:
- Environment-specific configurations
- Sensitive information (API keys, passwords)
- Runtime data that shouldn't be version controlled
- Local development settings

## To Restore POC Configuration:

1. Copy the `.poc` files back to their original locations:
   ```bash
   cp poc-backup/librechat.yaml.poc librechat.yaml
   cp poc-backup/docker-compose.override.yml.poc docker-compose.override.yml
   cp poc-backup/.env.poc .env
   cp poc-backup/.env.production.poc .env.production
   cp poc-backup/violations.json.poc data/violations.json
   ```

2. Or use the restore script (if created)

## Branch Information:
- POC Branch: `randy/mcp-demo`
- Created: September 26, 2025
- Files backed up: September 26, 2025

## Notes:
- These files contain the complete POC configuration
- Keep this backup safe as these changes are not tracked in Git
- Consider creating example/template versions for sharing (without sensitive data)
