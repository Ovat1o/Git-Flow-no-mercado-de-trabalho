# Git Flow no Mercado de Trabalho

Projeto acadêmico em grupo sobre o uso do **Git Flow** em ambientes profissionais de desenvolvimento de software.

## Tópicos:

Cada integrante do grupo contribuiu com um tópico, em um commit próprio:

1. [O que é Git Flow e por que surgiu](01-o-que-e-git-flow.md)
2. [Branches no dia a dia da empresa](02-branches-no-dia-a-dia.md)
3. [Pull Requests, Code Review e CI/CD](03-pull-requests-code-review-cicd.md)
4. [Git Flow vs. alternativas modernas](04-git-flow-vs-alternativas.md)
5. [Boas práticas e erros comuns](05-boas-praticas-e-erros-comuns.md)

## Integrantes:

| Integrante       | Tópico |
| ---------------- | ------ |
| Otavio Leão      | 1      |
| Tales Cavalcanti | 2      |
| Victor Julius    | 3      |
| Pedro Henrique   | 4      |
| Filipe Sousa     | 5      |

---

# 1. O que é Git Flow e por que surgiu?

## Origem:
O Git Flow é basicamente um manual de organização para equipes que criam software. Ele foi criado em 2010 por Vincent Driessen para resolver um problema prático: a bagunça na hora de juntar o trabalho de várias pessoas.

Antes dele, cada programador fazia as coisas do seu jeito. O resultado era dor de cabeça: o trabalho de um atropelava o do outro, e ninguém sabia ao certo o que estava realmente pronto para ser entregue ao cliente. O Git Flow surgiu para colocar ordem na casa, definindo regras claras de como separar e juntar as partes do projeto sem gerar caos.

## O problema que ele resolve:

O Git Flow organiza o desenvolvimento separando claramente:

- O que está **em produção** (estável).
- O que está **em desenvolvimento** (próxima versão).
- O que são **funcionalidades em andamento**.
- O que são **correções urgentes**.

Isso dá previsibilidade ao processo e facilita o trabalho de várias pessoas no mesmo projeto.

## Os tipos de branches

O modelo define cinco tipos de branches, divididos entre **permanentes** e **temporárias**.

### Branches permanentes

| Branch | Função |
|--------|--------|
| `main` (ou `master`) | Contém o código em produção. Cada commit aqui representa uma versão liberada. |
| `develop` | Reúne todo o trabalho concluído que entrará na próxima versão. É a base de integração. |

### Branches temporárias

| Branch | Origem | Volta para | Função |
|--------|--------|-----------|--------|
| `feature/*` | `develop` | `develop` | Desenvolvimento de novas funcionalidades. |
| `release/*` | `develop` | `develop` e `main` | Preparação de uma nova versão (ajustes finais, testes). |
| `hotfix/*` | `main` | `develop` e `main` | Correção urgente de um bug em produção. |

## Fluxo resumido

1. Uma nova funcionalidade nasce de `develop` em uma branch `feature/`.
2. Concluída, ela volta (merge) para `develop`.
3. Quando há funcionalidades suficientes, cria-se uma `release/` a partir de `develop`.
4. A release é testada, ajustada e enviada para `main` (vira uma versão oficial) e também de volta para `develop`.
5. Se um bug crítico aparece em produção, um `hotfix/` corrige direto a partir de `main`.

## Por que ainda é relevante

Mesmo com alternativas mais simples surgindo, o Git Flow continua sendo ensinado e usado porque oferece uma estrutura disciplinada — especialmente útil em projetos com **versões bem definidas, prazos de release e equipes maiores**.

---
# 2. Branches no dia a dia da empresa

Entender a teoria do Git Flow é uma coisa; ver como ela funciona na rotina de uma equipe é outra. Este tópico mostra como as branches são usadas na prática dentro de um time de desenvolvimento.

## O ciclo de uma feature

Imagine que um desenvolvedor recebeu a tarefa de criar uma tela de login. O caminho típico é:

```bash
# Parte da branch de desenvolvimento
git checkout develop
git pull origin develop

# Cria a branch da funcionalidade
git checkout -b feature/tela-de-login

# ... trabalha, faz commits ...
git add .
git commit -m "feat: adiciona formulário de login"

# Envia para o repositório remoto
git push origin feature/tela-de-login
```

Depois de concluída e revisada, a branch é integrada de volta à `develop` (geralmente via Pull Request) e então deletada.

## Trabalho em paralelo sem caos

A grande vantagem das branches é permitir que **várias pessoas trabalhem ao mesmo tempo** sem atrapalhar umas às outras:

- A Heloísa desenvolve `feature/cadastro-usuario`.
- O João desenvolve `feature/dashboard`.
- A Maria corrige `hotfix/erro-pagamento`.

Cada um tem seu ambiente isolado. O código só "se encontra" no momento do merge.

## Como times grandes evitam conflitos

Conflitos de merge acontecem quando duas pessoas alteram o mesmo trecho de código. Para reduzir isso, as equipes adotam práticas como:

- **Branches pequenas e de vida curta** — quanto mais tempo uma branch fica aberta, mais ela "diverge" da `develop` e maior a chance de conflito.
- **Atualizar a branch com frequência** — trazer as mudanças recentes da `develop` para a feature regularmente:

```bash
git checkout feature/minha-feature
git merge develop   # ou git rebase develop
```

- **Dividir tarefas grandes** em funcionalidades menores e independentes.
- **Comunicação clara** sobre quem está mexendo em quais arquivos.

## Nomeação de branches

Uma convenção de nomes consistente facilita a vida do time. Padrões comuns:

```
feature/nome-da-funcionalidade
bugfix/descricao-do-bug
hotfix/descricao-do-erro
release/1.2.0
```

Alguns times incluem o número do ticket: `feature/PROJ-123-tela-login`.

---

# 3. Pull Requests, Code Review e CiCd

## O Pull Request (PR)

Um bom PR costuma ter:

- Um **título claro** do que foi feito.
- Uma **descrição** explicando o porquê da mudança.
- **Referência ao ticket/issue** relacionado.
- Uma lista do que foi testado.

> No GitHub esse recurso se chama *Pull Request*; no GitLab, *Merge Request*. A ideia é a mesma.

## Code Review

Antes de o PR ser aprovado, outros desenvolvedores **revisam o código**. O objetivo não é só achar bugs, mas também:

- Garantir que o código segue os padrões do time.
- Identificar problemas de performance ou segurança.
- Compartilhar conhecimento (quem revisa aprende sobre aquela parte do sistema).
- Manter a qualidade e a legibilidade.

### Boas práticas de revisão

- Comentários devem ser **construtivos**, focados no código e não na pessoa.
- PRs **pequenos** são revisados melhor e mais rápido que PRs gigantes.
- O autor responde aos comentários e faz ajustes até a aprovação.

## CI/CD

**CI/CD** significa *Continuous Integration* (Integração Contínua) e *Continuous Delivery/Deployment* (Entrega/Implantação Contínua). São pipelines automatizados que rodam a cada PR ou merge.

### Continuous Integration (CI)

Quando alguém abre um PR, o sistema automaticamente:

1. **Roda os testes** automatizados.
2. **Faz o build** da aplicação.
3. **Verifica o estilo do código** (linting).
4. Reporta se algo quebrou.

Assim, o time descobre problemas **antes** do merge, não depois.

### Continuous Delivery/Deployment (CD)

Depois que o código é aprovado e integrado, o pipeline pode:

- Fazer **deploy automático** para um ambiente de testes (staging).
- Em casos mais maduros, fazer deploy direto para produção.

## Como tudo se conecta ao Git Flow

```
feature/login  ──>  Pull Request  ──>  Code Review  ──>  CI (testes/build)
                                                              │
                                                              ▼
                                                   merge na develop  ──>  CD (deploy staging)
```

Ferramentas comuns nesse processo: **GitHub Actions**, **GitLab CI**, **Jenkins**, **CircleCI**.

---
## 4. Git Flow vs. Alternativas Modernas

O **Git Flow** foi um divisor de águas quando surgiu, padronizando o desenvolvimento de software com regras estritas e múltiplas branches (`main`, `develop`, `feature`, `release`, `hotfix`). No entanto, a complexidade desse modelo fez com que muitas equipes migrassem para abordagens mais enxutas, especialmente com a ascensão das práticas de CI/CD (Integração e Entrega Contínuas).

Abaixo, comparamos o Git Flow com as duas principais alternativas modernas do mercado.

---

## 1. GitHub Flow
Criado pelo próprio GitHub, é uma alternativa minimalista e focada em entregas rápidas e contínuas.

*   **Como funciona:** Existe apenas uma branch principal (`main`), que deve estar sempre pronta para produção. Novas funcionalidades ou correções são feitas em branches derivadas diretamente da `main`. Quando prontas, abre-se um Pull Request (PR) para revisão, e após aprovação, o código é mesclado de volta à `main` e implantado imediatamente.
*   **Vantagens:** Simplicidade extrema. Elimina a necessidade de branches de `release` ou `develop`, acelerando o ciclo de feedback.
*   **Quando usar:** Ideal para aplicações web, SaaS (Software as a Service) e projetos onde a entrega contínua é possível (vários deploys por dia).

## 2. Trunk-Based Development (TBD)
Adotado por gigantes da tecnologia, o TBD leva a integração contínua ao extremo, focando em manter todo o time trabalhando em um único "tronco" de código.

*   **Como funciona:** Os desenvolvedores fazem commits diretamente na branch principal (`main` ou `trunk`) várias vezes ao dia, ou utilizam *feature branches* de curtíssima duração (no máximo dois dias). Para evitar que código incompleto vá para produção, utiliza-se a técnica de **Feature Flags** (chaves que ativam ou desativam funcionalidades no código).
*   **Vantagens:** Evita o temido "Merge Hell" (conflitos gigantes ao tentar unir branches muito longas) e força a equipe a escrever testes automatizados robustos e integrar o código constantemente.
*   **Quando usar:** Empresas com alta maturidade em DevOps e automação de testes, e times que precisam de altíssima velocidade de iteração sem quebrar a produção.

---

## Resumo: Qual modelo escolher?

| Modelo | Foco Principal | Melhor Cenário de Uso |
| :--- | :--- | :--- |
| **Git Flow** | Controle rigoroso e versões isoladas | Softwares com versões marcadas (ex: apps mobile, jogos, sistemas embarcados) e janelas de deploy programadas. |
| **GitHub Flow** | Simplicidade e Deploy Contínuo | Aplicações Web, APIs e sistemas onde é fácil fazer *rollback* (desfazer) rapidamente em caso de erro. |
| **Trunk-Based** | Velocidade extrema e CI/CD avançado | Times de alta performance, arquiteturas de microserviços e empresas maduras em cultura DevOps. |

Embora o Git Flow continue sendo uma excelente ferramenta didática e organizacional para projetos que exigem controle estrito de versões, a tendência atual do mercado de desenvolvimento web e serviços em nuvem caminha para a agilidade do GitHub Flow e do Trunk-Based Development.

---

# 5. Boas práticas e erros comuns

Adotar o Git Flow não garante, sozinho, um repositório saudável. A qualidade vem de bons hábitos no dia a dia. Este tópico reúne as boas práticas mais valorizadas no mercado e os erros que mais aparecem nas equipes.
Mensagens de commit: Conventional Commits
Mensagens de commit claras facilitam entender o histórico do projeto. O padrão mais usado é o Conventional Commits, com a estrutura:

```
tipo(escopo opcional): descrição

[corpo opcional]
```

Principais tipos e quando usar

- `feat` Nova funcionalidade
- `fix` Correção de bug
- `docs` Mudanças na documentação
- `style` Formatação, sem mudar lógica
- `refactor` Refatoração de código
- `test` Adição ou ajuste de testes
- `chore` Tarefas de manutenção (build, deps)

Exemplos

```bash
git commit -m "feat: adiciona autenticação via Google"
git commit -m "fix: corrige cálculo de frete no checkout"
git commit -m "docs: atualiza instruções de instalação no README"
```

Além de organizar o histórico, esse padrão permite gerar changelogs automaticamente e ajuda no versionamento.
Versionamento semântico (SemVer)
O Semantic Versioning define versões no formato `MAJOR.MINOR.PATCH` (ex: `2.4.1`):

`MAJOR` - mudanças incompatíveis com versões anteriores (quebram código existente).

`MINORP` - novas funcionalidades compatíveis com o que já existe.

`PATCH` correções de bugs compatíveis.
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

## Boas práticas gerais

- **Commits pequenos e atômicos**: cada commit deve realizar apenas uma mudança.
- **Commit com frequência**, mas apenas de código que esteja funcionando.
- **Nunca commite segredos** (senhas, tokens ou chaves de API). Utilize `.gitignore` e variáveis de ambiente.
- **Mantenha a branch `main` sempre estável**: somente código testado deve ser mesclado nela.
- **Remova branches já mescladas** para evitar poluição no repositório.
- **Escreva um bom README** explicando o propósito, configuração e uso do projeto.

## Erros comuns

- **Branches muito grandes ou de longa duração**: aumentam a chance de conflitos durante o merge.
- **Mensagens de commit vagas**: termos como `ajustes`, `wip` ou `teste` não descrevem claramente a alteração realizada.
- **Commitar arquivos desnecessários**: evite incluir `node_modules`, arquivos de build ou configurações locais.
- **Usar `git push --force` em branches compartilhadas**: pode sobrescrever e apagar o trabalho de outras pessoas.
- **Misturar mudanças não relacionadas** em um mesmo commit ou Pull Request.
- **Ignorar o code review**: aprovar PRs sem uma análise adequada compromete a qualidade do código.
- **Não sincronizar a branch com a `develop`** regularmente, acumulando divergências e conflitos.
