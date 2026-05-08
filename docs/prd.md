# Calculadora Grêmio Product Requirements Document (PRD)

**Documento:** Product Requirements Document
**Versão:** 1.0
**Data:** 2026-05-08
**Autor:** Morgan (PM) — orquestração AIOX
**Status:** Draft — pronto para handoff a `@sm`
**Fonte primária:** `docs/project-brief.md` v1.1

---

## Goals and Background Context

### Goals

- Entregar uma calculadora web client-side com identidade visual marcante do Grêmio Foot-Ball Porto Alegrense, executável por duplo-clique em `index.html`
- Suportar as 4 operações aritméticas básicas (+, −, ×, ÷) com encadeamento ativo de operações (`2+3+5=` retorna `10`)
- Funcionar 100% offline em protocolo `file://`, sem dependências externas, sem build step e sem backend
- Aplicar a identidade Grêmio de forma dominante (listras tradicionais azul/preto/azul + cores oficiais `#0099CC`, `#000000`, `#FFFFFF`)
- Garantir responsividade entre `>=320px` (mobile) e `>=1024px` (desktop) nos navegadores Chrome, Edge e Firefox (3 últimas versões)
- Validar end-to-end o fluxo Story Development Cycle (SDC) do AIOX em um caso greenfield de baixa complexidade (meta-projeto)

### Background Context

A Calculadora Grêmio responde a duas demandas simultâneas: (1) torcedores que querem uma ferramenta utilitária do dia a dia com a identidade visual do clube, sem instalar aplicativos ou depender de serviços online; e (2) a necessidade interna da equipe de validar o orquestrador AIOX em um cenário real de baixa complexidade antes de aplicá-lo a projetos críticos. O produto entrega valor de produto (calculadora temática offline) e valor de processo (caso de teste do SDC) na mesma execução.

A solução é um único arquivo `index.html` com HTML5/CSS3/JavaScript vanilla, sem frameworks ou CDNs. As alternativas existentes (calculadora do SO, Google) não oferecem personalização visual, e calculadoras temáticas online exigem conexão. O escopo é deliberadamente mínimo — operações aritméticas básicas com encadeamento — para que a entrega caiba em uma sessão de trabalho e o foco fique na qualidade da identidade visual e na correção do fluxo SDC.

### Change Log

| Date       | Version | Description                                                                                              | Author |
|------------|---------|----------------------------------------------------------------------------------------------------------|--------|
| 2026-05-08 | 1.0     | Versão inicial do PRD derivada do Project Brief v1.1. Logo referenciada como `gremio-logo.png` (renomeada). | Morgan (PM) |

---

## Requirements

### Functional

- **FR1:** A calculadora deve exibir um display numérico que mostra o valor em digitação ou o resultado da operação corrente, atualizado em tempo real a cada interação do usuário. (Origem: brief FR-1)
- **FR2:** A calculadora deve oferecer botões clicáveis para os dígitos 0 a 9, permitindo a inserção de operandos numéricos. (Origem: brief FR-2)
- **FR3:** A calculadora deve oferecer botões para as quatro operações aritméticas básicas: soma (+), subtração (−), multiplicação (×) e divisão (÷). (Origem: brief FR-3)
- **FR4:** O botão Igual (=) deve executar o cálculo da operação corrente e exibir o resultado no display. A calculadora deve suportar **encadeamento ativo de operações**: ao pressionar um operador após uma operação pendente, o sistema resolve a operação anterior e usa o resultado como operando da próxima. Avaliação da esquerda para a direita, **sem precedência de operadores**. Exemplo canônico: `2 + 3 + 5 =` deve retornar `10` (resolve `2+3=5`, depois `5+5=10`). (Origem: brief FR-4 + Decisão Confirmada #1)
- **FR5:** O botão Clear (C) deve resetar o display e o estado interno da calculadora ao valor zero. (Origem: brief FR-5)
- **FR6:** A calculadora deve aceitar entrada de números fracionários através de um botão de vírgula decimal (`,`), seguindo a convenção pt-BR. (Origem: brief FR-6)
- **FR7:** A logo oficial do Grêmio Foot-Ball Porto Alegrense deve ser exibida no topo da interface, centralizada e em container full-width, referenciando o arquivo `gremio-logo.png` na raiz do projeto via `<img src="gremio-logo.png" alt="Grêmio Foot-Ball Porto Alegrense">`. Dimensionamento sugerido: altura 80–120px em desktop, 60–80px em mobile. (Origem: brief FR-7 + Decisão Confirmada #4 + atualização do sponsor: arquivo renomeado de `gremio-logo.png.png` para `gremio-logo.png`)
- **FR8:** A operação de divisão por zero deve exibir o texto literal `"Erro"` no display, em vez de retornar `Infinity`, `NaN` ou crashar a aplicação. O estado da calculadora deve permanecer estável após a exibição do erro, permitindo que o usuário pressione Clear para retomar uso normal. (Origem: brief Decisão Confirmada #2)

### Non Functional

- **NFR1:** O stack tecnológico está restrito a HTML5, CSS3 e JavaScript vanilla. É **proibido** o uso de frameworks (React, Vue, Angular, Svelte), bibliotecas externas (jQuery, Lodash, etc.), CDNs e build steps (Webpack, Vite, Parcel, Rollup). (Origem: brief NFR-1 + CON-1, CON-2)
- **NFR2:** A aplicação deve abrir e funcionar corretamente ao se executar duplo-clique no arquivo `index.html`, operando sob protocolo `file://`. Não deve haver dependência de servidor HTTP, processo Node ou ferramenta de build em runtime. (Origem: brief NFR-2 + CON-3)
- **NFR3:** A identidade visual do Grêmio deve ser aplicada de forma **forte e marcante**, não como acento sutil. Requisitos obrigatórios:
  1. **Listras tradicionais do clube** (alternância vertical clássica azul/preto/azul) presentes em pelo menos um destes locais: fundo do container principal da calculadora, header/faixa atrás ou abaixo da logo, ou bordas/molduras dos elementos.
  2. **Botões com forte presença das 3 cores oficiais** (`#0099CC` azul celeste, `#000000` preto, `#FFFFFF` branco):
     - Botões numéricos: paleta com as 3 cores (sugestão: fundo preto, texto branco)
     - Botões de operadores (+, −, ×, ÷): destaque em azul celeste `#0099CC` com texto branco
     - Botão Igual (=): combinação contrastante (ex: branco com borda azul, ou preto com texto branco)
     - Botão Clear (C): cor distintiva indicando reset (ex: branco com texto azul)
  3. **Tipografia:** sans-serif legível, com peso adequado para identidade esportiva (medium/bold em títulos).
  4. **Proibido:** fundo neutro genérico (cinza claro, off-white, etc.). A identidade do clube deve ser dominante na interface. (Origem: brief NFR-3 + CON-4 + Decisão Confirmada #5)
- **NFR4:** O layout deve ser responsivo, funcionando sem quebras visuais ou de usabilidade em viewports de `>=320px` (mobile) até `>=1024px` (desktop). (Origem: brief NFR-4 + OBJ-4)
- **NFR5:** A aplicação deve ser compatível com as 3 últimas versões estáveis dos navegadores Chrome, Edge e Firefox. (Origem: brief NFR-5 + OBJ-1)
- **NFR6:** O código deve ser limpo e auto-documentado, com comentários em pontos não-óbvios suficientes para revisão por humano ou agente AIOX. (Origem: brief NFR-6)
- **NFR7:** Suporte a teclado físico está **explicitamente fora do escopo do MVP**. A interação deve ocorrer exclusivamente via clique do mouse ou toque (touch). (Origem: brief Decisão Confirmada #3)

---

## User Interface Design Goals

### Overall UX Vision

Calculadora utilitária com **identidade visual tricolor dominante** que faz o torcedor se sentir representado em uma ferramenta do dia a dia. A experiência é minimalista em funcionalidade (apenas 4 operações + decimal + clear), mas **expressiva visualmente**: as listras azul/preto/azul, a logo do Grêmio no topo e as cores oficiais devem comunicar imediatamente a identidade do clube. A calculadora deve ser reconhecível como "do Grêmio" antes mesmo de o usuário começar a usar.

### Key Interaction Paradigms

- **Toque / clique único**: cada botão executa uma ação atômica (digitar dígito, aplicar operador, calcular, limpar)
- **Feedback imediato no display**: toda interação atualiza o display em tempo real (FR-1)
- **Encadeamento natural**: o usuário pode digitar `2 + 3 + 5 =` em sequência sem precisar pressionar `=` entre operações; a calculadora resolve da esquerda para a direita (FR-4)
- **Recuperação simples**: em caso de erro (divisão por zero), o usuário pressiona Clear para voltar ao estado zerado (FR-5, FR-8)
- **Sem teclado físico no MVP**: o usuário interage exclusivamente via clique/touch nos botões da interface (NFR-7)

### Core Screens and Views

- **Tela única — Calculadora Grêmio**: layout vertical contendo (de cima para baixo) logo do Grêmio centralizada, display numérico, grid de botões (dígitos 0–9, operadores +/−/×/÷, vírgula, igual, clear). Não há outras telas, modais ou navegação.

### Accessibility: None

Acessibilidade WCAG completa está **fora do escopo do MVP**. Boas práticas mínimas (contraste de cores legível, alt-text na logo, tamanho de fonte adequado) devem ser aplicadas pelo @dev por bom senso, mas certificação WCAG não é requisito. (Origem: brief seção 6 — Out of Scope)

### Branding

A identidade Grêmio é o elemento central da experiência visual. Diretrizes obrigatórias (detalhadas em NFR3):

- **Cores oficiais dominantes:** azul celeste `#0099CC`, preto `#000000`, branco `#FFFFFF`
- **Listras tradicionais** (padrão clássico do uniforme tricolor: azul/preto/azul em alternância vertical) presentes no fundo do container, header ou bordas
- **Logo real do Grêmio** (`gremio-logo.png`, arquivo na raiz do projeto) no topo, centralizada, full-width
- **Tipografia** sans-serif esportiva, medium/bold em títulos
- **Proibido:** fundo neutro genérico (cinza claro, off-white)

Refinamento da paleta exata por elemento, posicionamento das listras e hierarquia visual pode ser feito por `@ux-design-expert` (opcional) ou pelo `@dev` durante a implementação, desde que respeite NFR3.

### Target Device and Platforms: Web Responsive

Web Responsive em modo `file://` — desktop (>=1024px) e mobile (>=320px). Sem necessidade de PWA, app nativo ou empacotamento. O entregável é o arquivo `index.html` mais a logo `gremio-logo.png` na raiz.

---

## Technical Assumptions

### Repository Structure: Monorepo (single-folder, flat)

Estrutura mínima de um único diretório plano contendo `index.html`, `gremio-logo.png` e (opcionalmente) arquivos `style.css` e `script.js` se o `@dev` optar por separar HTML/CSS/JS — embora seja igualmente válido manter tudo inline no `index.html`. Não há sub-pacotes, monorepo manager ou separação por workspaces.

### Service Architecture

**100% client-side, single-page, single-file (ou no máximo 3 arquivos: HTML + CSS + JS).** Não há backend, banco de dados, API ou serviço de qualquer natureza. Toda a lógica de cálculo, estado e renderização ocorre no navegador do usuário, em runtime, em memória. (Origem: brief CON-3, NFR-1, NFR-2)

### Testing Requirements

**Manual testing only no MVP.** Testes automatizados (unit, integration, e2e) estão **fora do escopo** (brief seção 6). O `@qa` deve executar verificação manual:
- 4 operações básicas com inteiros e decimais
- Encadeamento (`2+3+5=10`, `10−2−3=5`, etc.)
- Divisão por zero retorna `"Erro"`
- Clear reseta estado
- Layout em viewports `320px`, `768px`, `1024px+`
- Cross-browser em Chrome, Edge, Firefox (últimas 3 versões)

Testes automatizados podem ser adicionados em iteração futura, fora deste PRD.

### Additional Technical Assumptions and Requests

- **Logo file:** o arquivo da logo na raiz é `gremio-logo.png` (renomeado de `gremio-logo.png.png` antes da fase de implementação). Todas as referências em HTML/CSS devem usar `gremio-logo.png`.
- **Convenção decimal:** vírgula (`,`) como separador decimal (padrão pt-BR), conforme FR6. A representação interna em JavaScript usa ponto, mas a apresentação ao usuário usa vírgula.
- **Precisão de ponto flutuante:** limitação inerente ao JavaScript (`0.1 + 0.2 ≠ 0.3`) é aceita. O `@dev` pode aplicar arredondamento opcional na exibição (ex: `parseFloat(result.toFixed(10))`) para evitar resultados visualmente desagradáveis, sem alterar comportamento funcional. (Origem: brief RIS-1)
- **Modo de execução:** protocolo `file://` apenas. Sem `localhost`, sem servidor HTTP local. Validação obrigatória: duplo-clique em `index.html` deve abrir e funcionar.
- **Sem internacionalização:** apenas pt-BR (label `"Erro"`, separador decimal `,`).
- **CI/CD e DevOps:** fora do exercício. Não há pipeline, deploy automatizado ou versionamento de release.

---

## Epic List

Para um MVP de baixa complexidade entregue em uma sessão de trabalho (CON-5), a estrutura é minimalista — **1 único epic** que entrega a calculadora completa. As stories dentro do epic são ordenadas como vertical slices sequenciais, cada uma entregando incremento testável.

- **Epic 1 — Calculadora Grêmio MVP:** Entregar uma calculadora web client-side funcional com as 4 operações aritméticas, encadeamento de operações, tratamento de divisão por zero e identidade visual marcante do Grêmio (listras, logo real, paleta oficial), executável por duplo-clique no `index.html` em navegadores modernos.

> **Nota de sequenciamento:** todas as stories deste epic compartilham o mesmo arquivo (`index.html`) e são logicamente dependentes (visual sem cálculo é vazio; cálculo sem visual não é a Calculadora Grêmio). A ordenação reflete uma construção incremental: estrutura → lógica → polish.

---

## Epic 1 — Calculadora Grêmio MVP

**Expanded Goal:** Entregar a Calculadora Grêmio completa em condição de uso real — abrir por duplo-clique em `index.html`, executar as 4 operações aritméticas com encadeamento ativo da esquerda para a direita, tratar divisão por zero exibindo `"Erro"`, e apresentar identidade visual Grêmio dominante (listras tradicionais azul/preto/azul, logo `gremio-logo.png` no topo, paleta oficial em todos os botões). O epic encerra com a calculadora pronta para QA gate manual e validação cross-browser.

### Story 1.1 — Estrutura HTML, identidade visual Grêmio e logo

As a torcedor tricolor,
I want abrir o `index.html` e ver imediatamente a Calculadora Grêmio com a logo do clube no topo, listras tradicionais e paleta oficial dominante,
so that eu reconheça que esta é a calculadora do Grêmio antes mesmo de começar a usar.

#### Acceptance Criteria

1. **AC1.1.1:** O arquivo `index.html` existe na raiz do projeto e abre corretamente em Chrome, Edge e Firefox via duplo-clique (protocolo `file://`), sem erros no console. (Origem: NFR2, NFR5)
2. **AC1.1.2:** A logo do Grêmio é exibida no topo, centralizada e em container full-width, referenciando o arquivo `gremio-logo.png` da raiz via tag `<img src="gremio-logo.png" alt="Grêmio Foot-Ball Porto Alegrense">`. Altura visual aproximada: 80–120px em desktop, 60–80px em mobile. (Origem: FR7)
3. **AC1.1.3:** A interface contém as listras tradicionais do Grêmio (alternância vertical clássica azul/preto/azul) aplicadas como elemento visual em pelo menos um destes locais: fundo do container principal, header atrás/abaixo da logo, ou bordas/molduras dos elementos. (Origem: NFR3.1)
4. **AC1.1.4:** A paleta oficial está presente e dominante: `#0099CC` (azul celeste), `#000000` (preto), `#FFFFFF` (branco). **Não há fundo neutro genérico** (cinza claro, off-white). (Origem: NFR3.4)
5. **AC1.1.5:** O layout estrutural contém todos os botões previstos (dígitos 0–9, operadores +, −, ×, ÷, vírgula, igual, clear) e um display numérico, organizados em grid usável — mesmo que sem lógica funcional ainda. (Origem: FR1, FR2, FR3, FR5, FR6)
6. **AC1.1.6:** O layout é responsivo: funciona sem quebras em viewports de `>=320px` (mobile) e `>=1024px` (desktop). Validação: testar em DevTools em pelo menos 3 larguras (320, 768, 1024). (Origem: NFR4)
7. **AC1.1.7:** Tipografia sans-serif legível com peso medium/bold em títulos/display. (Origem: NFR3.3)
8. **AC1.1.8:** A página NÃO carrega nenhum recurso externo (CDN, Google Fonts via rede, frameworks). Todos os assets vêm do diretório local. (Origem: NFR1, NFR2)

---

### Story 1.2 — Lógica da calculadora: operações, encadeamento e tratamento de erro

As a torcedor tricolor,
I want clicar nos botões da calculadora e obter resultados aritméticos corretos, incluindo encadeamento de múltiplas operações e tratamento de divisão por zero,
so that eu consiga realizar cálculos do dia a dia com confiança na correção dos resultados.

#### Acceptance Criteria

1. **AC1.2.1:** Cada clique em um botão de dígito (0–9) anexa o dígito ao operando atual no display. Se o display estiver mostrando `0` (estado inicial) ou um resultado anterior, o novo dígito substitui o display. (Origem: FR1, FR2)
2. **AC1.2.2:** O botão de vírgula decimal (`,`) anexa um separador decimal ao operando atual. Múltiplas vírgulas no mesmo operando são ignoradas (não devem produzir `1,2,3`). (Origem: FR6)
3. **AC1.2.3:** Cada um dos 4 botões de operador (+, −, ×, ÷) registra a operação pendente e prepara a calculadora para receber o segundo operando. (Origem: FR3)
4. **AC1.2.4:** O botão Igual (=) executa a operação pendente e exibe o resultado no display. Validação obrigatória dos cenários:
   - `1 + 1 =` → `2`
   - `10 − 3 =` → `7`
   - `4 × 5 =` → `20`
   - `10 ÷ 4 =` → `2,5`
   - `0,1 + 0,2 =` → `0,3` (arredondamento na exibição é permitido para evitar ruído de ponto flutuante) (Origem: FR4)
5. **AC1.2.5:** **Encadeamento ativo de operações** — pressionar um operador após uma operação pendente resolve a operação anterior e usa o resultado como primeiro operando da próxima. Avaliação esquerda → direita, sem precedência. Validação obrigatória:
   - `2 + 3 + 5 =` → `10` (resolve `2+3=5`, depois `5+5=10`)
   - `10 − 2 − 3 =` → `5`
   - `2 + 3 × 4 =` → `20` (resolve `2+3=5`, depois `5×4=20` — sem precedência matemática) (Origem: FR4 + Decisão Confirmada #1)
6. **AC1.2.6:** **Divisão por zero** exibe o texto literal `"Erro"` no display. O estado da calculadora permanece estável após o erro: pressionar Clear retorna ao estado zerado e permite uso normal. (Origem: FR8 + Decisão Confirmada #2)
7. **AC1.2.7:** O botão Clear (C) reseta o display ao valor `0` e zera o estado interno (operandos pendentes, operação pendente). (Origem: FR5)
8. **AC1.2.8:** Não há suporte a teclado físico — apenas cliques/toques nos botões da interface produzem efeito. Pressionar teclas no teclado físico não deve causar nenhuma alteração na calculadora nem gerar erros no console. (Origem: NFR7 + Decisão Confirmada #3)
9. **AC1.2.9:** O código JavaScript está inline em `<script>` no `index.html` ou em um arquivo `script.js` local, sem CDN, sem bundler e sem `import`/`require` de pacotes externos. (Origem: NFR1)

---

### Story 1.3 — Polish, cross-browser e validação manual

As a stakeholder e meta-projeto AIOX,
I want garantir que a Calculadora Grêmio funciona corretamente nos 3 navegadores alvo, em desktop e mobile, com qualidade visual e de código aceitáveis,
so that o entregável passe no QA gate manual e o exercício do SDC seja considerado validado.

#### Acceptance Criteria

1. **AC1.3.1:** Validação cross-browser manual: a calculadora abre, renderiza corretamente e executa todas as operações (FR1–FR8) nas 3 últimas versões estáveis de Chrome, Edge e Firefox. (Origem: NFR5, OBJ-1)
2. **AC1.3.2:** Validação responsiva manual em DevTools nas larguras 320px, 768px e 1024px+: nenhum elemento sai do viewport, nenhum botão fica inalcançável, a logo permanece legível, o display permanece legível. (Origem: NFR4, OBJ-4)
3. **AC1.3.3:** Console do navegador limpo: nenhum erro (`Uncaught Error`, `404`, `CORS`) ao abrir e ao executar todas as operações em cada navegador alvo. (Origem: NFR2, NFR6)
4. **AC1.3.4:** Validação `file://`: abrir o `index.html` por duplo-clique no Windows Explorer / Finder / file manager funciona — não há recursos bloqueados por política de origem ou dependência de servidor. (Origem: NFR2, CON-3)
5. **AC1.3.5:** Qualidade de código: o código possui comentários em pontos não-óbvios (lógica de encadeamento, tratamento de erro, edge cases de vírgula decimal). Nomes de variáveis e funções são autoexplicativos. Indentação consistente. (Origem: NFR6)
6. **AC1.3.6:** Identidade visual final aprovada por verificação manual: listras presentes e visíveis, logo nítida, paleta oficial dominante, sem fundo neutro genérico. (Origem: NFR3, OBJ-3)
7. **AC1.3.7:** Suite de smoke-test manual documentada e executada — registro em formato lista (`docs/qa/smoke-test-1.3.md` ou inline na story) com cada cenário marcado ✅/❌:
   - 4 operações básicas (inteiros)
   - 4 operações básicas (decimais)
   - Encadeamento (3 cenários canônicos: `2+3+5=10`, `10−2−3=5`, `2+3×4=20`)
   - Divisão por zero (`5 ÷ 0 =` → `"Erro"`)
   - Clear após erro (volta a `0`, calculadora utilizável)
   - Vírgula múltipla ignorada (`1,2,3` deve resultar em `1,23` ou primeira vírgula apenas)
8. **AC1.3.8:** O entregável final consiste exclusivamente de: `index.html`, `gremio-logo.png` e (opcionalmente) `style.css` + `script.js`. Nenhum outro arquivo de runtime é necessário. (Origem: CON-1, CON-2, CON-3)

---

## Checklist Results Report

> **Nota:** O `pm-checklist` ainda não foi executado. Após a aprovação deste PRD pelo sponsor, executar `*execute-checklist pm-checklist` para popular esta seção. Como este PRD foi gerado em modo YOLO a partir de um Project Brief já aprovado (v1.1, sponsor confirmou decisões), recomenda-se que o checklist seja executado pelo `@po` durante a fase de validação de stories como cross-check.

---

## Next Steps

### UX Expert Prompt

> **Para `@ux-design-expert` (Uma) — opcional:**
>
> Refine a aplicação visual da identidade Grêmio na Calculadora Grêmio (`docs/prd.md`). Foco em: (1) posicionamento exato e proporção das listras tradicionais azul/preto/azul (fundo, header ou bordas — escolher e justificar); (2) hierarquia visual da paleta nos botões — qual cor para qual grupo (numéricos, operadores, igual, clear) garantindo contraste e identidade marcante; (3) breakpoints CSS para responsividade entre 320px e 1024px+; (4) tipografia esportiva legível. Respeitar NFR3 (sem fundo neutro genérico, listras obrigatórias, paleta dominante) e gerar `docs/front-end-spec.md` como input para `@dev`. Comando sugerido: `*create-front-end-spec`.

### Architect Prompt

> **Arquitetura formal NÃO é requerida** para este MVP. O stack está fixado por NFR1/NFR2 (HTML5/CSS3/JS vanilla, sem build, sem backend), a estrutura é trivial (1 a 3 arquivos planos), e não há decisões de integração, persistência, autenticação ou escalabilidade a tomar.
>
> **Próximo handoff recomendado: direto para `@sm`** com este PRD como input.
>
> Comando sugerido: `@sm` → `*draft` → começar pela Story 1.1.
>
> Caso o sponsor ou `@po` identifiquem necessidade de decisão arquitetural durante a validação (ex: uso de `<canvas>` para listras, estrutura de eventos, padrão de gerenciamento de estado), aí sim envolver `@architect` (Aria) com escopo cirúrgico.

---

*Documento gerado por Morgan (PM) — AIOX SDC Phase 1 (Create PRD).*
*Próximo handoff: `@sm *draft` (começando pela Story 1.1).*
