# lopsia-deploy

Dépôt de déploiement des produits LopsIA sur VPS client.

## Prérequis

- Ubuntu 24.04
- Docker + Docker Compose
- Accès SSH depuis le bastion staging

## Déploiement

```bash
git clone https://github.com/mclpfr/lopsia-deploy.git
cd lopsia-deploy
cp .env.example .env
# Renseigner les variables dans .env
docker compose up -d
```

## Structure

```
lopsia-deploy/
├── docker-compose.yml      # Traefik + n8n (base)
├── .env.example            # Template variables
├── traefik/
│   └── traefik.yml         # Config reverse proxy
└── workflows/              # Workflows n8n (copiés par l'agent au déploiement)
```

## Produits disponibles

L'agent ajoute automatiquement le(s) produit(s) achetés dans `docker-compose.yml` :

| Produit | Image Docker | Variable env |
|---------|-------------|--------------|
| InvoiSage | `mclpfr/ivs:latest` | `SUPABASE_URL_IVS` + `SUPABASE_SERVICE_KEY_IVS` |
| CRM IA | `mclpfr/crm:latest` | `SUPABASE_URL_CRM` + `SUPABASE_SERVICE_KEY_CRM` |
| RAG | `mclpfr/rag:latest` | `SUPABASE_URL_RAG` + `SUPABASE_SERVICE_KEY_RAG` |

## Convention de nommage

- **Trigramme** : TeckCorp → `tkp` / Martin Dupont → `mdu`
- **URL** : `ivs-tkp.lopsia.fr`, `crm-tkp.lopsia.fr`, `rag-tkp.lopsia.fr`
- **Projet Supabase** : `teckcorp` ou `martin-dupont`
