# 3. Pull Requests, Code Review e CI/CD

No mercado de trabalho, raramente alguém envia código direto para a `develop` ou `main`. O caminho passa por **Pull Requests**, **revisão de código** e **pipelines automatizados**. Essas três práticas são o que transformam o Git Flow em um processo confiável.

## O Pull Request (PR)

Um Pull Request é um pedido para integrar o código de uma branch em outra (por exemplo, de `feature/login` para `develop`). Ele não é só um "botão de merge" — é um espaço de **discussão e validação**.

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
