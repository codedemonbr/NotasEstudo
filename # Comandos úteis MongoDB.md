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

### CRUD

Create -> Criar um recurso

- insert({})
- insertOne({})
- insertMany([{}, {}, {}])

Read -> Ler o recurso

- find(<query>, <projection>)
- findOne(<query>, <projection>)

Update -> Atualizar o recurso

```javascript
- update(<query>, <update>, <options>)
- updateOne(<query>, <update>, <options>)
- updateMany(<query>, <update>, <options>)
```

Delete -> Deletar o recurso

- deleteOne(<query>)
- deleteMany(<query>)
