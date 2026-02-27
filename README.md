# EcoRide (University SQL Project)

EcoRide is a team SQL implementation project for a bicycle ride-sharing system.

## Team Branch Setup

This repository is set up with these working branches:

- `main` -> stable integration branch
- `harish` -> Harish's working branch
- `virginia` -> Virginia's working branch
- `yon` -> Yon's working branch

### Important Rule

Each teammate should work only on their own branch and then merge changes into `main` after review.

## Project Structure

- `docs/ER_DIAGRAM_ECORIDE.png` -> ER diagram (source of truth for tables/relationships)
- `sql/ddl/` -> table creation scripts
- `sql/dml/` -> seed/sample data scripts
- `sql/indexes/` -> indexes for performance
- `sql/queries/` -> final query set for demo/report
- `supabase/migrations/` -> Supabase CLI migration files
- `.env.example` -> shared environment variable template

## One-Time Setup (Each Teammate)

If already cloned, skip to step 3.

1. Clone repo:

```bash
git clone https://github.com/harish885/ecoride.git
cd ecoride
```

2. Fetch all remote branches:

```bash
git fetch --all
```

3. Checkout your branch:

```bash
# Harish
git checkout harish

# Virginia
git checkout virginia

# Yon
git checkout yon
```

4. Verify branch:

```bash
git branch --show-current
```

## Supabase Setup (EcoRide_Unicatt)

Project details used for this repo:

- Project name: `EcoRide_Unicatt`
- Project ID / ref: `coteafnoftedqsfeffho`
- Project URL: `https://coteafnoftedqsfeffho.supabase.co`
- Security mode for now: basic working DB only (no RLS/policies yet)

### 1. Create local env file

```bash
cp .env.example .env
```

Fill these values in `.env`:

- `SUPABASE_ANON_KEY` -> your project's anon key
- `SUPABASE_ACCESS_TOKEN` -> your Supabase CLI access token

Do not commit `.env`.

### 2. Install Supabase CLI

macOS (Homebrew):

```bash
brew install supabase/tap/supabase
```

Verify:

```bash
supabase --version
```

### 3. Link this repo to the cloud Supabase project

```bash
supabase login
supabase link --project-ref coteafnoftedqsfeffho
```

### 4. Create and maintain migrations

Create a new migration when schema changes:

```bash
supabase migration new init_schema
```

This creates a SQL file under `supabase/migrations/`. Put table SQL in this order:

1. `users.sql`
2. `stations.sql`
3. `bikes.sql`
4. `subscriptions.sql`
5. `rides.sql`
6. `maintenances.sql`

Then append index SQL from `sql/indexes/` if needed.

### 5. Push schema changes to Supabase

```bash
supabase db push
```

### 6. Pull remote schema changes (if someone else pushed)

```bash
supabase db pull
```

## Suggested SQL + Supabase Workflow

1. Update your SQL source files in `sql/ddl/`.
2. Create a new migration (`supabase migration new <name>`).
3. Copy/finalize SQL in the migration file.
4. Run `supabase db push`.
5. Test in Supabase SQL editor.
6. Commit both your SQL source files (`sql/...`) and migration files (`supabase/migrations/...`).

## Daily Workflow (Pull -> Work -> Commit -> Push)

Run this flow every time before and after work.

1. Go to your branch:

```bash
git checkout <your-branch>
```

2. Pull latest updates from your branch:

```bash
git pull origin <your-branch>
```

3. Bring latest `main` into your branch (to avoid conflicts later):

```bash
git fetch origin
git merge origin/main
```

4. Make your SQL changes, then commit:

```bash
git add .
git commit -m "Add users and stations DDL"
```

5. Push your branch:

```bash
git push origin <your-branch>
```

Supabase sync in daily flow:

```bash
supabase db pull
```

## Merge into `main` (Example)

This is usually done by the integration owner (recommended: Harish) after checking teammate changes.

1. Update local `main`:

```bash
git checkout main
git pull origin main
```

2. Merge a teammate branch into `main`:

```bash
# example: merge virginia's completed work
git merge origin/virginia
```

3. Push updated `main`:

```bash
git push origin main
```

## Conflict Handling (Quick Example)

If merge shows conflicts:

1. Open conflicted file(s) and keep the correct SQL.
2. Mark resolved and commit:

```bash
git add <conflicted-file>
git commit -m "Resolve merge conflict in rides.sql"
```

3. Push again:

```bash
git push origin <current-branch>
```

## SQL Execution Order (Recommended)

When creating schema, run files in this order based on likely dependencies:

1. `users.sql`
2. `stations.sql`
3. `bikes.sql`
4. `subscriptions.sql`
5. `rides.sql`
6. `maintenances.sql`

## Current Status

- Team branches created and published:
  - `origin/harish`
  - `origin/virginia`
  - `origin/yon`
- ER diagram is available in `docs/ER_DIAGRAM_ECORIDE.png`
- SQL files are present and ready to be implemented
- Supabase migration folder initialized at `supabase/migrations/`
