# 📨 JCorreioResgate - Sistema de Correio e Gerenciamento de Itens(givar)
---

## 📋 Descrição

O **JCorreioResgate** é um mod para Minecraft Forge 1.16.5 que implementa um sistema de correio completo e um gerenciador de itens customizados para o servidor. Este sistema permite que administradores criem itens personalizados, configuráveis via arquivos YAML, que podem ser entregues diretamente ou enviados para a caixa de correio dos jogadores.

## 🌟 Funcionalidades Principais

### 📬 Sistema de Correio
- **Envio de itens**: Itens customizados podem ser enviados para o correio dos jogadores
- **Interface gráfica com categorias**: Organização por categorias para melhor visualização
- **Sistema de expiração**: Itens podem ser configurados para expirar após um período
- **Histórico de ações**: Registro completo de todas as ações (adições, resgates, expirações)
- **Comandos automáticos**: Executa comandos customizados quando um item é resgatado

### 🎁 Sistema de Itens Customizados
- **Configuração via YAML**: Itens definidos em arquivos de configuração simples
- **Preview gráfica**: Interface gráfica para visualizar e gerenciar itens
- **Metadados customizados**: Nome, lore, CustomModelData e outros atributos
- **Comandos vinculados**: Executar comandos ao resgatar ou receber um item
- **VIP Integration**: Verificação de permissões para itens VIP

### 📊 Sistema de Logs
- **Logs detalhados**: Registros de todas as ações em arquivos separados
- **Correio e Givar**: Logs separados para cada sistema
- **Formato detalhado**: Data, hora, jogador e detalhes da ação

## 🔧 Comandos Disponíveis

### Para Jogadores
| Comando | Descrição |
|---------|-----------|
| `/correio` | Abre a interface do correio com categorias |

### Para Administradores
| Comando | Descrição |
|---------|-----------|
| `/admincorreio <jogador> <item_id> [quantidade]` | Envia um item para o correio do jogador |
| `/givar <jogador> <item_id> [quantidade]` | Dá um item diretamente ao jogador |
| `/givargui <jogador>` | Abre a interface admin para dar itens ao jogador |
| `/admincorreiover <jogador> [página]` | Visualiza o histórico de correio do jogador |
| `/jcorreio reload` | Recarrega todas as configurações do mod |

## 📝 Configuração

### Exemplo de Configuração de Item
```yaml
items:
  kit_vip:
    material: CHEST
    display_name: "&6&lKit VIP"
    lore:
      - "&7Um conjunto de itens especiais"
      - "&7para jogadores VIP"
    custom_model_data: 1004
    commands:
      - "givar %player% espada_diamante"
      - "givar %player% capacete_ouro"
      - "give %player% minecraft:diamond 10"
    expiry_hours: 120
```

### Configuração do Correio
```yaml
correio:
  menu:
    title: "&6&lCorreio do Servidor"
    rows: 6
  messages:
    item_received: "&aVocê recebeu um item no correio!"
    item_claimed: "&aItem resgatado com sucesso!"
```

## 🛠️ Recursos Técnicos

- **Banco de dados SQLite**: Armazenamento persistente de dados
- **GUI avançada**: Interface baseada em GooeyLibs2
- **Sistema de categorias dinâmico**: Categorização automática de itens
- **Compatibilidade com LuckPerms**: Integração com sistemas de permissão
- **Tab Completion**: Preenchimento automático para facilitar uso dos comandos

## 💎 Características Especiais

### Sistema VIP
O mod verifica automaticamente se o jogador já possui um VIP antes de entregar um novo, evitando duplicação. Para usar esta função, basta nomear o item como `vip_<nome>` e o sistema verificará a permissão `group.<nome>` no LuckPerms.

### Itens com Comandos
Os itens podem executar comandos customizados quando resgatados do correio. Ideal para criar kits complexos ou funcionalidades especiais.

### Logs Detalhados
Todos os eventos são registrados em arquivos de log no formato:
```
[dd/MM/yyyy - HH:mm:ss] RECEBEU: Jogador NerdYuri recebeu o item kit_vip (x1) no seu correio de Segara
[dd/MM/yyyy - HH:mm:ss] RESGATADO: Jogador Zaniraw resgatou o item Kit VIP (ID: 123, x1) do correio
```

### Interface Categorizada
A interface do correio organiza automaticamente os itens em categorias, facilitando a visualização quando há muitos itens.

---

## 🔄 Instalação e Requisitos

### Requisitos
- Minecraft Forge 1.16.5 / Archlight 1.16.5
- GooeyLibs (incluído como dependência)
- LuckPerms

### Instalação
1. Coloque o arquivo JAR na pasta `mods/`
2. Inicie o servidor para gerar as configurações padrão
3. Personalize os arquivos de configuração conforme necessário
4. Use `/jcorreio reload` para aplicar as alterações

---

## 📋 Permissões

| Permissão | Descrição |
|-----------|-----------|
| `jcorreioresgate.user.correio` | `minecraft.command.correio` | Permite usar o comando /correio |
| `jcorreioresgate.user.givargui` | `minecraft.command.givargui` | Permite usar o comando /givargui |
| `jcorreioresgate.admin.correio` | `minecraft.command.admincorreio` | Permite enviar itens para o correio |
| `jcorreioresgate.admin.givar` | `minecraft.command.givar` | Permite dar itens diretamente |
| `jcorreioresgate.admin.correio.ver` | `minecraft.command.admincorreiover` | Permite ver histórico de correio |
| `jcorreioresgate.admin.givargui` | `minecraft.command.givargui` | Permite usar a GUI admin |
| `jcorreioresgate.admin.reload` | `minecraft.command.reload` | Permite recarregar configurações |

---

## ⚙️ Tutorial de Uso

### Para Administradores

1. **Criando um novo item**
   - Edite um dos arquivos YAML em `config/jcorreioresgate/givarmenus/`
   - Adicione uma nova entrada no formato mostrado acima
   - Use `/jcorreio reload` para carregar a configuração

2. **Enviando um item para o correio de um jogador**
   - Use `/admincorreio <jogador> <item_id> [quantidade]`
   - Ou abra a GUI com `/givargui <jogador>` e use shift+click

3. **Dando um item diretamente**
   - Use `/givar <jogador> <item_id> [quantidade]`
   - Ou abra a GUI com `/givargui <jogador>` e clique no item

4. **Verificando o histórico de correio**
   - Use `/admincorreiover <jogador>` para abrir a interface de histórico

### Para Jogadores

1. **Verificando o correio**
   - Use `/correio` para abrir a interface do correio

2. **Visualizando itens disponíveis**
   - Use `/givargui` para ver os itens disponíveis
   - Clique para obter um item 

---

## 🚀 Dicas e Boas Práticas

1. **Organização de Itens**
   - Crie arquivos YAML separados por categorias (vips, kits, cosméticos)
   - Use prefixos consistentes nos IDs (vip_, kit_, cosm_)

2. **Balanceamento**
   - Configure tempos de expiração adequados para cada tipo de item ou use 0 para nunca expirar
   - Use o recurso de comandos para verificar ingame os arquivos

3. **Backup**
   - Faça backup regular do arquivo `correio.db` para preservar os dados (extremamente importante esse arquivo nunca falhar)
   - Se necessário recriar o banco de dados, os dados da db atual serão perdidos (nunca deletar obrigado)

4. **Monitoramento**
   - Verifique regularmente os arquivos de log para detectar problemas
   - Use `/admincorreiover` para verificar o histórico de jogadores específicos

---

## 🛑 Solução de Problemas

| Problema | Solução |
|----------|---------|
| **Item não aparece no correio** | Verifique a configuração do item e se o arquivo foi carregado corretamente |
| **Comandos não executam** | Verifique a sintaxe dos comandos e se a variável %player% está presente |
| **Erro no banco de dados** | Verifique permissões da pasta e se o SQLite está funcionando corretamente |
| **Interface não abre** | Verifique se o GooeyLibs está instalado corretamente |

---

## 📊 Performance

O JCorreioResgate foi projetado para ser eficiente e consumir poucos recursos. Algumas dicas para manter a performance:

1. Não crie itens com lores extremamente longos (somente se precisar pessoal)
2. Evite comandos que façam operações pesadas durante resgates em massa
3. Para servidores grandes, considere configurar expirações mais curtas (servidor com 2000 jogadores semanais não façam muitos itens que duram mais de 30dias)
4. O mod realiza limpeza automática de itens expirados

---

## 📜 Changelog

### v1.0.0
- Lançamento inicial com sistema de correio básico
- Comandos /givar e /admincorreio
- Interface de gerenciamento para admins

### v1.1.0
- Adicionado sistema de categorias
- Logs detalhados
- Integração com LuckPerms
- Comandos ao resgatar itens
- Interface renovada

### v1.2.0
- Correção de bugs
- Performance aprimorada
- Comandos Tab Completion
- Novas opções de configuração
- GUI para visualização de itens (/givargui)

---

## 📰 Todo

- Sistema de remover itens do correio de outros jogadores
- Remover o baú que vem quando resgata ou é givado um item
- Tela maior do givargui
- Sistema de quantidade de slots necessários


## 📩 Contato e Suporte

Para sugestões, dúvidas ou relato de bugs, contate-nos através de:

- **GitHub**: [[jose2D](https://github.com/jose2d)] | [[gobb1](https://github.com/Gobb1)]

---

*Este mod foi desenvolvido com ❤️ pela equipe de desenvolvimento do BrunoeJoséCorp para melhorar a experiência do servidor.*