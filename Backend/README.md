# 🚀 API de Usuários (Backend)

Este `README` explica todas as rotas e como usar as funcionalidades disponíveis na API de usuários.

## � Repositório
Clone o repositório oficial:
```bash
git clone https://github.com/JosueModesto/App-Mobile.git
cd App-Mobile/Backend
```

## 📁 Estrutura de pastas
- Backend: `App-Mobile/Backend`
- Frontend: `App-Mobile/Frontend`

## �🛠️ Tecnologias Utilizadas
* Node.js + Express
* PostgreSQL
* Docker, Docker Compose
* Swagger (OpenAPI)
* pg (driver PostgreSQL)

---

## 📋 Pré-requisitos
1. Git
2. Node.js 18+
3. Docker Desktop (com contêiner PostgreSQL ativo)

---

## 🚀 Como rodar localmente
No terminal (dentro de `App-Mobile/Backend`):

```bash
# 1) Iniciar containers do banco
docker compose up -d

# 2) Instalar dependências Node
npm install

# 3) Rodar backend
node --watch server.js
```

A API fica disponível em `http://localhost:3000`.

---

## 📌 Endpoints da API (funcionalidades)
### 1) Listar todos os usuários
GET `http://localhost:3000/usuarios`
Resposta 200: lista JSON de usuários.

### 2) Criar um usuário
POST `http://localhost:3000/usuarios`
Body (JSON):
```json
{
  "nome": "João",
  "email": "joao@example.com"
}
```
Resposta 201: usuário recém-criado.

### 3) Atualizar um usuário
PUT `http://localhost:3000/usuarios/{id}`
Body (JSON):
```json
{
  "nome": "João Silva",
  "email": "joao.silva@example.com"
}
```
Resposta 200: usuário atualizado.

### 4) Deletar um usuário
DELETE `http://localhost:3000/usuarios/{id}`
Resposta 200: usuário deletado.

---

## 🧪 Testar com Swagger
Acesse: `http://localhost:3000/api-docs`.

---

## 💡 Dicas rápidas (CORS/Conexão)
* Se o frontend falhar com `Failed to fetch`, verifique se o backend está rodando.
* Verifique `app.use(cors())` em `app.js` e as rotas com `app.use('/usuarios', usuarioRoutes);`
* Use `http://127.0.0.1:3000` no frontend para evitar problemas de `localhost` em Web.


### Passo 1: Clonar o Repositório
Abra o seu terminal e clone este repositório para a sua máquina local:
```bash
git clone https://github.com/ipolato/opt120-backend-exemplo.git
cd opt120-backend-exemplo
```

### Passo 2: Subir a Infraestrutura (Banco de Dados)
Não precisamos instalar o PostgreSQL no computador! Vamos usar o Docker para baixar e rodar um contêiner pronto com o banco de dados e a interface do pgAdmin. No terminal, execute:

```bash
docker compose up -d
```
A flag -d significa "detached", liberando o seu terminal para o próximo passo. O Postgres estará rodando na porta 5432.

### Passo 3: Instalar as Dependências do Node.js
Agora precisamos baixar as bibliotecas de código (como o Express e o driver do Postgres) que a nossa API utiliza. Execute:

```bash
npm install
```

### Passo 4: Ligar o Servidor Backend
Com o banco rodando e as dependências instaladas, inicie a API. O nosso código já possui uma rotina de inicialização automática: ao ligar, ele verificará o banco de dados e criará a tabela usuarios sozinho caso ela não exista.

```bash
node --watch server.js
```
A flag --watch faz com que o servidor reinicie automaticamente toda vez que você salvar uma alteração no código.

## 🧪 Como Testar a API (Swagger)

A nossa API não tem uma interface visual tradicional (Frontend), mas implementamos o Swagger para facilitar os testes!

Abra o seu navegador e acesse: http://localhost:3000/api-docs

Para Cadastrar um Usuário (POST):

Clique na rota verde POST /usuarios.

Clique no botão "Try it out".

Altere os valores de "nome" e "email" no campo de texto JSON.

Clique em "Execute". Role para baixo e verifique se o Server response retornou código 201.

Para Listar os Usuários (GET):

Clique na rota azul GET /usuarios.

Clique no botão "Try it out" e depois em "Execute".

Você verá a lista de usuários salvos vindo diretamente do banco de dados!
