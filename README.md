# ComparaMiAfore (CMA) v3.0

Aplicación web para comparar AFORE/SIEFORE en México basada en el **Índice de Rendimiento Neto (IRN)** oficial de CONSAR.

## Arquitectura

```
CONSAR (fuente oficial)
    ↓
Pipeline de adquisición (scripts/)
    ↓
Cloudflare D1 (fuente canónica)
    ↓
┌──────────────────┬──────────────────────┬──────────────────┐
│  Worker (API)    │  JSON estático      │  Admin Dashboard │
│  Hono + Drizzle  │  irn-current.json   │  Analytics BI    │
└────────┬─────────┴──────────┬──────────┴────────┬─────────┘
         │                    │                   │
         └──────────┬─────────┘                   │
                    ↓                             ↓
              Frontend público              Módulo Admin
              (comparación)                 (login + BI)
```

## Stack

| Capa | Tecnología |
|------|------------|
| Frontend público | Vite + React 19 + TypeScript + Tailwind + Recharts |
| Admin Dashboard | Vite + React 19 + TypeScript + Tailwind + Recharts |
| Backend | Cloudflare Workers + Hono + Drizzle ORM |
| Base de datos | Cloudflare D1 (SQLite) |
| PDF | pdf-lib |
| Monorepo | pnpm workspaces |

## Inicio rápido

```bash
pnpm install
pnpm dev:web      # http://localhost:5173
pnpm dev:admin    # http://localhost:5174
pnpm dev:worker   # API Worker
pnpm db:migrate
```

Admin login: `ADMIN_API_KEY` de `wrangler.toml` (default: `change-me-in-production`).

API comercial demo key: `cma_demo_key_2026`

Ver `DEPLOY.md` para publicación en Cloudflare Pages/Workers.

## Licencia

Uso educativo / no oficial. No sustituye a CONSAR.
