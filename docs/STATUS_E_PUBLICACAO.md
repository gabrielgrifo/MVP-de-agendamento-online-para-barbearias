# Status e publicação — AgendaZap

## Estado no momento da publicação desta documentação

- Nome do projeto: AgendaZap.
- Aplicação de demonstração publicada no Lovable: https://agenda-zap-schedule-spark.lovable.app/
- Repositório GitHub: `MVP-de-agendamento-online-para-barbearias` (conforme captura compartilhada pelo responsável pelo projeto).
- Escopo: MVP para uma barbearia-piloto.
- Documentação inicial preparada para publicação no GitHub.
- Código-fonte da aplicação: ainda não incluído neste pacote de documentação.

## O que esta publicação representa

Esta publicação registra a visão do produto, o escopo funcional, os requisitos, o prompt de construção e o endereço da demonstração pública.

Ela **não** declara que o sistema está pronto para operação comercial, que o backend foi auditado ou que todos os fluxos foram testados. Uma URL pública comprova que existe uma versão acessível, mas não comprova a segurança nem o funcionamento de gravação de dados e autenticação.

## Checklist antes de uso com clientes reais

- [ ] Testar solicitação de agendamento com dados fictícios.
- [ ] Confirmar que o pedido realmente é gravado no banco.
- [ ] Confirmar que todo pedido começa como `pending`.
- [ ] Confirmar que o visitante não consegue consultar pedidos de outras pessoas.
- [ ] Confirmar que preço e status são definidos/validados no servidor.
- [ ] Testar data passada e fuso `America/Sao_Paulo`.
- [ ] Testar link e número de WhatsApp.
- [ ] Criar o primeiro administrador de forma segura.
- [ ] Confirmar que rotas administrativas exigem autenticação e papel `admin`.
- [ ] Revisar as políticas RLS.
- [ ] Substituir telefone, endereço e demais dados fictícios.
- [ ] Testar em dispositivos móveis e desktop.
- [ ] Exportar ou sincronizar o código-fonte do Lovable para o GitHub.

## Como enviar estes arquivos ao GitHub pelo navegador

1. Abra o repositório `MVP-de-agendamento-online-para-barbearias`.
2. Clique em **Add file** e depois em **Upload files**.
3. Extraia o ZIP deste pacote no computador.
4. Arraste `README.md`, `.gitignore` e a pasta `docs` para a área de upload. Se o navegador não preservar as pastas, crie os arquivos dentro de `docs/` usando **Add file → Create new file**.
5. Revise a lista de arquivos.
6. No campo de mensagem do commit, use: `docs: adiciona documentação inicial do AgendaZap`.
7. Clique em **Commit changes**.

## Observação sobre o código-fonte

Não envie somente os arquivos de documentação como se fossem o aplicativo completo. Depois, use a opção de integração/exportação do Lovable para sincronizar o projeto com o repositório. Antes de enviar o código, confira se nenhum arquivo `.env`, chave privada, token ou segredo foi incluído.
