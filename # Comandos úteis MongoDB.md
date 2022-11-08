# Comandos úteis MongoDB


## Como criar um container docker com mongoDb 
```shell
docker run --name mongodb -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=codedemobr -e MONGO_INITDB_ROOT_PASSWORD=123abc mongo
```

## Como se conectar
```shell
mongodb://codedemobr:123abc@localhost:27017/admin
```
## Como parar ou subir um container docker
```shell
# SUBIR
docker container start nome_ou_id
# PARAR
docker container stop nome_ou_id
```

## Comandos

Listar todos os documentos de uma collection:

```
db.minhacollection.find()
```

Listar o primeiro documento de uma collection:

```
db.minhacollection.findOne()
```

Saber a data de um documento:
```
db.minhaCollection.findOne()._id.getTimestamp()
```
