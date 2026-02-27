# EcoRide (SQL + Supabase Project)

EcoRide is a beginner-friendly university database project.
This guide explains exactly what to run, in what order.

## Team Branches

- `main` -> stable branch (final combined work)
- `harish` -> Harish's branch
- `virginia` -> Virginia's branch
- `yon` -> Yon's branch

Rule: everyone works in their own branch, then merges to `main`.

## Folder Guide

- `docs/ER_DIAGRAM_ECORIDE.png` -> ER diagram
- `sql/ddl/` -> table creation SQL
- `sql/dml/` -> insert/sample data SQL
- `sql/indexes/` -> indexes SQL
- `sql/queries/` -> output/demo queries
- `supabase/migrations/` -> migration files pushed to Supabase
- `.env.example` -> env template

## Part 1: First-Time Git Setup

Run these once.

1. Clone:

```bash
git clone https://github.com/harish885/ecoride.git
cd ecoride
```

Example: if you are Harish

```bash
git checkout harish
```

Example: if you are Virginia

```bash
git checkout virginia
```

Example: if you are Yon

```bash
git checkout yon
```

Check current branch:

```bash
git branch --show-current
```

## Part 2: Supabase Access You Need

This project uses one shared Supabase project.

Project info:

- Name: `EcoRide_Unicatt`
- Project ref: `coteafnoftedqsfeffho`
- URL: `https://coteafnoftedqsfeffho.supabase.co`

Each teammate must contact **Harish** to get:

- `SUPABASE_DB_PASSWORD` (required for `supabase link` and DB push)
- confirmation of active project ref/URL (if changed)

Each teammate should create their own Supabase access token from their own account.

## Part 3: Supabase Environment Setup

1. Create your local env file:

```bash
cp .env.example .env
```

2. Open `.env` and fill values:

- `SUPABASE_ANON_KEY`
- `SUPABASE_ACCESS_TOKEN`
- `SUPABASE_DB_PASSWORD` (ask Harish)

Important:

- `.env` is local only
- never commit `.env`

## Part 4: Install and Connect Supabase CLI

Install (macOS):

```bash
brew install supabase/tap/supabase
```

Check install:

```bash
supabase --version
```

Login to CLI:

```bash
supabase login
```

Link this repository to EcoRide project:

```bash
supabase link --project-ref coteafnoftedqsfeffho --password "$SUPABASE_DB_PASSWORD"
```

## Part 5: Daily Work Flow (Beginner Safe)

Run in this sequence every work session.

1. Switch to your branch:

```bash
git checkout <your-branch>
```

Example:

```bash
git checkout harish
```

2. Pull latest branch changes:

```bash
git pull origin <your-branch>
```

Example:

```bash
git pull origin harish
```

3. Bring latest `main` into your branch:

```bash
git fetch origin
git merge origin/main
```

4. Make SQL changes in `sql/` folders.

5. Create migration for your schema change:

```bash
supabase migration new add_ecoride_schema
```

6. Open new file in `supabase/migrations/` and paste SQL.

Example migration SQL:

```sql
-- =====================================
-- Create EcoRide Schema
-- =====================================
CREATE SCHEMA IF NOT EXISTS ecoride;
```

7. Push migration to Supabase DB:

```bash
supabase db push
```

8. Commit and push to GitHub:

```bash
git add .
git commit -m "Create ecoride schema migration"
git push origin <your-branch>
```

Example:

```bash
git push origin harish
```

## Part 6: Merge to Main

After your branch work is ready:

1. Open GitHub -> create PR from your branch to `main`.
2. Get review/approval.
3. Merge PR.

After merge, update local main:

```bash
git checkout main
git pull origin main
```

## Part 7: SQL Execution Order

When building schema, use this order:

1. `users.sql`
2. `stations.sql`
3. `bikes.sql`
4. `subscriptions.sql`
5. `rides.sql`
6. `maintenances.sql`

## Part 8: Common Commands Quick Reference

Current branch:

```bash
git branch --show-current
```

See changed files:

```bash
git status
```

Get latest from remote:

```bash
git fetch origin
```

Pull current branch:

```bash
git pull origin <your-branch>
```

Push current branch:

```bash
git push origin <your-branch>
```

Create migration:

```bash
supabase migration new <migration_name>
```

Apply migrations:

```bash
supabase db push
```

## Part 9: If Something Fails

- `supabase link` fails -> check project ref and DB password (ask Harish)
- `supabase db push` fails -> run `supabase link` again, then retry
- git conflicts -> resolve file, then `git add`, `git commit`, `git push`
