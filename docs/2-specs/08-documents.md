# 📜 Module Documents : La Preuve Officielle

## Le Problème de la Fraude
Au Cameroun (et ailleurs), "acheter" un diplôme ou falsifier un relevé est un sport national.
Skooly doit être **la source de vérité infalsifiable**.

## Entités Principales

### 1. `OfficialDocument`
*   `type`: `TRANSCRIPT` (Relevé), `CERTIFICATE` (Attestation), `DIPLOMA`.
*   `secure_hash`: SHA-256 du contenu sémantique (Notes + ID Étudiant + Date).
*   `qr_data`: URL signée pointant vers `verify.skooly.io`.

### 2. `TemplateEngine`
On n'utilise pas de simples HTML. On utilise `Puppeteer` ou `PDFKit` pour générer des PDFs vectoriels parfaits.
*   **Watermark dynamique** : L'ID de l'étudiant est incrusté invisiblement dans le fond.
*   **Signature Numérique** : Le PDF est signé avec la clé privée de l'institution.

## Workflow de Vérification (Public)

1.  Un employeur reçoit le CV d'un candidat avec son relevé de notes Skooly.
2.  Il scanne le QR code en bas de page.
3.  Il atterrit sur `skooly.io/verify/XYZ...`.
4.  Si le document est vrai ✅ : Il voit la version numérique originale.
5.  Si le document est faux ❌ : "DOCUMENT INCONNU".

## Portabilité
Si l'étudiant quitte l'école, il peut exporter son **Portfolio Académique** (ZIP avec tous ses PDFs signés).
C'est son passeport numérique.
