# Troubleshooting

## Problemas Comuns e Soluções

### 1. Bot Não Inicia

#### Erro: "TOKEN não definido" ou "Improper token"

**Sintomas:**
```
Error: TOKEN is invalid
Error: An invalid token was provided
```

**Causas:**
- Token não configurado nas variáveis de ambiente da ShardCloud
- Token incorreto ou mal formatado
- Token expirado ou regenerado

**Soluções:**
1. **Verifique as variáveis de ambiente na ShardCloud:**
   - Acesse as configurações do projeto
   - Confirme que a variável `TOKEN` está configurada
   - Certifique-se de que não há espaços extras no valor

2. **Verifique o token no Discord:**
   - Acesse o [Discord Developer Portal](https://discord.com/developers/applications)
   - Vá até sua aplicação > aba "Bot"
   - Se necessário, clique em "Reset Token" e copie o novo

3. **Atualize na ShardCloud:**
   - Cole o token correto na variável `TOKEN`
   - Salve as configurações
   - Faça um novo deploy do bot

---

#### Erro: "Cannot find module"

**Sintomas:**
```
Error: Cannot find module 'discord.js'
```

**Causa:**
- Dependências não foram instaladas corretamente

**Solução na ShardCloud:**
1. Verifique se o arquivo `package.json` está presente no projeto
2. A ShardCloud deve instalar as dependências automaticamente
3. Se o erro persistir, verifique os logs de deploy
4. Tente fazer um novo deploy do projeto

---

### 2. Bot Não Responde a Comandos

#### Bot está online mas não responde ao !ping

**Causas Possíveis:**

**1. MESSAGE CONTENT INTENT desativada**

**Solução:**
1. Acesse [Discord Developer Portal](https://discord.com/developers/applications)
2. Selecione sua aplicação → aba **"Bot"**
3. Em **"Privileged Gateway Intents"**, ative:
   - ✅ **MESSAGE CONTENT INTENT**
4. Clique em **"Save Changes"**
5. Reinicie o bot

**2. Prefix incorreto**

Verifique o prefix configurado no `.env`:
```env
PREFIX=!
```

Se você definiu um prefix diferente (ex: `/`), use `/ping` ao invés de `!ping`.

**3. Bot sem permissões**

Verifique se o bot tem as seguintes permissões no servidor:
- ✅ View Channels
- ✅ Send Messages
- ✅ Read Message History

**Solução:**
1. Configurações do servidor → Funções
2. Encontre a função do bot
3. Ative as permissões necessárias

---

### 3. Erros de Versão do Node.js

#### Erro: SyntaxError em import statements

**Sintomas:**
```
SyntaxError: Cannot use import statement outside a module
```

**Causa:**
- Node.js muito antigo
- Falta da configuração `"type": "module"` no package.json

**Soluções:**
1. Atualize o Node.js para versão 16.9.0 ou superior:
   ```bash
   node --version
   ```
2. Verifique se `package.json` contém:
   ```json
   {
     "type": "module"
   }
   ```

---

### 4. Problemas de Conexão

#### Bot desconecta frequentemente

**Sintomas:**
- Bot aparece offline constantemente
- Mensagens de reconexão no console

**Causas:**
- Problemas de rede/internet
- Token inválido ou expirado
- API do Discord instável

**Soluções:**
1. Verifique sua conexão com a internet
2. Regenere o token do bot
3. Verifique o status da API do Discord: https://discordstatus.com
4. Adicione tratamento de erros no código:
   ```javascript
   client.on("error", (error) => {
     console.error("Erro no cliente:", error);
   });
   ```

---

### 5. Bot Não Aparece Online

#### Bot autentica mas não aparece nos membros

**Causa:**
- Intent `GatewayIntentBits.Guilds` não configurada

**Solução:**
O código já inclui esta intent. Se o problema persistir:
1. Verifique se o bot foi convidado corretamente
2. Remova o bot do servidor
3. Gere um novo link de convite no OAuth2:
   - Scopes: `bot`
   - Permissions: `Send Messages`, `Read Messages/View Channels`
4. Convide novamente

---

### 6. Erros de Sintaxe

#### Erro após editar o código

**Sintomas:**
```
SyntaxError: Unexpected token
```

**Soluções:**
1. Verifique parênteses, chaves e colchetes
2. Certifique-se de que strings estão entre aspas
3. Use um editor com syntax highlighting
4. Compare com o código original

---

### 7. Problemas com Variáveis de Ambiente

#### Variáveis não são lidas

**Sintomas:**
- `process.env.TOKEN` retorna `undefined`
- Bot não inicia ou dá erro de autenticação

**Soluções na ShardCloud:**
1. Verifique se as variáveis estão configuradas corretamente:
   - Acesse as configurações do projeto na ShardCloud
   - Confirme que `TOKEN` está definido
   - Verifique se não há espaços em branco no início ou fim

2. Certifique-se de que salvou as configurações após adicionar as variáveis

3. Faça um novo deploy após alterar variáveis de ambiente

4. Verifique os logs do console para mensagens de erro específicas

---

## Logs e Depuração

### Ativar Logs Detalhados

Adicione logs para depuração:

```javascript
client.on("messageCreate", async (message) => {
  console.log(`Mensagem recebida: ${message.content}`);
  console.log(`Autor: ${message.author.tag}`);
  console.log(`É bot: ${message.author.bot}`);
  
  // resto do código...
});
```

### Verificar Status do Bot

Adicione um log de status completo:

```javascript
client.on("ready", () => {
  console.log(`Logged in as ${client.user.tag}`);
  console.log(`Prefix: ${prefix}`);
  console.log(`Servidores: ${client.guilds.cache.size}`);
  console.log(`Usuários: ${client.users.cache.size}`);
});
```

---

## Comandos Úteis para Depuração

### Verificar instalação do Node.js
```bash
node --version
```

### Verificar instalação do npm
```bash
npm --version
```

### Verificar variáveis de ambiente na ShardCloud
1. Acesse as configurações do projeto
2. Vá para a seção "Variáveis de Ambiente" ou "Environment"
3. Confirme que `TOKEN` está definido e não está vazio

---

## Ainda com Problemas?

Se nenhuma das soluções acima resolveu seu problema:

1. **Verifique os logs de erro completos** - Leia toda a mensagem de erro, não apenas a primeira linha
2. **Teste com o código original** - Confirme que o código base funciona
3. **Verifique a documentação do discord.js** - [discord.js Guide](https://discordjs.guide/)
4. **Verifique versões das dependências** - Execute `npm list` para ver versões instaladas

### Informações Úteis para Suporte

Ao buscar ajuda, forneça:
- Versão do Node.js (`node --version`)
- Versão do discord.js (veja no `package.json`)
- Sistema operacional
- Mensagem de erro completa
- Código que está causando o problema

---

## Recursos Adicionais

- [Documentação do discord.js](https://discord.js.org/)
- [Discord.js Guide](https://discordjs.guide/)
- [Discord Developer Portal](https://discord.com/developers/applications)
- [Status da API do Discord](https://discordstatus.com/)

---

[Voltar para Visão Geral](README.md)

