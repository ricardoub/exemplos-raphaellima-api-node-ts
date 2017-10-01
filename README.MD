# API - NODE - TYPESCRIPT - EXPRESS - POSTGRESQL - SEQUELIZE

## Criação do projeto
```
npm init -y
git init
git remote add origin  https://github.com/ricardoub/exemplos-raphaellima-api-node-ts.git

```

https://github.com/ricardoub/api-node-typescript.git
---

# Passo a passo do projeto
1.  criação do arquivo **tsconfig.json** na raiz do projeto
2.  executar o comando ``` npm init -y ```
3.  executar a instalação da **dependencia de projeto nro.1**
    2. No meu caso foi preciso utilizar o sudo, verifique isso ao executar

4.  criar o diretório src
    1.  mudar para o diretório src
    2.  criar o arquivo **test.ts** com o conteúdo    
    3.  executar o comando ``` node_modules/.bin/tsc ```

5.  criação do arquivo gulpfile.js na raiz do projeto
    1.  executar a instalação da **dependencia de projeto nro.2**.
    2.  executar o comando ``` gulp ```
        * pode ser necessário criar o diretório dist se houver erro na execução do comando

6.  executar a instalação da **dependencia de projeto nro.3, 4, 5 e 6** para a instalação do express e suas dependencias

7.  criação do arquivo **index.ts** dentro de **src**
8.  criação do arquivo **App.ts** dentro de **src**
9.  criação da pasta **routes**
    1. criação do arquivo **routes/personRoutes**


---


# Dependencias de projeto
1.  ``` npm install typescript@2.0.6 --save-dev ```
2.  ``` npm install gulp@3.9.1 gulp-typescript@3.1.1 --save-dev ```
3.  ``` npm install express@4.14.0 debug@2.2.0 --save ```
4.  ``` npm install @types/node@6.0.46 @types/express@4.0.33 @types/debug@0.0.29 --save-dev ```
5.  ``` npm install express@4.14.0 body-parser@1.15.2 morgan@1.7.0 --save ```
6.  ``` npm install @types/body-parser@0.0.33 @types/morgan@1.7.32 --save-dev ```


---

# Conteúdos dos arquivos utilizados no passo a passo do projeto

## Arquivos da aplicação
### routes/personRoutes.ts
```
import { Router, Request, Response, NextFunction } from 'express';

export class PersonRouter {
    router: Router

constructor() {
        this.router = Router();
        this.init();
    }

public get(req: Request, res: Response, next: NextFunction) {
        res.send("Person");
    }

init() {
        this.router.get('/', this.get);
    }
}

const personRouter = new PersonRouter();
personRouter.init();

export default personRouter.router;
```

### src/index.ts
```
import * as http from 'http';
import * as debug from 'debug';

import App from './App';

debug('ts-express:server');

const port = normalizePort(process.env.PORT || 3000);
App.set('port', port);

const server = http.createServer(App);
server.listen(port);
server.on('error', onError);
server.on('listening', onListening);

function normalizePort(val: number|string): number|string|boolean {
  let port: number = (typeof val === 'string') ? parseInt(val, 10) : val;
  if (isNaN(port)) return val;
  else if (port >= 0) return port;
  else return false;
}

function onError(error: NodeJS.ErrnoException): void {
  if (error.syscall !== 'listen') throw error;
  let bind = (typeof port === 'string') ? 'Pipe ' + port : 'Port ' + port;
  switch(error.code) {
    case 'EACCES':
      console.error(`${bind} requires elevated privileges`);
      process.exit(1);
      break;
    case 'EADDRINUSE':
      console.error(`${bind} is already in use`);
      process.exit(1);
      break;
    default:
      throw error;
  }
}

function onListening(): void {
  let addr = server.address();
  let bind = (typeof addr === 'string') ? `pipe ${addr}` : `port ${addr.port}`;
  debug(`Listening on ${bind}`);
}
```

---

## Arquivos de configuração
### tsconfig.json
```
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "dist"
  },
  "include": [
    "src/**/*.ts"
  ],
  "exclude": [
    "node_modules"
  ]
}
```

### gulpfile.js
```
const gulp = require('gulp');

const ts = require('gulp-typescript');
const JSON_FILES = ['src/*.json', 'src/**/*.json'];

const tsProject = ts.createProject('tsconfig.json');

gulp.task('scripts', () => {
  const tsResult = tsProject.src()
  .pipe(tsProject());
  return tsResult.js.pipe(gulp.dest('dist'));
});

gulp.task('watch', ['scripts'], () => {
  gulp.watch('src/**/*.ts', ['scripts']);
});

gulp.task('assets', function() {
  return gulp.src(JSON_FILES)
  .pipe(gulp.dest('dist'));
});

gulp.task('default', ['watch', 'assets']);
```

---

## Arquivos de teste
### test.ts
```
console.log('Hello world!');
```
