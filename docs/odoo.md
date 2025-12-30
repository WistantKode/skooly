# Analyse — ERP scolaire modulaire façon Odoo

## 1. Problématique

Les ERP scolaires classiques échouent pour une raison simple :

* ils stockent des **états**
* pas des **faits traçables**

Résultat :

* impossible de répondre clairement à :

  * qui a fait quoi ?
  * quand ?
  * dans quel cadre ?
  * est-ce validé ?

L’objectif de Skooly est différent :
👉 construire un **ERP scolaire modulaire**, inspiré d’Odoo, basé sur la **vérité événementielle**.

---

## 2. Principe Odoo appliqué à l’éducation

Odoo repose sur :

* un **core commun**
* des **modules activables**
* un **store de fonctionnalités**
* une **traçabilité totale**

Ce modèle est **100 % compatible** avec le monde scolaire.

Une institution éducative =

* une organisation
* des processus répétitifs
* des rôles clairs
* des obligations légales

---

## 3. Core indispensable (non négociable)

Le Core ne gère aucun métier spécifique.
Il garantit la cohérence globale.

### Core contient :

* Tenant (institution)
* Utilisateurs & identités
* Rôles & permissions
* Calendrier académique
* Event system
* Audit log

👉 Sans ce core, aucun module n’est fiable.

---

## 4. Modules comme micro-applications

Chaque module est :

* autonome
* activable/désactivable
* dépendant du core

### Exemples de modules :

* Enseignement
* Présences
* Notes & calculs
* Délibérations
* Scolarité & paiements
* Documents officiels
* CRM académique

Les modules ne communiquent pas directement.
Ils passent par les **events**.

---

## 5. Tracking parfait : le cœur du système

### Principe

Tout ce qui se passe dans l’institution génère un événement.

```
Event
 ├─ id
 ├─ type
 ├─ tenant_id
 ├─ actor_id
 ├─ target_id
 ├─ module
 ├─ timestamp
 └─ metadata
```

Aucune action silencieuse.

---

## 6. Exemple détaillé : un cours

Un cours est une **instance** (pas juste une matière).

Données liées :

* UE / EC
* Enseignant
* Groupe / classe
* Salle
* Date & durée

### Événements générés

* course.started
* attendance.recorded
* attendance.validated
* attendance.sheet.generated

À tout moment, le système sait :

* qui enseignait
* combien d’étudiants étaient présents
* si la présence est validée
* si un document officiel existe

---

## 7. CRM académique (indispensable)

Toute personne = un **contact institutionnel**.

Un contact possède une timeline :

* inscriptions
* présences
* notes
* paiements
* sanctions
* communications

👉 Exactement comme un CRM, appliqué à l’éducation.

---

## 8. Modules ≠ données

Les modules ne sont que :

* des règles métier
* des vues
* des workflows

La donnée source reste :

* les entités
* les événements

Cela permet :

* audit
* reporting
* IA

---

## 9. Difficulté réelle du projet

### Ce qui est difficile

* design du modèle événementiel
* cohérence des règles académiques
* discipline de développement

### Ce qui est faisable

* monolithe modulaire
* évolution vers microservices
* ajout progressif de modules

---

## 10. Bénéfices long terme

* vérité institutionnelle
* confiance administrative
* reporting fiable
* base solide pour l’IA

---

## 11. Conclusion

Oui, un ERP scolaire façon Odoo est possible.

Mais seulement si :

* le core est solide
* les events sont centraux
* les modules restent secondaires

Skooly ne doit pas être un logiciel de formulaires.

Skooly doit être un **registre vivant de l’institution**.
