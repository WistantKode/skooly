# 🛠️ Stack Technique : Le Choix de la Raison

Pourquoi j'ai choisi cette stack ? Pas pour la hype. Pour la **Robustesse**.

## Backend : NestJS
*   **Pourquoi ?** C'est le "Angular du Backend".
*   Architecture imposée (Modules, Controllers, Services).
*   Ça empêche le code spaghetti.
*   L'Injection de Dépendance est vitale pour nos Tests Unitaires.

## Frontend : Next.js (App Router)
*   **Pourquoi ?** Server Components.
*   On charge les données côté serveur (près de la DB).
*   On envoie du HTML pur au client (rapide sur les réseaux 3G africains).
*   Pas de spinner infini.

## Database : PostgreSQL + Prisma
*   **PostgreSQL** : La seule vraie base de données Open Source. Solide comme le roc.
*   **Prisma** : Type-safety.
    *   Si je renomme une colonne en DB, VS Code me souligne en rouge toutes les lignes de code qui l'utilisent.
    *   C'est notre assurance vie contre les bugs de refactoring.

## Monorepo : Turborepo
*   On a plusieurs apps (`web`, `api`, `mobile`).
*   On a du code partagé (`packages/database`, `packages/ui`).
*   Turbo gère le cache de build. Si je ne touche que le frontend, il ne recompile pas le backend.

## Infrastructure : Docker
*   `docker-compose up` : Lance la DB, Redis, MinIO (S3 local) et l'API.
*   Zéro "Ah mais ça marche sur ma machine".
