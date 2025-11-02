# Database Schema (PostgreSQL)

- Requires PostgreSQL 13+
- Enables `pgcrypto` for UUIDs (`gen_random_uuid()`)
- Enables `btree_gist` to enforce non-overlapping bookings per property using an EXCLUDE constraint

## Run

```bash
psql -d your_db -f schema.sql
```