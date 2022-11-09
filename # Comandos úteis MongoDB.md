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

```javascript
-insert({}) - insertOne({}) - insertMany([{}, {}, {}]);
```

Read -> Ler o recurso

```javascript
- find(<query>, <projection>)
- findOne(<query>, <projection>)
```

Update -> Atualizar o recurso

```javascript
- update(<query>, <update>, <options>)
- updateOne(<query>, <update>, <options>)
- updateMany(<query>, <update>, <options>)
```

Delete -> Deletar o recurso

```javascript
- deleteOne(<query>)
- deleteMany(<query>)
```

## O que cada query significa?

A forma abaixo é depreciada e deve ser evitada.

```
db.crud.insert({a: 123})
db.crud.insert([{a: 123}, {b: 456}])
```

Inserindo mais de um elemento forma correta:

```
db.crud.insertMany([{a:123}, {b:456}, {c:789}])
```

Se ordered for true ele para no meio das inserções em caso de erro.

```
db.crud.insertMany([{a:123}, {b:123}, {c:345}], {ordered: false})
```

Da maneira que está a query abaixo, estamos inserindo e forçando valores para o campo id:

```
db.testInsertMany.insertMany([{_id: 1, a: 123}, {_id: 2, b: 456}, {_id: 3, c:789}])
```

O valor padrão do ordered é true. Neste caso não vai ser possível inserir porque já temos um documento com o mesmo id forçado na query acima.

```
db.testInsertMany.insertMany([{_id: 2}, {_id: 7, msg: 'test'}], {ordered: true})
```

Quando ordered é false temos a possibilidade de continuar inserindo apesar do erro ocorrido.

```
db.testInsertMany.insertMany([{_id: 2}, {_id: 7, msg: 'test'}], {ordered: false})
```

Inserindo um documento com muitos dados diferentes.

```
db.alunos.insertOne({
  'nome': 'Toninho',
  'idade': 12,
  'gostaDe': [
    'futebol',
    'carrinho',
    'video game'
  ],
  'naEscola': true,
  'materias': {
    'português': 8.9,
    'matemática': 9.5,
    'história': 2.4
  }
})
```

O método find encontra todos os documentos que dão match com a query.

```
db.crud.find({b: 456})
db.crud.find({b: 123})
```

O método findOne encontra apenas o primeiro.

```
db.crud.findOne({b: 456})
```

A query abaixo encontra todos os documentos que contem a chave c.
$exists é um boolean que define se queremos que c exista ou não na busca.

```
db.crud.find({c: {$exists: true}})
```

No caso abaixo não há ninguém com esse campo nos documentos.
O retorno é null.

```
db.alunos.findOne({altura: 1.84})
```

### Projetions

Nessa query estamos usando projeção. Campos marcados com 1 serão exibidos. \_id foi marcado para ser omitido como o resultado no resultado das buscas.

```
db.alunos.findOne({}, { nome: 1, materias: 1, _id: 0 })
```

Exatamente a mesma query acima.

```
db.alunos.findOne({}, { nome: true, materias: true, _id: false })
```

O resultado é parecido com o da query acima, porém \_id é exibido por padrão.

```
db.alunos.findOne({}, { nome: 1, materias: 1 })
```
