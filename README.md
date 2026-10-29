# 🤖 Chatbot AI Agent com Memória e Google Sheets (n8n)

Este projeto contém um workflow do **n8n** para um Chatbot Inteligente utilizando **LangChain AI Agent**, **Groq LLM**, memória de contexto por sessão, ferramentas externas (Calculadora e Wikipedia) e registro automático de conversas no **Google Sheets**.

## 🚀 Arquitetura do Fluxo

1. **When chat message received (`Chat Trigger`)**: Inicia o fluxo quando o usuário envia uma mensagem no chat público do n8n.
2. **Edit Fields (`Set`)**: Extrai e padroniza os campos `idConversa` (`sessionId`) e `Mensagem` (`chatInput`).
3. **AI Agent (`LangChain Agent`)**:
   - **Modelo de Linguagem (`Groq Chat Model`)**: Utiliza o modelo `openai/gpt-oss-20b` via Groq API para respostas rápidas.
   - **Memória (`Window Buffer Memory`)**: Mantém o histórico da conversa vinculado ao `idConversa`.
   - **Tools (`Calculator` & `Wikipedia`)**: Permite ao agente realizar cálculos matemáticos exatos e consultar informações na Wikipedia quando necessário.
4. **Append row in sheet (`Google Sheets`)**: Salva automaticamente o histórico contendo `idConversa`, `Mensagem` do usuário e `Resposta` da IA em uma planilha do Google Sheets.

## 🛠️ Pré-requisitos

- Uma instância do [n8n](https://n8n.io/) (Self-hosted ou Cloud).
- Chave de API da **Groq** ([GroqCloud](https://console.groq.com/)).
- Conta do **Google Cloud / Google Sheets** conectada via OAuth2 no n8n.

## 📦 Como Importar e Configurar

1. Baixe o arquivo [`chatbot.json`](./chatbot.json) deste repositório.
2. No seu **n8n**, clique em **Create Workflow** -> menu superior direito (**...**) -> **Import from File...** e selecione o arquivo `chatbot.json`.
3. Configure suas credenciais nos nós correspondentes:
   - **Groq Chat Model**: Adicione sua API Key da Groq.
   - **Append row in sheet**: Conecte sua conta Google Sheets e selecione a sua planilha (com as colunas `idConversa`, `Mensagem` e `Resposta`).
4. Ative o workflow na chave **Active** e teste pelo chat integrado!
