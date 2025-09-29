# DevOps Challenge — Docker / K8s / Debug

Twoje zadanie:
1) **Docker Compose:** uruchom aplikację tak, by strona była dostępna na `http://localhost:8080`
2) **Kubernetes:** uruchom w namespace `challenge` i wystaw przez Ingress np. w minikube
3) Masz **120** minut na wykonanie zadania

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

## Zasady Challenge

- Ten challenge należy zrealizować w swoim forku tego repozytorium.
- **Limit czasu: 2 godziny** liczone od momentu utworzenia forka na GitHubie.
- Limit egzekwowany jest automatycznie przez GitHub Actions (`Deadline Guard`).
- Jeżeli spróbujesz oddać rozwiązanie po czasie — workflow się nie powiedzie.
- Nie wyłączaj ani nie modyfikuj workflow — traktowane będzie jako niezaliczenie.
- Po zakończeniu pracy zrób Pull Request **do swojego forka** (nie do repo głównego).
- Wszystkie zmiany będą widoczne w historii PR w Twoim repo.


## Kryteria zaliczenia
- `GET /health` zwraca `OK` (200)
- `GET /` zwraca „Welcome to DevOps Challenge!”
- `GET /api/messages` zwraca wpisy z bazy (po seedzie lub twoich insertach)

## Co oddać
- fork + PR do swojego forka
- Opis kroków naprawy (e-mail lub w PR)
- `docker compose ps` i `kubectl get pods -o wide` (e-mail lub w PR)
- Krótkie uzasadnienie diagnozy (e-mail lub w PR)

### Tipy
- `docker compose logs -f`
- `docker compose exec app sh`
- `kubectl -n challenge logs DEPLOY/NAME -f`
- `kubectl -n challenge exec -it POD -- sh`
