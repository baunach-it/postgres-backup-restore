---
type: index
repo: postgres-backup-restore
workspace: baunach-postgres
tenant: baunach
---

# postgres-backup-restore Repo-Vault

Image-spezifische Doku fuer `postgres-backup-restore` (kombiniertes Image, in-memory Migration).

## Inhalt

- `concepts/funktionsweise.md` — Ablauf: pg_dump (Source) → /tmp → dos2unix → psql (Target)
- `decisions/` — Image-spezifische Entscheidungen (TBD)
- `playbooks/` — Image-spezifische Prozeduren (TBD)
- `troubleshooting/` — Fehlerbilder

## Besonderheit: kein S3, kein Volume

Anders als `postgres-backup` und `postgres-restore` arbeitet dieses Image vollstaendig
in-memory ueber `/tmp`. Use-Case: 1-Schritt-Migration zwischen Umgebungen (z.B. Prod → Test).

## Cross-Image-Themen → Workspace-Vault

- Praefix-Pattern: `concepts/env-var-prefix-pattern.md`
- Image-Konventionen: `stack/image-konventionen.md`
- Env-Var-Tabellen: `stack/env-var-konventionen.md`
- Project-MOC: `projects/postgres-backup-restore.md`

## Doku-Output

`docs/src/content/docs/projekte/docker-images/Postgres-Backup-Restore/`
