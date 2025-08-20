# Configuração do Supabase - EPB Sistema

## ✅ O que foi configurado

O sistema EPB foi atualizado para usar Supabase como banco de dados, incluindo:

- **Driver postgres-js**: Conexão otimizada para Supabase
- **Connection pooling**: Configurado com `prepare: false` para Supabase
- **Drizzle ORM**: Mantido para type-safety com Supabase
- **Esquema existente**: Todas as tabelas (users, files, shared_folders) compatíveis
- **Microsoft Auth**: Integração mantida funcionando com Supabase

## 🚀 Como configurar o Supabase

### 1. Criar projeto no Supabase

1. **Acesse**: [https://supabase.com](https://supabase.com)
2. **Clique**: "Start your project"
3. **Crie** uma nova organização (se necessário)
4. **Clique**: "New Project"
5. **Configure**:
   - **Name**: EPB Sistema Arquivos
   - **Database Password**: Escolha uma senha segura (anote!)
   - **Region**: South America (São Paulo) para melhor latência
6. **Aguarde** a criação do projeto (~2 minutos)

### 2. Obter a string de conexão

1. **No dashboard** do seu projeto Supabase
2. **Vá em**: Settings → Database
3. **Encontre**: "Connection string"
4. **Copie** a URL de **"Connection pooling"** (recomendado para produção):

```
postgresql://postgres.PROJECT_REF:PASSWORD@aws-0-sa-east-1.pooler.supabase.com:6543/postgres?sslmode=require
```

5. **Substitua** `PASSWORD` pela senha que você definiu

### 3. Configurar variáveis de ambiente

Crie/edite seu arquivo `.env`:

```env
# Supabase Database
DATABASE_URL="postgresql://postgres.SEU_PROJECT_REF:SUA_SENHA@aws-0-sa-east-1.pooler.supabase.com:6543/postgres?sslmode=require"

# Microsoft Authentication  
VITE_MICROSOFT_CLIENT_ID="seu-microsoft-client-id"
VITE_MICROSOFT_AUTHORITY="https://login.microsoftonline.com/common"
```

### 4. Executar migrações

Com o Supabase configurado, execute:

```bash
# Fazer push do esquema para o Supabase
npm run db:push
```

**Se aparecer erro**: O Supabase pode ter algumas extensões que causam conflito. Você pode:
- Usar `npm run db:push --force` se necessário
- Ou criar as tabelas manualmente via Supabase Dashboard → Database → Tables

### 5. Testar a conexão

1. **Reinicie** o servidor: O workflow será reiniciado automaticamente
2. **Acesse** o sistema
3. **Tente** fazer login ou criar conta
4. **Verifique** se os dados aparecem no Supabase Dashboard → Database → Tables

## 🔧 Vantagens do Supabase

### Performance
- **Connection pooling**: Suporte nativo a milhares de conexões
- **Edge locations**: CDN global para menor latência  
- **Auto-scaling**: Escala automaticamente com demanda

### Facilidade
- **Dashboard visual**: Gerenciar dados pela interface
- **SQL Editor**: Executar consultas direto no dashboard
- **Backups automáticos**: Restauração point-in-time
- **Monitoramento**: Métricas de performance em tempo real

### Recursos extras
- **Auth nativo**: Supabase Auth (se quiser migrar do Microsoft futuramente)
- **Storage**: Para arquivos grandes (imagens, documentos)
- **Edge Functions**: Serverless functions integradas
- **Real-time**: Subscriptions em tempo real

## 🔍 Troubleshooting

### Erro "connection refused"
- ✅ Verifique se a DATABASE_URL está correta
- ✅ Confirme se a senha não tem caracteres especiais sem encoding
- ✅ Teste a conexão no Supabase Dashboard → SQL Editor

### Erro "relation does not exist"
- ✅ Execute `npm run db:push` para criar as tabelas
- ✅ Verifique se as migrações rodaram no Supabase Dashboard

### Tabelas não aparecem no Dashboard
- ✅ Aguarde alguns segundos após `db:push`
- ✅ Refresh a página do dashboard
- ✅ Verifique na aba "Database" → "Tables"

### Performance lenta
- ✅ Use connection pooling URL (porta 6543)
- ✅ Verifique se a região é South America
- ✅ Considere índices nas consultas frequentes

## 📊 Monitoramento

No Supabase Dashboard você pode monitorar:

- **Database Health**: CPU, memória, conexões ativas
- **Query Performance**: Consultas mais lentas
- **Connection Pool**: Uso de conexões
- **Storage**: Tamanho do banco de dados

## 🔒 Segurança

- **SSL obrigatório**: Todas as conexões criptografadas
- **Row Level Security**: Controle granular de acesso
- **Firewall**: Restringir IPs se necessário
- **Backups**: Automáticos e criptografados

## 🎯 Status da migração

- ✅ **Backend**: Configurado para Supabase
- ✅ **Schema**: Compatible com postgres-js
- ✅ **Conexão**: Connection pooling ativado
- ✅ **Autenticação**: Microsoft Auth mantida
- ⏳ **Pendente**: Configuração da DATABASE_URL no .env

Após configurar a DATABASE_URL, o sistema estará 100% funcional com Supabase!