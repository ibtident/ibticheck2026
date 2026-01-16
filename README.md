# IBTI'CHECK® — Pré-tri prothétique & orientation (MVP)

**Version :** 2026-01-16  
**Stack :** Next.js (App Router) + Prisma (PostgreSQL) + Stripe (placeholder)

> ⚠️ IBTI'CHECK® n'effectue **aucun diagnostic médical**. Le produit réalise un **pré-tri technique** sur photos de prothèses (hors bouche) et peut orienter vers un **télé-avis dentaire**.

## Démarrage (local)

1. Installer les dépendances

```bash
pnpm install
```

2. Configurer une base PostgreSQL (Supabase/Neon/Vercel Postgres) et renseigner `DATABASE_URL` + `DIRECT_URL`

3. Lancer les migrations (si vous ajoutez des migrations Prisma)

```bash
pnpm prisma migrate dev
```

4. Démarrer

```bash
pnpm dev
```

### Variables d'environnement (exemple `.env.local`)

```
DATABASE_URL="postgresql://..."
DIRECT_URL="postgresql://..."
JWT_SECRET="change_me"

STRIPE_SECRET_KEY="sk_test_xxx"
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY="pk_test_xxx"
STRIPE_WEBHOOK_SECRET="whsec_xxx"

NODEMAILER_HOST="smtp.example.com"
NODEMAILER_PORT="587"
NODEMAILER_USER="..."
NODEMAILER_PASS="..."
```
