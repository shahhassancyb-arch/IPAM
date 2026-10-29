# Build status and verification

## What was delivered

A fresh Django project reconstructed from the pasted IPAM specification. The original `ipam_source.tar.gz` was not present in the workspace, so this is a specification-based implementation and cannot reproduce source-only details that are not described in the handover.

## Verification performed

- `python manage.py check` — passed.
- `python manage.py test` — 9 tests passed, covering strict CIDR validation, parent containment, inherited permission precedence, dashboard counts/free-block drilldown, manual Full/Free state, audit writes, and tree rename.
- `python manage.py makemigrations --check --dry-run` — no model changes pending.
- Staff smoke check: dashboard, inventory, add form, IP segregation, sections, regions, cities, permissions, users, audit, reports, CSV import, and phpIPAM import returned HTTP 200.

## Before production

1. Compare this implementation with the actual archived source and database conventions.
2. Pin reviewed Python and OS package versions; configure secrets and `DJANGO_ALLOWED_HOSTS`.
3. Confirm PostgreSQL schema/data migration, overlap policy, classification labels, and phpIPAM workbook headers.
4. Complete security review of all management routes and test section-permission scenarios against intended operational policy.
5. Add representative seed data and run the documented acceptance matrix in a staging environment.
