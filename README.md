# firebase-demo

Hello-World-Seite (`public/index.html`) auf Firebase Hosting, deployed per GitHub Actions
(`.github/workflows/firebase-hosting.yml`) – kein lokales Terminal nötig.

- Pull Request → Vorschau-URL als Kommentar im PR
- Push/Merge auf `main` oder manueller Run (Actions → "Run workflow") → Live-Seite

Benötigt im Repo (Settings → Secrets and variables → Actions):

| Typ      | Name                       | Inhalt                                   |
|----------|----------------------------|------------------------------------------|
| Secret   | `FIREBASE_SERVICE_ACCOUNT` | kompletter JSON-Key eines Service-Accounts |
| Variable | `FIREBASE_PROJECT_ID`      | optional – sonst wird `project_id` aus dem Key genutzt |

## Firestore

Angemeldete Nutzer speichern Notizen unter `users/{uid}/notes`. Die Regeln in `firestore.rules`
erlauben jedem nur Zugriff auf die eigenen Notizen. Sie werden bei jedem Push auf `main`
deployed (Job `firestore-rules`). Dafür braucht der Service-Account zusätzlich die Rolle
**Firebase Rules Admin**.
