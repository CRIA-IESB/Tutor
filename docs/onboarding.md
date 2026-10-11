# Onboarding — Tutor (CRIA/IESB)

Leia no primeiro dia (~15 min). As regras do projeto moram em três lugares, e só neles:

| Documento | Responde |
|---|---|
| este arquivo | como o time funciona: horas, rotina, combinados |
| [CONTRIBUTING.md](../CONTRIBUTING.md) | como o código entra na `main` |
| [arquitetura.md](arquitetura.md) | como o sistema é construído. **Obrigatório seguir; muda só por PR aprovado pelo líder.** |

## 1. O que é o Tutor

Chat de tutoria por disciplina: a IA responde **só** com base no material que o professor enviou, cita a fonte e, quando não há base, não inventa: encaminha a dúvida ao professor. Detalhes em [visão](visao.md), [perfis e permissões](rbac.md), [telas](sitemap.md) e [épicos](epicos/).

Três regras que não se negociam:

1. **Nenhuma LLM externa.** Os modelos rodam na nossa infraestrutura. Nada de API da OpenAI, Gemini, AWS Bedrock etc. no produto.
2. **Sem fonte, sem resposta.** Toda resposta cita trechos do material. Sem trecho que sustente, o sistema recusa e escala ao professor.
3. **Dado de aluno não sai.** Não vai para log, Git, print, issue, nem para ferramenta de IA externa (ChatGPT, Gemini, Copilot etc.). O código é público (GPL-3.0); os dados, nunca.

## 2. Primeiro dia

- [ ] Ler este arquivo, o CONTRIBUTING e a arquitetura
- [ ] Assinar o termo de compromisso (com o líder)
- [ ] Aceitar os convites: GitHub, Clockify e canal do time
- [ ] Instalar a extensão do Clockify no navegador: ela põe um botão de timer em cada issue do GitHub
- [ ] Subir o ambiente pelo [README](../README.md) e rodar `pip install pre-commit && pre-commit install`
- [ ] Pegar uma issue `good first issue` e abrir o primeiro PR

## 3. Horas e comprovação

- **Carga:** 4 h por dia útil, de segunda a sexta (20 h/semana). O horário dentro do dia é livre, fora as reuniões marcadas.
- **Registro:** tudo no Clockify, **no mesmo dia**, projeto `Tutor`. A descrição começa com o nº da issue: `#148 Matrícula de aluno em turma` (o botão do Clockify na issue já preenche). Reunião ou estudo sem issue: tag `reunião` ou `estudo` + o que foi feito.
- **Revisar PR de colega é trabalho:** registre com o nº da issue do PR.
- **Falta:** avise no canal e compense na mesma semana, registrando no Clockify.
- **Como se comprova:** o Clockify mostra *quanto* tempo; o GitHub mostra *o quê* (issues, commits, PRs, reviews). Toda segunda o líder confere a semana anterior: 4 h por dia útil e trabalho correspondente no GitHub. Todo mês, o relatório do Clockify (PDF) e o resumo do GitHub vão para a coordenação do CRIA.
- Hora sem issue ou PR correspondente não conta.

## 4. Rotina

- **Planejamento semanal** (30 min, dia e horário definidos pelo líder): revisa o quadro e distribui as issues.
- **Fim do dia, 1 mensagem no canal:** `Fiz #148, #150 · Amanhã #151 · Bloqueio: nenhum`.
- **Quadro** no GitHub Projects: Backlog → A fazer → Em andamento → Em revisão → Feito. No máximo 2 issues suas em andamento.
- Travou por mais de 1 hora? Pergunte no canal.

## 5. Dados, segurança e IA: nunca

- Usar dado real de aluno em dev ou teste. Use dados fictícios.
- Commitar `.env`, dumps, planilhas ou CSV. O pre-commit bloqueia; não contorne com `--no-verify`.
- Logar ou devolver ao cliente conteúdo de mensagem, e-mail, matrícula, token, senha ou `str(e)`.
- Colar dado de aluno, log de produção, `.env` ou segredo em ferramenta de IA externa.
- Adicionar dependência ou serviço que mande dado para fora (API de LLM, analytics, CDN de terceiros).
- Achou falha de segurança ou vazamento? **Fale com o líder em privado**, não abra issue pública.

## 6. Glossário

| Termo | Significado |
|---|---|
| RAG | a IA busca trechos do material e responde só a partir deles |
| Chunk | trecho de um material indexado, com a página ou o minuto de origem |
| Embedding | vetor numérico do chunk, usado na busca por semelhança (pgvector) |
| Escalonamento | a dúvida que a IA não consegue sustentar vai para o professor |
| Turma + matéria | o material é por turma e matéria; o aluno só vê as matérias da sua turma |

## 7. Contatos

| Papel | Quem | Contato |
|---|---|---|
| Líder técnico | Gabriel Henrique Kuhn Paz | _preencher_ |
| Coordenação do CRIA | _preencher_ | _preencher_ |
| Encarregado de dados (DPO) do IESB | _preencher_ | _preencher_ |
