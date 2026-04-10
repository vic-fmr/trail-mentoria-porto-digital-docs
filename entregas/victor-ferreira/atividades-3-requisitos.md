# 📄 Entrega: Backlog e Priorização do MVP — Projeto Trail

Este documento consolida o backlog inicial do MVP, priorizado e estruturado para orientar o desenvolvimento técnico e a arquitetura do produto.

---

## 📋 Itens do Backlog (MVP)

**ID:** MVP-01  
**Título:** Autenticação e Perfis de Acesso  
**User story:** Como usuário, quero acessar o sistema com um perfil (estudante, mentor ou gestor) para visualizar as funcionalidades e dados pertinentes ao meu papel.  
**Valor:** Garante a segurança e o isolamento multi-tenant, assegurando que cada empresa acesse apenas seus próprios dados.  
**Critério de aceite (mínimo):** Login via JWT funcional com diferenciação de permissões entre os perfis definidos.  
**Prioridade:** Now.  
**Dependências:** Nenhuma.  
**Riscos/observações:** Complexidade na implementação correta do isolamento de dados no Entity Framework.

---

**ID:** MVP-02  
**Título:** Visualização da Trilha e Desafios  
**User story:** Como estudante, quero visualizar minha trilha e marcos para entender o que devo fazer e onde estou na jornada.  
**Valor:** Reduz a dispersão de informações e centraliza o roteiro de aprendizagem em um único local.  
**Critério de aceite (mínimo):** Lista de desafios carregada do banco indicando o status (pendente/concluído).  
**Prioridade:** Now.  
**Dependências:** MVP-01.  
**Riscos/observações:** Requer que a estrutura de Programas -> Trilhas -> Módulos esteja bem modelada no banco.

---

**ID:** MVP-03  
**Título:** Submissão de Entrega  
**User story:** Como estudante, quero enviar minha entrega (link ou arquivo) para que ela fique registrada para avaliação do mentor.  
**Valor:** Formaliza o processo de entrega e permite o rastreio do progresso do estudante.  
**Critério de aceite (mínimo):** Registro da submissão com link/arquivo, timestamp e status "submetido".  
**Prioridade:** Now.  
**Dependências:** MVP-02.  
**Riscos/observações:** Necessidade de configurar o Azure Blob Storage se o upload de arquivos for habilitado.

---

**ID:** MVP-04  
**Título:** Avaliação e Feedback  
**User story:** Como mentor, quero avaliar uma entrega e registrar feedback para orientar o estudante e alimentar as métricas do sistema.  
**Valor:** Reduz o lead time de feedback e fornece dados qualitativos sobre a performance do aluno.  
**Critério de aceite (mínimo):** Mentor define status, nota e comentário; o sistema registra o timestamp da avaliação.  
**Prioridade:** Now.  
**Dependências:** MVP-03.  
**Riscos/observações:** O fluxo deve ser simples para garantir a adoção por parte dos mentores da Avanade.

---

**ID:** MVP-05  
**Título:** Dashboard de Métricas Operacionais (KPIs)  
**User story:** Como gestor ou mentor, quero visualizar os KPIs mandatórios (Lead Time, Conclusão e Cobertura) para acompanhar a saúde da turma.  
**Valor:** Transforma dados operacionais em inteligência para o Porto Digital e empresas parceiras.  
**Critério de aceite (mínimo):** Exibição de métricas calculadas dinamicamente após cada avaliação de mentor.  
**Prioridade:** Now.  
**Dependências:** MVP-04.  
**Riscos/observações:** Risco de cálculos imprecisos se os timestamps não forem capturados corretamente.

---

**ID:** MVP-06  
**Título:** Snapshot de Performance do Estudante  
**User story:** Como gestor ou estudante, quero ver um painel individual com evolução e métricas para apoiar decisões de contratação.  
**Valor:** Serve como "sistema de registro" de talentos para as empresas do ecossistema.  
**Critério de aceite (mínimo):** Tela com percentual de conclusão da trilha, histórico de feedbacks e KPIs pessoais.  
**Prioridade:** Next.  
**Dependências:** MVP-04 e MVP-05.  
**Riscos/observações:** Deve garantir que um gestor de uma empresa não veja dados de estudantes de outra.

---

## 🏠 Entrega 02 — Dúvidas, Riscos e Hipóteses

### ❓ Dúvidas Principais
* Qual será a escala exata de notas (0-10 ou conceitos A/B/C) para o cálculo de performance?
* O upload de arquivos via Azure Blob Storage é mandatório para o MVP ou apenas links de GitHub bastam?

### ⚠️ Riscos Percebidos
* **Prazo:** A implementação da arquitetura multi-tenant com isolamento rigoroso de dados pode ser complexa para o tempo de 3 meses.
* **Engajamento:** Se o processo de feedback for mais burocrático que o atual (planilhas), os mentores podem não utilizar a ferramenta.

### 💡 Hipóteses a Validar
* A centralização das submissões reduzirá o tempo de espera do estudante por feedback em 40%.
* A visibilidade dos KPIs ajudará gestores a identificar top performers de forma 2x mais rápida que o método manual.
