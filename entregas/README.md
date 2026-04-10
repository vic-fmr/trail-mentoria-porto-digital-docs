# Guia de Entregas dos Alunos (`/entregas`)

Bem-vindo(a)! Esta pasta é o local onde cada aluno deve enviar seus arquivos de entrega.

## 1) Onde entregar

- Use **apenas a sua própria pasta** dentro de `/entregas`.
- Padrão da pasta: `nome-sobrenome` (minúsculo e separado por hífen).
- Exemplo: `/entregas/joao-silva/`.

> Se sua pasta ainda não existir, fale com o mentor antes de criar uma nova.

## 2) O que entregar

Dentro da sua pasta, organize os materiais por encontro ou tema:

- `encontro-03.md`
- `encontro-04.md`
- `mvp.md`
- `links.md`
- `evidencias/` (opcional: prints, diagramas, etc.)

Use nomes de arquivos claros e objetivos. O ideal é manter um tema/entrega por arquivo.

## 3) Checklist básico de qualidade

Antes de enviar, verifique:

- [ ] O conteúdo está na pasta correta do aluno.
- [ ] Os arquivos estão claros e legíveis (formato Markdown).
- [ ] A entrega referencia a atividade/encontro solicitado.
- [ ] Decisões e premissas estão explicadas.
- [ ] Links e referências estão funcionando.

## 4) Regras de contribuição

- **Não** altere arquivos fora de `/entregas/**`.
- **Não** edite a pasta de outro aluno.
- Faça commits objetivos e descritivos.

## 5) Formato recomendado para mensagem de commit

Use mensagens curtas e claras, como:

- `docs(entregas): adiciona entrega do encontro 03`
- `docs(entregas): atualiza rascunho do MVP`

## 6) Recursos do repositório que você deve usar

Use as pastas abaixo como apoio de estudo e execução das entregas:

- `README.md` → contexto geral do projeto.
- `encontros/` → temas dos encontros e resultados esperados.
- `atividades/` → atividades e desafios técnicos.
- `regras/` → governança, colaboração e uso do repositório.
- `referencias/` → arquitetura, boas práticas e links úteis.
- `discovery/` → contexto de discovery e definição de problema.
- `feedbacks/` → feedbacks de ciclos e melhorias.

## 7) Dicas para uma boa entrega

- Comece pelo arquivo do encontro correspondente em `encontros/`.
- Cruze as orientações com `atividades/` e `regras/` antes de enviar.
- Inclua referências de `referencias/links-uteis.md` quando fizer sentido.
- Escreva de forma objetiva: problema, abordagem, resultado e próximos passos.

## 8) Fluxo oficial de envio (Fork + Pull Request)

Para este repositório, o fluxo padrão dos alunos é via **fork**. Isso evita erro de permissão (`403`) no push.

### Passo a passo

1. Faça um **fork** deste repositório para sua conta do GitHub.
2. No seu fork, crie uma branch (ex.: `docs/minha-entrega-encontro-03`).
3. Edite **somente** arquivos dentro da sua pasta em `/entregas/`.
4. Faça commit e push para o **seu fork**.
5. Abra um **Pull Request** do seu fork para a `main` do repositório principal.
6. Aguarde revisão/validação do mentor.

### Regra de ouro

- Se o push estiver apontando para o repositório principal, você pode receber `403`.
- O push do aluno deve ir para o **fork** (repositório da conta do aluno).

### Nome sugerido de branch

- `docs/entrega-encontro-03-seu-nome`
- `docs/entrega-mvp-seu-nome`

### Antes de abrir o PR

- [ ] Alterei apenas minha pasta em `/entregas/`
- [ ] Não alterei arquivos de `encontros/`, `regras/`, `referencias/` etc.
- [ ] Título e descrição do PR estão claros
- [ ] O PR mostra somente os arquivos esperados

---

Se tiver dúvida sobre onde colocar um arquivo, pergunte antes de subir. É melhor alinhar cedo do que corrigir estrutura depois. 🚀
