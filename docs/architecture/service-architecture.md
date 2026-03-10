# Service Architecture

## Objetivo

Este documento define a arquitetura de serviços do backend do Água Nativa.

Ele existe para deixar claro:

- como o backend será dividido em módulos
- qual a responsabilidade de cada módulo
- o que cada módulo pode ou não pode fazer
- como os módulos se comunicam
- qual será a base estrutural para o backend em NestJS

Este documento complementa os materiais já existentes de arquitetura geral, estratégia multi-tenant e modelagem de dados.

## Direção arquitetural

O Água Nativa deve começar como um **monólito modular**.

Isso significa:

- um backend único no início
- módulos internos bem separados
- responsabilidades claras
- baixo acoplamento entre partes
- base preparada para crescer sem bagunça

Essa decisão foi tomada porque ela entrega o melhor equilíbrio entre:

- simplicidade operacional
- organização técnica
- velocidade com controle
- escalabilidade futura sem overengineering

## Regra estrutural principal

Mesmo sendo um backend único no início, ele **não será um sistema solto ou misturado**.

Ele será dividido em módulos de negócio com limites claros.

Cada módulo deve ter:

- responsabilidade própria
- regras próprias
- contratos claros de entrada e saída
- separação entre regra de negócio e infraestrutura

## Princípios obrigatórios

A arquitetura de serviços deve seguir estes princípios:

1. todo processamento relevante deve respeitar o tenant
2. nenhum módulo pode acessar dados de outro tenant indevidamente
3. regras de negócio não devem ficar espalhadas
4. controllers não devem carregar lógica de negócio
5. infraestrutura não pode mandar na regra de negócio
6. módulos devem se comunicar com clareza
7. ações importantes devem ser auditáveis
8. segurança deve existir desde o início

## Contexto multi-tenant

O sistema é multi-tenant desde o primeiro dia.

Por isso, todo módulo backend deve operar com estas regras:

- identificar o tenant da requisição
- validar se o usuário pertence ao tenant
- limitar leitura e escrita ao tenant correto
- registrar eventos importantes com contexto de tenant
- impedir vazamento de dados entre associações

O tenant não é detalhe técnico.
O tenant é parte estrutural da arquitetura.

## Grandes blocos do backend

O backend será organizado em áreas principais:

- autenticação e acesso
- tenants
- associações
- usuários
- clientes
- unidades consumidoras
- hidrômetros
- leituras
- tarifas
- cobranças extras
- faturas
- pagamentos
- notificações
- relatórios
- auditoria
- armazenamento de arquivos
- administração da plataforma

Essas áreas representam os limites principais de serviço dentro do backend.

## Módulo de autenticação e acesso

Responsabilidade:

- login
- identidade do usuário
- contexto autenticado
- permissões
- vínculo com tenant
- controle de acesso

Esse módulo cuida de quem é o usuário, a que tenant ele pertence e o que ele pode fazer.

Esse módulo não deve cuidar de:

- faturamento
- leituras
- pagamentos
- relatórios de negócio

## Módulo de tenants

Responsabilidade:

- cadastro do tenant
- status do tenant
- metadados do tenant
- configurações gerais de isolamento
- base de segregação da operação

Esse módulo existe para sustentar a arquitetura SaaS multi-tenant.

## Módulo de associações

Responsabilidade:

- dados da associação
- configurações operacionais da associação
- identidade institucional da operação local
- parâmetros próprios daquela associação

Ele representa a operação da associação dentro do tenant.

## Módulo de usuários

Responsabilidade:

- cadastro de usuários internos
- perfis operacionais
- vínculo com associação
- ativação e desativação
- papéis como administrador, operador e leiturista

## Módulo de clientes

Responsabilidade:

- cadastro dos consumidores
- situação do consumidor
- dados de contato
- vínculo com unidade consumidora
- histórico cadastral relevante

## Módulo de unidades

Responsabilidade:

- unidades consumidoras
- localização
- vínculo com cliente
- situação da unidade
- organização operacional das ligações

## Módulo de hidrômetros

Responsabilidade:

- cadastro do hidrômetro
- instalação
- troca
- status
- histórico técnico
- vínculo com unidade

## Módulo de leituras

Responsabilidade:

- registro das leituras
- validação de leitura
- anomalias
- histórico de consumo
- suporte ao fluxo operacional do leiturista

Esse módulo é crítico porque ele alimenta o faturamento.

## Módulo de tarifas

Responsabilidade:

- tabelas tarifárias
- faixas de cobrança
- vigência
- regras de cálculo base
- configuração por associação quando aplicável

## Módulo de cobranças extras

Responsabilidade:

- cobranças não recorrentes
- taxas operacionais adicionais
- lançamentos manuais
- cobranças futuras vinculadas à próxima fatura
- justificativa e rastreabilidade

Esse módulo é importante porque já foi definido como requisito do negócio.

## Módulo de faturas

Responsabilidade:

- geração das faturas
- composição dos itens cobrados
- totalização
- vencimento
- status da fatura
- histórico de faturamento

Esse é um dos módulos mais críticos do sistema.

Ele deve consumir dados de:

- leituras
- tarifas
- cobranças extras
- clientes
- unidades
- hidrômetros

## Módulo de pagamentos

Responsabilidade:

- registro de pagamentos
- vínculo entre pagamento e fatura
- status do pagamento
- conciliação
- histórico financeiro

No futuro, este módulo poderá integrar com:

- Pix
- boleto
- outros meios definidos pelo negócio

## Módulo de notificações

Responsabilidade:

- geração de notificações
- organização por canal
- status de envio
- histórico de comunicação
- suporte a avisos operacionais e financeiros

Canais possíveis no futuro:

- app
- e-mail
- SMS
- WhatsApp
- push

## Módulo de relatórios

Responsabilidade:

- consultas consolidadas
- indicadores operacionais
- indicadores financeiros
- visão gerencial
- exportações
- apoio à tomada de decisão

Esse módulo deve priorizar leitura e consolidação.
Ele não deve ser o dono da verdade transacional.

## Módulo de auditoria

Responsabilidade:

- trilha de auditoria
- rastreio de ações críticas
- registro de alterações importantes
- contexto de usuário
- contexto de tenant
- apoio à conformidade e investigação

A auditoria é obrigatória para ações relevantes.

## Módulo de storage

Responsabilidade:

- arquivos
- documentos
- comprovantes
- anexos
- abstração de armazenamento em objeto

A direção inicial é usar S3 como storage principal.

## Módulo de administração da plataforma

Responsabilidade:

- visão global da plataforma
- supervisão operacional
- ações administrativas controladas
- suporte central da solução SaaS

Esse módulo deve existir com muito cuidado para não quebrar o isolamento entre tenants.

## Comunicação entre módulos

A comunicação entre módulos deve seguir esta ordem de preferência:

1. chamada direta por interface interna clara
2. eventos internos para efeitos secundários
3. processamento assíncrono quando fizer sentido

Exemplos:

- a geração de fatura pode chamar diretamente os dados necessários de leituras e tarifas
- após gerar uma fatura, pode haver um evento para disparar notificação
- após confirmação de pagamento, pode haver atualização de relatório e auditoria

## Regras de fronteira

As seguintes regras são obrigatórias:

- controller não decide regra de negócio
- service não deve virar depósito desorganizado de lógica
- repository não orquestra fluxo de negócio
- regra de domínio não depende de HTTP
- tenant deve ser validado antes de alterar dados
- ações sensíveis exigem autorização clara
- ações críticas exigem auditoria
- financeiro exige rigor extra

## Estrutura esperada no NestJS

A implementação futura deve respeitar uma organização parecida com esta:

- controllers
- application
- domain
- infrastructure
- dto
- repositories
- events
- policies

Exemplo conceitual:

src/modules/invoices/
  controllers/
  application/
  domain/
  infrastructure/
  dto/
  repositories/
  events/
  policies/

A estrutura exata pode ser ajustada depois, mas os limites entre responsabilidades devem permanecer claros.

## Módulos mais críticos desde o início

Os módulos com maior criticidade são:

- autenticação e acesso
- tenants
- leituras
- faturas
- pagamentos
- auditoria

Esses módulos exigem mais rigor porque impactam:

- segurança
- isolamento entre associações
- consistência financeira
- rastreabilidade
- continuidade operacional

## Direção final

O backend do Água Nativa será construído como um **monólito modular multi-tenant, auditável, seguro e preparado para evolução**.

Essa arquitetura foi escolhida para garantir:

- clareza
- segurança
- organização
- escalabilidade com disciplina
- prevenção de retrabalho
- redução de dívida técnica evitável

Este documento deve servir como base direta para a futura estruturação dos módulos do backend em NestJS.
