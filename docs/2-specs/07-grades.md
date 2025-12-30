# 📊 Module Grades : La Justice Académique

## Pourquoi c'est complexe ?
Parce qu'une note n'est pas juste un chiffre. C'est une conséquence légale.
Le système LMD (Licence-Master-Doctorat) a des règles de compensation tordues.

## Entités Principales ("Models")

### 1. `Evaluation` (Devoir)
*   **Type** : `CC` (Contrôle Continu), `SN` (Session Normale), `SR` (Rattrapage).
*   **Weight** : Coefficient (ex: CC=30%, SN=70%).
*   **Anonymity** : Si activé, la saisie se fait par Code Anonymat.

### 2. `GradeEntry` (La Note)
*   `value` : 14.5/20.
*   `is_absent`: Booléen.
*   `history`: Array des modifications (Audit Trail).

### 3. `Deliberation` (Le PV)
C'est l'acte de figer les notes.
Une fois délibéré, **plus aucune note n'est modifiable** sans réouvrir le PV (Action Admin majeure).

## Le Moteur de Calcul LMD

Le système ne stocke pas les moyennes. Il les **calcule à la volée** (ou en cache).

1.  **Moyenne EC** = (CC * 0.3) + (SN * 0.7).
2.  **Moyenne UE** = Somme(Moyenne EC * Crédits EC) / Somme Crédits.
3.  **Validation** :
    *   Si Moyenne UE >= 10/20 -> `VALIDATED`.
    *   Si Moyenne UE < 10 mais > 8 et Moyenne Semestre > 10 -> `COMPENSATED`.
    *   Sinon -> `FAILED`.

## Sécurité des Notes
*   **Double Saisie** (Option enterprise) : Deux opérateurs saisissent. Si différence > 0, alerte.
*   **Log Immutable** : On ne fait pas `UPDATE grade SET value=15`. On fait `INSERT grade_revision`.
