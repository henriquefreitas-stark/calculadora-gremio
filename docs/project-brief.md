# Project Brief: Calculadora Grêmio

**Documento:** Project Brief
**Versão:** 1.1
**Data:** 2026-05-08
**Autor:** Atlas (Analyst) — orquestração AIOX
**Status:** Draft — pronto para handoff a `@pm`

**Changelog**
- **v1.1 (2026-05-08):** Encadeamento de operações ativado; identidade visual Grêmio reforçada com listras tradicionais; logo real (`gremio-logo.png.png`) substitui placeholder.
- **v1.0 (2026-05-08):** Versão inicial.

---

## 1. Executive Summary

**Calculadora Grêmio** é uma calculadora web client-side, escrita em HTML5/CSS3/JavaScript vanilla, com identidade visual oficial do Grêmio Foot-Ball Porto Alegrense. O produto entrega cálculos aritméticos básicos (soma, subtração, multiplicação, divisão) em um único arquivo `index.html` executável por duplo-clique no navegador, sem dependências externas, sem backend e sem build step.

Além do valor de produto, o projeto serve como **exercício prático de orquestração do fluxo Story Development Cycle (SDC)** do AIOX — passando pelos handoffs `@analyst → @pm → @sm → @po → @dev → @qa`.

---

## 2. Problem Statement

### Dor primária
Usuários precisam realizar cálculos aritméticos simples no navegador sem instalar aplicativos, abrir planilhas ou acessar serviços online. Soluções existentes (calculadora do SO, Google) não oferecem personalização visual nem rodam offline em arquivo único.

### Dor secundária (meta-projeto)
A equipe precisa de um **caso real de baixa complexidade** para validar o fluxo end-to-end de agentes AIOX em um cenário greenfield, antes de aplicá-lo a projetos críticos.

### Por que agora
- Demanda imediata de torcedores por uma calculadora temática personalizável
- Necessidade de validar a maturidade do orquestrador AIOX em ciclo completo SDC

---

## 3. Target Users

### Usuário Primário — Torcedor Tricolor
- **Perfil:** Torcedor do Grêmio, faixa etária ampla, familiarizado com navegação web básica
- **Contexto de uso:** Casual, em desktop ou mobile, abrindo `index.html` localmente
- **Motivação:** Identidade visual do clube em uma ferramenta utilitária do dia a dia
- **Frequência esperada:** Uso esporádico, cálculos rápidos

### Usuário Secundário — Usuário genérico de calculadora
- **Perfil:** Qualquer pessoa que precise de uma calculadora simples no navegador
- **Contexto de uso:** Cálculo rápido offline, sem instalação
- **Motivação:** Funcionalidade e simplicidade

### Não-usuários (excluídos do escopo)
- Profissionais que precisam de calculadora científica/financeira
- Usuários que dependem de histórico ou memória de cálculos

---

## 4. Goals & Success Metrics

### Objetivos de Produto
| ID | Objetivo | Métrica |
|----|----------|---------|
| OBJ-1 | Calculadora abre e executa em navegadores modernos | Funciona em Chrome, Edge, Firefox (3 últimas versões) |
| OBJ-2 | Operações aritméticas básicas funcionam sem erros | 100% das 4 operações (+, −, ×, ÷) operacionais |
| OBJ-3 | Identidade visual Grêmio aplicada de forma consistente | Cores oficiais (#0099CC, preto, branco) presentes em todos os elementos visuais relevantes |
| OBJ-4 | Layout responsivo desktop + mobile | Funciona em viewports >=320px e >=1024px sem quebras |
| OBJ-5 | Zero dependências externas | `index.html` abre em modo `file://` e funciona offline |

### Objetivos de Processo (meta-projeto)
| ID | Objetivo | Métrica |
|----|----------|---------|
| META-1 | Validar SDC end-to-end | Story passa por todas as 4 fases (Create → Validate → Implement → QA Gate) |
| META-2 | Handoffs entre agentes sem perda de contexto | Cada handoff produz artifact em `.aiox/handoffs/` |
| META-3 | Conformidade com Constitution AIOX | Nenhuma violação dos artigos I–VI |

---

## 5. MVP Scope

### Funcionalidades Incluídas

**FR-1 — Display numérico**
Exibe o valor atual em digitação e/ou a operação em curso. Atualização em tempo real a cada interação do usuário.

**FR-2 — Teclado numérico (0 a 9)**
Botões clicáveis para inserção de dígitos.

**FR-3 — Operações aritméticas básicas**
Botões para soma (+), subtração (−), multiplicação (×) e divisão (÷).

**FR-4 — Botão Igual (=) com encadeamento de operações**
Executa o cálculo da operação corrente e exibe o resultado no display. **Suporte obrigatório a operações encadeadas:** ao pressionar um operador após uma operação pendente, a calculadora deve resolver a operação anterior e usar o resultado como operando da próxima. Exemplo: `2 + 3 + 5 =` deve retornar `10` (resolvendo `2+3=5`, depois `5+5=10`). Avaliação da esquerda para a direita, sem precedência de operadores (mantém simplicidade do MVP).

**FR-5 — Botão Clear (C)**
Reseta o display e o estado interno da calculadora ao valor zero.

**FR-6 — Vírgula decimal (,)**
Permite digitação de números fracionários. Convenção: vírgula como separador (padrão pt-BR).

**FR-7 — Logo do Grêmio no topo**
A imagem real da logo oficial está disponível na raiz do projeto como **`gremio-logo.png.png`** (nome do arquivo conforme está no filesystem — extensão duplicada). O dev deve referenciá-la no HTML via tag `<img src="gremio-logo.png.png" alt="Grêmio Foot-Ball Porto Alegrense">`. Posicionamento: topo centralizado, full-width container. Dimensionar para boa legibilidade em desktop e mobile (sugestão: altura 80–120px desktop, 60–80px mobile).

> **Nota técnica:** se o dev optar por renomear o arquivo para `gremio-logo.png` (corrigindo a extensão duplicada), atualizar a referência no HTML correspondentemente. Decisão delegada à fase de implementação.

### Requisitos Não-Funcionais

**NFR-1 — Stack mínimo**
HTML5, CSS3 e JavaScript vanilla. Proibido: frameworks (React, Vue, Angular), bibliotecas externas (jQuery, Lodash), CDNs, build steps (Webpack, Vite, Parcel).

**NFR-2 — Execução**
Deve abrir e funcionar com duplo-clique no `index.html` (protocolo `file://`).

**NFR-3 — Identidade Visual Marcante (Grêmio)**

Aplicar a identidade do Grêmio de forma **forte e marcante**, não como acento sutil. As 3 cores oficiais devem dominar a interface:

- **Azul celeste:** `#0099CC`
- **Preto:** `#000000`
- **Branco:** `#FFFFFF`

**Diretrizes obrigatórias:**

1. **Listras tradicionais do clube** — usar o padrão de listras azul/preto/azul (alternância vertical clássica do uniforme tricolor) como elemento visual em pelo menos um dos seguintes locais:
   - Fundo do container principal da calculadora, OU
   - Header (faixa atrás/abaixo da logo), OU
   - Bordas/molduras dos elementos
2. **Botões com forte presença das cores oficiais:**
   - Botões numéricos: paleta com as 3 cores (sugestão: fundo preto, texto branco)
   - Botões de operadores (+, −, ×, ÷): destaque em azul celeste `#0099CC` com texto branco
   - Botão de igual (=): pode usar combinação contrastante (ex: branco com borda azul, ou preto com texto branco)
   - Botão Clear (C): cor distintiva para indicar reset (sugestão: branco com texto azul, ou contraste forte)
3. **Tipografia:** sans-serif legível, peso adequado para identidade esportiva (medium/bold em títulos)
4. **Proibido:** fundo neutro genérico (cinza claro, off-white, etc.) — a identidade do clube deve ser dominante.

> **Decisão de design final** (paleta exata por elemento, posicionamento das listras, hierarquia visual) pode ser refinada por `@ux-design-expert` ou pelo `@dev` durante implementação, desde que respeite as diretrizes acima.

**NFR-4 — Responsividade**
Layout funciona em desktop (>=1024px) e mobile (>=320px).

**NFR-5 — Compatibilidade**
Suporte às 3 últimas versões de Chrome, Edge e Firefox.

**NFR-6 — Qualidade de código**
Código limpo, com comentários em pontos não-óbvios suficientes para revisão por humano ou agente.

---

## 6. Out of Scope (MVP)

Itens explicitamente excluídos deste MVP:

- ❌ Operações científicas (raiz, potência, trigonometria, logaritmos)
- ❌ Histórico de cálculos
- ❌ Memória (M+, M−, MR, MC)
- ❌ Conversão de unidades
- ❌ Backend, banco de dados, persistência
- ❌ Autenticação ou multiusuário
- ❌ Testes automatizados (será exercitado em fase futura)
- ❌ Build/deploy pipeline (DevOps fora do exercício)
- ❌ Internacionalização (apenas pt-BR)
- ❌ Acessibilidade WCAG completa (boa prática mínima, sem certificação)

---

## 7. Restrições e Premissas

### Restrições (CON)
| ID | Restrição | Origem |
|----|-----------|--------|
| CON-1 | Stack obrigatório: HTML5/CSS3/JS vanilla | Decisão de produto |
| CON-2 | Sem dependências externas (CDN, npm) | Decisão de produto |
| CON-3 | 100% client-side, sem backend | Decisão de produto |
| CON-4 | Identidade visual Grêmio (cores oficiais) | Decisão de produto |
| CON-5 | Prazo: 1 sessão de trabalho | Exercício de treinamento |
| CON-6 | Logo do Grêmio: usar `gremio-logo.png.png` da raiz do projeto | Imagem fornecida pelo sponsor |

### Premissas
- Usuário tem navegador moderno instalado
- Usuário consegue abrir arquivos HTML por duplo-clique no SO
- Cores oficiais do Grêmio fornecidas no briefing são suficientemente fiéis para o exercício
- Não há expectativa de SLA, monitoramento ou suporte pós-entrega

---

## 8. Riscos e Questões em Aberto

### Riscos Identificados
| ID | Risco | Severidade | Mitigação |
|----|-------|-----------|-----------|
| RIS-1 | Precisão de ponto flutuante em divisões | Baixa | Documentar limitação; arredondamento opcional na exibição |
| RIS-2 | Layout quebrar em viewports muito estreitos (<320px) | Baixa | Definir breakpoint mínimo; testar em DevTools |
| RIS-3 | Cores oficiais do Grêmio podem variar entre fontes | Baixa | Adotar `#0099CC` informado no briefing como verdade |

### Decisões Confirmadas (sponsor — 2026-05-08)
| # | Tópico | Decisão final |
|---|--------|--------------|
| 1 | Sequência de operações | **Encadeamento ATIVO** — `2+3+5=` retorna `10` (avaliação esquerda→direita, sem precedência) |
| 2 | Divisão por zero | Exibir `"Erro"` no display |
| 3 | Suporte a teclado físico | Fora do MVP — apenas clique/touch |
| 4 | Posição do logo | Topo centralizado, full-width — usando `gremio-logo.png.png` (arquivo real na raiz) |
| 5 | Tema visual | **Identidade Grêmio MARCANTE** — listras tradicionais azul/preto/azul + botões com forte presença das 3 cores oficiais. Sem fundo neutro. |

> Decisões 1, 4 e 5 foram revisadas e aprovadas pelo sponsor após v1.0. Demais defaults seguem como originalmente propostos.

---

## 9. Stakeholders

| Papel | Pessoa/Agente | Responsabilidade |
|-------|--------------|------------------|
| Sponsor / Owner | henrique.freitas@starkmkt.com | Decisão final de escopo |
| Analyst | @analyst (Atlas) | Project brief (este documento) |
| PM | @pm (Morgan) | PRD e priorização |
| SM | @sm (River) | Criação de stories |
| PO | @po (Pax) | Validação de stories |
| Dev | @dev (Dex) | Implementação |
| QA | @qa (Quinn) | Quality gate |
| UX (opcional) | @ux-design-expert (Uma) | Refinamento visual da identidade Grêmio |

---

## 10. Próximos Passos (Recomendação de Handoff)

1. **Handoff a `@pm`** para criação do PRD a partir deste brief
   - Comando sugerido: `@pm` → `*create-prd`
2. **Handoff a `@ux-design-expert`** (opcional) para refinar layout e aplicação das cores Grêmio
   - Comando sugerido: `@ux-design-expert` → `*create-front-end-spec`
3. **Sequência completa SDC esperada:**
   ```
   @pm *create-prd
   → @sm *draft (Story 1.1 — MVP da calculadora)
   → @po *validate-story-draft
   → @dev *develop-story
   → @qa *qa-gate
   ```

---

## 11. Apêndice — Resumo Executivo (1 parágrafo)

Construir uma calculadora web em HTML/CSS/JS vanilla, executável por duplo-clique no `index.html`, sem dependências externas, com identidade visual **marcante** do Grêmio (listras tradicionais azul/preto/azul, paleta oficial dominante, logo real `gremio-logo.png.png` no topo) e suporte às 4 operações aritméticas básicas com **encadeamento de operações** (`2+3+5=10`). O projeto também valida o fluxo SDC do AIOX em um caso greenfield de baixa complexidade. Entrega em uma sessão de trabalho.

---

*Documento gerado por Atlas (Analyst) — AIOX SDC Phase 0.*
*Próximo handoff: `@pm *create-prd`.*
