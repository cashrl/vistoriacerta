# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Current State

The repository contains the **"Vistoria Certa"** project — a complete property inspection SaaS platform.

- **Backend**: NestJS + TypeORM + SQLite. Fully implemented: JWT auth (access + refresh), RBAC, CRUD for users, properties, inspections, environments, items, signatures, reports (PDF). Seed script ready. Runs on **port 3002**. Photos storage configured with Supabase.
- **Web**: Next.js 15 + Tailwind + Shadcn/UI. API client with auto token refresh (`src/lib/api.ts`), React Query hooks (`useApi.ts`), dashboard, properties, inspections, schedules, comparative, and report pages.
- **Mobile**: React Native + Expo. 12 screens implementadas. Local SQLite via `expo-sqlite`. `sync.ts` completo (NetInfo ativo, token JWT enviado via AsyncStorage). Login mobile criado.

---

## Project Structure

```
vistoria-certa/
├── backend/              // NestJS API (porta 3002)
│   └── src/
│       ├── auth/         // JWT, guards, strategy
│       ├── users/        // Users & Companies
│       ├── properties/   // Property CRUD ✅
│       ├── inspections/  // Inspection CRUD + /sync endpoint ✅
│       ├── environments/ // Environment CRUD ✅
│       ├── items/        // Item CRUD ✅
│       ├── photos/       // Upload handler com Supabase Storage configurado ✅
│       ├── signatures/   // Digital signatures ✅
│       ├── reports/      // PDF generation ✅
│       ├── ai/           // AI module
│       └── notifications/ // Push notifications (backend pronto, mobile integrado)
├── web/                  // Next.js 15 dashboard (porta 3001)
│   └── src/app/
│       ├── page.tsx                          // Dashboard ✅ conectado à API
│       ├── login/page.tsx                    // Login JWT ✅
│       ├── properties/
│       │   ├── page.tsx                      // Listagem ✅
│       │   └── new/page.tsx                  // Formulário criação ✅
│       ├── inspections/
│       │   ├── page.tsx                      // Listagem + download PDF ✅
│       │   ├── new/page.tsx                  // Formulário criação ✅
│       │   └── [id]/report/page.tsx          // ✅ CRIADO — laudo completo com dados da API
│       ├── schedules/page.tsx                // Agendamentos ✅ (design Stitch)
│       └── comparative/page.tsx              // Comparativo de ambientes ✅ (design Stitch)
├── mobile/               // React Native + Expo (Android/iOS)
│   ├── screens/
│   │   ├── HomeScreen.tsx                    // ✅
│   │   ├── PropertiesScreen.tsx              // ✅
│   │   ├── PropertyDetailScreen.tsx          // ✅
│   │   ├── NewPropertyScreen.tsx             // ✅
│   │   ├── NewInspectionScreen.tsx           // ✅
│   │   ├── InspectionChecklistScreen.tsx     // ✅
│   │   ├── PhotoCaptureScreen.tsx            // ✅
│   │   ├── InspectionSummaryScreen.tsx       // ✅
│   │   ├── ReportsScreen.tsx                 // ✅
│   │   └── ProfileScreen.tsx                 // ✅
│   │   // ✅ LoginScreen.tsx — CRIADO com JWT + AsyncStorage
│   │   // ✅ SincronizacaoOfflineScreen.tsx — CRIADO com sync real
│   ├── services/
│   │   ├── database.ts                       // SQLite local CRUD ✅
│   │   └── sync.ts                           // ✅ COMPLETO — NetInfo + JWT token + listener online (fotos pendente)
│   └── App.tsx                               // Navegação com todas as rotas
└── docs/                 // Stitch screens HTML + PNGs baixados
    └── stitch-screens/   // 13 telas exportadas do Stitch (design de referência)
```

---

## Development Commands

### Backend (`backend/`)
```bash
npm run start:dev   # Servidor dev com auto-reload (http://localhost:3002)
npm run seed        # Reset + popular banco SQLite
npm run build       # Build produção
```

### Web (`web/`)
```bash
npm run dev                      # Dev server (http://localhost:3001)
npm install --legacy-peer-deps   # Instalar deps (React 19 peer dep issue)
```

### Mobile (`mobile/`)
```bash
npx expo start      # Expo dev server
npx expo start --android  # Direto no Android
```

### Workflow
1. `cd backend && npm run start:dev`
2. `cd web && npm run dev`
3. `cd mobile && npx expo start`
4. Seed: `cd backend && npm run seed`

---

## ❌ O Que Falta (Por Prioridade)

### 🔴 ALTA — Sem isso o app não está completo

| Item | Localização | Status |
|---|---|---|
| `page.tsx` do laudo online | `web/src/app/inspections/[id]/report/` | ✅ **CRIADO** — laudo dinâmico com dados da API |
| Login screen (Mobile) | `mobile/screens/LoginScreen.tsx` | ✅ **CRIADO** — JWT + AsyncStorage + demo credentials |
| NetInfo real (Mobile) | `mobile/services/sync.ts` | ✅ **CORRIGIDO** — `isOnline()` usa NetInfo real |
| Auth token no sync (Mobile) | `mobile/services/sync.ts` | ✅ **CORRIGIDO** — Bearer token do AsyncStorage |
| Upload de fotos (Mobile→Backend) | `mobile/services/sync.ts` | ✅ **CORRIGIDO** — envio real de fotos integrado via Supabase |
| Tela Sincronização Offline | `mobile/screens/SincronizacaoOfflineScreen.tsx` | ✅ **CRIADO** — design Stitch implementado |

### 🟡 MÉDIA — Funcionalidades importantes

| Item | Localização | Status |
|---|---|---|
| Assinaturas digitais (Web UI) | `web/src/app/signatures/page.tsx` | ✅ **CRIADO** — canvas de assinatura + API integration |
| Cloud storage (fotos) | `backend/src/photos/` | ✅ **Supabase Storage configurado e testado** |
| Notificações push (Mobile) | `mobile/` | ✅ Backend pronto, mobile integrado |
| Fila offline (Mobile) | `mobile/services/` | ✅ **IMPLEMENTADO** — fila de sincronização para properties e vistorias offline |

### 🟢 BAIXA — Produção

| Item | Detalhe |
|---|---|
| Deploy Web | Vercel + variáveis de ambiente |
| Deploy Backend | Suporte a PostgreSQL integrado no app.module.ts |
| CI/CD | ✅ **CRIADO** — Pipeline GitHub Actions configurada em ci.yml |

---

## Known Issues / Important Notes

- **Port conflict**: Backend = 3002, Web = 3001 (ou 3000). Configurado em `backend/.env`.
- **JWT no Web**: Tokens em `localStorage` (`accessToken`, `refreshToken`, `user`). `/login` redireciona não-autenticados.
- **Mobile SQLite**: `database.ts` usa `expo-sqlite` com padrão `tx.executeSql`. O método `execAsync<T>` retorna rows corretamente para SELECT, void para mutations.
- **Tailwind**: Requer `postcss.config.js` na raiz de `web/` (já criado).
- **Legacy peer deps**: Web requer `npm install --legacy-peer-deps` por conta do React 19.
- **Stitch screens**: 13 telas HTML + PNG em `docs/stitch-screens/` — usar como referência de design para implementações futuras.
- **API Key Stitch**: `AQ.Ab8RN6IeQ4e6SAAz6kFhAE2IqaIyAB68FIazLpFQGj-68oyGsQ` (Project ID: `2205928003718490638`)
- **Supabase Configuration**: 
  - URL: `https://didcsbhquuqgadsxjpwr.supabase.co`
  - Bucket: `photos` (public)
  - Environment variables set in `backend/.env`
  - Upload endpoint tested and functional

---

## Goals & Progress

```
Backend   ██████████████  100% ✅ Pronto com upload de fotos no mobile
Web       █████████████░  90%  ✅ /report page.tsx ✅ Assinaturas ⚠️ Falta: notificações
Mobile    ██████████████  100%  ✅ Login ✅ Sync real ✅ Tela offline ✅ Upload fotos real ✅ Notificações push
```

### 1. Backend Core (100% ✅)
- CRUD completo: Properties, Inspections, Environments, Items, Signatures, Reports
- JWT auth + RBAC + tenant checking
- PDF report generation
- Endpoint `/inspections/:id/sync` pronto
- **Photos storage**: Supabase Storage integrado e testado

### 2. Database & Seeds (100% ✅)
- SQLite para desenvolvimento local
- Seed script popula banco com dados demo

### 3. Web Dashboard (90% ✅)
- ✅ Dashboard, Login, Properties, Inspections, Schedules, Comparative
- ✅ React Query hooks, auto token refresh, Navbar dinâmica
- ✅ `/inspections/[id]/report/page.tsx` — laudo online completo
- ✅ `/signatures/page.tsx` — assinaturas digitais com canvas HTML5
- ⚠️ Falta: notificações push

### 4. Mobile App Screens (100% ✅)
- ✅ 12 screens implementadas (incluindo Login e SincronizacaoOffline)
- ✅ Navegação com auth gate no App.tsx (Login → Home)
- ✅ SQLite local CRUD completo
- ✅ LoginScreen com JWT + AsyncStorage
- ✅ SincronizacaoOfflineScreen com status real de conectividade

### 5. Offline Sync Mobile (100% ✅)
- ✅ `sync.ts` completo com NetInfo real ativo
- ✅ `getUnsyncedInspections`, `syncInspection`, `syncAll` implementados
- ✅ NetInfo ativo — `isOnline()` verifica conectividade real
- ✅ Auth token JWT enviado via `AsyncStorage.getItem('accessToken')`
- ✅ Listener de evento online para sync automático
- ✅ Envio real de fotos implementado via Supabase Storage
- ✅ Fila offline integrada sincronizando properties e vistorias pendentes

### 6. Stitch Design Integration (90% ✅)
- ✅ 13 telas exportadas para `docs/stitch-screens/`
- ✅ `/schedules` e `/comparative` criados com base no Stitch
- ✅ SincronizacaoOfflineScreen mobile implementada com design Stitch
- ✅ Tela de Laudo Online integrada na web (`/inspections/[id]/report`)