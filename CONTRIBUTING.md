# Como contribuir com o Tutor

Regras curtas, valem para todo mundo (inclusive o líder). Se uma regra atrapalha mais do que ajuda, abra um PR mudando a regra — não contorne.

## Fluxo: issue → branch → PR → merge

1. **Toda tarefa é uma issue** (template *Tarefa*, com etiqueta de estimativa). Sem issue, sem código e sem hora no Clockify.
2. **Branch a partir da `main`:** `tipo/nº-descricao-curta`, ex.: `feat/148-matricula-aluno`.
3. **Commits pequenos.** O pre-commit roda a cada commit e corrige ou barra o que estiver fora do padrão.
4. **PR cedo** (rascunho vale). Título em Conventional Commits, corpo com `Closes #nº`.
5. **Merge com CI verde + 1 aprovação**, sempre *Squash and merge*. Caminhos críticos (`.github/CODEOWNERS`) pedem o líder.

Ninguém dá push direto na `main`. A branch `develop` não é mais usada.

## Título do PR

`tipo(escopo): descrição no imperativo`, com tipo `feat`, `fix`, `refactor`, `test`, `docs`, `chore`, `ci` ou `perf`.
Ex.: `fix(usuarios): exige login em /usuarios/buscar`. O histórico já segue esse padrão; agora a CI confere.

## Pronto é quando

- [ ] CI verde e 1 aprovação
- [ ] Regra de negócio nova ou alterada tem teste
- [ ] Segue a [arquitetura](docs/arquitetura.md)
- [ ] Nenhum dado pessoal em log, teste, print ou commit
- [ ] Doc atualizado se mudou comportamento, rota ou variável de ambiente

## Padrão de código

Estilo não se discute em review: as ferramentas decidem.

| O quê | Ferramenta | Config |
|---|---|---|
| Python (backend) | ruff: lint + formatação | `backend/ruff.toml` |
| TypeScript/CSS (frontend) | Biome: lint + formatação | `biome.json` |
| Camadas do backend | import-linter | `backend/.importlinter` |

**Backend**
- Camadas: `routes/` e `socket/` (entrada) → `services/` (regra de negócio e acesso a dados) → `models/`. Rota e socket não importam model nem `db`: chamam um service. A CI barra import novo fora disso.
- Nomes como já existem: `route_*.py`, `service_*.py`, `model_*.py`; funções e variáveis em `snake_case`, em português.
- Toda rota nasce com `@token_obrigatorio` e o decorator de papel (`@apenas_admins`, `@apenas_professores`, `@apenas_alunos`). Rota pública só com justificativa no PR.
- Nunca devolva `str(e)` ao cliente nem logue conteúdo de mensagem, e-mail, matrícula, token ou senha.

**Frontend**
- Páginas em `app/(pages)/<área>/`; componente em `components/<Nome>/<Nome>.tsx` + `<Nome>.module.css` (CSS Modules; Tailwind não está ativo).
- Chamada HTTP só em `app/services/service_*.ts`, pelo `api.ts`. Componente não usa `fetch`/axios direto.
- Estado com React Context + `useState`. Lib nova de estado só com decisão na arquitetura.

**Dependência nova** (pip ou npm): justifique no PR. Nada que mande dado de aluno para serviço externo.

## Ambiente

Suba o projeto pelo [README](README.md). Depois, uma vez por máquina:

```bash
pip install pre-commit && pre-commit install
```

A partir daí o `git commit` já roda os hooks. Rodar em tudo: `pre-commit run --all-files`. O hook do frontend usa `npx` (precisa de Node instalado).

## O que a CI confere em todo PR

| Check | O que faz | Bloqueia merge? |
|---|---|---|
| `padrao` | pre-commit nos arquivos alterados: ruff, Biome e bloqueio de dados, `.env` e chave privada | sim |
| `backend` | camadas (import-linter) | sim |
| `frontend` | `npm run build`, que inclui a checagem de tipos | sim |
| `pr` | título em Conventional Commits + `Closes #nº` | sim |
| Security Pipeline | CodeQL, Semgrep, Sonar etc. | ainda não (ver `docs/checklist-implantacao.md`) |

O padrão vale para os **arquivos que você alterou**: tocou num arquivo antigo, deixe-o no padrão. Assim o legado converge sem um PR gigante.

Depois do merge na `main`, o job `deploy-alpha` atualiza o ambiente alpha sozinho (fica inativo até o servidor existir).
