# Bate Papo Simples - Servidor e Cliente em VB6

## 📋 Descrição do Projeto

Este é um sistema de chat simples desenvolvido em Visual Basic 6.0 que implementa uma arquitetura cliente-servidor. O projeto permite a comunicação em tempo real entre múltiplos clientes através de um servidor centralizado.

## 🚀 Funcionalidades

### Servidor
- ✅ Aceita múltiplas conexões simultâneas
- ✅ Gerencia lista de usuários conectados
- ✅ Retransmite mensagens para todos os clientes
- ✅ Notifica entrada/saída de usuários
- ✅ Interface com chat e lista de usuários
- ✅ Buffer de dados para lidar com pacotes TCP fragmentados

### Cliente
- ✅ Conecta-se ao servidor via IP e porta
- ✅ Envia e recebe mensagens em tempo real
- ✅ Visualiza lista de usuários online
- ✅ Reconexão automática (tecla ESC)
- ✅ Interface amigável com chat

## 📁 Estrutura do Projeto

```
SimpleChat/
├── frmChat.frm          # Interface principal (Servidor/Cliente)
├── frmChat.frx          # Recursos do formulário
├── frmStart.frm         # Tela de início do servidor
├── frmConnect.frm       # Tela de conexão do cliente
├── ModChat.bas          # Módulo do servidor
├── ModClient.bas        # Módulo do cliente
├── ModGeneral.bas       # Funções gerais
├── ModProtocol.bas      # Protocolo de comunicação
└── ModServer.bas        # Configurações do servidor
```

## 🔧 Tecnologias Utilizadas

- **Visual Basic 6.0**
- **Winsock Control** - Comunicação TCP/IP
- **RichTextBox Control** - Exibição de mensagens formatadas

## 📦 Componentes Obrigatórios

Para executar o projeto, os seguintes controles OCX são necessários:

- **MSWINSCK.OCX** - Winsock Control
- **RICHTX32.OCX** - RichTextBox Control

## 🔌 Protocolo de Comunicação

O protocolo utiliza delimitadores para estruturar os pacotes:

- **Chr$(2)** - Separador de campos
- **Chr$(4)** - Delimitador de pacote

### Tipos de Pacotes

| Código | Descrição | Estrutura |
|--------|-----------|-----------|
| `CON` | Conexão | `CON + Chr$(2) + Nickname + Chr$(4)` |
| `MSG` | Mensagem | `MSG + Chr$(2) + Nickname + Chr$(2) + Mensagem + Chr$(4)` |
| `ENT` | Entrada | `ENT + Chr$(2) + Nickname + Chr$(4)` |
| `LEA` | Saída | `LEA + Chr$(2) + Nickname + Chr$(4)` |
| `LST` | Lista de usuários | `LST + Chr$(2) + User1 + vbCrLf + User2 + vbCrLf + UserN + Chr$(4)` |

## 🎯 Como Executar

### Servidor
1. Abra o projeto no Visual Basic 6.0
2. Execute `frmStart.frm`
3. Defina um nickname para o servidor
4. Escolha uma porta (padrão: 1234)
5. Clique em "Start »"

### Cliente
1. Execute o mesmo projeto (ou compile separadamente)
2. A tela de conexão aparecerá automaticamente
3. Preencha:
   - **Server:** IP do servidor (ex: 127.0.0.1 para local)
   - **Porta:** Mesma porta configurada no servidor
   - **Nickname:** Seu nome no chat
4. Clique em "Connect »"

### Comandos do Cliente
- **ENTER** - Envia a mensagem
- **ESC** - Reconecta ao servidor (caso a conexão seja perdida)

## ⚠️ Observações Importantes

### Tratamento de Pacotes TCP
O sistema implementa um buffer inteligente para lidar com a fragmentação de pacotes TCP, garantindo que mensagens longas ou múltiplas mensagens sejam processadas corretamente.

### Limitações
- Máximo de conexões: 32.767 (limitado pelo Integer)
- Tamanho máximo da mensagem: 1024 caracteres
- Desenvolvido para ambientes Windows com VB6 Runtime

## 🛠️ Personalização

Para adicionar novas funcionalidades:

1. **Novos tipos de pacote:** Adicione no `Select Case` em `sckServer_DataArrival` (servidor) e `sckClient_DataArrival` (cliente)

2. **Novos campos no usuário:** Modifique a estrutura `CHAT_USER` em `ModChat.bas`

3. **Interface:** Os formulários estão configurados com redimensionamento automático via `GetClientRect`

## 📝 Notas de Desenvolvimento

- O projeto utiliza `KeyPreview = True` para capturar teclas em todo o formulário
- O redimensionamento é feito pixel-perfect usando API do Windows
- O sistema de buffer garante integridade dos dados mesmo com pacotes fragmentados

## 📄 Licença

Projeto de código aberto para fins educacionais. Sinta-se à vontade para modificar e distribuir.

---

**Desenvolvido em Visual Basic 6.0**
