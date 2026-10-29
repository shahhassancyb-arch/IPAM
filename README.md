# Prefix Manager (IPAM)

A Django 5.2-era reconstruction based on the supplied technical specification. This workspace did not contain the original `ipam_source.tar.gz`, so this is a fresh implementation from the document, not a source-faithful rebuild. Import workbook mappings, some admin workflows, and undocumented behavior require verification against the original application/data.

## Local development

```sh
python -m venv .venv
. .venv/bin/activate
pip install -r requirements.txt
export DJANGO_SECRET_KEY='replace-me'
export DJANGO_DEBUG=1
export DB_ENGINE=django.db.backends.sqlite3
export DB_NAME=./db.sqlite3
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver 0.0.0.0:8000
```

PostgreSQL is the default backend. Configure `DB_NAME`, `DB_USER`, `DB_PASSWORD`, `DB_HOST`, and `DB_PORT`. Set `DJANGO_ALLOWED_HOSTS` to a comma-separated host list and set `DJANGO_DEBUG=0` in production. Never commit secrets.

## Implemented areas

- Region, hierarchical Section, City, Prefix, SectionPermission, and AuditEvent models.
- Strict canonical CIDR validation, derived network metadata, parent/child containment checks, and soft deletion.
- Login/logout, idle timeout, staff management pages, inherited section access checks on key inventory endpoints.
- Dashboard pool and capacity calculations, inventory filters, CSV import/export, basic XLSX import, space map with manual Full/Free parent override, reports, and bulk deletion/move.

## Important scope gaps

This reconstruction is not production-ready without review. The original archive was not present, so the supplied specification is the only source. In particular, confirm exact PHPIPAM workbook headers, section/city management behavior, classification conventions, authorization of every route, audit coverage, and production dependency versions. Global overlap prevention is not implemented at the model layer. The UI is a functional starting point rather than a pixel-identical recreation.

## Checks

```sh
python manage.py check
python manage.py test
python manage.py makemigrations --check --dry-run
```
