# Checklist de implantação no CRIA

Dono: líder técnico. Marque por PR ou copie para uma issue fixada. Itens marcados já estão neste repositório.

## 1. Comprovação de horas

- [x] Modelo do [termo de compromisso](termo-de-compromisso.md)
- [x] Regras de registro e conferência no [onboarding](onboarding.md#3-horas-e-comprovação)
- [ ] Validar o termo com a coordenação do CRIA (o tipo de vínculo — bolsa, estágio, voluntariado — pode mudar as cláusulas)
- [ ] Escolher o plano do Clockify. O Free vai só até 5 usuários; acima disso, Basic (US$ 3,99/usuário/mês no anual) ou Standard (US$ 5,49, com aprovação e trava de timesheet). Preços de out/2026
- [ ] Criar o workspace "CRIA – Tutor": projeto `Tutor`, tags `reunião` e `estudo`; convidar o time
- [ ] Coletar os termos assinados (físico ou assinatura eletrônica, ex.: gov.br)
- [ ] Rotina do líder: conferência toda segunda e relatório mensal à coordenação (PDF do Clockify + resumo do GitHub)

## 2. Estrutura de comprovação de trabalho

- [x] Templates de issue (tarefa, bug) e de PR
- [x] Check `pr`: todo PR cita a issue (`Closes #nº`), ligando código, issue e horas
- [ ] Criar o quadro no GitHub Projects: Backlog → A fazer → Em andamento → Em revisão → Feito
- [ ] Combinar no canal a mensagem de fim do dia (1 linha)

## 3. Padronização do código

- [x] `CONTRIBUTING.md`: fluxo, título de PR, definição de pronto, padrões
- [x] pre-commit: ruff, Biome e bloqueio de arquivos de dados, `.env` e chave privada
- [x] CI: `ci.yml` (checks `padrao`, `backend`, `frontend`) e `pr.yml` (check `pr`)
- [x] Camadas do backend verificadas pelo import-linter (16 violações antigas listadas como dívida)
- [x] `backend/data/` (uploads locais) no `.gitignore`
- [ ] Levar o repositório para a org do CRIA (transferir ou fork) e dar acesso ao time
- [ ] Branch protection na `main`: exigir PR, 1 aprovação, checks `padrao`, `backend`, `frontend` e `pr`, review de Code Owners; bloquear force-push
- [ ] Ativar secret scanning e push protection (grátis em repositório público)
- [ ] Trocar `@gblzera` no `CODEOWNERS` por um time com 2 ou mais líderes
- [ ] Desativar o `ci-cd.yml` (faz deploy no EKS da AWS do Bayarea) até existir o ambiente do CRIA
- [ ] `security.yml` está vermelho desde jul/2026 (Semgrep e SonarCloud da org fabrica-bayarea): corrigir os achados ou rodar só semanalmente
- [ ] Corrigir os 8 testes que falham na `main` e adicionar o pytest como passo obrigatório do job `backend`
- [ ] Arquivar a branch `develop` (tem 1 commit fora da `main`, "Configurando kubernetes": revisar antes)
- [ ] Opcional: formatar o legado de uma vez num PR só de formatação, registrado em `.git-blame-ignore-revs`

## 4. Arquitetura

- [x] [arquitetura.md](arquitetura.md) (proposta v1)
- [ ] Aprovar com a coordenação do CRIA e mudar o status para "vigente"
- [ ] TI do IESB: GPU para produção e quem opera, integração com dados acadêmicos (consulta), login institucional, SMTP
- [ ] Encarregado (DPO) do IESB: RIPD, retenção das conversas, base legal
- [ ] Orçamento: GPU na nuvem do alpha/beta, plano do Clockify, bases licenciadas (só com cláusula de uso por IA)

## P0: antes de qualquer aluno real usar

- [ ] Tirar o AWS Bedrock do chat (D-01)
- [ ] Autenticar o socket do chat
- [ ] Fechar `GET /alunos/buscar` e `GET /mensagens/chat/<id>` e reativar os papéis em `route_vinculos.py`
- [ ] Trocar o `os.system` do ffmpeg por `subprocess` sem shell
- [ ] Contrato de resposta (arquitetura, seção 3) implementado e passando no eval
