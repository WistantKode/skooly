# 💰 Module Finance : Le Système Hybride (UBA + Mobile Money)

## La Réalité Camerounaise
L'Université de Douala ne blague pas avec l'argent.
La scolarité (tranches de 50,000 FCFA) passe OBLIGATOIREMENT par la banque (**UBA**, Compte Trésor).
Les "petits frais" (Concours, Certificats, Pénalités) peuvent passer par Mobile Money.

Skooly doit réconcilier ces deux mondes.

---

## 1. UBA Integration (Le "Guichet Unique")

### Le Workflow Étudiant
1.  L'étudiant va à l'agence UBA (ou utilise l'app UBA).
2.  Il verse 50,000 au guichet avec son matricule Skooly.
3.  Le caissier lui remet un **Reçu Bancaire (Bordereau)** avec un numéro de transaction (`TRX-1234`).
4.  L'étudiant se connecte à Skooly -> Onglet "Paiements".
5.  Il saisit `TRX-1234` et uploade la photo du reçu.

### Le Workflow Comptable (Réconciliation)
Skooly ne croit pas l'étudiant sur parole.
1.  Chaque soir, le Comptable uploade le **Fichier Relevé UBA (Excel/CSV)** dans Skooly.
2.  **Matching Automatique** :
    *   Le système cherche `TRX-1234` dans le fichier banque.
    *   Si trouvé et montant correspond -> ✅ **VALIDATED**.
    *   Si non trouvé -> ⏳ **PENDING_BANK_CHECK**.

### Schéma de Données (Dual Ledger)
*   `BankStatementLine` : La vérité de la banque.
*   `StudentPaymentClaim` : La déclaration de l'étudiant.
*   `Reconciliation` : Le lien entre les deux.

---

## 2. Mobile Money (Native Integration)

Pour les frais < 10,000 FCFA (Relevés, Attestations, Badge perdu).
Ici, c'est **Temps Réel**.

1.  Skooly appelle l'API MTN MoMo / Orange Money.
2.  L'étudiant tape son code PIN.
3.  Confirmation instantanée (Webhook).
4.  Pas de réconciliation manuelle nécessaire.

---

## 3. Plan Comptable (Odoo Style)

Skooly gère ça comme des écritures comptables rigoureuses.

| Journal | Débit | Crédit | Compte |
| :--- | :--- | :--- | :--- |
| **Vente** | Client (Étudiant) | Vente (Scolarité) | 50,000 |
| **Banque (UBA)** | Banque UBA | Client (Étudiant) | 50,000 |

*   Si le paiement Mobile Money échoue, la dette reste.
*   Si le paiement UBA est rejeté (faux bordereau), la dette reste.

## 4. Architecture Technique

### Adapter : `UbaFileParser`
Un service spécialisé pour parser les CSV exotiques de UBA.
*   Détecte les colonnes "Date", "Val", "Libellé", "Montant".
*   Gère les doublons (Idempotence).

### Adapter : `MobileMoneyGateway`
Une abstraction pour switcher entre MTN, Orange, et Express Union.
