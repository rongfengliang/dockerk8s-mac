# basic k8s operate on mac
## init docker-mac
```bash
https://docs.docker.com/docker-for-mac/kubernetes/
```
## first nginx deploy
```bash
  kubectl run nginx --image=nginx
```
## expose with service
```bash
kubectl create -f nginx-svc.yml
```
## get my k8s node info
```bash
kubectl get node

that will print this
NAME                 STATUS    ROLES     AGE       VERSION
docker-for-desktop   Ready     master    37m       v1.8.2
```
## deploy application with docke-compose stack
```bash
version: '3.3'

services:
  web:
    build: web
    image: dockerdemos/lab-web
    volumes:
     - "./web/static:/static"
    ports:
     - "80:80"

  words:
    build: words
    image: dockerdemos/lab-words
    deploy:
      replicas: 5
      endpoint_mode: dnsrr
      resources:
        limits:
          memory: 16M
        reservations:
          memory: 16M

  db:
    build: db
    image: dockerdemos/lab-db


docker stack deploy -c docker-compose.yml  mynginx-demo
```

> note

> you network must can be access google docker image

