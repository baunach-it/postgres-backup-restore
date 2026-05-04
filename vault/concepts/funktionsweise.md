---
type: concept
repo: postgres-backup-restore
status: active
tags: [pg_dump, psql, migration, in-memory]
---

# Funktionsweise — postgres-backup-restore

Sichert die Quell-DB und stellt den Dump direkt in der Ziel-DB wieder her — alles in einem
Container-Run, ohne Zwischenablage in S3 oder einem Volume.

## Ablauf

1. **`pg_dump`** erstellt SQL-Dump der Quell-DB nach `/tmp/source_dump.sql`.
2. **`dos2unix`** normalisiert Zeilenumbrueche.
3. **`psql -f`** spielt den Dump in die Ziel-DB ein.

## Warum kein S3, kein Volume?

Das Image ist **fuer einen Use-Case** gebaut: DB-Kopie zwischen zwei erreichbaren Postgres-Servern
(meist Prod → Test). Persistenz, Versionierung und Retention machen hier keinen Sinn — wer einen
Snapshot will, nimmt `postgres-backup`.

## Konfiguration

**Quell-DB** (`POSTGRES_BACKUP_RESTORE_SOURCE_*`):
`DB_HOST`, `DB_PORT`, `USER`, `PASSWORD`, `DB_NAME`

**Ziel-DB** (`POSTGRES_BACKUP_RESTORE_TARGET_*`):
`DB_HOST`, `DB_PORT`, `USER`, `PASSWORD`, `DB_NAME`

## Caveat: Memory-Footprint

Dump liegt komplett in `/tmp` — bei sehr grossen DBs kann das Container-Memory eng werden.
Fuer grosse DBs `postgres-backup` (Volume) + `postgres-restore` (Volume oder S3) als zwei Schritte.

## Bezug

- Workspace-Vault: `stack/env-var-konventionen.md`
- Doku-Output: `docs/src/content/docs/projekte/docker-images/Postgres-Backup-Restore/uebersicht.md`
