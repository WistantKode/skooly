<div align="center">

# Skooly : Système d'Exploitation Universitaire

<img src="./assets/schoolmanagemntphoto.jpg" alt="Skooly Banner" width="1000" style="border-radius: 12px;">

<br />

**L'infrastructure logicielle souveraine pour l'enseignement supérieur en Afrique.**

<br />

[![GitHub Stars](https://img.shields.io/github/stars/WistantKode/skooly?style=flat-square&color=black)](https://github.com/WistantKode/skooly/stargazers)
[![License](https://img.shields.io/badge/License-MIT+%20Enterprise-black?style=flat-square)](./LICENSE)
[![Forks](https://img.shields.io/github/forks/WistantKode/skooly?style=flat-square&color=black)](https://github.com/WistantKode/skooly/network/members)

<br />

[📖 Documentation](./docs/00-INDEX.md) · [⚡ Démarrage Rapide](#démarrage-rapide) · [🛠️ Guide Développeur](./docs/4-guides/DEV-JOURNEY.md)

<br />

<img src="./assets/erp.jpg" alt="Skooly Interface" width="1000" style="border-radius: 12px; box-shadow: 0 20px 50px rgba(0,0,0,0.1);">

<br />

## Atouts Stratégiques

Contrairement aux solutions génériques, Skooly est architecturé pour les réalités du terrain camerounais et de la zone CEMAC.

### 1. Moteur LMD Algorithmique
Automatisation stricte des délibérations selon les normes LMD : calcul des crédits, compensations inter-UE et gestion des dettes académiques.

### 2. Réconciliation Bancaire Native
Double intégration UBA (fichiers de flux) et Mobile Money (API). La banque est la seule source de vérité, éliminant toute tentative de fraude aux reçus.

### 3. Architecture Multi-Niveaux
Structure de Tenant hiérarchique permettant à une Université (ex: UD) de piloter plusieurs instituts (IUT, ENSET) avec une consolidation globale des données.

### 4. Résilience Offline (PWA)
Fonctionnement ininterrompu en zone blanche ou signal instable. Les données sont synchronisées automatiquement dès le retour du réseau.

### 5. Certification Numérique
Signature cryptographique et QR Code de vérification publique pour chaque relevé de notes et diplôme émis.

<br />

## Stack Technologique

| Composant | Technologie | Icône & Lien |
| :--- | :--- | :--- |
| **Backend** | NestJS | [![](https://img.shields.io/badge/NestJS-E0234E?style=flat-square&logo=nestjs&logoColor=white)](https://nestjs.com/) |
| **Frontend** | Next.js | [![](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white)](https://nextjs.org/) |
| **Database** | PostgreSQL | [![](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)](https://www.postgresql.org/) |
| **ORM** | Prisma | [![](https://img.shields.io/badge/Prisma-2D3748?style=flat-square&logo=prisma&logoColor=white)](https://www.prisma.io/) |
| **Styling** | TailwindCSS | [![](https://img.shields.io/badge/TailwindCSS-06B6D4?style=flat-square&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/) |
| **Cache** | Redis | [![](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)](https://redis.io/) |

<br />

## Démarrage Rapide

### Pré-requis
Node.js v20+ · pnpm v9+ · Docker

### Installation
```bash
git clone https://github.com/WistantKode/skooly.git
cd skooly
pnpm install
pnpm dev
```

<br />

## Communauté et Maintenance

<a href="https://github.com/WistantKode/skooly/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=WistantKode/skooly" alt="Contributors" />
</a>

<br />

**[WistantKode](https://github.com/WistantKode)**
*Lead Architect*

<br />

## Statistiques du Projet

![Repobeats analytics](https://repobeats.axiom.co/api/embed/b1bf4dc0226458617adbdbf5586f2df953eb0922.svg 'Repobeats analytics image')

<br />

© 2024 WistantKode. [Mentions Légales](./docs/1-concepts/06-compliance.md)

</div>
