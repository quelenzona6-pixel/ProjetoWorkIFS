
## Como Executar o Projeto

### Pré-requisitos

- Navegador web  (Chrome, Firefox, Edge, Safari)
- Extensão Live Server (VS Code)

### Opção 1: Usando Live Server (VS Code)

1. Instale a extensão **Live Server** no VS Code
2. Clone ou baixe o projeto
3. Abra a pasta do projeto no VS Code
4. Clique com botão direito no arquivo `index.html`
5. Selecione "Open with Live Server"
6. O navegador abrirá automaticamente em 
`http://localhost:5500` ou `http://127.0.0.1:5500`

**Atenção**: Algumas funcionalidades (como OAuth) podem não funcionar corretamente ao abrir diretamente sem servidor local.

## Configuração do Google OAuth 2.0 (API)

O projeto já está configurado com um Client ID do Google OAuth. Para usar a funcionalidade de login social:

### URIs Configurados:
- `http://localhost:5500/pages/auth/oauth-callback.html`
- `http://127.0.0.1:5500/pages/auth/oauth-callback.html`

### Como foi configurado o Client ID:

1. Acesse o [Google Cloud Console](https://console.cloud.google.com/)
2. Crie um novo projeto ou selecione um existente
3. Vá em **APIs e Serviços** → **Credenciais**
4. Clique em **Criar credenciais** → **ID do cliente OAuth 2.0**
5. Configure:
   - Tipo de aplicativo: **Aplicativo da Web**
   
   - Origens JavaScript autorizadas:
     - `http://localhost:5500`

     - `http://127.0.0.1:5500`

   - URIs de redirecionamento autorizados:
     - `http://localhost:5500/pages/auth oauth-callback.html`

     - `http://127.0.0.1:5500/pages/auth/oauth-callback.html`

6. Copie o Client ID gerado
7. Substitua no arquivo `pages/auth/login.html` na linha:
   ```javascript
   const GOOGLE_CLIENT_ID = 'SEU_CLIENT_ID_AQUI';
   ```

## Armazenamento de Dados

O projeto utiliza **localStorage** do navegador para persistência de dados. Os dados são armazenados localmente e não há backend ou banco de dados SQL.

### Estruturas de Dados:
- `contasAlunos[]` - Contas de estudantes
- `contasEmpresas[]` - Contas de empresas
- `vagasEmpresa[]` - Vagas publicadas
- `candidaturas[]` - Candidaturas realizadas
- `userLogado` / `empresaLogada` - Sessão ativa


## Segurança

- Validação de formulários no cliente
- OAuth 2.0 com state e nonce para prevenção de CSRF
- Sessões gerenciadas com localStorage/sessionStorage
- Validação de tokens JWT no callback