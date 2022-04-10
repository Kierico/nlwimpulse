# Comandos

<!-- package.json -->
1. `yarn init -y`

## Instalar Express, Prisma e Typescript

<!-- instalando dependencias -->
2. `yarn add express`

3. `yarn add -D @types/express typescript ts-node-dev`

<!-- started typescritp -->
4. `yarn tsc --init`

<!-- add no package.json -->
```json
    "scripts": {
        "dev": "ts-node-dev src/app.ts"
    },
```
5. `yarn dev`

<!-- install prisma.io -->
[prima.io](https://www.prisma.io/docs/getting-started/setup-prisma/add-to-existing-project/relational-databases-typescript-postgres)

6. `yarn add prisma -D`

7. `yarn prisma init`

<!-- apagar tudo de .env -->

<!-- add prisma/schema.prisma -->
```prisma
    datasource db {
        provider = "sqlite"
        url      = "file:./dev.db"
    }
```
[SQLite](https://www.prisma.io/docs/concepts/database-connectors/sqlite)

## Configurar Github OAuth

[OAuth Apps](https://github.com/settings/developers)

<!-- add .env -->
GITHUB_CLIENT_SECRET={client secret}
GITHUB_CLIENT_ID={client id}

## Criar rota login github

<!-- app.js -->
<!-- para usar o process.env -->
8. `yarn add dotenv`

```ts
    import "dotenv/config"
```

<!-- rodar aplicacao -->
9. `yarn dev`

<!-- cria rota login github -->
```ts
    app.get("/github", (request, response) => {
        response.redirect(`https://github.com/login/oauth/authorize?client_id=${process.env.GITHUB_CLIENT_ID}`);
    });
```

<!-- url de callback -->
```ts
    app.get("/signin/callback", (request, response) => {
        const { code } = request.query;

        return response.json(code);
    });
```

## Autenticação usuário recebendo o código

<!-- fazendo uma chamada para o github -->
10. `yarn add axios`

11. `yarn add @types/axios -D`

<!-- gerando token dentro da aplicação com o access_token -->
12. `yarn add jsonwebtoken`

13. `yarn add @types/jsonwebtoken -D`

<!-- instalar o plugin do Prisma: Prisma e Prisma - Insider -->
<!-- setting.json do VSCode -->
```prisma
    "[prisma]": {
        "editor.defaultFormatter": "Prisma.prisma"
    }
```

14. `yarn add @prisma/client`

15. `yarn prisma migrate dev`

? Enter a name for the new migration: >> create-user

<!-- alterar no package.json para fazer o Reload -->
```json
    "scripts": {
        "dev": "ts-node-dev --exit-child src/app.ts"
    }
```

## Cadastro das mensagens

16. `yarn prisma migrate dev`
? Enter a name for the new migration: >> create-messages

<!-- Criando as mensagens -->
<!-- OBS: se estiver dando erro em "request.user_id = sub" no arquivo 'ensureAuthenticated.ts', add o typeRoots que está logo abaixo. -->
```json
    "typeRoots": ["./src/@types", "node_modules/@types"]
```

    Se precisar `yarn dev`

17. `yarn prisma studio`

## Configurando do websocket

[Socket.io](https://socket.io/get-started/chat)

18. `yarn add socket.io`

19. `yarn add @types/socket.io -D`

<!-- app.ts, subindo servidor via http-->
<!-- cors, permite ou barra as requisições na aplicação -->
20. `yarn add cors`

21. `yarn add @types/cors -D`

<!-- Create paste public/index.html, e dentro do "body" colocar o código abaixo. -->
```html
    <script
        src="https://cdnjs.cloudflare.com/ajax/libs/socket.io/4.0.1/socket.io.min.js"
        integrity="sha512-eVL5Lb9al9FzgR63gDs1MxcDS2wFu3loYAgjIH0+Hg38tCS8Ag62dwKyH+wzDb+QauDpEZjXbMn11blw8cbTJQ=="
        crossorigin="anonymous">
        </script>
```

<!-- alterar no "package.json". Vai ficar ouvindo o "sever.ts" e não mais o 'app.ts' -->
```json
    "scripts": {
        "dev": "ts-node-dev --exit-child src/server.ts"
    },
```

## Retornar o profile do user

