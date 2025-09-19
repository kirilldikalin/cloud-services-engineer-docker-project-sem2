

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

## Соберка и запуска компоуза

```bash
docker compose build
```

```
[+] Building 2/2
 ✔ backend   Built                                                                                                                                0.0s 
 ✔ frontend  Built    
```

```bash
docker compose up -d
```

```
WARN[0000] /Users/kirilldikalin/work/ITMO/practicum/cloud-services-engineer-docker-project-sem2/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
[+] Running 2/2
 ✔ Container momo-backend   Started                                                                                                               0.2s 
 ✔ Container momo-frontend  Started     
 ```

 ### Проверка логов

 ```
 kirilldikalin@MacBook-Air-Kirill-2 cloud-services-engineer-docker-project-sem2 % docker compose logs -f backend
docker compose logs -f frontend
WARN[0000] /Users/kirilldikalin/work/ITMO/practicum/cloud-services-engineer-docker-project-sem2/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
momo-backend  | {"level":"debug","ts":1758275365.9354858,"caller":"api/main.go:40","msg":"creating app instance"}
momo-backend  | {"level":"info","ts":1758275365.9413557,"caller":"api/main.go:57","msg":"starting HTTP server","address":":8081"}
momo-backend  | {"level":"debug","ts":1758275404.8392031,"caller":"api/router.go:50","msg":"got request","method":"GET","uri":"/health"}
^Cexit status 130
WARN[0000] /Users/kirilldikalin/work/ITMO/practicum/cloud-services-engineer-docker-project-sem2/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
momo-frontend  | /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
momo-frontend  | /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
momo-frontend  | /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
momo-frontend  | 10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
momo-frontend  | 10-listen-on-ipv6-by-default.sh: info: /etc/nginx/conf.d/default.conf differs from the packaged version
momo-frontend  | /docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
momo-frontend  | /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
momo-frontend  | /docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
momo-frontend  | /docker-entrypoint.sh: Configuration complete; ready for start up
momo-frontend  | 2025/09/19 09:49:26 [notice] 1#1: using the "epoll" event method
momo-frontend  | 2025/09/19 09:49:26 [notice] 1#1: nginx/1.25.5
momo-frontend  | 2025/09/19 09:49:26 [notice] 1#1: built by gcc 13.2.1 20231014 (Alpine 13.2.1_git20231014) 
momo-frontend  | 2025/09/19 09:49:26 [notice] 1#1: OS: Linux 6.10.14-linuxkit
momo-frontend  | 2025/09/19 09:49:26 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
momo-frontend  | 2025/09/19 09:49:26 [notice] 1#1: start worker processes
momo-frontend  | 2025/09/19 09:49:26 [notice] 1#1: start worker process 29
momo-frontend  | 2025/09/19 09:49:26 [notice] 1#1: start worker process 30
momo-frontend  | 2025/09/19 09:49:26 [notice] 1#1: start worker process 31
momo-frontend  | 2025/09/19 09:49:26 [notice] 1#1: start worker process 32
momo-frontend  | 2025/09/19 09:49:26 [notice] 1#1: start worker process 33
momo-frontend  | 2025/09/19 09:49:26 [notice] 1#1: start worker process 34
momo-frontend  | 2025/09/19 09:49:26 [notice] 1#1: start worker process 35
momo-frontend  | 2025/09/19 09:49:26 [notice] 1#1: start worker process 36
momo-frontend  | 192.168.65.1 - - [19/Sep/2025:09:50:09 +0000] "HEAD / HTTP/1.1" 200 0 "-" "curl/8.7.1" "-"
^Cexit status 130
```

Успешный успех =)