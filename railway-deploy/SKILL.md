---
name: railway-deploy
description: Railway deployment via GraphQL API and GitHub integration. Use when creating Railway projects, linking GitHub repos, deploying services, or managing the full deploy lifecycle (create repo -> create Railway project -> link -> auto-deploy). Triggers on mentions of Railway, deploy to Railway, Railway project, or production deployment pipeline.
---

# Railway Deploy Skill

## When to use this skill
- Creating new Railway projects programmatically
- Linking GitHub repositories to Railway services
- Managing the full deployment pipeline: GitHub repo -> Railway project -> auto-deploy
- Querying Railway project status, services, and deployments
- Deleting or managing Railway projects

## Prerequisites
- **Railway API Token**: Must be set as environment variable or in `~/.bashrc`
- **GitHub CLI (`gh`)**: For creating repos and pushing code
- Token stored locally per agent — not shared across machines

## Full Deployment Pipeline

### Step-by-step lifecycle
```
1. Create GitHub repo:        gh repo create <name> --public --clone
2. Write & push code:         git add . && git commit && git push
3. Create Railway project:    Railway GraphQL API -> projectCreate
4. Create service:            Railway GraphQL API -> serviceCreate
5. Link to GitHub repo:       Railway GraphQL API -> serviceConnect
6. Auto-deploy:               Railway watches repo, deploys on push
```

### Railway GraphQL API

**Endpoint**: `https://backboard.railway.com/graphql/v2`
**Auth**: `Authorization: Bearer $RAILWAY_TOKEN`

### Create a project
```graphql
mutation {
  projectCreate(input: { name: "my-project" }) {
    id
    name
    environments {
      edges {
        node {
          id
          name
        }
      }
    }
  }
}
```

### Create a service in a project
```graphql
mutation {
  serviceCreate(input: {
    projectId: "PROJECT_ID"
    name: "web"
  }) {
    id
    name
  }
}
```

### Connect service to GitHub repo
```graphql
mutation {
  serviceConnect(
    id: "SERVICE_ID"
    input: {
      source: { repo: "owner/repo-name" }
      branch: "main"
    }
  ) {
    id
  }
}
```

### Query project details
```graphql
query {
  project(id: "PROJECT_ID") {
    id
    name
    services {
      edges {
        node {
          id
          name
          serviceInstances {
            edges {
              node {
                domains {
                  serviceDomains { domain }
                  customDomains { domain }
                }
              }
            }
          }
        }
      }
    }
  }
}
```

### Delete a project
```graphql
mutation {
  projectDelete(id: "PROJECT_ID")
}
```

## Curl Pattern
```bash
curl -X POST https://backboard.railway.com/graphql/v2 \
  -H "Authorization: Bearer $RAILWAY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"query": "mutation { projectCreate(input: { name: \"my-app\" }) { id name } }"}'
```

## Environment Variables
Railway auto-detects common frameworks (Next.js, Express, FastAPI, etc.) and sets build/start commands. For custom config, set environment variables via:

```graphql
mutation {
  variableUpsert(input: {
    projectId: "PROJECT_ID"
    environmentId: "ENV_ID"
    serviceId: "SERVICE_ID"
    name: "DATABASE_URL"
    value: "postgres://..."
  })
}
```

## Common Patterns

### Full-stack deploy (frontend + API)
```
1. Create Railway project
2. Create "web" service -> link to frontend repo
3. Create "api" service -> link to backend repo
4. Set shared env vars (API URL, DB connection)
5. Railway auto-deploys both on push
```

### Monorepo deploy
```
1. Create Railway project
2. Create service per sub-package
3. Set root directory per service via serviceUpdate
4. Link all to same repo, different build paths
```

## Important Notes
- Railway token is per-agent (stored in local env), not shared via MCP
- GitHub CLI (`gh`) is also per-agent — verify with `gh auth status`
- Railway auto-deploys on every push to the connected branch
- Free tier has limits — check Railway pricing for production workloads
- Use `serviceUpdate` to change build commands, start commands, or root directory
