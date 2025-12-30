# ⚙️ Workflows Opérationnels : Le Cycle de Vie des Données

> Ce document répond à la question : "Concrètement, comment les données entrent, bougent et changent dans le système ?"

---

## 🏗️ 1. La Genèse : Créer l'Écosystème (Admin Setup)

Avant d'inscrire des élèves, il faut bâtir les murs.

### Q: Comment créer un nouveau Département / Salle ?
**Réponse :** Approche Top-Down (Hiérarchique).

1.  **Institution Setup** (Fait une fois) : Création du Tenant.
2.  **Infrastructure Physique** :
    *   Création des **Campus** -> **Bâtiments** -> **Salles** (`Classroom`).
    *   *Attributs Salle* : Capacité (50 places), Type (Labo/Amphi), Équipement (Projecteur).
3.  **Infrastructure Académique** :
    *   **Département** ("Génie Info") -> **Program** ("Licence GL").
    *   **Structure** : Définition des UEs et ECs pour l'année.

**Le Workflow "Rentrée Académique" :**
L'admin clique sur **"Dupliquer année N-1"**.
Tout est cloné : les filières, les cours, les salles. Il n'a plus qu'à ajuster les petits changements.

---

## 👥 2. Identité & Accès (Qui est Qui ?)

### Q: Les enseignants utilisent-ils leur Gmail perso ?
**Réponse :** OUI et NON. Stratégie Hybride.

1.  **Enseignants Permanents** : On leur impose l'email institutionnel (`@univ-douala.cm`). C'est pro, c'est carré.
2.  **Vacataires (60% du staff)** : Ils ont déjà 4 adresses mail. On accepte leur **Gmail/Yahoo**.
    *   *Sécurité* : On ne leur envoie jamais de mot de passe par mail. On envoie un "Magic Link" qui expire en 1h.

### Q: Comment gérer les Rôles (RBAC) ?
On ne donne pas "Toutes les clés" à tout le monde.
Skooly utilise des **Rôles Cumulatifs**.

*   M. Talla est **Enseignant** (voit ses cours) ET **Chef de Département** (voit tous les cours du départment).
*   **Workflow d'Attribution** :
    1.  RH crée la fiche "Partner" (La personne physique).
    2.  RH ajoute le rôle "Teacher" -> Accès App Prof.
    3.  Admin ajoute le rôle "HeadOfDept(GenieInfo)" -> Accès Dashboard Admin (Restreint).

### Q: Tracking - Qui a fait quoi ? (L'Espion)
Chaque action sensible laisse une trace indélébile (Audit Trail).

*   **Le Cas :** Un enseignant change une note de 08/20 à 12/20.
*   **Le Log (Database) :**
    ```json
    {
      "event": "GRADE_UPDATED",
      "who": "user_id_123 (Prof. Talla)",
      "when": "2024-12-31T14:00:00Z",
      "target": "grade_id_999 (Etudiant Kamga)",
      "diff": { "old": 8, "new": 12 },
      "ip": "192.168.1.55",
      "reason": "Erreur de report (Copie vérifiée)"
    }
    ```
*   **La Vue Admin :** "Historique des modifications" sur chaque fiche étudiant. Impossible de tricher sans être vu.

---

## 📆 3. L'Orchestration (Assignation des Ressources)

### Q: Comment assigner une Salle à un Programme ?
**Réponse :** C'est le module **Scheduling**.

Le système ne lie pas "Une salle à un programme". Il lie :
> **Session Cours** = ( **Matière** + **Enseignant** + **Salle** + **Groupe Étudiants** + **Créneau** )

**Le Workflow :**
1.  Le Responsable Pédagogique ouvre la vue "Planning L3 Info".
2.  Il glisse l'UE "Java" sur le créneau "Lundi 8h".
3.  **Le Système (Conflict Solver)** :
    *   Vérifie si le Prof est libre.
    *   Vérifie si la Salle est libre.
    *   Suggère la meilleure salle (capacité >= taille du groupe).
4.  **Réservation** : La salle est bloquée ("Booked").

---

## 🔄 4. La Synchronisation Externe (Le Cas du Paiement UBA)

### Q: Comment le système sait qu'un élève a payé ?
**Réponse :** Le principe de la **Réconciliation Asynchrone**.

**L'Événement Déclencheur (Le Pont UBA) :**
1.  L'étudiant paie à la banque. Il reçoit un reçu papier.
2.  Le soir, UBA transmet un fichier (Excel/API) à l'Université.
3.  **Job de Nuit Skooly** :
    *   Lit le fichier UBA.
    *   Cherche le Matricule dans le fichier.
    *   Trouve la Facture correspondante.
    *   Passe la Facture à `PAID`.

**Conséquence (Event Driven) :**
*   L'événement `InvoicePaid` est émis.
*   Le module **AccessControl** écoute -> Débloque l'impression de la carte.
