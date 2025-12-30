# 🗄️ Database Schema : La Source de Vérité

## Modélisation Prisma

On n'utilise pas UML. On utilise `schema.prisma`. C'est lisible et exécutable.

### Core (Users & Tenants)

```prisma
model User {
  id        String   @id @default(cuid())
  email     String   @unique
  password  String
  tenants   UserTenant[]
}

model Institution {
  id        String   @id @default(cuid())
  name      String
  domain    String?  // custom domain
}
```

### Academic (LMD)

```prisma
model Student {
  id        String   @id @default(cuid())
  matricule String   @unique
  enrollments Enrollment[]
}

model TeachingUnit { // UE
  id        String   @id
  code      String   // INF101
  credits   Int
  elements  CourseElement[]
}

model Grade {
  id        String   @id
  value     Float
  studentId String
  elementId String
  isLocked  Boolean // After deliberation
}
```

### Finance (Double Entry)

```prisma
model JournalEntry {
  id        String   @id
  reference String   // INV/2024/001
  state     EntryState // DRAFT, POSTED
  lines     JournalLine[]
}

model JournalLine {
  id        String   @id
  accountId String
  debit     Float
  credit    Float
}
```

## Règles de Design
1.  **CUIDs** : Pas d'auto-increment integers (`1, 2, 3`). On utilise des CUIDs (`clh3...`) pour éviter l'énumération par des hackers.
2.  **Soft Delete** : On ajoute `deletedAt DateTime?` sur les tables critiques. On ne supprime rien physiquement.
3.  **Audit Fields** : `createdAt`, `updatedAt`, `createdById` sur TOUTES les tables.
