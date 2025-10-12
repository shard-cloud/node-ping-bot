# Instalação

## 🎯 Após Clonar na ShardCloud

Você acabou de clonar este template na plataforma ShardCloud! Agora vamos configurar seu bot Discord.

## 📋 Pré-requisitos

Para usar este template, você precisará:

- ✅ Template já clonado na ShardCloud
- ✅ Conta no [Discord Developer Portal](https://discord.com/developers/applications)
- ✅ Servidor Discord para adicionar o bot

> **Nota:** As dependências do Node.js já estão configuradas no template. A ShardCloud instalará automaticamente ao fazer o deploy.

## 🔧 Dependências Incluídas

O template já vem com:
- `discord.js` (v14.22.1) - Biblioteca principal do Discord
- `dotenv` (v17.2.2) - Gerenciador de variáveis de ambiente

## Passo 1: Criar um Bot no Discord

1. Acesse o [Discord Developer Portal](https://discord.com/developers/applications)
2. Clique em **"New Application"**
3. Dê um nome ao seu bot (ex: "Meu Ping Bot") e clique em **"Create"**
4. Na aba **"Bot"**, clique em **"Add Bot"**
5. Confirme clicando em **"Yes, do it!"**

## Passo 2: Obter o Token do Bot

1. Na página do bot, em **"TOKEN"**, clique em **"Reset Token"** (ou **"Copy"** se já tiver um)
2. **Copie o token** - você precisará dele na ShardCloud
3. ⚠️ **Importante:** Guarde o token com segurança, nunca compartilhe

## Passo 3: Configurar Intents

Na página do bot, role até **"Privileged Gateway Intents"** e ative:

- ✅ **MESSAGE CONTENT INTENT** (obrigatório para ler mensagens)
- ✅ **SERVER MEMBERS INTENT** (opcional)

Clique em **"Save Changes"**.

## Passo 4: Configurar Variáveis de Ambiente na ShardCloud

Na plataforma ShardCloud, configure as variáveis de ambiente do projeto:

1. Acesse as configurações do seu projeto clonado
2. Vá para a seção **"Variáveis de Ambiente"** ou **"Environment Variables"**
3. Adicione as seguintes variáveis:

| Variável | Valor | Obrigatório |
|----------|-------|-------------|
| `TOKEN` | Cole o token copiado do Discord | ✅ Sim |
| `PREFIX` | `!` (ou outro de sua preferência) | ❌ Não (padrão: `!`) |

**Exemplo:**
```
TOKEN=SEU_TOKEN_AQUI
PREFIX=!
```

## Passo 5: Convidar o Bot para seu Servidor

1. No Discord Developer Portal, vá para **"OAuth2"** > **"URL Generator"**
2. Em **"SCOPES"**, selecione:
   - ✅ `bot`
3. Em **"BOT PERMISSIONS"**, selecione:
   - ✅ `Send Messages`
   - ✅ `Read Messages/View Channels`
   - ✅ `Read Message History`
4. Copie a **URL gerada** na parte inferior da página
5. Cole a URL no navegador
6. Selecione o servidor Discord onde deseja adicionar o bot
7. Clique em **"Authorize"** (Autorizar)
8. Complete o captcha (se solicitado)

## Passo 6: Fazer Deploy na ShardCloud

1. Na plataforma ShardCloud, acesse seu projeto
2. Verifique se as variáveis de ambiente estão configuradas
3. Inicie o deploy/execução do bot
4. Aguarde a mensagem de sucesso no console

**Console deve mostrar:**
```
Logged in as SeuBot#1234
```

## ✅ Verificação Final

Para confirmar que tudo está funcionando:

1. Abra o Discord e vá ao servidor onde adicionou o bot
2. Verifique se o bot aparece **online** na lista de membros
3. Em qualquer canal de texto, digite: **`!ping`**
4. O bot deve responder: **`🏓 Pong! WS Ping: XXms`**

## 🎉 Pronto!

Seu bot está funcionando! Agora você pode:

- [Personalizar configurações](config.md) - Alterar prefix, adicionar comandos
- [Resolver problemas](troubleshooting.md) - Se algo não funcionar
- Expandir funcionalidades editando o código no projeto

## 🆘 Problemas na Instalação?

Se encontrou algum problema, consulte o [Guia de Troubleshooting](troubleshooting.md) com soluções detalhadas.

