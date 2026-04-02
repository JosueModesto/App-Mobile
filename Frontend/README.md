# 📱 Frontend Flutter Web: API de Usuários

Este `README` ensina a usar todas as funcionalidades do aplicativo:
- CADASTRAR usuário
- LISTAR usuários
- EDITAR usuário
- DELETAR usuário

O app consome a API em `http://127.0.0.1:3000/usuarios`.

## 🛠️ Tecnologias Utilizadas
* Flutter & Dart
* package:http para requisições HTTP
* Material Design

---

## 📋 Pré-requisitos
1. Flutter SDK instalado.
2. Backend rodando em `http://127.0.0.1:3000` (Node.js + PostgreSQL + CORS ativo).
3. `flutter pub get` executado na pasta Frontend.

---

## 🚀 Como rodar
```bash
cd App-Mobile/Frontend
flutter pub get
flutter run -d chrome
```

---

## 🧩 Como usar o app
1. Tela inicial (`TelaPrincipal`):
   - botão `CADASTRAR USUÁRIO`: abre `TelaCadastro` para criar novo usuário.
   - botão `LISTAR USUÁRIOS`: abre `TelaListagem`.

2. Tela de listagem (`TelaListagem`):
   - Consulta GET automático em `/usuarios`.
   - Lista usuários em cards.
   - Botão de lixeira (delete): chama DELETE `/usuarios/{id}` com confirmação.
   - Botão de lápis (editar): abre `TelaCadastro` com dados preenchidos para edição.

3. Tela de cadastro/edição (`TelaCadastro`):
   - Campo nome e e-mail.
   - Botão SALVAR:
     * Se `usuarioParaEditar` existir, chama PUT `/usuarios/{id}`.
     * Caso contrário, chama POST `/usuarios`.
   - Após salvar, retorna à tela anterior e atualiza lista.

---

## ⚙️ Ajustes importantes no código
* `lib/services/api_service.dart`:
  - `getUsuarios()` -> GET `/usuarios`
  - `criarUsuario()` -> POST `/usuarios`
  - `atualizarUsuario()` -> PUT `/usuarios/{id}`
  - `deleteUsuario()` -> DELETE `/usuarios/{id}`

* `lib/models/usuario_model.dart`:
  - `id` é `int?` para permitir criar novos registros sem id inicial.

---

## 🐞 Problemas comuns
- `Failed to fetch`: backend offline ou CORS ausente.
- `404 /usuarios` : backend rodando em porta errada.
- `401/403`: verifique CORS no projeto Node.js.

3. **Crucial:** O backend deve estar com a biblioteca `cors` configurada e ativada no `app.js`, caso contrário o navegador bloqueará a comunicação!

---

## 🚀 Como Rodar o Projeto

### Passo 1: Clonar o Repositório
Abra o terminal e clone este projeto em uma pasta separada do backend:
```bash
git clone https://github.com/ipolato/opt120_fontend_exemplo.git
cd opt120_fontend_exemplo
```
### Passo 2: Instalar as Dependências
Baixe os pacotes necessários (como o pacote http) definidos no arquivo pubspec.yaml:

```bash
flutter pub get
```

### Passo 3: Executar no Navegador
Como o nosso foco para evitar travamentos com emuladores é a Web, execute o aplicativo diretamente no Google Chrome:

```bash
flutter run -d chrome
```

## 📁 Arquitetura do Projeto
Nós não misturamos regras de internet com botões! O código fonte (dentro da pasta lib/) está estruturado da seguinte forma:

* models/usuario_model.dart: A "fôrma" dos nossos dados. Ele traduz o JSON que vem da internet para um Objeto Dart, e vice-versa.

* services/api_service.dart: O nosso "carteiro". É o único arquivo que sabe o endereço do servidor (http://127.0.0.1:3000) e usa o pacote http para fazer as chamadas.

* screens/: Onde a mágica visual acontece.

- tela_principal.dart: O menu com os botões de navegação.

- tela_cadastro.dart: O formulário que captura a digitação e faz o POST.

- tela_listagem.dart: Usa um FutureBuilder poderoso para ler a resposta do GET e desenhar a lista na tela automaticamente.

* main.dart: O ponto de partida limpo, que apenas configura as cores (Tema) e chama a tela principal.

## 🚨 Resolução de Problemas Comuns (Troubleshooting)
Erro: ClientException: Failed to fetch
Este é o erro número 1 de comunicação. Se ele aparecer, verifique duas coisas:

1. O Servidor Node.js está ligado? Você precisa rodar node server.js no terminal do outro projeto.

2. Problema de Localhost: No arquivo lib/services/api_service.dart, certifique-se de que a baseUrl está usando http://127.0.0.1:3000 em vez de http://localhost:3000. O Flutter Web costuma se confundir com a palavra localhost.

3. CORS Bloqueado: Verifique se no arquivo app.js do seu Node.js, a linha app.use(cors()); está antes da linha de rotas (app.use('/usuarios', usuarioRoutes);)..
