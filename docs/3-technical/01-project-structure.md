# 🏗️ Architecture du Code : Le Monolithe Modulaire

## Arborescence Monorepo (Turborepo)

Oubliez le spaghetti. Voici où chaque chose vit.

```bash
skooly/
├── apps/
│   ├── api/                 # Le Backend NestJS (Le Cerveau)
│   │   ├── src/
│   │   │   ├── modules/     # 1 Dossier = 1 Module Fonctionnel
│   │   │   │   ├── core/    # Users, Auth
│   │   │   │   ├── academic/
│   │   │   │   └── finance/
│   │   │   └── common/      # Guards, Interceptors, Decorators
│   ├── web/                 # Le Frontend Next.js (Le Visage)
│   │   ├── app/             # App Router
│   │   │   ├── (dashboard)/ # Routes protégées
│   │   │   └── (public)/    # Login, Verify Page
│   │   └── components/      # Shadcn UI
│   └── mobile/              # React Native (Futur)
├── packages/
│   ├── database/            # Prisma Schema & Client (Partagé)
│   ├── ui/                  # Composants UI partagés (Boutons, Forms)
│   ├── business-rules/      # Logique pure (Calcul moyenne, Taxe)
│   └── ts-config/           # Config TypeScript stricte
```

## Règles de Séparation

1.  **Logic-Free Frontend** : Le Frontend ne calcule rien. Il affiche.
    *   ❌ `const total = price * 1.19` (Interdit dans Next.js)
    *   ✅ `price.total` (Venant de l'API)
2.  **Database-First** : Tout part du schéma Prisma (`packages/database`).
3.  **Module Isolation** : Dans `apps/api`, le module `Finance` ne doit pas importer `AcademicService`. Il doit écouter `StudentRegisteredEvent`.

## Pourquoi `business-rules` ?
C'est un package sans framework (pas de Nest, pas de React). Juste du pur TypeScript.
On y met les algos complexes (Calcul LMD, Pénalités Biblio).
**Avantage** : On peut tester ces règles en 1ms avec Vitest, sans lancer toute l'app.
