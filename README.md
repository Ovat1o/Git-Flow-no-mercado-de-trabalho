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
| _(nome)_         | 1      |
| Tales Cavalcanti | 2      |
| _(nome)_         | 3      |
| Pedro Henrique   | 4      |
| Filipe Sousa     | 5      |

## Como o repositório pratica o próprio tema

---

## 5. Boas práticas e erros comuns

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

# Boas Práticas Gerais

✅ **Commits pequenos e atômicos**

- Cada commit deve realizar apenas uma mudança específica.

✅ **Commitar com frequência**

- Faça commits regulares, mas somente de código que esteja funcionando.

✅ **Nunca commitar segredos**

- Senhas, tokens e chaves de API devem ficar fora do repositório.
- Utilize `.gitignore` e variáveis de ambiente.

✅ **Manter a `main` sempre estável**

- Apenas código testado e validado deve ser integrado.

✅ **Remover branches já mescladas**

- Evita poluição visual e facilita a manutenção do repositório.

✅ **Escrever um bom README**

- Documente o objetivo, instalação, uso e principais características do projeto.

---

### Erros Comuns

❌ **Branches muito grandes e de longa duração**

- Quanto mais tempo uma branch permanece aberta, maiores são as chances de conflitos no merge.

❌ **Mensagens de commit vagas**

- Evite mensagens como:
  - `ajustes`
  - `wip`
  - `teste`
- Prefira descrições claras e objetivas.

❌ **Commitar arquivos desnecessários**

- Exemplos:
  - `node_modules`
  - arquivos de build
  - configurações locais da máquina

❌ **Usar `git push --force` em branches compartilhadas**

- Pode sobrescrever ou apagar o trabalho de outros colaboradores.

❌ **Misturar mudanças não relacionadas**

- Evite incluir várias funcionalidades ou correções diferentes no mesmo commit ou PR.

❌ **Ignorar o Code Review**

- Não aprove Pull Requests sem revisar cuidadosamente as alterações.

❌ **Não sincronizar com a `develop`**

- Deixar de atualizar a branch frequentemente aumenta divergências e conflitos.

---

## Resumo

O **Git Flow** funciona melhor quando combinado com:

- 📝 Mensagens padronizadas (**Conventional Commits**)
- 🔖 Versionamento consistente (**SemVer**)
- 🔄 Commits pequenos e frequentes
- 👀 Revisão cuidadosa de código
- 🌱 Boa gestão de branches
