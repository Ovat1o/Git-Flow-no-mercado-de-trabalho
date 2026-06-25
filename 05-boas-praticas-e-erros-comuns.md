# 5. Boas práticas e erros comuns

Adotar o Git Flow não garante, sozinho, um repositório saudável. A qualidade vem de **bons hábitos** no dia a dia. Este tópico reúne as boas práticas mais valorizadas no mercado e os erros que mais aparecem nas equipes.

## Mensagens de commit: Conventional Commits

Mensagens de commit claras facilitam entender o histórico do projeto. O padrão mais usado é o **Conventional Commits**, com a estrutura:

```
tipo(escopo opcional): descrição

[corpo opcional]
```

### Principais tipos

| Tipo | Quando usar |
|------|-------------|
| `feat` | Nova funcionalidade |
| `fix` | Correção de bug |
| `docs` | Mudanças na documentação |
| `style` | Formatação, sem mudar lógica |
| `refactor` | Refatoração de código |
| `test` | Adição ou ajuste de testes |
| `chore` | Tarefas de manutenção (build, deps) |

### Exemplos

```bash
git commit -m "feat: adiciona autenticação via Google"
git commit -m "fix: corrige cálculo de frete no checkout"
git commit -m "docs: atualiza instruções de instalação no README"
```

Além de organizar o histórico, esse padrão permite **gerar changelogs automaticamente** e ajuda no versionamento.

## Versionamento semântico (SemVer)

O **Semantic Versioning** define versões no formato `MAJOR.MINOR.PATCH` (ex: `2.4.1`):

- **MAJOR** — mudanças incompatíveis com versões anteriores (quebram código existente).
- **MINOR** — novas funcionalidades compatíveis com o que já existe.
- **PATCH** — correções de bugs compatíveis.

Exemplo de evolução:
```
1.0.0  →  1.1.0  (nova feature)  →  1.1.1  (bugfix)  →  2.0.0  (mudança que quebra compatibilidade)
```

No Git Flow, cada `release` ou `hotfix` que vai para a `main` normalmente recebe uma nova tag de versão:

```bash
git tag -a v1.2.0 -m "Versão 1.2.0"
git push origin v1.2.0
```

## Boas práticas gerais

- **Commits pequenos e atômicos** — cada commit faz uma coisa só.
- **Commit com frequência**, mas só de código que funciona.
- **Nunca commitar segredos** (senhas, chaves de API) — use `.gitignore` e variáveis de ambiente.
- **Manter a `main` sempre estável** — só código testado entra nela.
- **Deletar branches** já mescladas para não poluir o repositório.
- **Escrever um bom README** explicando o projeto.

## Erros comuns

1. **Branches gigantes e de vida longa** — quanto mais tempo aberta, mais conflitos no merge.
2. **Mensagens de commit vagas** — "ajustes", "wip", "teste" não dizem nada sobre a mudança.
3. **Commitar arquivos que não deveriam ir** — `node_modules`, builds, arquivos de configuração local.
4. **`git push --force` na branch compartilhada** — pode apagar o trabalho dos colegas.
5. **Misturar várias mudanças não relacionadas** no mesmo commit ou PR.
6. **Ignorar o code review** — aprovar PRs sem ler de verdade.
7. **Não atualizar a branch** com a `develop`, acumulando divergências.

## Resumo

O Git Flow funciona bem quando acompanhado de disciplina: mensagens padronizadas (Conventional Commits), versionamento claro (SemVer), commits pequenos e atenção aos erros clássicos. São esses detalhes que separam um repositório amador de um profissional.
