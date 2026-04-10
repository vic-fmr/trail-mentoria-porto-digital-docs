# Pull Request — Projeto Trail

## 📌 Resumo da mudança
Descreva de forma objetiva o que este PR implementa, corrige ou refatora.

Exemplo:
- Implementa endpoint `POST /submissions`
- Adiciona tela de login
- Corrige cálculo de Lead Time
- Ajusta relacionamento entre `Trail` e `Challenge`

---

## 🎯 Item do Backlog relacionado
Marque **apenas o item principal** deste PR.

- [ ] MVP‑01 — Autenticação e Perfis
- [ ] MVP‑02 — Visualização da Trilha e Desafios
- [ ] MVP‑03 — Submissão de Entrega
- [ ] MVP‑04 — Avaliação e Feedback
- [ ] MVP‑05 — KPIs Operacionais
- [ ] Outro (descrever): ____________

---

## 🧭 Tipo de mudança
Marque o tipo principal deste PR.

- [ ] Feature nova
- [ ] Correção de bug
- [ ] Refatoração
- [ ] Ajuste de banco / migration
- [ ] Ajuste de frontend / UI
- [ ] Ajuste de backend / API
- [ ] Documentação
- [ ] Testes
- [ ] Infra / pipeline / cloud

---

## 🗺️ Diagrama(s) impactado(s)
Indique qual(is) diagrama(s) este PR implementa ou altera.

### ER / Modelo de Dados
- [ ] USER
- [ ] TRAIL
- [ ] CHALLENGE
- [ ] SUBMISSION

### Fluxo Funcional
- [ ] Login
- [ ] Visualizar trilha
- [ ] Selecionar desafio
- [ ] Submeter entrega
- [ ] Visualizar submissões
- [ ] Avaliar entrega
- [ ] Calcular métricas
- [ ] Exibir dashboard

### Diagramas de Sequência
- [ ] Login do usuário
- [ ] Autorização por perfil
- [ ] Visualização de trilha e desafios
- [ ] Submissão de entrega
- [ ] Listagem de submissões do mentor
- [ ] Avaliação e feedback
- [ ] Snapshot / progresso do estudante
- [ ] Cálculo de KPIs
- [ ] Dashboard e visualização de métricas

---

## 🧱 Entidades / Campos impactados
Liste as entidades e campos alterados neste PR.

### Entidades
- [ ] USER
- [ ] TRAIL
- [ ] CHALLENGE
- [ ] SUBMISSION
- [ ] Nenhuma entidade persistida

### Campos alterados / adicionados
Exemplo:
- `USER.Role`
- `SUBMISSION.SubmittedAt`
- `SUBMISSION.ReviewedAt`
- `CHALLENGE.Order`

```text
Preencher aqui:
-
-
-
```

---

## 🔍 Descrição técnica
Explique o que foi feito no código.

Inclua:
- endpoints criados/alterados
- serviços alterados
- componentes/telas criadas
- migrations geradas
- regras de negócio afetadas

```text
Preencher aqui.
```

---

## ✅ Como esta mudança respeita os diagramas do MVP
Explique rapidamente como este PR está alinhado com os diagramas oficiais.

Exemplo:
- “Este PR implementa o fluxo do diagrama de sequência de submissão”
- “Este PR mantém o relacionamento Trail → Challenge conforme o ER”

```text
Preencher aqui.
```

---

## 🧪 Como validar este PR
Explique passo a passo como testar.

### Backend
```text
Exemplo:
1. Rodar a API
2. Chamar POST /auth/login
3. Validar retorno do JWT
```

### Frontend
```text
Exemplo:
1. Abrir tela de login
2. Informar credenciais válidas
3. Confirmar redirecionamento
```

### Banco / Migration
```text
Exemplo:
1. Executar migration
2. Confirmar tabela criada
3. Verificar colunas esperadas
```

---

## 📸 Evidências (quando aplicável)
Inclua prints, GIFs, payloads ou trechos de resposta úteis para revisão.

```text
Opcional
```

---

## 🤖 Uso de IA neste PR
Se houve uso de IA (Copilot / chat / assistente), descreva como foi usado.

- [ ] Não usei IA
- [ ] Usei IA para boilerplate
- [ ] Usei IA para gerar rascunho de código
- [ ] Usei IA para depuração
- [ ] Usei IA para testes
- [ ] Usei IA para documentação

### Descrição do uso
```text
Exemplo:
Usei Copilot para gerar DTOs e rascunho do endpoint, depois revisei manualmente.
```

### Confirmação obrigatória
- [ ] Eu entendo o código gerado/alterado e consigo explicá-lo
- [ ] Revisei o código antes de subir
- [ ] Não incluí segredos, credenciais ou dados sensíveis

---

## ⚠️ Riscos / pontos de atenção
Liste qualquer risco percebido neste PR.

Exemplos:
- impacto em autenticação
- risco de quebrar cálculo de métricas
- migration irreversível
- dependência de dados seed

```text
Preencher aqui.
```

---

## 🚫 Fora de escopo deste PR
Declare explicitamente o que **não** está sendo resolvido aqui.

Exemplo:
- “Não implementa dashboard”
- “Não inclui upload de arquivos”
- “Não trata multi-tenant completo”

```text
Preencher aqui.
```

---

# ✅ Checklist do autor do PR

## Geral
- [ ] Este PR está vinculado a um item real do backlog
- [ ] O escopo está claro e limitado
- [ ] O PR não mistura múltiplos problemas sem relação
- [ ] A implementação está alinhada com pelo menos um diagrama oficial do MVP

## Modelo de Dados
- [ ] Não criei entidade nova sem necessidade clara
- [ ] Mantive coerência com o ER
- [ ] Relacionamentos continuam válidos
- [ ] Campos novos têm propósito claro no fluxo do MVP

## Fluxo Funcional
- [ ] A mudança respeita a ordem lógica do fluxo do sistema
- [ ] Não pulei etapas críticas do MVP
- [ ] Não movi regra de negócio para a camada errada

## Frontend
- [ ] O frontend não implementa regra de negócio crítica
- [ ] A UI reflete respostas reais da API
- [ ] Há tratamento mínimo de loading e erro, quando aplicável

## Backend
- [ ] O backend concentra validações e regras de domínio
- [ ] Os endpoints seguem os fluxos definidos
- [ ] A segurança/autorização foi respeitada

## Banco / EF Core
- [ ] A migration reflete corretamente as mudanças
- [ ] Os campos e relações seguem o modelo do MVP
- [ ] Não persisti métricas sem necessidade

## IA / Segurança
- [ ] Revisei tudo que foi gerado com IA
- [ ] Não subi dados sensíveis
- [ ] Eu consigo explicar o que este PR faz

---

# 🧑‍💻 Checklist do revisor

## Alinhamento com o MVP
- [ ] O PR está claramente conectado ao backlog
- [ ] O PR está coerente com os diagramas
- [ ] O PR não aumenta escopo sem necessidade

## Modelo e Fluxo
- [ ] O ER continua consistente
- [ ] O fluxo funcional não foi quebrado
- [ ] O comportamento implementado condiz com o(s) diagrama(s) de sequência

## Qualidade técnica
- [ ] O código está claro
- [ ] O PR é revisável
- [ ] Não há overengineering
- [ ] O risco está aceitável para o estágio do MVP

---

## 📌 Regra de ouro
``
> Se esta mudança não aparece em nenhum diagrama do MVP  
> ou não se conecta a um item do backlog,  
> ela deve ser questionada antes da aprovação.
``