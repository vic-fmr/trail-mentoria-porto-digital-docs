# Atividade 02: Requisitos e Definição de MVP — Projeto Trail

## ✅ Atividade 01 — Extração do Problema

Com base no documento de discovery, seguem os pontos centrais identificados:

* **Problema central identificado:** A ausência de uma ferramenta centralizada que conecte a jornada de aprendizagem, o fluxo de mentoria e as métricas de performance para programas de formação em TI.
* **Público‑alvo principal:** Estudantes de ADS, Mentores da Avanade e Gestores do Porto Digital ou empresas parceiras.
* **Dor mais crítica:** A dificuldade de escala e a falta de visibilidade de dados. Atualmente, o processo é disperso (PDFs, e-mails, planilhas), resultando em feedbacks atrasados e na incapacidade das empresas de identificarem talentos prontos para contratação.
* **Evidência no briefing:** O documento cita que "programas são mais difíceis de escalar, coordenar e medir" e aponta sintomas como "feedbacks de mentoria atrasados, não rastreáveis e sem métrica consolidada".

---

## ✅ Atividade 02 — Derivação de Requisitos do MVP

Esta tabela delimita o que é essencial para o sucesso do projeto nos primeiros 3 meses:

| Requisito derivado do briefing | É MVP? | Justificativa |
| :--- | :---: | :--- |
| **Autenticação e controle de acesso (JWT/Identity)** | ✅ Sim | Essencial para garantir a separação de papéis e o isolamento de dados (Multi-tenancy). |
| **Visualização de Trilhas e Desafios** | ✅ Sim | É a funcionalidade base para o estudante saber o que estudar e o que entregar. |
| **Submissão de Desafios (Link/Arquivo)** | ✅ Sim | Core do produto; sem a entrega, não há ciclo de feedback ou métricas. |
| **Painel de Avaliação para Mentores** | ✅ Sim | Necessário para reduzir o lead time de feedback e centralizar a comunicação mentor-aluno. |
| **Dashboard com 3 KPIs (Lead Time, Conclusão, Cobertura)** | ✅ Sim | Requisito estratégico para provar o valor do programa para os stakeholders. |
| **Snapshot de Performance por Estudante** | ✅ Sim | Principal ferramenta para apoiar a decisão de contratação pelas empresas parceiras. |
| **Chat em tempo real** | 🚫 Não | Fora de escopo; a comunicação pode ocorrer via comentários no feedback ou canais externos no MVP. |
| **Customização visual por marca (White-label)** | 🚫 Não | Embora a arquitetura preveja, a interface UI não terá foco em self-service/customização agora. |

---

## ✅ Atividade 03 — Requisito → Persona → Valor

Mapeamento da importância de cada funcionalidade para os envolvidos:

| Requisito | Persona impactada | Problema que resolve |
| :--- | :--- | :--- |
| **Autenticação com perfis distintos** | Todos | Garante que o estudante veja apenas sua trilha e o gestor veja apenas os dados de sua empresa. |
| **Envio de solução via link/upload** | Estudante | Resolve a dispersão de entregas por e-mail ou Forms, centralizando o histórico do aluno. |
| **Painel de pendências de avaliação** | Mentor | Resolve o problema de "perder entregas" e ajuda a manter o lead time de feedback baixo. |
| **Dashboard de KPIs consolidados** | Gestor | Substitui a análise manual de planilhas por uma visão em tempo real da saúde da turma. |
| **Snapshot de Performance (Perfil)** | Empresa Parceira | Resolve a dificuldade de identificar rapidamente quem são os "top performers" para contratação. |

---

### 📦 Resumo da Estratégia
O foco deste MVP é validar o **Ciclo de Feedback Funcional**. Se o estudante conseguir entregar, o mentor avaliar e o gestor visualizar o impacto disso em métricas reais dentro do Azure, o objetivo terá sido alcançado.

