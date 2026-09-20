# Apply Create Contract filter on main (`cpercibal2018-cmyk/nurse_appV03`)

The GitHub App connected to this workspace can **read** `cpercibal2018-cmyk/nurse_appV03` but gets **403** on write. Apply locally (or grant the app write access to that repo/org), then push.

## Option A — one-liner patch

```bash
cd nurse_appV03   # clone of https://github.com/cpercibal2018-cmyk/nurse_appV03.git
git checkout main && git pull

curl -sL https://raw.githubusercontent.com/percibalvillegas18/nurse_appV03/main/patches/create-contract-filter.patch | git apply

git add app/src/lib/store.tsx app/src/modules/contracts/ContractsPage.tsx
git commit -m "feat(contracts): Create dropdown = no Approved/Active; onboard creates Draft"
git push origin main
```

## What changes

1. **`app/src/lib/store.tsx`** — Onboard Atomically creates contract status **`Draft`** (was `Approved`).
2. **`app/src/modules/contracts/ContractsPage.tsx`** — Create Contract employee dropdown uses `createContractEmployees` (no Approved/Active coverage; newest hireDate first).

## After apply

1. Workforce → Onboard Employee → new hire gets **Draft** contract.
2. Contracts → **Create Contract (New Employee)** → dropdown shows that hire (and any other without Approved/Active).
3. After **Approved/Active**, they leave Create list; use **Renew Contract** later.
4. Clear site localStorage once if an old demo session still has Approved onboard contracts.

## Grant write so the assistant can push next time

Reconnect the GitHub connector and allow access to **`cpercibal2018-cmyk/nurse_appV03`** (org/user must install/authorize the app with Contents: Write).
