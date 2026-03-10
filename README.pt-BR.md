# Água Nativa

Água Nativa é uma plataforma SaaS multi-tenant projetada para a gestão profissional de associações rurais de água.

A plataforma fornece uma infraestrutura digital moderna que permite que associações responsáveis pela distribuição comunitária de água gerenciem consumidores, propriedades, hidrômetros, leituras, faturamento, pagamentos e transparência operacional de forma confiável e escalável.

O projeto está sendo desenvolvido utilizando práticas de engenharia de nível enterprise, com foco em qualidade arquitetural, manutenibilidade, segurança e evolução do sistema no longo prazo.

Água Nativa não foi concebido como uma simples ferramenta interna. Ele está sendo projetado como uma plataforma SaaS robusta capaz de atender múltiplas associações de água, mantendo isolamento rigoroso de dados entre os tenants.

---

## Contexto do Problema

Muitas associações rurais de água ainda operam utilizando planilhas, cadernos ou sistemas fragmentados para gerenciar suas operações essenciais.

Isso normalmente gera problemas como:

- faturamento inconsistente
- baixa rastreabilidade do consumo
- processos operacionais manuais e suscetíveis a erro
- dificuldade para auditoria de registros financeiros
- falta de transparência operacional para os associados
- dificuldade de escalar práticas de gestão

Água Nativa foi criado para resolver esses desafios fornecendo uma plataforma especializada desenvolvida especificamente para a gestão da distribuição comunitária de água.

O objetivo é levar capacidades profissionais de gestão de sistemas para associações que atualmente operam com infraestrutura tecnológica limitada.

---

## Escopo da Plataforma

A plataforma foi projetada para suportar todo o ciclo operacional de associações rurais de água.

Principais capacidades incluem:

- gestão de associações
- gestão do ciclo de vida de consumidores
- gestão de propriedades e unidades
- controle do ciclo de vida de hidrômetros
- operações de leitura de hidrômetros
- cálculo de consumo de água
- configuração de tarifas e preços
- geração de faturas
- cobranças extras para ciclos de faturamento futuros
- controle e conciliação de pagamentos
- notificações operacionais
- relatórios e análises
- trilha completa de auditoria operacional

---

## Arquitetura SaaS Multi-Tenant

Água Nativa foi projetado desde o início como uma **plataforma SaaS multi-tenant**.

Cada associação de água opera como um tenant independente dentro do sistema.

Essa arquitetura garante:

- isolamento rigoroso de dados entre associações
- usuários e permissões vinculados ao tenant
- ambientes operacionais independentes
- registros financeiros e ciclos de faturamento isolados
- auditoria no nível do tenant

Cada entidade do domínio referencia obrigatoriamente seu tenant, e a validação de tenant é aplicada em todas as operações do sistema.

Esse modelo permite que a plataforma escale para suportar muitas associações sem comprometer isolamento de dados ou integridade operacional.

---

## Interfaces da Plataforma

O sistema é estruturado em quatro interfaces principais.

### Plataforma Administrativa

Ambiente central responsável pela administração global da plataforma e governança do SaaS.

### Painel Web da Associação

Interface operacional utilizada pelas equipes da associação para gerenciar atividades diárias como consumidores, hidrômetros, leituras, faturas e pagamentos.

### Aplicativo do Leiturista

Aplicativo móvel utilizado por operadores de campo para registrar leituras de hidrômetros.

O aplicativo será projetado para suportar **operações offline-first**, com sincronização posterior.

### Aplicativo do Cliente

Aplicativo utilizado pelos consumidores para acessar faturas, histórico de pagamentos, notificações e informações de consumo.

---

## Arquitetura do Sistema

A plataforma segue uma arquitetura em camadas para garantir separação clara de responsabilidades.

- Camada de Apresentação
- Camada de Aplicação
- Camada de Domínio
- Camada de Persistência
- Camada de Infraestrutura

Essa arquitetura melhora manutenibilidade, testabilidade e escalabilidade.

O sistema também está sendo projetado com limites claros entre módulos para evitar dívida técnica desnecessária no futuro.

---

## Stack Tecnológica

### Frontend Web

- Next.js
- TypeScript
- React

### Backend

- Node.js
- TypeScript
- NestJS

### Banco de Dados

- PostgreSQL
- Supabase PostgreSQL (plataforma inicial preferencial)

### Aplicações Mobile

- React Native

### Infraestrutura

- AWS
- Docker

### Armazenamento

- Amazon S3

---

## Estrutura do Repositório

    apps
    backend
    frontend
    infra
    scripts
    docs

Essa estrutura separa código da aplicação, configuração de infraestrutura e documentação para garantir manutenibilidade no longo prazo.

---

## Documentação

O projeto segue uma abordagem **documentation-first e architecture-first**.

A documentação é mantida dentro do diretório /docs.

    docs/
    ├─ adr
    ├─ api
    ├─ architecture
    ├─ database
    ├─ devops
    ├─ modules
    ├─ rfc
    └─ security

Os documentos existentes incluem definições arquiteturais, modelos de banco de dados e registros de decisões arquiteturais.

### Documentos Atuais Principais

#### Arquitetura
- system-overview.md
- multi-tenant-strategy.md
- platform-architecture.md
- cloud-architecture.md

#### Banco de Dados
- conceptual-model.md
- water-domain-model.md
- core-entities.md
- integrity-rules.md
- logical-model.md
- physical-schema.md

#### ADR
- adr/0001-multi-tenant-architecture.md

---

## Princípios de Engenharia

O projeto segue princípios rigorosos de engenharia:

- arquitetura definida antes da implementação
- documentação antes da expansão do sistema
- prevenção de dívida técnica evitável
- limites fortes entre módulos
- decisões arquiteturais rastreáveis
- segurança por design
- evolução controlada do sistema

O objetivo é construir uma plataforma que possa evoluir sem degradação arquitetural.

---

## Status do Projeto

O projeto está atualmente na **fase de arquitetura e definição do sistema**.

As áreas de foco atuais incluem:

- definição de domínio
- consolidação da arquitetura
- modelagem de banco de dados
- definição de limites de módulos
- fortalecimento da documentação

A implementação começará quando a base arquitetural estiver suficientemente consolidada.

---

## Próximos Passos

Os próximos passos incluem:

- definição da arquitetura de serviços
- estruturação dos módulos do backend
- mecanismos de autenticação e isolamento de tenants
- implementação do motor de faturamento
- fundação das aplicações mobile
- automação de infraestrutura

---

## Direção do Projeto

Água Nativa está sendo desenvolvido como uma plataforma de software séria, com potencial SaaS, disciplina multi-tenant e padrões de engenharia de nível enterprise.

O objetivo de longo prazo é construir uma plataforma digital confiável capaz de atender muitas associações, mantendo padrões profissionais de operação e uma base arquitetural sólida.
