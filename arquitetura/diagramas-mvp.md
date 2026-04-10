# Projeto Trail — Arquitetura e Diagramas Consolidados do MVP- Evolução incremental, sem overengineering

---

# 1. 📊 Diagrama ER — Modelo de Dados do MVP

O diagrama ER representa as entidades persistidas no sistema e os seus relacionamentos principais.

Este modelo deve orientar:
- criação das entidades no backend
- mapeamento com Entity Framework Core
- migrations
- validação de PRs relacionados ao banco

```mermaid
erDiagram
    USER {
        GUID Id
        string Name
        string Email
        string PasswordHash
        string Role
        datetime CreatedAt
    }

    TRAIL {
        GUID Id
        string Name
        string Description
        datetime CreatedAt
    }

    CHALLENGE {
        GUID Id
        GUID TrailId
        string Title
        string Description
        int Order
        datetime CreatedAt
    }

    SUBMISSION {
        GUID Id
        GUID StudentId
        GUID ChallengeId
        string DeliveryUrl
        datetime SubmittedAt
        string Status
        GUID ReviewerId
        int Score
        string Feedback
        datetime ReviewedAt
    }

    USER ||--o{ SUBMISSION : "submits (student)"
    USER ||--o{ SUBMISSION : "reviews (mentor)"
    TRAIL ||--o{ CHALLENGE : "contains"
    CHALLENGE ||--o{ SUBMISSION : "receives"
```

## 1.1 Leituras importantes do modelo

### USER
Representa qualquer usuário do sistema:
- estudante
- mentor
- gestor

### TRAIL
Representa a trilha de aprendizagem.

### CHALLENGE
Representa os desafios da trilha.

### SUBMISSION
É a entidade central do MVP.  
Ela concentra:
- a entrega do estudante
- o status da entrega
- os dados de avaliação
- os timestamps necessários para cálculo dos KPIs

### Decisão intencional do MVP
No MVP, **a avaliação está embutida na própria SUBMISSION**.

Isso evita:
- criação prematura de uma entidade Review
- complexidade desnecessária
- excesso de joins

---

# 2. 🔄 Diagrama de Fluxo — Visão Funcional do Sistema

Este diagrama apresenta o fluxo funcional ponta a ponta do MVP.

Ele mostra, em alto nível, como o sistema entrega valor para:
- estudantes
- mentores
- gestores

```mermaid
flowchart TD
    subgraph Student["👤 Fluxo do Estudante"]
        A["🔐 Login"]
        B["📚 Visualiza Trilha"]
        C["🎯 Seleciona Desafio"]
        D["📤 Submete Entrega"]
    end

    subgraph System["⚙️ Backend do Sistema"]
        E["✅ Submission Criada"]
        I["📊 Cálculo de Métricas"]
    end

    subgraph Mentor["👨‍🏫 Fluxo do Mentor"]
        F["👀 Visualiza Submissões"]
        G["✏️ Avalia Entrega"]
        H["🔄 Submission Atualizada"]
    end

    subgraph Dashboard["📈 Visualização Compartilhada"]
        J["📊 Dashboard & Progresso"]
    end

    A --> B
    B --> C
    C --> D
    D --> E
    E --> F
    F --> G
    G --> H
    H --> I
    I --> J
```

## 2.1 O que este fluxo mostra

- O estudante inicia a jornada pelo login
- A trilha e os desafios são consumidos pelo frontend a partir do backend
- A submissão de entrega cria a entidade central do sistema
- O mentor atua sobre as submissões
- As métricas surgem a partir da atualização da submissão
- O dashboard é o reflexo final do fluxo operacional

---

# 3. 🔐 Diagramas de Sequência — Fluxos Técnicos do MVP

A seguir estão os diagramas de sequência que detalham **como frontend, backend e banco interagem ao longo do tempo**.

Cada diagrama cobre uma parte específica do MVP.

---

## 3.1 Diagrama de Sequência — Login do Usuário (MVP‑01)

Este fluxo descreve o processo de autenticação com JWT.

```mermaid
sequenceDiagram
    autonumber
    participant User as Usuário
    participant Frontend as Frontend (Next.js)
    participant Backend as Backend (.NET API)
    participant DB as Banco de Dados

    User ->> Frontend: Informa email e senha
    Frontend ->> Backend: POST /auth/login
    Backend ->> DB: Buscar usuário por email
    DB -->> Backend: Dados do usuário
    Backend ->> Backend: Validar senha e role
    Backend -->> Frontend: JWT + Role
    Frontend -->> User: Usuário autenticado
```

### Observações
- O frontend não valida credenciais
- O backend valida senha e perfil
- O JWT retornado passa a ser usado nas próximas requisições

---

## 3.2 Diagrama de Sequência — Autorização por Perfil (MVP‑01)

Este fluxo detalha como o backend usa o JWT para autorizar acesso.

```mermaid
sequenceDiagram
    autonumber
    participant Frontend as Frontend (Next.js)
    participant Backend as Backend (.NET API)

    Frontend ->> Backend: Requisição autenticada com JWT
    Backend ->> Backend: Validar token
    Backend ->> Backend: Ler claims e role
    Backend -->> Frontend: Acesso permitido ou negado
```

### Observações
- Autorização é responsabilidade do backend
- O frontend apenas reage ao resultado
- A role do usuário define o que ele pode acessar

---

## 3.3 Diagrama de Sequência — Visualização da Trilha e Desafios (MVP‑02)

Este fluxo cobre a leitura da trilha e de seus desafios pelo estudante.

```mermaid
sequenceDiagram
    autonumber
    participant Student as Estudante
    participant Frontend as Frontend (Next.js)
    participant Backend as Backend (.NET API)
    participant DB as Banco de Dados

    Student ->> Frontend: Acessa tela da trilha
    Frontend ->> Backend: GET /trails
    Backend ->> DB: Buscar trilhas
    DB -->> Backend: Trilhas
    Backend -->> Frontend: Dados da trilha

    Frontend ->> Backend: GET /trails/{id}/challenges
    Backend ->> DB: Buscar desafios da trilha
    DB -->> Backend: Lista de desafios
    Backend -->> Frontend: Desafios com status
```

### Observações
- O backend consulta trilhas e desafios no banco
- O frontend exibe os dados sem recalcular regra de negócio
- O status exibido deve refletir dados reais do progresso

---

## 3.4 Diagrama de Sequência — Submissão de Entrega (MVP‑03)

Este fluxo representa o nascimento da entidade **SUBMISSION**.

```mermaid
sequenceDiagram
    autonumber
    participant Student as Estudante
    participant Frontend as Frontend (Next.js)
    participant Backend as Backend (.NET API)
    participant DB as Banco de Dados

    Student ->> Frontend: Preenche link da entrega
    Frontend ->> Backend: POST /submissions
    Backend ->> Backend: Validar token e dados
    Backend ->> DB: Criar Submission (status: Submitted)
    DB -->> Backend: Submission persistida
    Backend -->> Frontend: HTTP 201 Created
    Frontend -->> Student: Confirmação da entrega
```

### Observações
- O campo `SubmittedAt` nasce neste momento
- O status inicial da entrega é `Submitted`
- A submissão é a base do fluxo de avaliação e métricas

---

## 3.5 Diagrama de Sequência — Listagem de Submissões para o Mentor (MVP‑04)

Este fluxo cobre a etapa em que o mentor acessa a fila de avaliações.

```mermaid
sequenceDiagram
    autonumber
    participant Mentor as Mentor
    participant Frontend as Frontend (Next.js)
    participant Backend as Backend (.NET API)
    participant DB as Banco de Dados

    Mentor ->> Frontend: Acessa tela de submissões
    Frontend ->> Backend: GET /submissions
    Backend ->> Backend: Validar role Mentor
    Backend ->> DB: Buscar submissões pendentes
    DB -->> Backend: Lista de submissions
    Backend -->> Frontend: Dados das submissions
    Frontend -->> Mentor: Lista renderizada
```

### Observações
- Apenas mentor deve acessar esse fluxo
- O backend deve validar a role antes de consultar o banco
- O frontend apenas renderiza a fila

---

## 3.6 Diagrama de Sequência — Avaliação e Feedback do Mentor (MVP‑04)

Este fluxo cobre a atualização da submissão com feedback e score.

```mermaid
sequenceDiagram
    autonumber
    participant Mentor as Mentor
    participant Frontend as Frontend (Next.js)
    participant Backend as Backend (.NET API)
    participant DB as Banco de Dados

    Mentor ->> Frontend: Envia avaliação
    Frontend ->> Backend: PUT /submissions/{id}/review
    Backend ->> Backend: Validar role Mentor
    Backend ->> DB: Atualizar Submission (score, feedback, status, reviewedAt, reviewerId)
    DB -->> Backend: Submission atualizada
    Backend -->> Frontend: HTTP 200 OK
    Frontend -->> Mentor: Avaliação registrada
```

### Observações
- O momento da avaliação define o campo `ReviewedAt`
- O status da submissão é atualizado
- A partir daqui o sistema já possui dados suficientes para KPIs

---

## 3.7 Diagrama de Sequência — Snapshot / Progresso do Estudante (MVP‑02 + MVP‑03 + MVP‑04)

Este fluxo mostra a visão consolidada do progresso do estudante.

```mermaid
sequenceDiagram
    autonumber
    participant Student as Estudante
    participant Frontend as Frontend (Next.js)
    participant Backend as Backend (.NET API)
    participant DB as Banco de Dados

    Student ->> Frontend: Abre tela de progresso
    Frontend ->> Backend: GET /students/{id}/progress
    Backend ->> DB: Buscar challenges e submissions do estudante
    DB -->> Backend: Dados de trilha e submissions
    Backend ->> Backend: Consolidar progresso
    Backend -->> Frontend: Progresso calculado
    Frontend -->> Student: Exibição do snapshot
```

### Observações
- Este fluxo apoia a visão do estudante sobre sua jornada
- O backend deve consolidar o progresso a partir de dados reais
- O frontend apenas apresenta o resultado

---

## 3.8 Diagrama de Sequência — Cálculo de KPIs Operacionais (MVP‑05)

Este fluxo descreve o cálculo dos indicadores operacionais.

```mermaid
sequenceDiagram
    autonumber
    participant Backend as Backend (.NET API)
    participant DB as Banco de Dados

    Backend ->> DB: Buscar submissions avaliadas
    DB -->> Backend: Dados brutos
    Backend ->> Backend: Calcular lead time
    Backend ->> Backend: Calcular taxa de conclusão
    Backend ->> Backend: Calcular cobertura de desafios
```

### Observações
- KPIs são calculados no backend
- Não existe tabela própria para métricas no MVP
- O cálculo deve refletir sempre os dados mais recentes

---

## 3.9 Diagrama de Sequência — Dashboard e Visualização dos KPIs (MVP‑05)

Este fluxo mostra a entrega final dos indicadores ao frontend.

```mermaid
sequenceDiagram
    autonumber
    participant User as Usuário
    participant Frontend as Frontend (Next.js)
    participant Backend as Backend (.NET API)
    participant DB as Banco de Dados

    User ->> Frontend: Acessa dashboard
    Frontend ->> Backend: GET /metrics/overview
    Backend ->> DB: Buscar dados necessários
    DB -->> Backend: Dados das submissions
    Backend ->> Backend: Calcular KPIs
    Backend -->> Frontend: Métricas calculadas
    Frontend -->> User: Dashboard renderizado
```

### Observações
- O frontend não recalcula métricas
- O backend entrega os KPIs já consolidados
- O dashboard é consequência de todo o fluxo anterior

---

# 4. ✅ Regras Arquiteturais do MVP

Para manter consistência entre código e domínio, o MVP deve obedecer às seguintes regras:

- O frontend **não implementa regra de negócio**
- O backend centraliza:
  - validações
  - segurança
  - cálculo de métricas
  - orquestração do fluxo
- O banco guarda apenas:
  - dados de domínio
  - timestamps necessários
- KPIs são sempre **derivados**, nunca persistidos no MVP

---

## 📌 Regra de Ouro do Projeto

> Se um endpoint, serviço, tela ou regra  
> não aparece em pelo menos um diagrama deste documento,  
> ele deve ser questionado antes de entrar no MVP.

---

# 5. 🚀 Como este documento deve ser usado

Este documento deve ser usado como referência para:

- criação das entidades
- criação de endpoints
- organização de frontend e backend
- revisão de pull requests
- discussão de bugs e divergências
- mentoria técnica
- onboarding de novos participantes

---

## ✅ Encerramento

Este documento consolida a arquitetura do MVP em sua forma atual.
A partir dele, o projeto está apto a evoluir com consistência técnica e clareza funcional.


Este documento consolida, em um único artefato, os diagramas oficiais do MVP do **Projeto Trail**.

Ele reúne:
- **Modelo de Dados (ER)**
- **Fluxo Funcional do Sistema**
- **Diagramas de Sequência completos do MVP**

Este material deve ser usado como:
- referência arquitetural oficial
- base para alinhamento técnico
- apoio à implementação do MVP
- apoio para revisão de código
- artefato de onboarding para novos participantes

---

## 🎯 Objetivo deste Documento

Garantir que todos os envolvidos no projeto tenham uma visão consistente sobre:

- quais entidades existem
- como elas se relacionam
- como o sistema se comporta
- como frontend, backend e banco interagem
- como os principais fluxos do MVP acontecem ponta a ponta

---

## 🧭 Visão Geral da Arquitetura

A arquitetura do MVP foi definida com foco em simplicidade, clareza e viabilidade de implementação.

### Stack adotada
- **Frontend:** Next.js
- **Backend:** ASP.NET Core (.NET API)
- **Persistência:** SQL Server com Entity Framework Core
- **Autenticação:** JWT
- **Nuvem:** Azure

### Princípios arquiteturais
- Simplicidade antes de sofisticação
- Regras de negócio centralizadas no backend
- Frontend orientado à experiência e consumo de API
- KPIs calculados dinamicamente, sem persistência redundante
