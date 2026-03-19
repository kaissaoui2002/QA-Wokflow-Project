# Configuration Jira

Ce fichier est lu par `story-analyzer` pour savoir où se trouve ton instance Jira.

## Paramètres

```
JIRA_BASE_URL=https://onclusive.atlassian.net/
JIRA_PROJECT_KEY=GEO_Module
```

## Comment ça fonctionne

`story-analyzer` utilise le navigateur Chrome (déjà ouvert et connecté à Jira) pour récupérer le contenu des tickets. Aucun token API n'est nécessaire — il suffit d'être connecté à Jira dans Chrome.

## Exemples d'URLs acceptées par `/qa-analyze`

```bash
# Epic spécifique
/qa-analyze https://VOTRE-DOMAINE.atlassian.net/browse/GEO-1

# Story unique
/qa-analyze https://VOTRE-DOMAINE.atlassian.net/browse/GEO-42

# Sprint actif d'un board
/qa-analyze https://VOTRE-DOMAINE.atlassian.net/jira/software/projects/GEO/boards/1

# Fichier local (toujours compatible)
/qa-analyze epics/epics.md
```
