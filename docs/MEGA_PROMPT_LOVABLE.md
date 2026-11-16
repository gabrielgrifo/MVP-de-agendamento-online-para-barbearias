# Prompt principal — AgendaZap (Lovable)

Este arquivo registra o prompt principal utilizado como base para construir o MVP. O consumo de créditos do Lovable depende do plano e das interações; este documento não garante um limite específico.

## Instrução

Construa o **AgendaZap**, um MVP de agendamento online para uma única barbearia-piloto. Toda a interface deve estar em português do Brasil (`pt-BR`), usar o fuso `America/Sao_Paulo` e valores em reais (R$). Não gere imagens.

### Páginas públicas

- `/`: landing page com cabeçalho (Início, Serviços, Agendar), hero “Seu próximo corte começa com um agendamento simples.”, serviços ativos (nome, descrição, duração e preço), seção “Como funciona” em três passos e rodapé. Endereço e contato de demonstração devem estar marcados como fictícios.
- `/servicos`: lista de serviços ativos.
- `/agendar`: formulário com nome, WhatsApp, serviço ativo, data, horário e observações.

Validar campos obrigatórios, telefone e data não passada em `America/Sao_Paulo`. Implementar estados de carregamento, erro e sucesso. Após salvar, exibir os dados e o aviso: “Seu horário foi solicitado, mas ainda depende da confirmação da barbearia.” Abrir `wa.me` com mensagem pré-preenchida, sem afirmar que a mensagem foi enviada.

### Área administrativa

- `/admin/login`: login por e-mail e senha, sem cadastro público.
- `/admin`: rota protegida com cards (pendentes, confirmados, total), tabela ordenada por data/hora, filtros por status/data, alteração de status, botão WhatsApp do cliente, estado vazio, aviso de confirmação manual, lista de clientes derivada dos pedidos e botão Sair.
- `/admin/servicos`: rota protegida para listar, criar, editar e ativar/desativar serviços. Não permitir excluir serviço associado a pedidos.

### Design

Visual grafite/preto e off-white, verde discreto para ações e detalhe dourado mínimo. Títulos fortes (referências: Archivo Black + Hind), cartões simples, mobile-first e foco visível.

### Backend e segurança

Usar Lovable Cloud para autenticação e banco de dados. Criar tabelas `services`, `appointments` e `user_roles`, com função `has_role` para verificar papel administrativo.

Aplicar RLS:
- Visitantes anônimos podem ler apenas serviços ativos.
- Visitantes anônimos não podem ler nem editar pedidos.
- A criação pública de pedidos deve ocorrer por função de servidor que valide os dados, confirme que o serviço está ativo, copie nome/preço vigentes para snapshots e force status `pending`.
- O visitante nunca escolhe preço ou status.
- Administradores autenticados com papel `admin` podem ler e alterar os dados necessários.
- Não habilitar cadastro público de usuários.

Provisionar o primeiro administrador por procedimento seguro, sem criar uma rota pública de cadastro.

### Dados iniciais

Criar somente estes serviços de demonstração:
- Corte tradicional — 30 min — R$ 35,00
- Barba — 20 min — R$ 25,00
- Corte + barba — 50 min — R$ 55,00

Não criar pedidos falsos.

### WhatsApp

Manter o número da barbearia em um único arquivo de configuração, claramente identificado como valor de demonstração a substituir antes da publicação. Usar link `wa.me` com texto codificado. Não integrar API oficial nem afirmar envio automático.

### Limites importantes

Este MVP atende uma única barbearia. Não implementar pagamentos, chatbot, Google Calendar, notificações automáticas, multiempresa ou bloqueio automático/garantia de disponibilidade de horários. A barbearia confirma manualmente cada solicitação.

### Critérios de conclusão

Testar o fluxo público, validação de data e telefone, criação de pedido como `pending`, snapshots de serviço, login, proteção das rotas, políticas RLS, gerenciamento de serviços e links de WhatsApp. Corrigir erros encontrados sem ampliar o escopo.

Ao final, informar o que foi implementado, quais configurações ainda precisam ser substituídas e quais testes foram executados.
