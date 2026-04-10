# Encontro 04 — Início da Implementação do MVP (Guia Técnico Completo)

Este documento marca o **início oficial do desenvolvimento do MVP** e deve ser
utilizado como **guia de execução diária**.

📌 Se você tiver dúvida sobre:
- o que desenvolver
- em qual ordem
- para que serve cada entidade
- para que serve cada campo

👉 a resposta deve estar **neste arquivo**.

---

## ✅ Stack do Projeto (fechada)

- **Frontend:** Next.js
- **Backend:** ASP.NET Core (C#) + Entity Framework Core
- **Banco de Dados:** SQL Server
- **Cloud:** Azure

A stack **não será discutida**.  
O foco agora é **implementar o MVP funcionando**.

---

## 📋 Backlog MVP — Itens NOW

Os itens abaixo vêm diretamente do Encontro 03 e **DEVEM ser implementados**:

- **MVP‑01** — Autenticação e Perfis de Acesso
- **MVP‑02** — Visualização da Trilha e Desafios
- **MVP‑03** — Submissão de Entrega
- **MVP‑04** — Avaliação e Feedback
- **MVP‑05** — KPIs Operacionais

Este encontro transforma esse backlog em **tasks técnicas executáveis**.

---

# 🧱 Modelo de Dados do MVP (Entidades e Campos)

Antes de codar, entenda **o domínio**.

---

## 👥 Entidade: User

Representa qualquer pessoa que acessa o sistema.

### Campos

- **Id**  
  Identificador único do usuário (GUID).  
  Usado em todos os relacionamentos.

- **Name**  
  Nome do usuário.  
  Exibido em telas, feedbacks e relatórios.

- **Email**  
  Identificador de login.  
  Usado na autenticação.

- **PasswordHash**  
  Senha criptografada.  
  **Nunca armazene senha em texto puro.**

- **Role**  
  Perfil do usuário:
  - Student
  - Mentor
  - Manager  

  Define permissões e acesso às funcionalidades.

📌 **Regra importante:**  
Role controla acesso no backend (Authorize), não no frontend.

---

## 🗺️ Entidade: Trail

Representa uma trilha de aprendizado.

### Campos

- **Id**  
  Identificador da trilha.

- **Name**  
  Nome da trilha (ex: “Full Stack .NET”).

- **Description**  
  Breve explicação do objetivo da trilha.

📌 No MVP, assume-se **uma trilha principal**.

---

## 🧩 Entidade: Challenge

Representa um desafio dentro da trilha.

### Campos

- **Id**  
  Identificador do desafio.

- **Title**  
  Nome do desafio.

- **Description**  
  Enunciado do desafio.

- **Order**  
  Ordem do desafio na trilha.  
  Controla progressão simples (1, 2, 3…).

- **TrailId**  
  FK para a trilha à qual o desafio pertence.

---

## 📤 Entidade: Submission

Representa a entrega realizada por um estudante.  
É a **entidade central do MVP**.

### Campos

- **Id**  
  Identificador da entrega.

- **StudentId**  
  FK para User.  
  Indica quem fez a entrega.

- **ChallengeId**  
  FK para Challenge.  
  Indica a qual desafio a entrega se refere.

- **DeliveryUrl**  
  Link da entrega (GitHub, Drive, etc.).  
  No MVP **não há upload de arquivo**.

- **SubmittedAt**  
  Data/hora da submissão.  
  Campo essencial para cálculo de métricas.

- **Status**  
  Estado da entrega:
  - Submitted
  - Reviewed  

  Controla o fluxo do processo.

---

## 📝 Avaliação (campos dentro da Submission)

No MVP, **não existe entidade Review separada**.  
A avaliação faz parte da Submission.

### Campos adicionais

- **ReviewerId**  
  FK para User.  
  Indica qual mentor avaliou.

- **Score**  
  Nota simples (ex: 0–10).  
  Usada para métricas e comparação.

- **Feedback**  
  Comentário textual do mentor.  
  Principal valor pedagógico do sistema.

- **ReviewedAt**  
  Data/hora da avaliação.  
  Base para cálculo de Lead Time.

---

## 📊 Métricas (não persistidas)

KPIs **não são salvos no banco**, são calculados dinamicamente.

### Exemplos

- **Lead Time**  
  `ReviewedAt - SubmittedAt`

- **% de Conclusão**  
  `desafios concluídos ÷ total de desafios`

- **Cobertura de Feedback**  
  `submissões avaliadas ÷ submissões entregues`

📌 Persistir métricas cedo gera inconsistência.  
Sempre calcular a partir dos dados brutos.

---

# 🔨 Plano de Implementação — Tasks Técnicas

## 🔐 MVP‑01 — Autenticação e Perfis

### Backend (.NET / EF Core)

**Tasks:**
1. Criar entidade `User` com todos os campos
2. Criar enum `UserRole`
3. Configurar DbContext
4. Criar migration inicial
5. Configurar autenticação JWT
6. Criar endpoint `POST /auth/login`
7. Proteger endpoints por Role

⏱️ **Estimativa:** 12–16h

---

### Banco

- Migration Users
- Executar migration local
- Validar leitura via API

⏱️ **Estimativa:** 4–6h

---

### Frontend (Next.js)

- Tela de login
- Client de autenticação
- Persistência do JWT
- Proteção de rotas
- Redirecionamento pós-login

⏱️ **Estimativa:** 8–10h

---

## 🗺️ MVP‑02 — Trilha e Desafios

### Backend
- Entidade Trail
- Entidade Challenge
- Relacionamento
- Endpoints GET

⏱️ **Estimativa:** 8–12h

### Banco
- Migration Trail + Challenge
- Seed básico

⏱️ **Estimativa:** 4–6h

### Frontend
- Tela da trilha
- Lista de desafios
- Status simples

⏱️ **Estimativa:** 6–8h

---

## 📤 MVP‑03 — Submissão

### Backend
- Entidade Submission
- Endpoint POST /submissions

⏱️ **Estimativa:** 6–8h

### Banco
- Migration Submission
- Relacionamentos

⏱️ **Estimativa:** 2–3h

### Frontend
- Formulário de submissão
- Feedback visual

⏱️ **Estimativa:** 6–8h

---

## 📝 MVP‑04 — Avaliação

### Backend
- Campos de avaliação
- Endpoint PUT /submissions/{id}/review
- Authorize Mentor

⏱️ **Estimativa:** 6–8h

### Frontend
- Lista de submissões
- Tela de avaliação
- Visualização do feedback

⏱️ **Estimativa:** 6–8h

---

## 📊 MVP‑05 — KPIs

### Backend
- Cálculos de métricas
- Endpoint GET /metrics/overview

⏱️ **Estimativa:** 8–12h

### Frontend
- Dashboard simples de KPIs

⏱️ **Estimativa:** 6–8h

---

## 🤖 Uso de IA (GitHub Copilot Free)

Vocês podem usar **GitHub Copilot gratuitamente no VS Code**.

### Usem Copilot para:
- gerar DTOs e entidades
- rascunhar endpoints
- exemplos de JSON
- explicar erros
- testes unitários básicos

### Regras obrigatórias:
- Sempre entender o código antes do commit
- Nunca subir dados sensíveis
- Se não souber explicar → não commitar

---

## 🏠 Entrega da Semana

Atualizar o arquivo:
``