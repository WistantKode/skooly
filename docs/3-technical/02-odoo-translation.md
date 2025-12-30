# 🔄 Guide de Traduction : Odoo vers NestJS

## C'est quoi ce document ?
Si tu viens du monde Odoo Python, tu es perdu. Tu cherches tes `models.Model` et tes `xml views`.
Ce document est ta pierre de Rosette.

## La Table de Mapping

| Concept Odoo (Python) | Concept Skooly (TypeScript) | Outil Utilisé |
| :--- | :--- | :--- |
| **Model** (`class Student(models.Model)`) | **Schema** (`model Student {}`) | Prisma (Schema.prisma) |
| **Fields** (`fields.Char()`) | **Types** (`String`, `Int`) | Prisma + Zod |
| **Computeds** (`@api.depends`) | **Getters / Services** | Class Method ou SQL View |
| **Constraints** (`@api.constrains`) | **Validation Pipe** | `class-validator` (DTO) |
| **Actions** (`def action_confirm`) | **Service Methods** | `StudentService.confirm()` |
| **Wizards** (Saisie étape par étape) | **Multi-step Form** | React Hook Form |
| **Security** (`ir.model.access.csv`) | **CASL Guards** | `@Can('read', 'Student')` |
| **Cron Jobs** | **Cron Jobs** | `@nestjs/schedule` |

## Exemple : Créer un Étudiant

### Odoo (Ancien Monde)
```python
class Student(models.Model):
    _name = 'skooly.student'
    name = fields.Char(required=True)
    
    def action_register(self):
        self.state = 'registered'
```

### Skooly (Nouveau Monde)

**1. Database (Prisma)**
```prisma
model Student {
  id      String @id @default(cuid())
  name    String
  status  StudentStatus @default(DRAFT)
}
```

**2. Logic (NestJS Service)**
```typescript
@Injectable()
class StudentService {
  async register(id: string) {
    const student = await this.prisma.student.findUnique({ where: { id } });
    // Validation Logic here
    return this.prisma.student.update({
      where: { id },
      data: { status: 'REGISTERED' }
    });
  }
}
```

## Ce qu'on a perdu (et tant mieux)
*   ❌ **L'Héritage Multiple** : C'était un enfer à debugger. On utilise la Composition.
*   ❌ **XML Views** : C'était rigide. React est infini.
*   ❌ **Python Global Interpreter Lock (GIL)** : Node.js est asynchrone par défaut.
