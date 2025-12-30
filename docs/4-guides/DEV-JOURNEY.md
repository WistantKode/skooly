# 🗺️ Parcours du Développeur : Skooly

Bienvenue dans l'équipe. Skooly n'est pas un CRUD classique. C'est un système événementiel modulaire. Pour éviter de te noyer, suis ce guide étape par étape.

---

## 🌊 Phase 1: Immersion (Jour 1)

Avant d'écrire une ligne de code, tu dois changer de mentalité. On ne stocke pas juste des données, on stocke des *faits*.

### 1. Comprendre la Philosophie
*   📖 **Lire [01. Vision Produit](../1-concepts/01-vision.md)** : Pourquoi on fait ça ? (Le problème du "Gmail-like")
*   📖 **Lire [02. Architecture (Odoo)](../1-concepts/02-architecture-philosophy.md)** : C'est le doc le plus important. Comprends pourquoi "Event > Module".
*   📖 **Lire [05. Open Core](../1-concepts/05-open-core-strategy.md)** : Comment on gagne de l'argent (MIT vs Enterprise).

### 2. Comprendre l'Architecture Technique
*   📖 **Lire [01. Structure du Projet](../3-technical/01-project-structure.md)** : Comprends pourquoi `apps/api` est différent de `packages/database`.
*   📖 **Lire [02. Guide de Traduction Odoo](../3-technical/02-odoo-translation.md)** : Si tu connais Odoo, c'est ta bible.
*   📖 **Lire [20. Stack Technique](../3-technical/20-stack.md)** : NestJS + Turborepo.

---

## 🛠️ Phase 2: Setup & Hello World (Jour 2)

### 1. Installation
```bash
# Clone & Install
pnpm install

# Base de données (Docker) - PostgreSQL + Redis
docker-compose up -d
pnpm db:push
```

### 2. Le Hello World "Skooly"
Ne fais pas juste un controller `GET /hello`.
Fais un controller qui **émet un événement**.

*   Crée un endpoint `POST /test-event`
*   Dans le service, n'écris pas en base directement.
*   Émets un évenement (ex: `TEST_EVENT_CREATED`).
*   Écoute cet événement (Event Handler) pour écrire en base.

C'est ça, la "Way of Skooly".

---

## 🧱 Phase 3: Implémenter un Module (Semaine 1)

Choisis un module simple pour commencer.

1.  📖 **Lire la spec du module** (ex: [Présences](../2-specs/04-attendance.md)).
2.  Implémente le **Schema Prisma** (`packages/database/prisma/schema.prisma`) en suivant [21. Database Schema](../3-technical/21-database-schema.md).
3.  Crée le module NestJS (`apps/api/src/modules/attendance`).
4.  Crée le premier Event : `ATTENDANCE_SESSION_STARTED`.

---

## 🧭 Boussole

*   **Tu es perdu dans le business ?** → Dossier `1-concepts`
*   **Tu ne sais pas comment coder ?** → Dossier `3-technical`
*   **Tu ne sais pas quoi coder ?** → Dossier `2-specs`

Bon code ! 🚀
