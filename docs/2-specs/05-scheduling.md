# 📅 Module Scheduling : Le Maître du Temps

## Le Problème NP-Complet
Générer un emploi du temps est mathématiquement impossible à résoudre parfaitement.
Skooly ne "génère" pas (au début), il **valide** les contraintes.

## Entités Principales ("Models")

### 1. `TimeSlot` (Créneau) (Odoo: `calendar.event`)
Un créneau n'est pas juste une date. C'est une intersection de ressources.

*   **Ressources :**
    *   1 Enseignant (ou N)
    *   1 Salle (Capacité X, Projecteur Y)
    *   1 Groupe d'étudiants (L1-A, L1-B)
*   **Contraintes Hard :**
    *   Le prof ne peut être à deux endroits.
    *   La salle ne peut accueillir plus que sa capacité.
    *   Le groupe ne peut avoir deux cours.
*   **Contraintes Soft :**
    *   Pas de cours le samedi soir.
    *   Éviter les trous de 4h.

## Workflow

1.  **Draft** : Le responsable pédagogique place les blocs (Drag & Drop UI).
2.  **Conflict Check** : Le système flague en rouge les collisions (Temps réel).
3.  **Publish** : L'emploi du temps devient visible.
4.  **Notify** : Les étudiants reçoivent une notif "Changement de salle".

## Vue "Gantt" (Odoo style)

On utilise une vue Gantt groupée par :
*   Salle (pour voir les taux d'occupation).
*   Enseignant (pour voir les charges horaires).
*   Promotion (pour voir l'agenda étudiant).

## API & Intégration

*   Export `.ics` pour Google Calendar / Outlook.
*   Sync automatique sur l'app mobile.
