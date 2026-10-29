# Docker Image to Backup & Restore Postgres databases
This image is based on a standard postgres image and supports backup & restore using pg_dump in one go.

[Dockerfile](https://github.com/baunach-it/postgres-backup-restore/blob/main/Dockerfile)

## Usage
Create a .env file in the desired location
```bash
POSTGRES_BACKUP_RESTORE_SOURCE_DB_HOST=localhost
POSTGRES_BACKUP_RESTORE_SOURCE_DB_PORT=5432
POSTGRES_BACKUP_RESTORE_SOURCE_USER=postgres
POSTGRES_BACKUP_RESTORE_SOURCE_PASSWORD=mypassword
POSTGRES_BACKUP_RESTORE_SOURCE_DB_NAME=source_db

POSTGRES_BACKUP_RESTORE_TARGET_DB_HOST=localhost
POSTGRES_BACKUP_RESTORE_TARGET_DB_PORT=5432
POSTGRES_BACKUP_RESTORE_TARGET_USER=postgres
POSTGRES_BACKUP_RESTORE_TARGET_PASSWORD=mypassword
POSTGRES_BACKUP_RESTORE_TARGET_DB_NAME=target_db
```
then reference the .env file when running the container
```bash
docker run --rm --env-file .env --network desired-network baunach/postgres-backup-restore:{VERSION}
```

## License
The Dockerfile and scripts in this repository are licensed under [MIT-0](LICENSE).

The image contains third-party software that is subject to its own licenses, including:
- PostgreSQL from the official `postgres` base image: PostgreSQL License
- Debian packages of the base image and those installed by the Dockerfile (`ca-certificates`, `dos2unix`, `gzip`, `curl`, `unzip`): their respective licenses
