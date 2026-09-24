# Users API

API REST para gerenciamento de usuários, desenvolvida com **NestJS**, **TypeScript**, **Prisma ORM** e **PostgreSQL**.

Projeto desenvolvido com foco em boas práticas de desenvolvimento de APIs REST, validação de dados, organização modular e persistência de dados.

## 🚀 Tecnologias

- Node.js
- NestJS
- TypeScript
- Prisma ORM
- PostgreSQL
- Docker
- class-validator
- class-transformer

## 📋 Funcionalidades

- Criar usuário
- Listar usuários
- Buscar usuário por ID
- Atualizar usuário
- Remover usuário
- Validação dos dados recebidos
- Validação de e-mail
- Controle de e-mail duplicado
- Tratamento de recursos não encontrados
- Persistência no PostgreSQL

## 📁 Estrutura

```text
src/
├── prisma/
│   ├── prisma.module.ts
│   └── prisma.service.ts
│
├── users/
│   ├── dto/
│   │   ├── create-user.dto.ts
│   │   └── update-user.dto.ts
│   ├── users.controller.ts
│   ├── users.module.ts
│   └── users.service.ts
│
├── app.module.ts
└── main.ts

prisma/
└── schema.prisma
```

## ⚙️ Pré-requisitos

- Node.js
- npm
- Docker

## 🔧 Instalação

Clone o repositório:

```bash
git clone <REPOSITORY_URL>
```

Entre no diretório:

```bash
cd users-api
```

Instale as dependências:

```bash
npm install
```

## 🗄️ Configuração do banco

Crie um arquivo `.env` na raiz do projeto:

```env
DATABASE_URL="postgresql://USER:PASSWORD@HOST:PORT/DATABASE"
```

Configure os valores de acordo com o seu ambiente local.

Suba o PostgreSQL com Docker:

```bash
docker compose up -d
```

Execute as migrations:

```bash
npx prisma migrate dev
```

Gere o Prisma Client:

```bash
npx prisma generate
```

> O arquivo `.env` não deve ser versionado. Utilize o `.env.example` para documentar as variáveis necessárias.

## ▶️ Executando

Para iniciar a aplicação em modo de desenvolvimento:

```bash
npm run start:dev
```

A API será executada localmente em:

```text
http://localhost:3000
```

## 🔌 Endpoints

| Método | Endpoint     | Descrição           |
| ------ | ------------ | ------------------- |
| POST   | `/users`     | Cria um usuário     |
| GET    | `/users`     | Lista os usuários   |
| GET    | `/users/:id` | Busca um usuário    |
| PATCH  | `/users/:id` | Atualiza um usuário |
| DELETE | `/users/:id` | Remove um usuário   |

### Criar usuário

```http
POST /users
```

```json
{
  "name": "John Doe",
  "email": "john@example.com"
}
```

### Atualizar usuário

```http
PATCH /users/:id
```

```json
{
  "name": "John Smith"
}
```

## 🛡️ Validação

A API utiliza `class-validator` para validação dos dados recebidos.

Exemplo:

```typescript
export class CreateUserDto {
  @IsString()
  @IsNotEmpty()
  name: string;

  @IsEmail()
  email: string;
}
```

O `ValidationPipe` é configurado globalmente no NestJS para executar as validações dos DTOs.

## 🗃️ Modelo de dados

O usuário possui um identificador UUID e e-mail único:

```prisma
model User {
  id        String   @id @default(uuid())
  name      String
  email     String   @unique
  createdAt DateTime @default(now())
}
```

## 🧱 Estrutura da aplicação

```text
HTTP Request
     ↓
Controller
     ↓
DTO / Validation
     ↓
Service
     ↓
Prisma
     ↓
PostgreSQL
```

## 🎯 Objetivo

Projeto desenvolvido para estudo e portfólio, com o objetivo de praticar o desenvolvimento de APIs backend utilizando **NestJS, TypeScript, Prisma e PostgreSQL**.

## 📄 Licença

Este projeto está disponível para fins de estudo e portfólio.
