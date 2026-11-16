# AgendaZap — Agendamento online para barbearias

[![Aplicação publicada](https://img.shields.io/badge/aplica%C3%A7%C3%A3o-online-brightgreen)](https://agenda-zap-schedule-spark.lovable.app/)

O **AgendaZap** é um MVP de agendamento online desenvolvido para uma barbearia-piloto. A proposta é permitir que clientes consultem serviços e solicitem um horário pela internet, enquanto a barbearia acompanha e confirma os pedidos manualmente.

**Aplicação publicada:** https://agenda-zap-schedule-spark.lovable.app/

> **Estado do projeto:** primeira versão publicada no Lovable. Este repositório documenta o escopo, os requisitos e o prompt de construção. O código-fonte da aplicação ainda não foi incluído neste pacote. As funcionalidades de backend, autenticação, gravação dos pedidos e regras de segurança precisam ser testadas antes de considerar o sistema pronto para operação real.

## Objetivo

Simplificar o primeiro contato entre clientes e barbearias, organizando a solicitação de agendamentos em um formulário simples e deixando a confirmação final sob responsabilidade da barbearia.

## Funcionalidades planejadas para o MVP

### Área pública
- Página inicial com apresentação da barbearia.
- Listagem de serviços ativos, com descrição, duração e preço.
- Formulário para solicitar agendamento.
- Mensagem de confirmação deixando claro que o pedido ainda depende da aprovação da barbearia.
- Atalho para WhatsApp com mensagem pré-preenchida.

### Área administrativa
- Login por e-mail e senha, sem cadastro público.
- Painel com resumo dos pedidos.
- Listagem e filtros de agendamentos.
- Alteração manual do status dos pedidos.
- Atalho para WhatsApp do cliente.
- Cadastro, edição e ativação/desativação de serviços.

## Serviços de demonstração

| Serviço | Duração | Preço |
|---|---:|---:|
| Corte tradicional | 30 min | R$ 35,00 |
| Barba | 20 min | R$ 25,00 |
| Corte + barba | 50 min | R$ 55,00 |

Os valores são demonstrativos e devem ser confirmados pela barbearia antes do uso comercial.

## Fluxo esperado

1. Cliente acessa a aplicação e consulta os serviços.
2. Cliente preenche o formulário e solicita um horário.
3. O pedido é registrado como pendente (`pending`).
4. A barbearia analisa a solicitação e confirma ou altera o status manualmente.
5. O cliente pode ser contatado pelo WhatsApp.

**Importante:** solicitar um horário não significa que ele está confirmado. O MVP não promete bloqueio automático nem garantia de disponibilidade do horário. O link de WhatsApp abre uma conversa com texto pré-preenchido; não significa que a mensagem foi enviada.

## Escopo e limites

- Projeto-piloto para uma única barbearia.
- Interface em português do Brasil (`pt-BR`).
- Fuso horário: `America/Sao_Paulo`.
- Moeda: real brasileiro (R$).
- Sem imagens geradas.
- Sem pagamentos online.
- Sem API oficial do WhatsApp ou envio automático de mensagens.
- Sem integração com Google Calendar.
- Sem chatbot ou notificações automáticas.
- Sem operação multiempresa.
- Sem bloqueio automático ou garantia de disponibilidade de horários.

## Tecnologia e segurança previstas

A implementação foi planejada com Lovable Cloud, autenticação e banco de dados com políticas de segurança por linha (RLS).

Tabelas previstas:
- `services`
- `appointments`
- `user_roles`

Regras de segurança previstas:
- Visitantes anônimos consultam somente serviços ativos.
- Visitantes anônimos não consultam nem alteram pedidos existentes.
- A criação pública de pedidos valida os dados no servidor, verifica se o serviço está ativo, copia o nome e preço vigentes e força o status inicial `pending`.
- O visitante não escolhe preço nem status.
- A área administrativa exige autenticação e papel `admin`.
- Não há cadastro público de administradores.

Essas regras são requisitos do projeto e **não uma certificação de que a configuração publicada já foi auditada**. Devem ser verificadas no ambiente Lovable Cloud antes de receber dados reais.

## Estrutura deste repositório

```text
.
├── README.md
├── .gitignore
└── docs/
    ├── PRD.md
    ├── MEGA_PROMPT_LOVABLE.md
    └── STATUS_E_PUBLICACAO.md
```

## Documentação

- [PRD — Documento de requisitos](docs/PRD.md)
- [Prompt principal usado no Lovable](docs/MEGA_PROMPT_LOVABLE.md)
- [Status e checklist de publicação](docs/STATUS_E_PUBLICACAO.md)

## Como testar a demonstração

1. Abra https://agenda-zap-schedule-spark.lovable.app/.
2. Navegue pela página inicial e pela lista de serviços.
3. Abra o formulário de agendamento.
4. Antes de usar dados reais, confirme com a equipe do projeto se o backend, o armazenamento e as políticas de acesso foram testados.
5. Não utilize dados pessoais reais enquanto a segurança e o fluxo administrativo não tiverem sido validados.

## Próximos passos

- [ ] Validar envio e gravação de solicitações.
- [ ] Validar datas, horários e telefone.
- [ ] Validar link de WhatsApp.
- [ ] Configurar e testar o primeiro administrador por procedimento seguro.
- [ ] Testar proteção das rotas administrativas.
- [ ] Revisar as políticas RLS.
- [ ] Testar gerenciamento de serviços.
- [ ] Testar em celular e computador.
- [ ] Exportar/sincronizar o código-fonte do Lovable para este repositório.
- [ ] Atualizar esta documentação após os testes.

## Contexto de negócio

O produto começa como um piloto para validar se uma barbearia e seus clientes percebem valor em solicitar horários por uma página simples, com confirmação humana. Preço, demanda e conversão são hipóteses a validar com entrevistas e uso real; não são resultados comprovados.

## Licença

Nenhuma licença de código aberto foi definida neste momento. Todos os direitos sobre os materiais permanecem com seus respectivos titulares. Se o projeto for disponibilizado para reutilização por terceiros, escolha e adicione uma licença apropriada.
