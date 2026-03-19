Analyse les user stories ou spécifications (lien Jira ou fichier local) et extrait toutes les exigences testables.

## Instructions

Utilise l'agent `story-analyzer` pour effectuer l'analyse.

**Détection automatique de la source depuis `$ARGUMENTS` :**

| Format de l'argument | Action |
|---|---|
| URL Jira (`https://...atlassian.net/browse/XXX-123`) | Récupérer via API REST Jira |
| URL Jira (`https://...atlassian.net/jira/software/projects/...`) | Récupérer le sprint actif via API Jira |
| Chemin de fichier local (`epics/epics.md`, `specs/story.txt`) | Lire le fichier local |
| Aucun argument | Demander à l'utilisateur : lien Jira ou fichier ? |

**Étapes pour une source Jira :**
1. Lire `.claude/jira-config.md` pour récupérer `JIRA_BASE_URL`, `JIRA_EMAIL`, `JIRA_API_TOKEN`
2. Détecter le type d'URL (issue unique, epic, board, filtre JQL)
3. Appeler l'API REST Jira avec authentification Basic (base64 email:token)
4. Si epic → récupérer aussi toutes les stories enfants (`jql=parent={epicKey}`)
5. Si board → récupérer les issues du sprint actif
6. Extraire : summary, description, acceptance criteria, priority, status, story points

**Étapes pour une source fichier :**
1. Lire le fichier local indiqué
2. Parser le contenu (Markdown, texte libre)

**Actions communes :**
1. Identifier toutes les fonctionnalités et modules concernés
2. Extraire les critères d'acceptation explicites et implicites
3. Détecter les règles métier, cas limites et dépendances
4. Signaler les ambiguïtés ou manques dans les specs
5. Générer `outputs/requirements.md`

**À la fin**, afficher :
- Source analysée (URL Jira ou fichier)
- Nombre de tickets/stories récupérés (si Jira)
- Nombre de fonctionnalités identifiées
- Nombre de critères d'acceptation extraits
- Liste des ambiguïtés détectées
- Chemin du fichier généré

Source : $ARGUMENTS
