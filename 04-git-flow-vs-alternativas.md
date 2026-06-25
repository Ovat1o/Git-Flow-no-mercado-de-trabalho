# Git Flow vs. Alternativas Modernas

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
