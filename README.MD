# API - NODE - TYPESCRIPT - EXPRESS - POSTGRESQL - SEQUELIZE

## Criação do projeto
```
npm init -y
git init
git remote add origin  https://github.com/ricardoub/exemplos-raphaellima-api-node-ts.git
git add .
git commit -m "first commit - project created"
git push -u origin master
echo 'Ricardo Bomfim' >> contributors.txt
git add contributors.txt
git commit -m 'Initial commit with contributors'
git push -u origin master

```

## Dependencias de projeto
```
npm i body-parser express http morgan pg -S
npm i ts-node -D
npm i @types/express @types/body-parser @types/morgan -D
npm install @types/bluebird@ts2.2
npm i sequelize sequelize-cli -S
npm i sequelize @types/sequelize -D
```

---

# Conteúdos dos arquivos utilizados no passo a passo do projeto

### Arquivos da aplicação
#### routes/personRoutes.ts
