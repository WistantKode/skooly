# 🏗️ L'Ingénierie Skooly : L'Héritage Odoo modernisé

## Pourquoi Odoo avait raison (mais pourquoi Python me fatigue)

J'ai passé des années à analyser les ERP. Odoo est le seul qui a compris l'architecture modulaire.
Mais Odoo a un problème : c'est un monolithe Python/XML lourd, difficile à scaler sur mobile, et son UI est... datée.

**Skooly reprend le génie architectural d'Odoo, mais avec la puissance de l'écosystème TypeScript moderne.**

---

## 1. Event-First vs State-First

La plupart des apps scolaires stockent l'état actuel :
*   `Student.status = "Inscrit"`

C'est une erreur. Si l'étudiant a été suspendu puis réintégré, on a perdu cette info.

Skooly stocke les **Faits** (Events) :
1.  `StudentApplied` (Date T1)
2.  `StudentPaidRegistration` (Date T2) -> L'état devient "Inscrit" par déduction.
3.  `StudentSuspended` (Date T3)
4.  `StudentReinstated` (Date T4)

**L'État est une projection des Événements.**
Cela nous permet de :
*   Voyager dans le temps ("Quel était le statut de cet étudiant le 12 mars ?")
*   Auditer chaque changement (Qui a validé la réintégration ?).

---

## 2. Le "Modular Monolith"

On ne fait pas de Microservices (trop complexe pour rien).
On fait un **Monolithe Modulaire**.

### L'Appui sur Odoo
Dans Odoo, tout est un "Addon".
Dans Skooly, tout est un "Module NestJS" isolé.

| Concept Skooly | Inspiré de Odoo |
| :--- | :--- |
| **Prisma Schema** partagé | `ir.model` (Base de données unifiée) |
| **Modules NestJS** (`@Module`) | `__manifest__.py` (Définition de module) |
| **Service Methods** | `Server Actions` (Logique métier) |
| **Events** (`EventEmitter`) | `Signals` / `Automations` |

### La Règle d'Or de l'Isolation
Le module `Finance` ne doit JA-MAIS importer le module `Academic` directement.
Si la Finance a besoin de savoir qu'un étudiant est inscrit :
1.  Academic émet l'event `StudentRegistered`.
2.  Finance écoute cet event et crée une facture.

**Avantage :** Je peux désactiver le module Finance, et Academic continue de marcher parfaitement.

---

## 3. Pourquoi TypeScript (Next.js + NestJS) ?

Odoo utilise QWeb/XML pour ses vues. C'est propriétaire et lent.
Skooly utilise **React (Next.js)**.

1.  **Talent Pool** : Il est plus facile de trouver un dev React à Douala qu'un expert Odoo QWeb.
2.  **Performance UI** : Le client-side navigation de Next.js est instantané.
3.  **Type Safety** : De la base de données (Prisma) au Frontend (React), tout est typé. Si je change un champ en DB, mon compilateur me crie dessus avant même que je lance l'app. **Zéro runtime error surprise.**

---

## Conclusion Technique

Skooly n'est pas "juste un site web".
C'est un **système distribué logique packagé dans un binaire unique**.
C'est le meilleur des deux mondes.
