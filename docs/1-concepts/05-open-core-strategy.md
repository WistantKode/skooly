# 💰 Business Model : Open Core Strategy

## Pourquoi "Open Core" et pas "100% Gratuit" ?

Soyons réalistes. Maintenir un logiciel de cette complexité coûte cher (temps développeur, design, sécurité).
Si je donne tout gratuitement :
1.  Le projet meurt quand je me lasse.
2.  Je ne peux pas payer d'autres développeurs pour m'aider.
3.  Le support technique est inexistant.

**Le modèle Open Core est la seule façon viable de pérenniser Skooly pour les 20 prochaines années.**

---

## 🟢 Community Edition (CE) - Licence MIT

**Promesse :** Tout ce qui est nécessaire pour faire tourner une petite école primaire ou un petit institut sans budget.

Ce qui est inclus (Gratuit à vie) :
*   Gestion Étudiants & Enseignants
*   Structure Académique
*   Inscriptions
*   Présences (Mode manuel simple)
*   Relevés de notes (Format standard PDF)

C'est suffisant pour 80% des petites structures.

---

## 🔵 Enterprise Edition (EE) - Licence Commerciale

**Promesse :** Les outils de productivité et d'intégration pour les grandes universités (IUT, Yaoundé I, Privés de luxe).

Ce qui est payant (Module par module ou abonnement) :
*   **Finance Avancée** : Connecteur direct MTN/Orange Money (API temps réel).
*   **Anti-Fraude IA** : Détection des faux bulletins et faux scans.
*   **Audit Avancé** : Logs détaillés pour conformité légale.
*   **Mobile Apps Natives** : iOS/Android app (White label).
*   **Support Prioritaire** : SLA 24h.

---

## ⚙️ Architecture Technique de l'Open Core

Comment on code ça ?

```
/apps
  /api
    /src
      /modules
        /core (MIT) -> GitHub Public
        /enterprise (Private) -> GitHub Private Submodule
```

Le code Enterprise est injecté via des **Interfaces**.
Exemple : `IPaymentProvider`.
*   Community implémente `CashProvider` (bête saisie manuelle).
*   Enterprise implémente `MtnMomoProvider` (API complexe).

Si le module Enterprise n'est pas là, le système fallback sur la version Community.
C'est propre, légal, et technique.
