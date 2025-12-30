# 💼 Module Internships : Le Pont vers l'Emploi

## Le Chaos des Stages
Habituellement, c'est : "L'étudiant trouve un stage -> Il imprime une convention -> Le prof signe -> L'étudiant la perd -> L'entreprise ne paie pas".
C'est fini.

## Entités Principales

### 1. `Company` (Base Entreprises)
Un CRM B2B intégré.
*   Nom, Secteur, RH Contact.
*   `blacklist`: Booléen (Si l'entreprise maltraite les stagiaires).

### 2. `InternshipAgreement` (Convention)
C'est un contrat légal TRI-PARTITE (École / Étudiant / Entreprise).
*   **Workflow** : `DRAFT` -> `STUDENT_SIGNED` -> `COMPANY_SIGNED` -> `SCHOOL_SIGNED` -> `ACTIVE`.
*   Plus de papier. Signature électronique simple.

### 3. `Defense` (Soutenance)
La gestion du jury de fin de stage.
*   `date`, `room`.
*   `jury_members` (Enseignants + Invités pro).
*   `grade` (Note de stage).

## Le Suivi (Livret de Stage Numérique)

L'étudiant ne rend pas un rapport papier à la fin.
Il remplit un **Logbook Hebdomadaire** sur l'app.
*   Semaine 1 : "J'ai appris React".
*   Validation Tuteur Entreprise : "Vrai, il progresse".

**Avantage :** L'école détecte si un stage se passe mal dès la 2ème semaine (pas à la fin).
