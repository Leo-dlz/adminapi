# TP1 : exploration des API Docker et NetBox

## API Docker (http://127.0.0.1:2375)

| Commande | Code |
|---|---|
| `curl -s $D/version` | 200 |
| `curl -s "$D/containers/json?all=true"` | 200 |
| `curl -s --get $D/containers/json --data-urlencode 'all=true' --data-urlencode 'filters={"label":["adminapi.managed=true"]}'` | 200 |
| `curl -s $D/containers/web1/json` | 200 |
| `curl -i -X POST $D/containers/web1/stop` (1re fois) | 204 |
| `curl -i -X POST $D/containers/web1/stop` (2e fois) | 304 |
| `curl -i -X POST $D/containers/inexistant/stop` | 404 |
| `curl -i -X POST $D/containers/web1/start` | 204 |

- 204 : l'action a réussi, la réponse n'a pas de corps.
- 304 : le conteneur était déjà arrêté, Docker n'a rien modifié.
- 404 : le conteneur n'existe pas.
- Le filtre par label ne renvoie que `web1`, pas `intrus`.

## API NetBox (http://127.0.0.1:8080/api)

| Commande | Code |
|---|---|
| `POST /users/tokens/provision/` (username et password) | 201 |
| `POST /virtualization/cluster-types/` (Docker) | 201 |
| `POST /virtualization/clusters/` (docker-local) | 201 |

Le token est rangé dans `.env`, qui n'est pas versionné.
