# Git Flow no Mercado de Trabalho

Projeto acadêmico em grupo sobre o uso do **Git Flow** em ambientes profissionais de desenvolvimento de software.

## Tópicos

Cada integrante do grupo contribuiu com um tópico, em um commit próprio:

1. [O que é Git Flow e por que surgiu](01-o-que-e-git-flow.md)
2. [Branches no dia a dia da empresa](02-branches-no-dia-a-dia.md)
3. [Pull Requests, Code Review e CI/CD](03-pull-requests-code-review-cicd.md)
4. [Git Flow vs. alternativas modernas](04-git-flow-vs-alternativas.md)
5. [Boas práticas e erros comuns](05-boas-praticas-e-erros-comuns.md)

## Integrantes

| Integrante       | Tópico |
| ---------------- | ------ |
| Otávio Leão      | 1      |
| Tales Cavalcanti | 2      |
| Victor Julius    | 3      |
| Pedro Henrique   | 4      |
| Filipe Sousa     | 5      |

---

# 1. O que é Git Flow e por que surgiu?

## Origem
O Git Flow é basicamente um manual de organização para equipes que criam software. Ele foi criado em 2010 por Vincent Driessen para resolver um problema prático: a bagunça na hora de juntar o trabalho de várias pessoas.

Antes dele, cada programador fazia as coisas do seu jeito. O resultado era dor de cabeça: o trabalho de um atropelava o do outro, e ninguém sabia ao certo o que estava realmente pronto para ser entregue ao cliente. O Git Flow surgiu para colocar ordem na casa, definindo regras claras de como separar e juntar as partes do projeto sem gerar caos.

## O problema que ele resolve

O Git Flow organiza o desenvolvimento separando claramente:

- O que está **em produção** (estável).
- O que está **em desenvolvimento** (próxima versão).
- O que são **funcionalidades em andamento**.
- O que são **correções urgentes**.

Isso dá previsibilidade ao processo e facilita o trabalho de várias pessoas no mesmo projeto.

---

# 5. Boas práticas e erros comuns

Adotar o Git Flow não garante, sozinho, um repositório saudável. A qualidade vem de bons hábitos no dia a dia. Este tópico reúne as boas práticas mais valorizadas no mercado e os erros que mais aparecem nas equipes.
Mensagens de commit: Conventional Commits
Mensagens de commit claras facilitam entender o histórico do projeto. O padrão mais usado é o Conventional Commits, com a estrutura:

```
tipo(escopo opcional): descrição

[corpo opcional]
```

Principais tipos
Tipo Quando usar
`feat` Nova funcionalidade
`fix` Correção de bug
`docs` Mudanças na documentação
`style` Formatação, sem mudar lógica
`refactor` Refatoração de código
`test` Adição ou ajuste de testes
`chore` Tarefas de manutenção (build, deps)
Exemplos

```bash
git commit -m "feat: adiciona autenticação via Google"
git commit -m "fix: corrige cálculo de frete no checkout"
git commit -m "docs: atualiza instruções de instalação no README"
```

Além de organizar o histórico, esse padrão permite gerar changelogs automaticamente e ajuda no versionamento.
Versionamento semântico (SemVer)
O Semantic Versioning define versões no formato `MAJOR.MINOR.PATCH` (ex: `2.4.1`):
MAJOR — mudanças incompatíveis com versões anteriores (quebram código existente).
MINOR — novas funcionalidades compatíveis com o que já existe.
PATCH — correções de bugs compatíveis.
Exemplo de evolução:

```
1.0.0  →  1.1.0  (nova feature)  →  1.1.1  (bugfix)  →  2.0.0  (mudança que quebra compatibilidade)
```

No Git Flow, cada `release` ou `hotfix` que vai para a `main` normalmente recebe uma nova tag de versão:

```bash
git tag -a v1.2.0 -m "Versão 1.2.0"
git push origin v1.2.0
```

---

### ✅ Boas práticas gerais

- **Commits pequenos e atômicos**: cada commit deve realizar apenas uma mudança.
- **Commit com frequência**, mas apenas de código que esteja funcionando.
- **Nunca commite segredos** (senhas, tokens ou chaves de API). Utilize `.gitignore` e variáveis de ambiente.
- **Mantenha a branch `main` sempre estável**: somente código testado deve ser mesclado nela.
- **Remova branches já mescladas** para evitar poluição no repositório.
- **Escreva um bom README** explicando o propósito, configuração e uso do projeto.

### ❌ Erros comuns

- **Branches muito grandes ou de longa duração**: aumentam a chance de conflitos durante o merge.
- **Mensagens de commit vagas**: termos como `ajustes`, `wip` ou `teste` não descrevem claramente a alteração realizada.
- **Commitar arquivos desnecessários**: evite incluir `node_modules`, arquivos de build ou configurações locais.
- **Usar `git push --force` em branches compartilhadas**: pode sobrescrever e apagar o trabalho de outras pessoas.
- **Misturar mudanças não relacionadas** em um mesmo commit ou Pull Request.
- **Ignorar o code review**: aprovar PRs sem uma análise adequada compromete a qualidade do código.
- **Não sincronizar a branch com a `develop`** regularmente, acumulando divergências e conflitos.

## 📌 Resumo

O **Git Flow** funciona melhor quando acompanhado de disciplina e boas práticas:

- Utilização de **Conventional Commits** para padronização das mensagens.
- Adoção de **SemVer (Versionamento Semântico)** para controle de versões.
- Criação de **commits pequenos e bem definidos**.
- Atenção aos erros mais comuns do fluxo de trabalho.

São esses detalhes que diferenciam um repositório amador de um repositório profissional.
