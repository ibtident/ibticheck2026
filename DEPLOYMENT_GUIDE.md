# Guide de Déploiement Permanent : ibticheck-platform sur Vercel

Ce document détaille les étapes nécessaires pour déployer l'application **ibticheck-platform** de manière permanente en utilisant **Vercel** et une base de données **PostgreSQL**.

## 1. Prérequis Techniques

Avant de commencer, assurez-vous de disposer des éléments suivants :
*   Un compte [Vercel](https://vercel.com/) actif.
*   Une base de données **PostgreSQL** (ex: [Vercel Postgres](https://vercel.com/docs/storage/vercel-postgres), [Supabase](https://supabase.com/), ou [Neon](https://neon.tech/)).
*   Le code source du projet (fourni dans l'archive modifiée).

## 2. Configuration de la Base de Données

Le projet a été configuré pour utiliser **Prisma** avec PostgreSQL. Vous devrez obtenir deux URLs de connexion de votre fournisseur de base de données :

| Variable | Description | Exemple |
| :--- | :--- | :--- |
| `DATABASE_URL` | URL de connexion principale (avec pooling de sessions) | `postgres://user:pass@host:5432/db?pgbouncer=true` |
| `DIRECT_URL` | URL de connexion directe (pour les migrations Prisma) | `postgres://user:pass@host:5432/db` |

## 3. Variables d'Environnement à Configurer

Dans votre tableau de bord Vercel (**Settings > Environment Variables**), ajoutez les variables suivantes :

### Base de Données et Sécurité
*   `DATABASE_URL` : (Voir tableau ci-dessus)
*   `DIRECT_URL` : (Voir tableau ci-dessus)
*   `JWT_SECRET` : Une chaîne de caractères aléatoire et complexe pour sécuriser les tokens.

### Intégration Stripe (Paiements)
*   `STRIPE_SECRET_KEY` : Votre clé secrète Stripe (commence par `sk_`).
*   `NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY` : Votre clé publique Stripe (commence par `pk_`).
*   `STRIPE_WEBHOOK_SECRET` : Obtenue après avoir configuré le webhook dans le dashboard Stripe.

### Service Email (Nodemailer)
*   `NODEMAILER_HOST` : Serveur SMTP (ex: `smtp.resend.com` ou `smtp.gmail.com`).
*   `NODEMAILER_PORT` : Généralement `587` ou `465`.
*   `NODEMAILER_USER` : Votre identifiant SMTP.
*   `NODEMAILER_PASS` : Votre mot de passe SMTP ou clé d'API.

## 4. Étapes de Déploiement

1.  **Importer le projet** : Connectez votre dépôt Git (GitHub/GitLab) à Vercel ou utilisez la CLI Vercel (`vercel deploy`).
2.  **Configurer le Build** :
    *   Framework Preset : `Next.js`
    *   Build Command : `pnpm run build`
    *   Install Command : `pnpm install`
3.  **Lancer le Déploiement** : Vercel exécutera automatiquement `prisma generate` et `next build`.

## 5. Maintenance et Mises à jour

Pour mettre à jour le schéma de la base de données après une modification du fichier `schema.prisma`, exécutez localement :
```bash
npx prisma migrate dev
```
Puis poussez les changements sur votre branche principale pour déclencher un nouveau déploiement Vercel.

---
*Document généré par **Manus AI** le 15 Janvier 2026.*
