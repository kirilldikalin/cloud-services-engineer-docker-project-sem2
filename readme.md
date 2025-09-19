

## Сборка и запуск бэка

docker build -f backend/Dockerfile -t momo-backend:0.1 ./backend
docker run -d --rm --name momo-backend -p 8081:8081 momo-backend:0.1
curl -i http://localhost:8081/health
docker logs -f momo-backend
docker stop momo-backend

```
HTTP/1.1 200 OK
Vary: Origin
Date: Fri, 19 Sep 2025 09:36:05 GMT
Content-Length: 0
{"level":"debug","ts":1758274553.1832712,"caller":"api/main.go:40","msg":"creating app instance"}
{"level":"info","ts":1758274553.1884818,"caller":"api/main.go:57","msg":"starting HTTP server","address":":8081"}
{"level":"debug","ts":1758274565.235885,"caller":"api/router.go:50","msg":"got request","method":"GET","uri":"/health"}
```

## Сборка и запуск фронта

docker build -f frontend/Dockerfile -t momo-frontend:0.1 ./frontend
docker run -d --rm --name momo-frontend -p 80:8080 momo-frontend:0.1
curl -I http://localhost/

Результат

```
HTTP/1.1 200 OK
Server: nginx/1.25.5
Date: Fri, 19 Sep 2025 09:38:25 GMT
Content-Type: text/html
Content-Length: 1726
Last-Modified: Fri, 19 Sep 2025 09:38:03 GMT
Connection: keep-alive
ETag: "68cd247b-6be"
Accept-Ranges: bytes
```