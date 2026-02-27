# EcoRide (SQL + Supabase Project)

This guide explains exactly what to run, in what order.

## Team Branches

- `main` -> stable branch (final combined work)
- `harish` -> my branch
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

Run once.

```bash
git clone https://github.com/harish885/ecoride.git
cd ecoride
git fetch --all
```

Checkout your branch:

```bash
# me
git checkout harish

# Virginia
git checkout virginia

# Yon
git checkout yon
```

Check current branch:

```bash
git branch --show-current
```

## Part 2: Supabase Model (Very Important)

We use **one shared Supabase project** for the whole team.

Project info:

- Name: `EcoRide_Unicatt`
- Project ref: `coteafnoftedqsfeffho`
- URL: `https://coteafnoftedqsfeffho.supabase.co`

Virginia and Yon should **not** create a new Supabase project or database.
They should connect to this same shared project.

## Part 3: What Each Person Needs for `.env`

Each teammate creates their own local `.env` file from template.

macOS/Linux:

```bash
cp .env.example .env
```

Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Fill these values:

1. `SUPABASE_ANON_KEY`
- Shared project key.
- I will share this with teammates.

2. `SUPABASE_ACCESS_TOKEN`
- Personal token for each teammate.
- Each person creates their own token at:
  [https://supabase.com/dashboard/account/tokens](https://supabase.com/dashboard/account/tokens)

3. `SUPABASE_DB_PASSWORD`
- Shared project DB password.
- Teammates should contact me to get this.

Important:

- `.env` is local only
- never commit `.env`

## Part 4: Install Supabase CLI

### macOS (Homebrew)

```bash
brew install supabase/tap/supabase
supabase --version
```

### Windows (Scoop)

```powershell
scoop bucket add supabase https://github.com/supabase/scoop-bucket.git
scoop install supabase
supabase --version
```

If Scoop is not installed, install Scoop first:

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
irm get.scoop.sh | iex
```

## Part 5: Connect Local Repo to Supabase Project

Login:

```bash
supabase login
```

Link repo to shared project:

macOS/Linux:

```bash
supabase link --project-ref coteafnoftedqsfeffho --password "$SUPABASE_DB_PASSWORD"
```

Windows PowerShell:

```powershell
supabase link --project-ref coteafnoftedqsfeffho --password "$env:SUPABASE_DB_PASSWORD"
```

## Part 6: Daily Work Flow

1. Switch to your branch:

```bash
git checkout <your-branch>
```

Example:

```bash
git checkout harish
```

2. Pull latest branch updates:

```bash
git pull origin <your-branch>
```

3. Merge latest `main` into your branch:

```bash
git fetch origin
git merge origin/main
```

4. Make SQL changes in `sql/` files.

5. Create migration:

```bash
supabase migration new add_ecoride_schema
```

6. Put SQL in the new migration file under `supabase/migrations/`.

Example:

```sql
-- =====================================
-- Create EcoRide Schema
-- =====================================
CREATE SCHEMA IF NOT EXISTS ecoride;
```

7. Push migration to cloud DB:

```bash
supabase db push
```

8. Commit and push your branch:

```bash
git add .
git commit -m "Create ecoride schema migration"
git push origin <your-branch>
```

## Part 7: Merge to Main (GitHub)

1. Open GitHub.
2. Create PR from your branch to `main`.
3. Get approval.
4. Merge PR.

Then update local `main`:

```bash
git checkout main
git pull origin main
```

## Part 8: Sync All Branches With Main

```bash
git checkout main
git pull origin main

git checkout harish
git merge main
git push origin harish

git checkout virginia
git merge main
git push origin virginia

git checkout yon
git merge main
git push origin yon

git checkout main
```

## Part 9: SQL Execution Order

1. `users.sql`
2. `stations.sql`
3. `bikes.sql`
4. `subscriptions.sql`
5. `rides.sql`
6. `maintenances.sql`

## Part 10: Common Issues

- `supabase link` fails:
  - verify project ref is `coteafnoftedqsfeffho`
  - verify `SUPABASE_DB_PASSWORD` (contact me)
- `supabase db push` fails:
  - run `supabase link` again
  - rerun `supabase db push`
- git merge conflict:
  - resolve file
  - `git add <file>`
  - `git commit`
  - `git push`
