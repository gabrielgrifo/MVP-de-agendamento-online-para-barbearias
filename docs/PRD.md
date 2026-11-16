# PRD — AgendaZap

**Produto:** AgendaZap  
**Versão:** MVP 0.1  
**Estado:** primeira versão publicada para demonstração  
**Idioma:** pt-BR  
**Fuso horário:** `America/Sao_Paulo`  
**Moeda:** BRL (R$)  
**Mercado inicial:** uma barbearia-piloto

## 1. Visão do produto

O AgendaZap é uma aplicação web simples para apresentar os serviços de uma barbearia e receber solicitações de agendamento. A equipe acompanha os pedidos em uma área administrativa e confirma os horários manualmente.

## 2. Problema e hipótese

**Problema a validar:** clientes e barbearias podem perder tempo trocando mensagens para descobrir serviços, preços e horários.

**Hipótese:** uma página com serviços e formulário estruturado reduz o esforço inicial para solicitar um horário, enquanto a confirmação manual mantém a operação simples para o piloto.

A hipótese precisa ser validada com entrevistas e uso real.

## 3. Objetivos do MVP

- Permitir que visitantes consultem os serviços ativos.
- Permitir o envio de uma solicitação de agendamento.
- Informar claramente que a solicitação ainda não é uma reserva confirmada.
- Permitir que um administrador acompanhe pedidos e altere seus status.
- Permitir que o administrador mantenha o catálogo de serviços.

## 4. Fora do escopo

- Multiempresa ou SaaS com múltiplas barbearias.
- Bloqueio automático e garantia de disponibilidade de horários.
- Pagamentos online.
- API oficial do WhatsApp e envio automático de mensagens.
- Sincronização com Google Calendar.
- Chatbot, campanhas e notificações automáticas.
- Cadastro público de administradores.

## 5. Usuários

### Cliente
Pessoa que deseja consultar serviços e solicitar um horário.

### Administrador da barbearia
Pessoa autorizada a consultar pedidos, confirmar ou alterar status e gerenciar serviços.

## 6. Requisitos funcionais

### RF-01 — Página inicial (`/`)
Deve apresentar navegação, chamada principal, serviços ativos, explicação do funcionamento em três passos e rodapé. Endereço e contato de demonstração devem estar identificados como fictícios.

### RF-02 — Serviços (`/servicos`)
Deve listar somente serviços ativos, mostrando nome, descrição, duração e preço.

### RF-03 — Solicitar agendamento (`/agendar`)
Campos:
- Nome
- WhatsApp
- Serviço ativo
- Data
- Horário
- Observações (opcional)

Validações:
- Campos obrigatórios.
- Formato de telefone/WhatsApp válido.
- Data não pode estar no passado considerando `America/Sao_Paulo`.
- Serviço deve estar ativo no momento da criação.

A interface deve apresentar estados de carregamento, erro e sucesso.

Após salvar, mostrar os dados e o aviso: **“Seu horário foi solicitado, mas ainda depende da confirmação da barbearia.”** Pode abrir o WhatsApp com mensagem pré-preenchida. Não deve afirmar que a mensagem foi enviada.

### RF-04 — Login (`/admin/login`)
Autenticação por e-mail e senha. Não deve haver cadastro público.

### RF-05 — Painel (`/admin`)
Rota protegida. Deve apresentar contadores de pedidos pendentes, confirmados e total; tabela ordenada por data/hora; filtros por status e data; alteração de status; atalho de WhatsApp do cliente; estado vazio; aviso de confirmação manual; lista de clientes derivada dos pedidos; botão de sair.

### RF-06 — Serviços administrativos (`/admin/servicos`)
Rota protegida. Deve permitir listar, criar, editar e ativar/desativar serviços. Não deve permitir excluir um serviço associado a pedidos.

## 7. Regras de negócio

- Todo pedido novo começa com status `pending`.
- O visitante não escolhe status nem preço.
- O nome e o preço do serviço devem ser copiados para o pedido no momento da solicitação (snapshot), preservando o histórico.
- A confirmação do pedido é manual.
- O MVP não deve prometer disponibilidade garantida nem bloqueio automático de conflitos.
- Apenas administradores podem consultar e alterar pedidos.

## 8. Dados previstos

### `services`
- `id`
- `name`
- `description`
- `duration_minutes`
- `price`
- `is_active`
- `created_at`
- `updated_at`

### `appointments`
- `id`
- `customer_name`
- `customer_whatsapp`
- `service_id`
- `service_name_snapshot`
- `service_price_snapshot`
- `appointment_date`
- `appointment_time`
- `notes`
- `status` (`pending`, `confirmed`, `cancelled`, conforme implementação)
- `created_at`
- `updated_at`

### `user_roles`
- `id`
- `user_id`
- `role`

O papel administrativo deve ser mantido em tabela separada, com função de verificação `has_role`.

## 9. Segurança e permissões

- RLS habilitada nas tabelas relevantes.
- Anônimo pode ler somente serviços ativos.
- Anônimo não pode ler, listar, atualizar ou excluir agendamentos.
- A criação pública deve passar por função de servidor que valide os campos, confirme que o serviço está ativo, copie nome/preço vigentes e force status `pending`.
- O cliente não pode enviar ou definir papel administrativo.
- Acesso administrativo exige autenticação e verificação de papel `admin`.
- O primeiro administrador deve ser provisionado por procedimento seguro, nunca por cadastro público.

## 10. UX e visual

- Mobile-first e responsivo.
- Paleta grafite/preto e off-white, verde discreto para ações e detalhe dourado mínimo.
- Tipografia de títulos forte (referências: Archivo Black + Hind).
- Cartões simples, foco visível e estados de formulário claros.
- Interface em português do Brasil.

## 11. Critérios de aceite

- Visitante vê somente serviços ativos.
- Formulário impede dados inválidos e datas passadas no fuso de São Paulo.
- Pedido é salvo como `pending`, com snapshot do serviço.
- Mensagem de sucesso deixa claro que aguarda confirmação.
- Link de WhatsApp apenas abre conversa com texto preenchido.
- Usuário anônimo não consegue consultar nem modificar pedidos.
- Usuário sem papel admin não acessa rotas administrativas.
- Admin consegue filtrar pedidos, alterar status e gerenciar serviços.
- Serviço associado a pedidos não pode ser excluído.
- Nenhum pedido fictício é criado no banco.

## 12. Dados iniciais de demonstração

- Corte tradicional — 30 minutos — R$ 35,00
- Barba — 20 minutos — R$ 25,00
- Corte + barba — 50 minutos — R$ 55,00

Não inserir agendamentos fictícios.

## 13. Métricas e validação

Durante o piloto, observar:
- Quantidade de solicitações recebidas.
- Proporção de solicitações que viram agendamentos confirmados.
- Tempo entre solicitação e confirmação.
- Dúvidas ou dificuldades relatadas por clientes e barbearia.

Realizar entrevistas com barbearias antes de assumir que preço, demanda ou conversão estão validados.

## 14. Evolução futura (fora do MVP)

Após validação: prevenção de conflitos de agenda, notificações, integração oficial com WhatsApp, calendário, múltiplas unidades e cobrança recorrente.

## 15. Observação sobre implementação

Este PRD descreve o escopo e os requisitos acordados para o MVP. A existência de uma página pública não comprova, por si só, que autenticação, banco de dados, políticas RLS ou todas as funcionalidades administrativas estejam concluídas e auditadas.
