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

## Resumo

No dia a dia, as branches transformam o desenvolvimento em algo organizado e paralelo. A disciplina de manter branches pequenas, atualizadas e bem nomeadas é o que faz o Git Flow funcionar de verdade em equipes reais.
