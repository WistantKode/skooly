# 🎨 Stratégie UI/UX : L'OS Éducatif (Pas juste un site)

> **L'Objectif** : On ne fait pas un "Site Web de gestion". On fait le **Mac OS de l'Éducation**.
> L'utilisateur ne "visite" pas Skooly. Il **habite** dedans 8h/jour.

---

## 1. La Philosophie : "Linear-Like"
On s'inspire des meilleurs outils de productivité (Linear, Notion, Superhuman).

*   **Densité d'Information** : Pas de whitespace inutile. Un Recteur veut voir 50 lignes de stats, pas 3 grosses cartes avec des images de stock.
*   **Vitesse Perçue** :
    *   **Optimistic UI** : Quand on clique "Sauvegarder", ça passe vert **instantanément**. Le serveur traite après.
    *   **Keyboard First** : Un expert ne touche pas sa souris. `Cmd+K` pour naviguer, `Cmd+S` pour sauver.
*   **Mode Focus** : Quand je saisis des notes, les menus disparaissent. Juste la grille.

---

## 2. Structure du Layout (Le Shell)

### A. La Sidebar "Contextuelle"
Pas de sidebar statique four-tout.
*   **Niveau 1** : Sélecteur de Module (Icônes uniquement : 🎓 💰 📅).
*   **Niveau 2** : Menu du Module Actif (ex: Finance -> Factures, Impayés, Rapports).
*   **Collapsible** : Se replie (`[`) pour laisser place aux données.

### B. Le Command Center (`Cmd+K`)
C'est le GPS de Skooly.
*   "Aller à Étudiant : Kamga"
*   "Créer Facture"
*   "Changer Année Académique"
*   **Pourquoi ?** C'est 10x plus rapide que de chercher dans les menus.

---

## 3. Composants Clés & Design System

On utilise **Shadcn/ui** (Radix Primitives) customisé.

### Les Tableaux (Data Grid)
Le composant le plus important. C'est 80% de l'usage.
*   **Inspiré de Excel** : Colonnes redimensionnables, tri multiple.
*   **Row Actions** : Clic droit sur une ligne -> Menu contextuel ("Imprimer Reçu", "Exclure").
*   **Sticky Headers** : On ne perd jamais le contexte en scrollant.

### Les Formulaires (Drawer vs Modal)
*   **Petite action** (Changer MDP) -> **Modal** (Dialog).
*   **Grosse action** (Inscrire Étudiant) -> **Sheet/Drawer** (Volet latéral qui glisse).
    *   *Avantage* : On garde le contexte visible en arrière-plan.

### Le Feedback Visuel (Toasts)
*   Positif : "Sauvegardé" (Subtil, en bas à droite).
*   Critique : "Erreur Réseau" (Rouge, persistent).
*   **Sonore ?** : Un petit "bip" satisfaisant sur les actions critiques (optionnel).

---

## 4. Distinction Visuelle (Le "Premium Feel")

Comment on se distingue des ERPs moches (Odoo standard, Synoptrix) ?

1.  **Typographie Moderne** : `Inter` ou `Geist Sans`. Lisibilité parfaite sur petits écrans.
2.  **Micro-Interactions** :
    *   Un bouton clique s'enfonce légèrement (`scale-95`).
    *   Une liste qui se charge arrive avec une animation en cascade (Stagger).
3.  **Glassmorphism Subtil** : Des panneaux légèrement transparents pour donner de la profondeur (Depth).
4.  **Dark Mode Natif** : Indispensable pour les yeux des comptables qui bossent tard.

---

## 5. Mobile First (Action-Oriented)

Sur mobile, on ne montre pas tout le tableau Excel.
On montre des **Cartes d'Action**.
*   Prof : "Mon prochain cours" (Gros bouton "Faire l'appel").
*   Étudiant : "Ma dette" (Gros bouton "Payer").
*   **Bottom Navigation** : Les menus importants sont en bas (pouce).
