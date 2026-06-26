# 1. O que é Git Flow e por que surgiu

## Origem

O Git Flow é um modelo de ramificação (branching model) proposto por **Vincent Driessen** em 2010, no artigo "A successful Git branching model". Ele surgiu para resolver um problema comum em equipes que adotavam Git: a falta de um padrão claro sobre **quando criar branches, para que servem e como integrá-las**.

Antes de modelos como esse, era comum cada desenvolvedor trabalhar do seu jeito, o que gerava históricos confusos, conflitos frequentes e dificuldade para saber o que estava pronto para produção.

## O problema que ele resolve

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
