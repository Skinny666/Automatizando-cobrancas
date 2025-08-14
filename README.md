# Automatizando-cobrancas


# Workflow de Cobrança Preventiva com n8n e WhatsApp

Este repositório contém o template (`.json`) de um workflow de automação construído na plataforma n8n. O objetivo principal deste workflow é automatizar o processo de cobrança de faturas vencidas, enviando lembretes personalizados via WhatsApp para os clientes.

## 📄 Contexto e Problema Resolvido

A cobrança manual de clientes é um processo repetitivo, demorado e suscetível a falhas humanas. Manter a comunicação consistente, principalmente quando a base de clientes cresce, torna-se um grande desafio.

Este workflow foi criado para resolver esse problema, agindo como um agente de cobrança digital que:
1.  Identifica proativamente as faturas que venceram no dia anterior.
2.  Busca informações detalhadas sobre o contrato e o responsável financeiro em um sistema interno.
3.  Envia uma mensagem personalizada com o tom e a informação correta, baseando-se no status atual do contrato do cliente.

## ⚙️ Como Funciona

O fluxo de trabalho é projetado para ser executado periodicamente (ex: diariamente) e segue os seguintes passos:

1.  **Gatilho Agendado:** O workflow é iniciado de forma automática em um horário pré-definido.
2.  **Busca de Faturas Vencidas:** Conecta-se a uma API de um sistema de gestão (ERP/CRM) para obter uma lista de todas as faturas com status "Vencida" cuja data de vencimento foi no dia anterior.
3.  **Enriquecimento de Dados:** Para cada fatura, o workflow busca dados adicionais na API, como:
    * Detalhes do contrato vinculado.
    * O status do contrato (ex: `Ativo`, `Notificado`, `Em cancelamento`).
    * O nome e o telefone do responsável pelo contrato.
4.  **Lógica Condicional Inteligente:** Com todos os dados em mãos, o workflow utiliza uma estrutura de `IF` para decidir qual mensagem enviar:
    * **Se o contrato está "Ativo" ou "Notificado"**: Envia um lembrete amigável, informando sobre o débito e os próximos passos.
    * **Se o contrato já está "Em cancelamento"**: Envia uma mensagem mais direta e urgente, focada na resolução da pendência.
5.  **Envio Personalizado via WhatsApp:** Utilizando uma integração com uma API do WhatsApp (neste exemplo, Waha), o workflow envia a mensagem de texto formatada. Para tornar a interação mais humana, ele simula o status "digitando..." antes do envio.

## 🛠️ Componentes Principais

* **Plataforma de Automação:** [**n8n**](https://n8n.io/)
* **Fonte de Dados:** API REST de um sistema de gestão interno (ERP, CRM, etc.).
* **Canal de Comunicação:** API do WhatsApp (ex: **Waha - WhatsApp HTTP API**).


## ✨ Benefícios

* **Automação Completa:** Elimina 100% do trabalho manual de envio de primeiros lembretes.
* **Redução de Erros:** Garante que nenhum cliente seja esquecido e que a comunicação seja padronizada.
* **Escalabilidade:** O sistema funciona da mesma forma para 10 ou 10.000 clientes, sem custo adicional de mão de obra.
* **Melhora no Fluxo de Caixa:** Acelera o recebimento de pagamentos ao contatar os clientes de forma imediata após o vencimento.
* **Inteligência de Negócio:** Libera a equipe de cobrança para focar em negociações complexas e casos estratégicos, em vez de tarefas operacionais.
