# Skooly : L'OS des Universités Modernes

Skooly est une plateforme ERP universitaire modulaire et souveraine conçue pour l'Afrique Centrale. Elle centralise la scolarité, la finance, et la pédagogie dans un écosystème unique, sécurisé et performant.

## Caractéristiques Principales

*   **Gestion LMD Native** : Moteur de calcul automatique des moyennes, crédits et délibérations conforme aux standards CEMAC.
*   **Inclusion Financière** : Intégration bancaire (UBA) et Mobile Money (MTN, Orange) pour une réconciliation automatique et sans fraude.
*   **Sécurité Documentaire** : Certification des diplômes et relevés de notes via signature numérique et QR Code.
*   **Résilience Opérationnelle** : Architecture Offline-first permettant la saisie des données même sans connexion internet.
*   **Infrastructure Multi-Campus** : Gestion hiérarchique permettant à une Université Mère de piloter plusieurs instituts autonomes.

## Stack Technologique

Le projet repose sur un Monorepo moderne géré par Turborepo :
*   **Backend** : NestJS, Prisma, PostgreSQL, Redis.
*   **Frontend** : Next.js, Tailwind CSS, Shadcn UI.
*   **Langage** : TypeScript (100%).

## Démarrage Rapide

### Pré-requis
*   Node.js v20+
*   pnpm v9+
*   Docker & Docker Compose

### Installation
```bash
# cloner le projet
git clone https://github.com/wistantkode/skooly.git
cd skooly

# installer les dépendances
pnpm install

# démarrer l'environnement de développement
pnpm dev
```

## Documentation

L'intégralité de la réflexion stratégique et technique est disponible dans le dossier `/docs`.
*   [Index de la Documentation](./docs/00-INDEX.md)
*   [Guide du Développeur](./docs/4-guides/DEV-JOURNEY.md)

## Gouvernance et Sécurité

Nous appliquons des standards de sécurité rigoureux pour protéger les données académiques.
*   Consultez notre [Politique de Sécurité](./SECURITY.md).
*   Consultez le [Code de Conduite](./CODE_OF_CONDUCT.md) pour les contributions.

---

© 2024 WistantKode. Sous licence Enterprise. Les modules Core sont sous licence MIT.
