# 🥤 Sistema Multiagente de Pesquisa de Mercado — Pitanga com Gengibre

Este repositório contém a configuração e a documentação de um sistema baseado em **IA Agêntica de Múltiplos Agentes** desenvolvido no framework **AutoGen Studio**. 

O projeto foi construído como parte de uma **atividade prática da Accenture realizada no dia 15/05/2026**. O objetivo principal é coordenar de forma totalmente autônoma uma pesquisa de aceitação de mercado para um novo produto: um **refrigerante sabor Pitanga com Gengibre**. O sistema utiliza uma estratégia de comunicação linear fixa e roda localmente integrado ao **LM Studio**.

---

## 🛠️ Arquitetura e Engenharia de Prompt dos Agentes

O ecossistema foi estruturado seguindo os padrões de colaboração multiagente apresentados nos exercícios da Accenture. Ele é composto por um coordenador principal e três agentes avaliadores com personas e critérios de análise bem específicos. A comunicação segue o padrão **Round Robin Group Chat** (fila indiana fixa), onde cada integrante realiza sua análise e passa o gancho nominalmente para o próximo da fila.

### 📋 1. Coordenador Principal (`@PesquisaRefrigeranteAI`)
* **Função:** Apresentar o produto aos analistas, mediar o fluxo de turnos sem interferir precocemente e consolidar o feedback coletado em um relatório final de aceitação.
* **Mensagem de Sistema (Prompt):**
  > *"Você é o @PesquisaRefrigeranteAI. Na sua primeira resposta, copie e cole exatamente apenas este texto: 'Olá! Sou o @PesquisaRefrigeranteAI. Estou coordenando a pesquisa do novo refrigerante sabor Pitanga com Gengibre. @EsportistaAI, qual a sua avaliação individual?' ATENÇÃO: Não faça nenhuma conclusão na primeira mensagem. Aguarde a fila rodar inteira. Quando a palavra voltar para você no final (após o @TechLoverAI falar), leia as opiniões anteriores, faça um resumo curto de aceitação e encerre a atividade escrevendo exatamente a palavra de parada: FINISH"*

### 🏋️ 2. Perfil Fitness (`@EsportistaAI`)
* **Função:** Avaliar o produto sob a ótica de saúde, bem-estar, energia e encaixe em rotinas de treino.
* **Mensagem de Sistema (Prompt):**
  > *"Você é o @EsportistaAI. Quando for sua vez, dê uma resposta corta de até 3 linhas. Diga claramente se GOSTOU ou NÃO GOSTOU do refrigerante de Pitanga com Gengibre focado em refrescância e rotina fitness, justificando o motivo. No final da resposta, escreva exatamente: 'Passo a palavra para o @MinimalistaAI.'"*

### 🌿 3. Perfil Natural (`@MinimalistaAI`)
* **Função:** Analisar o produto baseado na simplicidade, pureza da proposta, ausência de excessos artificiais e uso de extratos naturais.
* **Mensagem de Sistema (Prompt):**
  > *"Você é o @MinimalistaAI. Quando for sua vez, dê uma resposta curta de até 3 linhas. Diga claramente se GOSTOU ou NÃO GOSTOU do refrigerante de Pitanga com Gengibre focado em simplicidade e ingredientes naturais, justificando o motivo. No final da resposta, escreva exatamente: 'Passo a palavra para o @TechLoverAI.'"*

### 🚀 4. Perfil Tecnológico/Inovação (`@TechLoverAI`)
* **Função:** Avaliar o potencial de mercado, diferencial competitivo da combinação exótica e as tendências de consumo modernas.
* **Mensagem de Sistema (Prompt):**
  > *"Você é o @TechLoverAI. Quando for sua vez, dê uma resposta curta de até 3 linhas. Diga claramente se GOSTOU ou NÃO GOSTOU do refrigerante de Pitanga com Gengibre focado em inovação e tendência de mercado, justificando o motivo. No final da resposta, escreva exatamente: 'Terminei minha avaliação. @PesquisaRefrigeranteAI, pode fazer a conclusão final.'"*

---

## 💻 Infraestrutura Local e Conectividade

Para garantir a total privacidade e os parâmetros exigidos no desenvolvimento da atividade da Accenture, o projeto foi integrado a um modelo de linguagem de código aberto rodando direto no hardware local:

* **Modelo LLM Utilizado:** `google/gemma-4-e4b`
* **Provedor de Servidor Local:** LM Studio (API compatível com OpenAI)
* **Porta do Endpoint Local:** `http://localhost:1234/v1`
* **Configuração Essencial de Memória:** A janela de contexto inicial foi expandida para **4096 tokens** nas opções de carregamento (*Load Settings*) do LM Studio. Isso impede interrupções por falta de espaço físico e permite suportar o histórico completo de mensagens do grupo de debate sem truncamento de texto.

---

## 🚀 Como Iniciar e Rodar o Projeto

### 1. Inicializar o Servidor da IA (LM Studio)
1. Abra o **LM Studio** e acesse a aba **Developer** (Servidor Local).
2. Carregue o modelo `google/gemma-4-e4b` e certifique-se de que o tamanho de contexto está configurado para `4096`.
3. Clique em **Start Server** e confirme que o status mudou para a cor verde (*Running*).

### 2. Subir o AutoGen Studio pelo Terminal
Abra o seu Prompt de Comando (CMD) ou terminal e execute o comando abaixo para iniciar a interface de gerenciamento conforme o guia do exercício:
```bash
autogenstudio ui --port 8081
