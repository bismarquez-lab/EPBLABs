# Configuração do Microsoft Authenticator - EPB Sistema

## ✅ O que foi implementado

O sistema EPB agora possui integração completa com Microsoft Authenticator, incluindo:

- **Login via Microsoft**: Botão azul na página de login para autenticação Microsoft
- **Criação automática de contas**: Usuários Microsoft são automaticamente criados no sistema
- **Vinculação de contas**: Contas Microsoft podem ser vinculadas a contas existentes via email
- **Interface moderna**: Botões de autenticação com ícones Microsoft e feedback visual
- **Segurança**: Uso da biblioteca oficial MSAL para autenticação segura

## 🔧 Próximos passos para ativação

### 1. Registrar aplicativo no Azure Portal

1. **Acesse**: [Azure Portal](https://portal.azure.com)
2. **Navegue**: App registrations → New registration
3. **Configure**:
   - **Nome**: Sistema EPB - Compartilhamento de Arquivos
   - **Tipos de conta**: "Accounts in any organizational directory and personal Microsoft accounts"
   - **URI de redirecionamento**: Single-page application
   - **URL**: `https://your-replit-domain.replit.app` (substitua pela URL real)

4. **Copie o Client ID** que será exibido após a criação

### 2. Configurar permissões

No seu app registration:
1. Vá em "API permissions"
2. Adicione as permissões Microsoft Graph:
   - `User.Read` ✓
   - `profile` ✓  
   - `email` ✓

### 3. Configurar variáveis de ambiente

Crie/edite seu arquivo `.env` com:

```env
# Microsoft Authentication
VITE_MICROSOFT_CLIENT_ID="SEU-CLIENT-ID-AQUI"
VITE_MICROSOFT_AUTHORITY="https://login.microsoftonline.com/common"

# Outras variáveis já existentes...
DATABASE_URL=...
```

### 4. Testar a integração

1. **Reinicie o servidor** após configurar as variáveis
2. **Acesse** a página de login 
3. **Clique** no botão "Entrar com Microsoft" (azul)
4. **Complete** o fluxo de autenticação Microsoft
5. **Verifique** se você foi redirecionado para o dashboard

## 🎯 Como funciona

### Fluxo de autenticação:

1. **Usuário clica** "Entrar com Microsoft"
2. **Popup/redirect** para login.microsoftonline.com
3. **Usuário autentica** com credenciais Microsoft
4. **Sistema recebe** dados: ID, email, nome
5. **Backend verifica** se usuário existe
6. **Se não existe**: Cria nova conta automaticamente
7. **Se existe**: Vincula conta Microsoft à existente
8. **Gera JWT token** para sessão
9. **Redireciona** para dashboard

### Dados armazenados:

- `microsoft_id`: ID único da conta Microsoft
- `email`: Email da conta Microsoft
- `name`: Nome da conta Microsoft
- Contas são vinculadas via email comum

## 🔍 Troubleshooting

### Erro "MSAL configuration error"
- ✅ Verifique se `VITE_MICROSOFT_CLIENT_ID` está definido
- ✅ Confirme se o Client ID está correto no Azure

### Erro "Redirect URI mismatch" 
- ✅ Certifique-se que a URL no Azure coincide com a URL do Replit
- ✅ URLs devem incluir protocolo (https://)

### Login não funciona
- ✅ Verifique se as permissões estão configuradas no Azure
- ✅ Confirme se o app está configurado como "Single-page application"

## 📊 Status atual

- ✅ Frontend: Biblioteca MSAL configurada
- ✅ Backend: Endpoint `/api/auth/microsoft` criado
- ✅ Database: Campo `microsoft_id` adicionado na tabela users
- ✅ UI: Botão Microsoft na página de login
- ✅ Linking: Sistema vincula contas automaticamente

⏳ **Pendente**: Configuração das credenciais Azure (Client ID)

## 🚀 Benefícios

- **Segurança**: Autenticação robusta da Microsoft
- **UX**: Login com um clique para usuários Microsoft
- **Compatibilidade**: Funciona com contas pessoais e organizacionais
- **Automático**: Criação e vinculação de contas transparente

Após configurar o Client ID do Azure, o sistema estará 100% funcional!