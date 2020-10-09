# egg

## plugin

## service

## controller

## public

## config

## schedule：计划任务

## i18n 国际化

i18n={
defaultLocal:'zh-CN'
}

### 扩展属性-

npm i egg-scripts --save

egg-scripts start --port=7001 --daemon --title=egg-server-showcase

egg-scripts stop [--title=egg-server]

install i alinode -g

install i egg-alinode --save

### sequelize

.sequelizerc //入口指定不同的文件的路径信息

```shell

npx sequelize init:config  //生成config 配置文件
npx sequelize init:migrations //生成migrations 文件夹
 npx sequelize init:models   //生成models文件夹 操作数据库模型
npx sequelize migration:generate --name init-users //生成建表数据规则文件
npx sequelize seed:generate --name init-users  //生成填充种子数据初始数据文件
npx sequelize db:seed:all //插入数据
npx sequelize db:migrate
npx sequelize db:migrate --env=test //测试库
```
