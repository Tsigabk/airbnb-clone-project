# Database Seed

Order of operations (after running `schema.sql`):

```bash
psql -d your_db -f ../database-script-0x02/seed.sql
```

Notes:
- Uses fixed UUIDs for reproducibility.
- Dates are set in 2025/2026 to avoid conflicts with `EXCLUDE` constraint examples.