# Configuração

## ⚙️ Variáveis de Ambiente

O bot utiliza variáveis de ambiente que devem ser configuradas na plataforma ShardCloud, na seção de configurações do projeto.

### TOKEN (Obrigatório)

O token de autenticação do seu bot do Discord.

```env
TOKEN=seu_token_aqui
```

**Como obter:**
1. Acesse o [Discord Developer Portal](https://discord.com/developers/applications)
2. Selecione sua aplicação
3. Vá para a aba **"Bot"**
4. Em **"TOKEN"**, clique em **"Reset Token"** ou **"Copy"**

⚠️ **ATENÇÃO:** Nunca compartilhe seu token publicamente! Ele concede acesso total ao seu bot.

**Como configurar na ShardCloud:**
1. Acesse as configurações/variáveis de ambiente do projeto
2. Adicione a variável `TOKEN` com o valor copiado do Discord Developer Portal

### PREFIX (Opcional)

O prefixo usado para os comandos do bot. Se não for definido, o padrão é `!`.

**Valor padrão:** `!`

**Exemplos de uso:**

| PREFIX | Comando | Uso |
|--------|---------|-----|
| `!`    | `!ping` | Mais comum |
| `/`    | `/ping` | Estilo slash |
| `bot`  | `botping` | Palavra completa |
| `.`    | `.ping` | Ponto simples |

**Como configurar na ShardCloud:**
1. Acesse as configurações/variáveis de ambiente do projeto
2. Adicione a variável `PREFIX` com o valor desejado (ex: `!`)

## 📝 Exemplo de Configuração na ShardCloud

Configure estas variáveis na plataforma:

| Nome | Valor | Descrição |
|------|-------|-----------|
| `TOKEN` | `SEU_TOKEN_DO_DISCORD_AQUI` | Token do Discord (obrigatório) |
| `PREFIX` | `!` | Prefixo dos comandos (opcional) |

## Intents do Discord

O bot utiliza as seguintes intents configuradas no código:

### GatewayIntentBits.Guilds
Permite que o bot receba eventos relacionados aos servidores (guilds).

### GatewayIntentBits.GuildMessages
Permite que o bot receba eventos de mensagens nos servidores.

### GatewayIntentBits.MessageContent
Permite que o bot leia o conteúdo das mensagens. **Esta intent é privilegiada** e deve ser ativada no Discord Developer Portal.

## Configuração das Intents no Discord Developer Portal

Para que o bot funcione corretamente, você deve ativar as intents privilegiadas:

1. Acesse [Discord Developer Portal](https://discord.com/developers/applications)
2. Selecione sua aplicação
3. Vá para a aba **"Bot"**
4. Role até **"Privileged Gateway Intents"**
5. Ative:
   - ✅ **MESSAGE CONTENT INTENT**
6. Clique em **"Save Changes"**

## Permissões do Bot

O bot precisa das seguintes permissões no servidor:

| Permissão | Descrição | Necessário |
|-----------|-----------|------------|
| View Channels | Ver canais de texto | ✅ Sim |
| Send Messages | Enviar mensagens | ✅ Sim |
| Read Message History | Ler histórico de mensagens | ⚠️ Recomendado |

Estas permissões são configuradas ao gerar o link de convite no OAuth2.

## Personalização

### Alterar a Mensagem de Resposta

Para personalizar a resposta do comando ping, edite o arquivo `index.js`:

```javascript
// Linha 18 - Resposta atual
message.reply(`🏓 Pong! WS Ping: ${client.ws.ping}ms`);

// Exemplo de personalização
message.reply(`🏓 Latência: ${client.ws.ping}ms | Resposta rápida!`);
```

### Adicionar Novos Comandos

Para adicionar um novo comando, adicione uma nova condição no evento `messageCreate`:

```javascript
client.on("messageCreate", async (message) => {
  if (message.author.bot) return;

  if (message.content === `${prefix}ping`) {
    message.reply(`🏓 Pong! WS Ping: ${client.ws.ping}ms`);
  }

  // Novo comando
  if (message.content === `${prefix}hello`) {
    message.reply(`👋 Olá, ${message.author.username}!`);
  }
});
```

## 🔒 Segurança

### Proteção do Token

✅ **Boas práticas:**
1. **Nunca** compartilhe seu token publicamente
2. **Nunca** faça commit do token no código
3. Use sempre variáveis de ambiente (como configurado na ShardCloud)
4. Mantenha o token apenas nas configurações da plataforma

### Regenerar Token Comprometido

Se seu token foi exposto acidentalmente:

1. Acesse o [Discord Developer Portal](https://discord.com/developers/applications)
2. Selecione sua aplicação
3. Vá para a aba **"Bot"**
4. Clique em **"Reset Token"**
5. **Atualize a variável `TOKEN` na ShardCloud** com o novo token
6. Faça um novo deploy do bot

## Próximos Passos

- [Troubleshooting](troubleshooting.md) - Resolva problemas comuns
- [Visão Geral](README.md) - Voltar para a página inicial

