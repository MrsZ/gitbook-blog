Sequelize

[http://docs.sequelizejs.com/manual/tutorial/migrations.html](http://docs.sequelizejs.com/manual/tutorial/migrations.html)

[http://sequelize.readthedocs.io/en/latest/docs/migrations/](http://sequelize.readthedocs.io/en/latest/docs/migrations/)

install cli

```bash
npm install --save sequelize-cli
```

init

```bash
node_modules/.bin/sequelize init
```

config file : `config/config.json`



generate migration file

```bash
node_modules/.bin/sequelize migration:create --name create-ticket-tiers
```

running migrate

```bash
node_modules/.bin/sequelize db:migrate
```

undo migration

```bash
node_modules/.bin/sequelize db:migrate:undo
```



running seed

```bash
node_modules/.bin/sequelize db:seed:all
```

undo seed

```bash
node_modules/.bin/sequelize db:seed:undo
```

```bash
node_modules/.bin/sequelize db:seed:undo:all
```

create seed

```js

```



