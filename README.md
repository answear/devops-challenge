# DevOps Challenge — Docker / K8s / Debug

Twoje zadanie:
1) **Docker Compose:** uruchom aplikację tak, by strona była dostępna na `http://localhost:8080`
2) **Kubernetes:** uruchom w namespace `challenge` i wystaw przez Ingress np. w minikube

## Skład
- **nginx**: reverse proxy
- **app (Node.js + Express)**: endpointy `/`, `/health`, `/api/messages`
- **mysql**: baza z tabelą `messages` i seedem

## Jak uruchomić (Docker Compose)
```bash
docker compose up -d
curl -fsS http://localhost:8080/health
curl -fsS http://localhost:8080/
curl -fsS http://localhost:8080/api/messages
```

## Jak uruchomić (Kubernetes)
```bash
kubectl apply -f k8s/namespace.yaml
kubectl -n challenge apply -f k8s/mysql.yaml
kubectl -n challenge apply -f k8s/app.yaml
kubectl -n challenge apply -f k8s/ingress.yaml
kubectl -n challenge get pods,svc,ingress
```

## Kryteria zaliczenia
- `GET /health` zwraca `OK` (200)
- `GET /` zwraca „Welcome to DevOps Challenge!”
- `GET /api/messages` zwraca wpisy z bazy (po seedzie lub twoich insertach)

## Co oddać
- fork + PR do swojego forka - ewentualnie zip na mail'a
- Opis kroków naprawy
- `docker compose ps` i `kubectl get pods -o wide`
- Krótkie uzasadnienie diagnozy

### Tipy
- `docker compose logs -f`
- `docker compose exec app sh`
- `kubectl -n challenge logs DEPLOY/NAME -f`
- `kubectl -n challenge exec -it POD -- sh`
