# OpenCode Design — Especificação Harness Completo

Harness de design agêntico para o OpenCode, especializado em **apps Next.js** e **landing pages HTML** de alta qualidade técnica e visual.
Documento de referência técnica para implementação.

---

## 1. Visão Geral

### 1.1 Problema

Agentes de codificação geram interfaces funcionais mas visualmente genéricas — gradientes blue-purple, cards com borda lateral colorida, emoji como ícones, tipografia padrão Inter/Roboto.
O resultado é "AI slop": páginas que parecem geradas, não desenhadas.

### 1.2 Solução

Um harness integrado que combina **4 skills de design de elite**, **8 referências visuais externas** (incluindo SearXNG para pesquisa na web), **DESIGN.md portáveis** e um **sistema de verificação anti-slop** para transformar o OpenCode em um agente capaz de produzir interfaces com nível de design profissional.

### 1.3 Alcance

- Landing pages HTML + Tailwind (single-file, alta performance)
- Apps Next.js (App Router, componentes modulares, design system)
- Design system extraction e geração a partir de briefs
- Iteração visual com vocabulário de design preciso
- Verificação de qualidade com gates determinísticos
- Redesign de projetos existentes

### 1.4 Não Inclui

- Geração de imagens (usa placeholders rotulados)
- Back-end development
- Deploy e infraestrutura
- Design de apps mobile nativos

---

## 2. Skills Externas Integradas

### 2.1 UI UX Pro Max — Motor de Design System

**Repositório:** `nextlevelbuilder/ui-ux-pro-max-skill` (101k⭐)
**URL:** https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
**Papel:** Cérebro do design system. Gera sistemas completos a partir de briefs.

**Recursos técnicos:**
- 161 regras de reasoning por indústria (SaaS, fintech, healthcare, e-commerce, etc.)
- 67 estilos UI (Glassmorphism, Bento Grid, Neubrutalism, AI-Native, etc.)
- 161 paletas de cores alinhadas 1:1 com tipos de produto
- 57 combinações tipográficas com Google Fonts
- Engine BM25 para matching inteligente de estilos
- CLI: `uipro init --ai opencode`

**Output esperado:** Design System completo com pattern, style, cores, tipografia, efeitos, anti-patterns, checklist pré-entrega.

**Instalação:**
```bash
npm install -g ui-ux-pro-max-cli
uipro init --ai opencode
```

### 2.2 Taste Skill — Anti-Slop

**Repositório:** `Leonxlnx/taste-skill` (56.2k⭐)
**URL:** https://github.com/Leonxlnx/taste-skill
**Papel:** Guarda de qualidade visual. Elimina padrões genéricos de IA.

**Variantes disponíveis:**
- `design-taste-frontend` (v2) — default: layout, tipografia, motion, spacing
- `gpt-taste` — versão mais estrita para GPT/Codex
- `redesign-existing-projects` — para melhorar codebases existentes
- `minimalist-ui` — estética editorial (Notion/Linear)
- `high-end-visual-design` — UI premium com whitespace e spring motion

**Dials configuráveis:**
| Dial | Range | Efeito |
|------|-------|--------|
| `DESIGN_VARIANCE` | 1-10 | 1=centrado/clean → 10=assimétrico/moderno |
| `MOTION_INTENSITY` | 1-10 | 1=hover apenas → 10=scroll/magnetic |
| `VISUAL_DENSITY` | 1-10 | 1=espaçoso → 10=dashboards densos |

**Regras anti-slop:**
- Ban de em-dash em copy
- Proibição de gradientes purple/pink genéricos
- SVGs de ícones obrigatórios (Heroicons/Lucide), nunca emoji
- Protocolo de redesign-audit
- Pre-flight check rigoroso antes de cada entrega

**Instalação:**
```bash
npx skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend"
```

### 2.3 Awesome DESIGN.md — Referências de Marca

**Repositório:** `VoltAgent/awesome-design-md` (95.6k⭐)
**URL:** https://github.com/VoltAgent/awesome-design-md
**Papel:** Biblioteca de 73 DESIGN.md de marcas reais para referência visual.

**Coleções por categoria:**
| Categoria | Marcas |
|-----------|--------|
| AI & LLM | Claude, Cursor, Vercel, Warp, Linear, xAI, Ollama, OpenCode |
| Developer Tools | Expo, Raycast, Superhuman, Lovable |
| Backend/DevOps | Supabase, Sentry, MongoDB, ClickHouse, HashiCorp |
| Fintech | Stripe, Coinbase, Revolut, Wise, Binance |
| E-commerce | Shopify, Airbnb, Nike, Starbucks |
| Consumer | Apple, Spotify, Tesla, SpaceX, Meta, Uber |
| Design | Figma, Framer, Webflow, Miro |

**Conteúdo de cada DESIGN.md:** paleta com hex + papel funcional, hierarquia tipográfica completa, estilos de componentes, princípios de layout, sistema de elevação, do's e don'ts, comportamento responsivo.

**Uso:** Quando o brief menciona "estilo Linear" ou "vibe Stripe", o harness carrega o DESIGN.md correspondente como referência visual.

**Instalação:** Clonar repositório e copiar para `.opencode/references/design-md/`.

### 2.4 Emil Kowalski Skills — Motion Design

**Repositório:** `emilkowalski/skills` (4.8k⭐)
**URL:** https://github.com/emilkowalski/skills
**Papel:** Especialista em micro-interações e motion design.

**Skills específicas:**
- `emil-design-eng` — regras de animação + design advice (experiência Vercel/Linear)
- `review-animations` — auditoria estrita de animações
- `animation-vocabulary` — vocabulário preciso para solicitar animações à IA

**Regras de animação:**
| Contexto | Easing | Duração | Spring |
|----------|--------|---------|--------|
| Enter animation | ease-out | 300-500ms | stiffness: 200, damping: 15 |
| Exit animation | ease-in | 200-300ms | stiffness: 300, damping: 20 |
| Hover state | ease-out | 150-200ms | — |
| Page transition | ease-in-out | 400-600ms | stiffness: 150, damping: 20 |
| Micro-interaction | spring | 200-400ms | stiffness: 300, damping: 15 |
| Scroll reveal | ease-out | 500-800ms | — |

**Princípios:**
- Semi-transparent shadows > solid borders
- Spring physics para micro-interações
- `prefers-reduced-motion` sempre respeitado
- GSAP como biblioteca preferida para motion complexa
- Nunca `ease-in` para enter, nunca `linear` para UI
- Nunca animar mais de 2 propriedades simultaneamente

**Instalação:**
```bash
npx skills add emilkowalski/skills
```

### 2.5 Anthropic frontend-design — Framework Filosófico (Integrado)

**Repositório:** `anthropics/skills` (158k⭐)
**URL:** https://github.com/anthropics/skills
**Papel:** Framework de pensamento de design. Nao e uma skill tecnica, mas um processo criativo integrado em `design-entry` e `design-critic`.

**O que integra (nao duplica, preenche lacunas):**

| Lacuna na spec original | O que frontend-design traz |
|-------------------------|----------------------------|
| Vai direto para construcao | **Workflow de 2 passes**: planejar → criticar → construir |
| Foca em output, nao no sujeito | **Ground it in the subject**: entender mundo do produto antes de desenhar |
| Tem anti-patterns, mas nao ensina a criar algo positivo | **Signature element**: definir o unico elemento memoravel |
| Tem verificadores externos | **Auto-critica**: regra Chanel (remover 1 acessorio antes de entregar) |
| Menciona copy formula | **Copy como material de design**: palavras sao design, nao decoracao |
| Lista anti-patterns | **Cluster awareness**: 3 clusters genéricos atuais (cream-serif, dark-acid, broadsheet) |

**Integracao na spec:**
- Secao 5.1 (`design-entry`): ground it in the subject, workflow de 2 passes, restricao e auto-critica, copy como material
- Secao 6.2 (`design-critic`): cluster awareness, auto-critica do plano
- Secao 8.4 (`anti-patterns.json`): 3 regras de cluster generico
- Secao 12 (Anti-Patterns): clusters adicionados a lista de deteccao

**Instalação:** Nao instalar como skill separada. Os principios sao integrados diretamente nas skills existentes.

---

## 3. Referências Visuais Externas

### 3.1 Refero — Biblioteca de Estilos

**URL:** https://styles.refero.design
**Conteúdo:** 2,000+ DESIGN.md de produtos reais.
**Integração:** MCP server remoto para busca em tempo real durante o workflow.
**Configuração:**
```json
{
  "refero": {
    "type": "remote",
    "url": "https://mcp.refero.design",
    "enabled": true
  }
}
```

### 3.2 Impeccable Style — Vocabulário de Design

**URL:** https://impeccable.style (40k⭐)
**Conteúdo:** 23 comandos de design com vocabulário preciso + 45 regras anti-slop.

**Comandos disponíveis:**
- `/typeset` — hierarquia tipográfica
- `/colorize` — paleta de cores
- `/animate` — motion design
- `/polish` — refinamento geral
- `/distill` — simplificar
- `/delight` — micro-interações
- `/overdrive` — máxima qualidade

**Regras anti-slop (45):**
- `gradient-text`, `side-stripe-border`, `ai-color-palette`
- `ghost-card`, `over-rounding`, `purple-pink-gradient`
- `emoji-as-icon`, `inter-default`, `blue-purple-bg`
- `decorative-stats`, `excessive-shadow`, `no-hover-state`
- `linear-easing`, `ease-in-enter`, `missing-reduced-motion`
- `tiny-touch-target`, `low-contrast`, `missing-alt`
- `missing-viewport`, `blocking-js`
- + 27 outras regras

**Detector CLI:** `npx impeccable detect src/` com exit codes para CI gates.

### 3.3 Design Spells — Micro-interações

**URL:** https://designspells.com
**Conteúdo:** Curadoria de detalhes de UI que parecem mágica: animações, transições, easter eggs, interações únicas.
**Uso:** Referência para o módulo de motion design do harness.

### 3.4 SVGL — Logos SVG

**URL:** https://svgl.app
**Conteúdo:** Biblioteca de logos SVG de marcas para social proof sections.
**Integração:** MCP tool para buscar logos em landing pages com seção "Used by" / "Trusted by".
**Configuração:**
```json
{
  "svgl": {
    "type": "remote",
    "url": "https://mcp.svgl.app",
    "enabled": true
  }
}
```

### 3.5 KITTL — Assets Gráficos

**URL:** https://www.kittl.com
**Conteúdo:** Plataforma para criação de gráficos, prints e identidade visual.
**Uso:** Referência para geração de assets de branding em landing pages.

### 3.6 Cult UI — Componentes Curados

**URL:** https://www.cult-ui.com
**Conteúdo:** Componentes e padrões de UI curados.
**Uso:** Referência para componentes reutilizáveis em apps Next.js.

### 3.7 Untitled UI — UI Kits

**URL:** https://www.untitledui.com
**Conteúdo:** UI kits e componentes prontos.
**Uso:** Referência para componentes em apps Next.js.

### 3.8 SearXNG — Pesquisa na Internet

**URL:** https://searxng.org
**Conteúdo:** Metasearch engine privacy-respecting para pesquisa na web.
**Papel:** Pesquisa de inspiração visual, tendencias de design, referencias de mercado, e conteudo real para landing pages.
**Integracao:** MCP server para busca em tempo real durante o workflow.
**Configuracao:**
```json
{
  "searxng": {
    "type": "remote",
    "url": "https://mcp.searxng.org",
    "enabled": true
  }
}
```

**Casos de uso no harness:**
| Fase | Uso | Exemplo de query |
|------|-----|-----------------|
| Phase 1 | Pesquisar tendencias de design por industria | "SaaS analytics dashboard design trends 2026" |
| Phase 2 | Buscar referencias visuais de concorrentes | "Linear analytics landing page", "Vercel dashboard UI" |
| Phase 2 | Pesquisar conteudo real para copy | "analytics SaaS features", "server monitoring stats" |
| Phase 3 | Buscar inspiracao para micro-interacoes | "best scroll animations SaaS landing page" |
| Phase 3 | Encontrar logos de marcas para social proof | "top SaaS companies logos" |
| Phase 4 | Verificar se o design segue tendencias atuais | "modern SaaS landing page patterns 2026" |

**Ferramentas disponiveis:**
- `searxng_web_search` — busca na web com filtros (categoria, idioma, tempo, engines)
- `searxng_web_url_read` — extrai conteudo de URLs como markdown
- `searxng_search_suggestions` — sugestoes de autocomplete para refinar queries
- `searxng_instance_info` — descobrir capacidades e engines disponiveis

**Boas praticas:**
- Usar `time_range: "year"` para tendencias recentes de design
- Usar `categories: "images"` para inspiracao visual
- Usar `num_results: 10` para amostra representativa
- Combinar `searxng_web_search` + `searxng_web_url_read` para extrair conteudo de referencias

### 3.9 Resiliência de MCP Servers

Todos os MCP servers externos são best-effort. Se indisponíveis:

| Server   | Fallback                              |
|----------|---------------------------------------|
| Refero   | Usar `references/design-md/` local    |
| SVGL     | Placeholders rotulados + instrução    |
| SearXNG  | Conhecimento interno do modelo        |
| Unsplash | Placeholders rotulados com descrição  |
| Standby  | UI UX Pro Max ou conhecimento interno |

Comportamento:
- Tentar conexão com timeout de 5s.
- Se falhar, logar aviso e continuar com fallback.
- Nunca abortar o workflow por falha de MCP server.

### 3.10 Unsplash MCP — Imagens Stock

**Repositório:** `hellokaton/unsplash-mcp-server` (227⭐)
**URL:** https://github.com/hellokaton/unsplash-mcp-server
**Papel:** Buscar imagens de stock para hero sections e ilustrações.

**Configuração:**
```json
{
  "unsplash": {
    "type": "remote",
    "url": "https://mcp.unsplash.com",
    "enabled": true,
    "description": "Buscar imagens de stock para hero sections"
  }
}
```

**Uso no harness:**
- Phase 2: buscar imagens de referência para hero sections.
- Placeholders: quando imagem não disponível, usar placeholder rotulado com descrição da imagem ideal.

### 3.11 Standby.Design — Gerador de Design Tokens

**Repositório:** `KarstenKreh/Standby.Design`
**URL:** https://github.com/KarstenKreh/Standby.Design
**Papel:** Gerador de paletas OKLCH, type scales, spacing e tokens via MCP.

**Configuração:**
```json
{
  "standby-design": {
    "type": "remote",
    "url": "https://mcp.standby.design",
    "enabled": true,
    "description": "Gerar paletas OKLCH, type scales, e design tokens"
  }
}
```

**Uso no harness:**
- Phase 1: gerar paletas oklch acessíveis a partir de cor de marca.
- Fallback para UI UX Pro Max quando indisponível.

---

## 4. Arquitetura do Harness

### 4.1 Estrutura de Arquivos

```
.opencode/
├── opencode.json                    # Config principal do projeto
├── plugins/
│   └── design-harness.js            # Plugin de bootstrap
├── skills/
│   ├── design-entry/                # Skill de entrada (front door)
│   │   └── SKILL.md
│   ├── design-system-gen/           # Geração de design system
│   │   └── SKILL.md
│   ├── design-wireframe/            # Wireframes e exploração
│   │   └── SKILL.md
│   ├── design-nextjs/               # App Next.js especializado
│   │   └── SKILL.md
│   ├── design-landing/              # Landing page HTML
│   │   └── SKILL.md
│   ├── design-motion/               # Animações e motion
│   │   └── SKILL.md
│   ├── design-a11y/                 # Acessibilidade
│   │   └── SKILL.md
│   ├── design-perf/                 # Performance
│   │   └── SKILL.md
│   ├── design-handoff/              # Handoff para desenvolvimento
│   │   └── SKILL.md
│   └── design-convert/              # Otimização de conversão
│       └── SKILL.md
├── agents/
│   ├── design-verifier.md           # Verificador de qualidade estrutural
│   └── design-critic.md             # Crítico visual (anti-slop)
├── tools/
│   ├── preview.js                   # Server de preview local
│   ├── audit-slop.js                # Detector de anti-patterns
│   └── audit-vitals.js              # Auditoria Core Web Vitals
├── references/
│   ├── design-md/                   # DESIGN.md de marcas
│   │   ├── linear/
│   │   │   ├── DESIGN.md
│   │   │   └── preview.html
│   │   ├── stripe/
│   │   │   └── DESIGN.md
│   │   ├── vercel/
│   │   │   └── DESIGN.md
│   │   └── ...                      # (73 marcas total)
│   └── anti-patterns.json           # 45 regras do Impeccable
└── design-systems/                  # Design systems gerados (storage local)
    └── <project>/
        ├── MASTER.md
        ├── tokens/
        │   ├── colors.css
        │   ├── typography.css
        │   ├── spacing.css
        │   ├── shadows.css
        │   └── borders.css
        ├── components/
        │   ├── buttons.css
        │   ├── forms.css
        │   └── cards.css
        └── pages/
            ├── landing.md
            └── dashboard.md
```

**Nota sobre caminhos:** Design systems são persistidos em dois locais:
- `.opencode/design-systems/` — storage local, descoberto pelo plugin (reutilização entre projetos)
- `output/design-systems/` — output do projeto atual (entrega e handoff)
- O plugin `design-harness.js` escaneia `.opencode/design-systems/` para reutilização.
- O output final é copiado para `output/design-systems/` durante Phase 5 (entrega).

### 4.2 Estrutura de Output

```
output/
├── pages/                           # Landing pages HTML
│   └── <slug>/
│       ├── index.html
│       └── assets/
├── apps/                            # Apps Next.js
│   └── <name>/
│       ├── app/
│       ├── components/
│       └── ...
├── design-systems/                  # Design systems gerados (entrega)
│   └── <name>/
│       ├── MASTER.md
│       └── tokens/
├── wireframes/                      # Wireframes e explorações
│   └── <project>/
│       ├── wireframe-01.html
│       ├── wireframe-02.html
│       └── wireframe-03.html
├── design-md/                       # DESIGN.md exportados
│   └── <project>/
│       └── DESIGN.md
└── handoff/                         # Handoff para desenvolvimento
    └── <project>/
        ├── README.md
        ├── tokens/
        ├── components/
        ├── breakpoints.md
        ├── notes/
        └── DESIGN.md
```

### 4.3 Fluxo de Trabalho

```
User request: "Crie uma landing page para meu SaaS de analytics"
     │
     ▼
┌──────────────────────────────────────────────────────┐
│  design-entry skill (front door)                     │
│  1. Ground it in the subject: sujeito, audiencia, funcao│
│  2. Parse brief → extrair produto, público, tom      │
│  3. Carregar skills externas (UI UX Pro Max, Taste)  │
│  4. Determinar tipo: landing HTML vs app Next.js     │
│  5. Estabelecer dials de design                      │
│  6. Definir signature element                        │
└───────────────────────┬──────────────────────────────┘
                        │
                        ▼
┌──────────────────────────────────────────────────────┐
│  PHASE 1: Design System Generation                   │
│  • Pass 1 — Planejar: cores, tipo, layout, signature │
│  • Pass 2 — Criticar: verificar unicidade do plano   │
│  • UI UX Pro Max: gerar design system completo       │
│  • 161 reasoning rules → match produto → estilo      │
│  • BM25 search: cores, tipografia, efeitos           │
│  • Output: MASTER.md + tokens CSS em oklch           │
└───────────────────────┬──────────────────────────────┘
                        │
                        ▼
┌──────────────────────────────────────────────────────┐
│  PHASE 2: Referências Visuais                        │
│  • Buscar DESIGN.md similar em references/           │
│  • Consultar Refero MCP para inspiração              │
│  • SearXNG MCP: pesquisar tendencias + referencias   │
│  • Carregar Taste Skill (anti-slop rules)            │
│  • Configurar dials: VARIANCE, MOTION, DENSITY       │
└───────────────────────┬──────────────────────────────┘
                        │
                        ▼
┌──────────────────────────────────────────────────────┐
│  PHASE 3: Construção                                 │
│  • Seguir plano revisado exatamente                  │
│  • Roteamento: design-nextjs OU design-landing       │
│  • Gerar código com design system aplicado           │
│  • design-convert: otimização CRO (landings)         │
│  • Taste Skill: validar contra anti-slop             │
│  • Emil Skills: adicionar motion e micro-interações  │
│  • Auto-critica: regra Chanel (remover 1 acessorio)  │
│  • Iterar com comandos de vocabulário (/polish,etc)  │
└───────────────────────┬──────────────────────────────┘
                        │
                        ▼
┌──────────────────────────────────────────────────────┐
│  PHASE 4: Verificação                                │
│  • 4a. design-a11y: checklist WCAG 2.1 AA (13 itens) │
│  • 4b. design-perf: audit-vitals + Lighthouse targets│
│  • 4c. design-verifier: checklist estrutural (25)    │
│  • 4d. design-critic: auditoria visual (48+ regras)  │
│  • 4e. audit-slop: detecção determinística           │
│  • 4f. Se qualquer gate falhar → loop de correção    │
└───────────────────────┬──────────────────────────────┘
                        │
                        ▼
┌──────────────────────────────────────────────────────┐
│  PHASE 5: Entrega                                    │
│  • design-handoff: docs, tokens, componentes         │
│  • Preview local em :8289                            │
│  • DESIGN.md export (Google Stitch format)           │
└──────────────────────────────────────────────────────┘
```

### 4.4 Loop de Correção

Quando um gate da Phase 4 falha:

1. **Coletar issues:** Agregar todas as issues dos verificadores, ordenadas por severidade (critical > warning > info).

2. **Limitar escopo:** Corrigir no máximo 5 issues por iteração. Issues críticas primeiro.

3. **Executor:** O agente principal (não um subagente) aplica as correções diretamente nos arquivos de output.
   - Para issues de design: usar tokens do design system.
   - Para issues de a11y: seguir regras de `design-a11y`.
   - Para issues de performance: seguir regras de `design-perf`.
   - Para issues de cluster genérico: reavaliar o signature element e derivar do mundo do produto.

4. **Re-verificar:** Rodar apenas os verificadores que falharam (não o checklist completo).

5. **Limite de iterações:** Máximo 3 iterações de correção. Se ainda houver issues críticas após 3 tentativas:
   - Reportar ao usuário com explicação do impasse.
   - Sugerir mudanças de abordagem (ex: trocar componente, simplificar layout).
   - NÃO entregar com issues críticas.

6. **Warnings e info:** Não bloqueiam entrega. Listar no relatório final como "recomendações para iteração futura".

---

## 5. Skills Detalhadas

### 5.1 `design-entry` — Skill de Entrada

**Arquivo:** `.opencode/skills/design-entry/SKILL.md`

**Frontmatter:**
```yaml
---
name: design-entry
description: Use when building, designing, or refining any UI — landing pages, Next.js apps, dashboards, or component libraries. Routes to specialist design skills.
---
```

**Funções:**
0. **Scan design systems existentes:**
   Verificar `.opencode/design-systems/` e `output/design-systems/`.
   - Nenhum → prosseguir com geração.
   - Um encontrado e relevante → carregar automaticamente, anunciar.
   - Múltiplos → inferir pelo tipo de tarefa ou perguntar.
1. Parsear o brief do usuário
2. Determinar o tipo de output (landing HTML vs app Next.js vs redesign)
3. Ativar skills externas: UI UX Pro Max + Taste Skill
4. Rotear para a skill especializada correta
5. Estabelecer dials de design (VARIANCE, MOTION, DENSITY)

**Brief intake (perguntas estruturadas):**

O intake de 10 perguntas é obrigatório APENAS para projetos novos.

| Tipo de request        | Intake necessário |
|------------------------|-------------------|
| "Crie uma landing page" | Completo (10 perguntas) |
| "Gere um design system" | Reduzido (5: produto, público, estilo, cores, output) |
| "Melhore o hero"        | Zero (inferir do contexto) |
| "Redesigne o dashboard" | Reduzido (3: estilo alvo, manter/alterar, foco) |
| "/polish", "/typeset"   | Zero (comando direto) |

Detecção de tipo:
- Se o request menciona um arquivo ou seção existente → refinamento
- Se o request começa com "/" → comando direto
- Se o request é "crie", "gere", "construa" + novo produto → novo projeto

Perguntas para projeto novo:
- Produto / serviço
- Público-alvo
- Tom de voz (formal, casual, técnico, premium, playful)
- Estilo visual desejado (ou referência de marca)
- Tipo de output (landing page / Next.js app / dashboard)
- Seções / funcionalidades desejadas
- Paleta de cores (ou "gerar automaticamente")
- Nível de fidelidade (wireframe / mid-fi / hi-fi)
- Restrições técnicas (framework, bundle, sem JS)
- Métrica de sucesso (conversão, velocidade, acessibilidade)

**Ground it in the subject:**
Antes de qualquer design, ancorar no mundo real do produto:
- Nomear sujeito concreto, audiencia, e funcao unica da pagina
- Extrair do vernacular do produto: materiais, instrumentos, artefatos, linguagem
- O design deve refletir o mundo do sujeito, nao um template generico
- Definir o "signature element": o unico elemento memoravel que a pagina sera lembrada por

**Workflow de 2 passes:**
1. **Pass 1 — Planejar:** Criar plano compacto com:
   - Cores: 4-6 hex nomeadas com justificativa
   - Tipografia: 2+ roles (display characterful, body complementar, utilitario se necessario)
   - Layout: conceito em ASCII wireframe para comparar opcoes
   - Signature: elemento unico que incorpora o brief
2. **Pass 2 — Criticar o plano:** Antes de codar, revisar o plano:
   - Se alguma parte parece o que produziria para qualquer pagina similar → revisar
   - Executar prompt similar mentalmente para verificar se chega ao mesmo resultado
   - So codar apos confirmar unicidade relativa do plano
3. **Construir:** Seguir o plano revisado exatamente, derivando cada decisao de cor e tipo dele

**Regras anti-slop padrão:**
- Sem gradientes excessivos
- Sem emoji como ícones (a menos que a marca use)
- Sem cards com borda colorida lateral
- Sem fontes overused como padrão (Inter, Roboto, Arial sem justificativa)
- Sem backgrounds blue-purple genéricos
- Sem dados, stats ou ícones decorativos desnecessários

**Cluster awareness (padroes genéricos atuais):**
Os 3 clusters de design generico mais comuns que a IA produz independentemente do sujeito:
1. **Cream serif:** fundo creme (#F4F1EA) + serif display de alto contraste + accent terracota
2. **Dark acid:** fundo preto + accent verde acido ou vermilion
3. **Broadsheet:** layout estilo jornal + hairline rules + zero border-radius + colunas densas

Todos tres sao legitimos para alguns briefs, sao defaults, nao escolhas. Se o brief nao pede explicitamente, nao usar nenhum.

**Regras de escala:**
- Touch targets: mínimo 44px mobile
- Body copy: mínimo 16px
- Headlines hero: mínimo 48px desktop, 32px mobile

**Restricao e auto-critica:**
- Gastar ousadia em um lugar: o signature element e a coisa memoravel, tudo ao redor fica quieto e disciplinado
- Cortar decoracao que nao serve ao brief
- Regra Chanel: antes de entregar, olhar no espelho e remover um acessorio
- Criticar proprio trabalho durante a construcao, fazer screenshots se o ambiente suportar
- Nao correr risco e um risco em si!

**Copy como material de design:**
- Palavras sao design material, nao decoracao
- Escrever do lado do usuario final, nunca do lado do sistema
- Voz ativa como padrao: "Save changes", nao "Submit"
- Falhas e vazios sao momentos para direcao, nao humor
- Registro conversacional e sintonizado: verbos simples, sentence case, sem filler
- Cada elemento faz exatamente um trabalho: label labeliza, example demonstra, nada faz dupla funcao

**Aesthetic padrão (sem marca definida):**
- 1-3 fontes máximo
- Temperatura definida: warm, cool, ou neutral
- 0-2 accent colors em oklch
- Anunciar escolha no plano, manter consistência

**Inferência de dials:**
Quando o usuário não especifica dials explicitamente, inferir do contexto:

| Sinal no brief | VARIANCE | MOTION | DENSITY |
|----------------|----------|--------|---------|
| "SaaS", "dashboard", "analytics" | 5 | 3 | 7 |
| "landing page", "startup", "modern" | 7 | 5 | 4 |
| "portfolio", "creative", "agency" | 8 | 7 | 3 |
| "enterprise", "corporate", "fintech" | 4 | 2 | 6 |
| "minimal", "clean", "editorial" | 3 | 2 | 3 |
| Não especificado (default) | 5 | 4 | 5 |

### 5.2 `design-system-gen` — Geração de Design System

**Arquivo:** `.opencode/skills/design-system-gen/SKILL.md`

**Frontmatter:**
```yaml
---
name: design-system-gen
description: Use when creating a design system from scratch — colors, typography, spacing, components, tokens. Powered by UI UX Pro Max reasoning engine.
---
```

**Workflow:**
1. Executar UI UX Pro Max Design System Generator:
    ```
    python3 .opencode/skills/ui-ux-pro-max/scripts/search.py \
      "<product keywords>" --design-system -p "<project name>" --persist
    ```
1b. **Fallback se UI UX Pro Max indisponível:**
    Se o script falhar ou não estiver instalado:
    - Usar conhecimento interno do modelo para gerar design system.
    - Consultar DESIGN.md similares em `references/design-md/`.
    - Se SearXNG disponível, pesquisar tendências do setor.
    - Gerar MASTER.md com mesma estrutura, anotando "(generated without UI UX Pro Max)" no cabeçalho.
2. Output para `.opencode/design-systems/<project>/MASTER.md` e copiar para `output/design-systems/<project>/`
3. Gerar tokens CSS:
   - `tokens/colors.css` — cores em oklch
   - `tokens/typography.css` — scale tipográfica
   - `tokens/spacing.css` — scale de espaçamento
   - `tokens/shadows.css` — elevação
   - `tokens/borders.css` — radius e bordas
4. Buscar DESIGN.md similar em `references/design-md/` para validação
5. Aplicar regras anti-slop do Taste Skill

**Output esperado:**
```
output/design-systems/<name>/
├── MASTER.md            # Source of truth
├── tokens/
│   ├── colors.css       # oklch variables
│   ├── typography.css   # font scale
│   ├── spacing.css      # spacing scale
│   ├── shadows.css      # elevation
│   └── borders.css      # radius, borders
├── components/
│   ├── buttons.css      # button variants
│   ├── forms.css        # input styles
│   └── cards.css        # card styles
└── pages/
    ├── landing.md       # overrides para landing
    └── dashboard.md     # overrides para dashboard
```

**Hierarquia de retrieval:**
1. Verificar `design-systems/<project>/pages/<page>.md` (overrides específicos)
2. Se existir, aplicar overrides sobre o MASTER
3. Se não, usar `MASTER.md` exclusivamente

### 5.3 `design-wireframe` — Wireframes Rápidos

**Arquivo:** `.opencode/skills/design-wireframe/SKILL.md`

**Frontmatter:**
```yaml
---
name: design-wireframe
description: Use when exploring landing page layout options quickly — multiple rough wireframes, not polished output.
---
```

**Diretrizes:**
- Produzir 3-5 variações em dimensões significativas: layout, hierarquia, posição de CTA
- HTML + CSS inline, sem assets externos
- Placeholders claramente rotulados para imagens e ícones
- Focar em estrutura e fluxo, não em polimento visual
- Cada variação em arquivo separado: `wireframe-01.html`, etc.
- Output em `output/wireframes/<project>/`

### 5.4 `design-nextjs` — App Next.js

**Arquivo:** `.opencode/skills/design-nextjs/SKILL.md`

**Frontmatter:**
```yaml
---
name: design-nextjs
description: Use when building a Next.js application with App Router — component architecture, design system integration, server components, and responsive layouts.
---
```

**Stack padrão:**
- Next.js 15+ com App Router
- Tailwind CSS v4 (CSS-first configuration)
- shadcn/ui para componentes base
- Framer Motion para animações
- TypeScript estrito

**Nota:** Tailwind v4 usa CSS-first configuration. Design tokens são definidos como CSS custom properties no `@theme` block do `globals.css`, não em `tailwind.config.ts`.

**Estrutura de output:**
```
output/apps/<name>/
├── app/
│   ├── layout.tsx                    # Root layout com design tokens
│   ├── page.tsx                      # Landing / home
│   ├── [routes]/
│   ├── globals.css                   # @theme block com design tokens
│   └── components/
│       ├── ui/                       # Componentes base (shadcn)
│       ├── sections/                 # Seções de página
│       └── shared/                   # Componentes compartilhados
├── public/
├── package.json
└── tsconfig.json
```

**Configuração Tailwind v4 (globals.css):**
```css
@import "tailwindcss";
@theme {
  --color-primary: oklch(78% .12 82);
  --color-accent: oklch(65% .15 250);
  --font-display: "Space Grotesk", sans-serif;
  --font-body: "Geist Sans", system-ui, sans-serif;
  /* design tokens como CSS custom properties */
}
```

**Regras de design:**
- Design tokens como CSS custom properties no `:root`
- Componentes recebem props tipadas, não estilos inline
- Server Components por padrão, Client Components apenas quando necessário
- Animações via Framer Motion com regras do Emil Skills
- Imagens via `next/image` com dimensões explícitas
- Fontes via `next/font` com `display: 'swap'`
- **Nunca usar Inter como fonte padrão sem justificativa de marca** (ver regra `inter-default` anti-slop)

### 5.5 `design-landing` — Landing Page HTML

**Arquivo:** `.opencode/skills/design-landing/SKILL.md`

**Frontmatter:**
```yaml
---
name: design-landing
description: Use when building a high-fidelity landing page as a single HTML file — optimized for conversion, performance, and visual quality.
---
```

**Stack padrão:**
- HTML5 semântico
- Tailwind CSS via CDN (ou inline critical CSS)
- Vanilla JS mínimo (async/defer)
- Google Fonts com `display=swap`
- SVG icons via Lucide/Heroicons inline

**Seções padrão (conversão):**
1. **Hero** — headline + subheadline + CTA primary + visual
2. **Social Proof** — logos de clientes / números
3. **Features** — bento grid ou cards
4. **How It Works** — 3-4 passos
5. **Testimonials** — com foto, nome, cargo
6. **Pricing** — 3 tiers, highlight no recomendado
7. **FAQ** — accordion
8. **Final CTA** — repetição do CTA primary
9. **Footer** — links, legal, social

**Performance targets:**
- LCP < 2.5s
- CLS < 0.1
- INP < 200ms
- Total HTML + CSS < 50KB (sem imagens, sem Tailwind CDN runtime)
- Opção build: `@tailwindcss/cli` para CSS purgado (< 15KB total)
- Zero JS blocking

**Princípios de conversão:**
- Above the fold: headline + subheadline + CTA primary visíveis sem scroll
- CTA hierarchy: 1 primary CTA (cor accent), secundários muted
- Social proof: logos de clientes, depoimentos, números — sempre com contexto
- Copy formula: Problem → Agitation → Solution → Proof → CTA
- Form design: mínimo de campos, labels claros, inline validation
- Urgência: quando genuína, nunca fabricada

### 5.5.1 Estratégia de CSS

Duas opções, selecionadas pelo nível de fidelidade:

**Opção A — Single File (rápido):**
- Usar script CDN do Tailwind (`<script src="cdn.tailwindcss.com">`)
- O budget de 50KB refere-se ao HTML + CSS custom, não incluindo o runtime do Tailwind CDN
- Indicador: "CDN tailwind loaded" no relatório de performance

**Opção B — Build (produção):**
- Rodar `@tailwindcss/cli` para purgar classes não usadas
- Inserir CSS resultante inline no `<head>`
- Resultado: HTML + CSS tipicamente < 15KB
- Usar quando brief pede "production-ready" ou "zero dependencies"

### 5.6 `design-motion` — Animações

**Arquivo:** `.opencode/skills/design-motion/SKILL.md`

**Frontmatter:**
```yaml
---
name: design-motion
description: Use when adding, reviewing, or refining animations and micro-interactions — page transitions, hover states, scroll effects, and motion design.
---
```

**Regras (baseadas em Emil Kowalski skills):**

| Contexto | Easing | Duração | Spring |
|----------|--------|---------|--------|
| Enter animation | ease-out | 300-500ms | stiffness: 200, damping: 15 |
| Exit animation | ease-in | 200-300ms | stiffness: 300, damping: 20 |
| Hover state | ease-out | 150-200ms | — |
| Page transition | ease-in-out | 400-600ms | stiffness: 150, damping: 20 |
| Micro-interaction | spring | 200-400ms | stiffness: 300, damping: 15 |
| Scroll reveal | ease-out | 500-800ms | — |

**Anti-patterns de animação:**
- Nunca `ease-in` para enter (parece que o elemento está "caindo")
- Nunca `linear` para UI (parece robótico)
- Nunca animar mais de 2 propriedades simultaneamente
- Sempre respeitar `prefers-reduced-motion`
- Nunca usar animações para transmitir informação crítica

### 5.7 `design-a11y` — Acessibilidade

**Arquivo:** `.opencode/skills/design-a11y/SKILL.md`

**Frontmatter:**
```yaml
---
name: design-a11y
description: Use when auditing or fixing accessibility — WCAG 2.1 AA compliance, keyboard navigation, screen reader support, and color contrast.
---
```

**Checklist automático:**
- Contraste mínimo 4.5:1 (texto normal), 3:1 (texto grande)
- Touch targets: mínimo 44px
- Body copy: mínimo 16px
- Headlines hero: mínimo 48px desktop, 32px mobile
- Keyboard navigation completa
- Focus indicators visíveis
- Alt text descritivo
- ARIA labels em ícones funcionais
- Skip links para navegação
- `lang` attribute no `<html>`
- Sem auto-play de mídia
- `prefers-reduced-motion` respeitado
- Sem dependência exclusiva de cor para transmitir informação

### 5.8 `design-perf` — Performance

**Arquivo:** `.opencode/skills/design-perf/SKILL.md`

**Frontmatter:**
```yaml
---
name: design-perf
description: Use when optimizing performance — Core Web Vitals, bundle size, image optimization, font loading, and render-blocking resources.
---
```

**Diretrizes:**
- Inline critical CSS, defer o resto
- Imagens: `loading="lazy"`, dimensões explícitas, formatos modernos (WebP/AVIF)
- Fontes: `font-display: swap`, preconnect, subset
- JS: mínimo, async/defer, sem blocking
- Target: < 50KB total (HTML + CSS inline) sem imagens
- Next.js: `next/image`, `next/font`, server components
- Lighthouse score: 95+ em todas as categorias

### 5.9 `design-handoff` — Handoff para Desenvolvimento

**Arquivo:** `.opencode/skills/design-handoff/SKILL.md`

**Frontmatter:**
```yaml
---
name: design-handoff
description: Use when preparing a finished design for developer handoff — documentation, tokens, components, and implementation notes.
---
```

**Output em `output/<project>/handoff/`:**
- `README.md` — resumo do design, decisões, trade-offs
- `tokens/` — variáveis CSS extraídas (copiar do design system)
- `components/` — lista de componentes com props e variantes
- `breakpoints.md` — comportamento responsivo por breakpoint
- `notes/` — caveats, dependências, instruções de deploy
- `DESIGN.md` — versão portátil (Google Stitch format)

**Workflow:**
1. Escanear output final e extrair design tokens usados.
2. Listar todos os componentes com descrição, props, e variantes.
3. Documentar comportamento responsivo (mobile → desktop).
4. Gerar DESIGN.md portátil compatível com outros agentes.
5. Incluir checklist de implementação para devs.

### 5.10 `design-convert` — Otimização de Conversão (CRO)

**Arquivo:** `.opencode/skills/design-convert/SKILL.md`

**Nota de nomeacao:** `design-convert` refere-se a "conversion rate optimization" (CRO), nao a conversao de formato.

**Frontmatter:**
```yaml
---
name: design-convert
description: Use when optimizing a page for conversion rate (CRO) — CTA placement, copywriting, social proof, form design, urgency, or A/B test variants.
---
```

**Princípios:**
- Above the fold: headline + subheadline + CTA primary visíveis sem scroll
- CTA hierarchy: 1 primary CTA (cor accent), secundários muted
- Social proof: logos, depoimentos, números — sempre com contexto
- Copy formula: Problem → Agitation → Solution → Proof → CTA
- Form design: mínimo de campos, labels claros, inline validation
- Urgência: quando genuína, nunca fabricada
- Variações A-B: testar headline, CTA copy, cor do botão, posição do form

**Quando usar:**
- Explicitamente solicitado: "otimize para conversão"
- Como sub-fase da Phase 3 para landing pages
- Em iterações: "a página não converte, melhore"

---

## 6. Agentes

### 6.1 `design-verifier` — Verificador de Qualidade

**Arquivo:** `.opencode/agents/design-verifier.md`

**Frontmatter:**
```yaml
---
name: design-verifier
description: Verifies design output against the design brief, quality checklist, and anti-slop rules.
mode: subagent
color: red
---
```

**Checklist de verificação (25 itens):**

| # | Categoria | Item | Severidade | Determinístico |
|---|-----------|------|------------|----------------|
| 1 | HTML | Tags HTML válidas (tags fechadas, atributos com aspas) | critical | Sim (regex/htmllint) |
| 2 | HTML | Meta tags essenciais (viewport, description, title, OG) | critical | Sim (regex) |
| 3 | Conversão | CTA primary acima da dobra | critical | Nao (requer layout awareness) |
| 4 | Conversão | Copy segue fórmula Problem → Solution → CTA | warning | Nao (semantico) |
| 5 | Conversão | Social proof contextualizado | warning | Nao (semantico) |
| 6 | A11y | Contraste WCAG AA em todos os textos | critical | Nao (requer calculo de cor) |
| 7 | A11y | Keyboard navigation completa | critical | Nao (requer teste interativo) |
| 8 | A11y | Alt text em imagens informativas | critical | Sim (regex) |
| 9 | A11y | Focus indicators visíveis | warning | Nao (requer inspecao CSS) |
| 10 | Perf | CSS critical inline | warning | Sim (regex) |
| 11 | Perf | Imagens com dimensões explícitas | critical | Sim (regex) |
| 12 | Perf | Sem JS blocking | warning | Sim (regex) |
| 13 | Perf | Total < 50KB (sem imagens) | info | Sim (file size) |
| 14 | Design | Design system aplicado consistentemente | critical | Nao (semantico) |
| 15 | Design | Sem gradientes excessivos | warning | Sim (audit-slop) |
| 16 | Design | Sem emoji como ícones | warning | Sim (audit-slop) |
| 17 | Design | Sem cards com borda lateral colorida | warning | Sim (audit-slop) |
| 18 | Design | Sem backgrounds blue-purple genéricos | warning | Sim (audit-slop) |
| 19 | Design | Sem fontes overused como padrão | info | Sim (audit-slop) |
| 20 | Design | SVGs de ícones (Heroicons/Lucide) | warning | Nao (semantico) |
| 21 | Motion | Easing correto (ease-out para enter) | warning | Sim (audit-slop) |
| 22 | Motion | Durações dentro dos limites | info | Nao (semantico) |
| 23 | Motion | prefers-reduced-motion respeitado | critical | Sim (audit-slop) |
| 24 | Responsivo | Breakpoints: 375px, 768px, 1024px, 1440px | critical | Nao (requer render) |
| 25 | Responsivo | Touch targets >= 44px mobile | critical | Nao (requer inspecao CSS) |

**Comportamento:**
- Se tudo passar: silencioso
- Se algo falhar: lista específica de issues com severidade
- Nunca refazer o trabalho — apenas reportar
- Exit code 1 se houver issues críticas

**Permissões:** `bash: deny`, `file_edits: deny`

**Nota sobre determinismo:** Os itens marcados como "Nao" nao sao verificaveis por regex e devem ser auditados pelo design-critic (agente semantico) ou pelo design-verifier com raciocinio LLM. Os itens "Sim" podem ser verificados por `audit-slop.js` ou checks determinísticos.

### 6.2 `design-critic` — Crítico Visual

**Arquivo:** `.opencode/agents/design-critic.md`

**Frontmatter:**
```yaml
---
name: design-critic
description: Visual critic that audits design output against Taste Skill and Impeccable anti-slop rules.
mode: subagent
color: orange
---
```

**Função:** Auditoria visual baseada em 45+ regras anti-slop combinadas do Impeccable e Taste Skill.

**Regras do Impeccable (45):**
- `gradient-text` — texto com gradiente
- `side-stripe-border` — borda lateral colorida em cards
- `ai-color-palette` — paleta de cores genérica de IA
- `ghost-card` — cards com fundo transparente e borda sutil
- `over-rounding` — border-radius excessivo
- `purple-pink-gradient` — gradientes purple/pink
- `emoji-as-icon` — emoji usado como ícone funcional
- `inter-default` — Inter como fonte padrão sem justificativa
- `blue-purple-bg` — background blue-purple genérico
- `decorative-stats` — números decorativos sem contexto
- + 35 outras regras

**Regras do Taste Skill:**
- Em-dash ban em copy
- Placeholders rotulados, nunca SVGs complexos decorativos
- Hierarquia tipográfica clara
- Espaçamento consistente
- Contraste adequado

**Cluster awareness (3 looks genéricos atuais):**
O detector deve identificar quando o design caiu em um dos 3 clusters padrão da IA:
| Cluster | Sinais | Acao |
|---------|--------|------|
| `cream-serif` | Fundo #F4F1EA ou similar + serif display + terracota | Sugerir alternativa alinhada ao sujeito |
| `dark-acid` | Fundo preto + accent verde acido/vermilion | Sugerir paleta derivada do mundo do produto |
| `broadsheet` | Hairline rules + zero radius + colunas densas estilo jornal | Sugerir layout com mais personalidade |

**Auto-critica do plano:**
- Verificar se o plano de design e unico para o brief ou seria valido para qualquer produto similar
- Se o signature element nao estiver claro, bloquear construcao ate definir
- Verificar se copy e material de design ou preenchimento generico
- Regra Chanel: antes de aprovar, identificar o que remover

**Output:** Relatório de issues com:
- Localização (arquivo:linha)
- Regra violada
- Sugestão de correção
- Severidade (critical / warning / info)

**Permissões:** `bash: deny`, `file_edits: deny`

---

## 7. Custom Tools

### 7.1 `preview.js` — Server de Preview

**Arquivo:** `.opencode/tools/preview.js`

**Descrição:** Inicia server local em `:8289` para preview de landing pages e apps Next.js.

**Funcionalidades:**
- Serve conteúdo de `output/` em `http://localhost:8289`
- Suporta página específica via parâmetro `page`
- Hot-reload para mudanças em arquivos HTML (via `fs.watch`)
- Interface com navegação entre páginas geradas
- Para apps Next.js: executa `npm run dev` em background no app especificado

**Uso:**
```javascript
// Via tool
preview({ page: "saas-analytics" })
// → http://localhost:8289/pages/saas-analytics/

preview()
// → http://localhost:8289/ (lista todas as páginas)
```

**Implementação:**
```javascript
import { tool } from "@opencode-ai/plugin";
import http from "http";
import fs from "fs";
import path from "path";
import { URL } from "url";

const MIME_TYPES = {
  ".html": "text/html",
  ".css": "text/css",
  ".js": "application/javascript",
  ".json": "application/json",
  ".svg": "image/svg+xml",
  ".png": "image/png",
  ".webp": "image/webp",
};

function createIndexPage(outputDir) {
  const pages = [];
  const apps = [];

  const pagesDir = path.join(outputDir, "pages");
  if (fs.existsSync(pagesDir)) {
    for (const slug of fs.readdirSync(pagesDir)) {
      pages.push({ name: slug, href: `/pages/${slug}/index.html` });
    }
  }

  const appsDir = path.join(outputDir, "apps");
  if (fs.existsSync(appsDir)) {
    for (const name of fs.readdirSync(appsDir)) {
      apps.push({ name, href: `/apps/${name}/` });
    }
  }

  return `<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Design Preview</title>
  <style>
    body { font-family: system-ui; max-width: 600px; margin: 2rem auto; padding: 0 1rem; }
    a { display: block; padding: 0.5rem 0; color: #111; text-decoration: none; }
    a:hover { color: #666; }
    h2 { margin-top: 2rem; }
  </style>
</head>
<body>
  <h1>Design Preview</h1>
  <h2>Landing Pages</h2>
  ${pages.map(p => `<a href="${p.href}">${p.name}</a>`).join("\n") || "<p>Nenhuma página gerada.</p>"}
  <h2>Apps Next.js</h2>
  ${apps.map(a => `<a href="${a.href}">${a.name}</a>`).join("\n") || "<p>Nenhum app gerado.</p>"}
</body>
</html>`;
}

export default tool({
  description: "Start a local preview server for design output on port 8289.",
  args: {
    page: { type: "string", optional: true, description: "Specific page slug to preview." },
  },
  async execute(args) {
    const outputDir = path.resolve(process.cwd(), "output");
    const port = 8289;

    const server = http.createServer((req, res) => {
      const url = new URL(req.url, `http://localhost:${port}`);
      let filePath = path.join(outputDir, url.pathname);

      if (!filePath.startsWith(outputDir)) {
        res.writeHead(403);
        res.end("Forbidden");
        return;
      }

      if (url.pathname === "/" || url.pathname === "/index.html") {
        res.writeHead(200, { "Content-Type": "text/html" });
        res.end(createIndexPage(outputDir));
        return;
      }

      if (!fs.existsSync(filePath)) {
        filePath = path.join(outputDir, "index.html");
      }

      const ext = path.extname(filePath);
      const contentType = MIME_TYPES[ext] || "text/plain";

      try {
        const content = fs.readFileSync(filePath);
        res.writeHead(200, { "Content-Type": contentType });
        res.end(content);
      } catch {
        res.writeHead(404);
        res.end("Not found");
      }
    });

    // Hot-reload: watch output/ for changes
    const watcher = fs.watch(outputDir, { recursive: true }, (eventType, filename) => {
      if (eventType === "change" && filename) {
        console.log(`[preview] Reloading: ${filename}`);
      }
    });

    server.listen(port, () => {
      const baseUrl = `http://localhost:${port}`;
      const url = args.page
        ? `${baseUrl}/pages/${args.page}/`
        : baseUrl;
      console.log(`Preview server started at ${url}`);
    });

    return `Preview server started at http://localhost:${port}${args.page ? `/pages/${args.page}/` : ""}`;
  },
});
```

### 7.2 `audit-slop.js` — Detector Anti-Slop

**Arquivo:** `.opencode/tools/audit-slop.js`

**Descrição:** Detector determinístico de anti-patterns visuais baseado em 45+ regras do Impeccable + regras do Taste Skill.

**Uso:**
```bash
node .opencode/tools/audit-slop.js --dir ./output/
```

**Regras implementadas (20+):**

| Regra | Descrição | Detecção |
|-------|-----------|----------|
| `gradient-text` | Texto com gradiente | `bg-clip-text text-transparent bg-gradient-to-r` |
| `side-stripe-border` | Borda lateral colorida em cards | `"type": "file"` — verificar border-[rltb] + border-{cor} no arquivo |
| `ai-color-palette` | Paleta genérica de IA | `from-purple-600 via-pink-500 to-orange-400` |
| `ghost-card` | Card com fundo transparente + borda sutil | `bg-transparent border border-gray-200` |
| `over-rounding` | Border-radius excessivo | `rounded-3xl` em containers grandes |
| `purple-pink-gradient` | Gradientes purple/pink | `from-purple-400 to-pink-400` |
| `emoji-as-icon` | Emoji como ícone funcional | Ranges Unicode `\u{1F300}-\u{1F9FF}`, `\u{2600}-\u{26FF}`, `\u{2700}-\u{27BF}` |
| `inter-default` | Inter como fonte padrão sem justificativa | `font-family: Inter` sem contexto de marca |
| `blue-purple-bg` | Background blue-purple genérico | `bg-gradient-to-br from-blue-900 to-purple-900` |
| `decorative-stats` | Números decorativos sem contexto | `99.9% uptime` sem fonte |
| `excessive-shadow` | Shadow pesado sem hierarquia | `shadow-2xl` em todos os cards |
| `no-hover-state` | Elemento clicável sem hover | `"type": "file"` — verificar cursor-pointer sem hover: no arquivo |
| `linear-easing` | Easing linear em UI | `transition: all 0.3s linear` |
| `ease-in-enter` | Ease-in para enter animation | `animation: fadeIn ease-in` |
| `missing-reduced-motion` | Sem prefers-reduced-motion | `"type": "file"` — verificar arquivo inteiro por `prefers-reduced-motion` |
| `tiny-touch-target` | Touch target < 44px | `"type": "file"` — verificar alturas < 44px em elementos clicaveis |
| `low-contrast` | Contraste < 4.5:1 | `"type": "visual"` — auditado pelo design-critic |
| `missing-alt` | Imagem sem alt text | `<img src="...">` sem `alt` |
| `missing-viewport` | Sem meta viewport | `"type": "file"` — verificar se `<meta name="viewport">` existe |
| `blocking-js` | Script blocking no head | `<script src="...">` sem async/defer |

**Output JSON:**
```json
{
  "issues": [
    {
      "file": "src/components/Hero.tsx:42",
      "rule": "gradient-text",
      "severity": "critical",
      "message": "Text gradient detected. Use solid color from design system.",
      "suggestion": "Replace gradient with oklch(78% .12 82) from tokens/colors.css"
    },
    {
      "file": "src/components/Card.tsx:8",
      "rule": "side-stripe-border",
      "severity": "warning",
      "message": "Side stripe border on card. Use elevation instead.",
      "suggestion": "Replace border-l-4 with shadow-sm and bg-white/80"
    }
  ],
  "total": 2,
  "critical": 1,
  "warnings": 1
}
```

**Exit codes:** 0 = clean, 1 = issues found

**Tipos de regras:**
- `"regex"` — verificação linha por linha (default)
- `"file"` — análise do conteúdo completo do arquivo
- `"visual"` — auditado pelo design-critic, não por regex

**Implementação:**
```javascript
import { tool } from "@opencode-ai/plugin";
import fs from "fs";
import path from "path";

const ANTI_PATTERNS = [
  {
    rule: "gradient-text",
    pattern: /bg-clip-text\s+text-transparent\s+bg-gradient/,
    type: "regex",
    severity: "critical",
    message: "Text gradient detected. Use solid color from design system.",
  },
  {
    rule: "side-stripe-border",
    pattern: /border-[rltb]-\d+\s+border-(?!white|black|transparent)/,
    type: "regex",
    severity: "warning",
    message: "Side stripe border on card. Use elevation instead.",
  },
  {
    rule: "missing-reduced-motion",
    pattern: /animation|transition/,
    type: "file",
    severity: "critical",
    message: "Animations without prefers-reduced-motion.",
    check: (content) => {
      const hasAnimation = /animation|transition/.test(content);
      const hasReducedMotion = /prefers-reduced-motion/.test(content);
      return hasAnimation && !hasReducedMotion;
    },
  },
      // ... mais regras
    ];

    // Parse check function strings into actual functions
    const parseCheck = (fnStr) => {
      if (typeof fnStr === 'function') return fnStr;
      if (!fnStr) return null;
      try {
        return new Function('content', `return ${fnStr}`);
      } catch {
        return null;
      }
    };

    function scanDirectory(dir, pattern) {
  const results = [];
  function walk(currentDir) {
    for (const entry of fs.readdirSync(currentDir, { withFileTypes: true })) {
      const fullPath = path.join(currentDir, entry.name);
      if (entry.isDirectory()) {
        if (entry.name === "node_modules" || entry.name === ".next" || entry.name === ".git") continue;
        walk(fullPath);
      } else if (pattern.test(entry.name)) {
        results.push(fullPath);
      }
    }
  }
  walk(dir);
  return results;
}

export default tool({
  description: "Scan files for AI-generated design anti-patterns (slop detection).",
  args: {
    dir: { type: "string", description: "Directory to scan for anti-patterns." },
    validateHtml: { type: "boolean", optional: true, description: "Run htmllint validation." },
  },
  async execute(args) {
    const issues = [];
    const files = scanDirectory(args.dir, /\.(html|tsx|jsx|css)$/);

    for (const file of files) {
      const content = fs.readFileSync(file, "utf8");
      const lines = content.split("\n");

      // Optional HTML validation
      if (args.validateHtml && file.endsWith(".html")) {
        try {
          const { execSync } = await import("child_process");
          execSync(`npx htmllint ${file}`, { stdio: "pipe" });
        } catch (err) {
          issues.push({
            file,
            rule: "html-invalid",
            severity: "critical",
            message: err.stdout?.toString() || "Invalid HTML",
          });
        }
      }

      for (const { rule, pattern, type, severity, message, check } of ANTI_PATTERNS) {
        if (type === "file") {
          const checkFn = parseCheck(check);
          if (checkFn && checkFn(content)) {
            issues.push({ file, rule, severity, message });
          }
        } else if (type !== "visual" && pattern) {
          for (let i = 0; i < lines.length; i++) {
            if (pattern.test(lines[i])) {
              issues.push({
                file: `${file}:${i + 1}`,
                rule,
                severity,
                message,
              });
            }
          }
        }
      }
    }

    const result = {
      issues,
      total: issues.length,
      critical: issues.filter(i => i.severity === "critical").length,
      warnings: issues.filter(i => i.severity === "warning").length,
    };

    return JSON.stringify(result, null, 2);
  },
});
```

### 7.3 `audit-vitals.js` — Auditoria Core Web Vitals

**Arquivo:** `.opencode/tools/audit-vitals.js`

**Descrição:** Audita HTML/Next.js para riscos de LCP, CLS e INP.

**Checks:**
| Check | Métrica | Risco |
|-------|---------|-------|
| Missing viewport meta | CLS | critical |
| Imagens sem dimensões | CLS | critical |
| Fontes externas sem `font-display: swap` | LCP | warning |
| Inline scripts | INP | warning |
| Tamanho total do arquivo | LCP | info |
| Recursos blocking (CSS/JS no head) | LCP | warning |

**Implementação:**
```javascript
import { tool } from "@opencode-ai/plugin";

export default tool({
  description: "Audit a landing page HTML file for Core Web Vitals risks: LCP candidates, CLS risks, render-blocking resources.",
  args: {
    file: { type: "string", description: "Path to the HTML file to audit." },
  },
  async execute(args) {
    const fs = await import("fs");
    const content = fs.readFileSync(args.file, "utf8");
    const issues = [];

    // Check for missing viewport meta
    if (!content.includes('name="viewport"')) {
      issues.push({ rule: "missing-viewport", severity: "critical", message: "MISSING: viewport meta tag" });
    }

    // Check for images without dimensions (CLS risk)
    const imgTags = content.match(/<img[^>]*>/g) || [];
    for (const img of imgTags) {
      if (!img.includes("width=") || !img.includes("height=")) {
        issues.push({ rule: "img-no-dimensions", severity: "critical", message: "CLS RISK: img without explicit width/height" });
      }
    }

    // Check for external fonts without swap
    if (content.includes('@import') && !content.includes('font-display: swap')) {
      issues.push({ rule: "fonts-no-swap", severity: "warning", message: "LCP RISK: external fonts without font-display: swap" });
    }

    // Check for inline scripts
    if (content.match(/<script[^>]*>(?![\s]*<\/script>)/)) {
      issues.push({ rule: "inline-script", severity: "warning", message: "INP RISK: inline script detected" });
    }

    // Estimate size
    const sizeKB = (new Blob([content]).size / 1024).toFixed(1);
    if (parseFloat(sizeKB) > 50) {
      issues.push({ rule: "file-size", severity: "info", message: `SIZE WARNING: HTML is ${sizeKB}KB (target < 50KB without images)` });
    }

    // Check for blocking resources
    const blockingLinks = content.match(/<link[^>]*rel="stylesheet"[^>]*>/g) || [];
    if (blockingLinks.length > 0 && !content.includes("media=\"print\"") && !content.includes("rel=\"preload\"")) {
      issues.push({ rule: "blocking-css", severity: "warning", message: "LCP RISK: render-blocking CSS detected" });
    }

    if (issues.length === 0) {
      return `Audit passed. File size: ${sizeKB}KB. No critical issues found.`;
    }

    return `Audit found ${issues.length} issue(s):\n${issues.map(i => `[${i.severity.toUpperCase()}] ${i.message}`).join("\n")}\n\nFile size: ${sizeKB}KB`;
  },
});
```

---

## 8. Configuração

### 8.1 `opencode.json`

**Arquivo:** `.opencode/opencode.json`

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "anthropic/claude-sonnet-4-5",
  "plugin": ["design-harness"],
  "instructions": ["AGENTS.md"],
  "skills": {
    "paths": [
      ".opencode/skills",
      ".opencode/skills/ui-ux-pro-max"
    ]
  },
  "mcp": {
    "refero": {
      "type": "remote",
      "url": "https://mcp.refero.design",
      "enabled": true,
      "timeout": 5000,
      "fallback": "local",
      "description": "Buscar 2000+ design systems de produtos reais"
    },
    "svgl": {
      "type": "remote",
      "url": "https://mcp.svgl.app",
      "enabled": true,
      "timeout": 5000,
      "fallback": "placeholder",
      "description": "Buscar logos SVG para social proof"
    },
    "searxng": {
      "type": "remote",
      "url": "https://mcp.searxng.org",
      "enabled": true,
      "timeout": 5000,
      "fallback": "internal",
      "description": "Pesquisa na web: tendencias de design, referencias visuais, conteudo real"
    },
    "unsplash": {
      "type": "remote",
      "url": "https://mcp.unsplash.com",
      "enabled": true,
      "timeout": 5000,
      "fallback": "placeholder",
      "description": "Buscar imagens de stock para hero sections"
    },
    "standby-design": {
      "type": "remote",
      "url": "https://mcp.standby.design",
      "enabled": true,
      "timeout": 5000,
      "fallback": "internal",
      "description": "Gerar paletas OKLCH, type scales, e design tokens"
    }
  },
  "references": {
    "landing-patterns": {
      "repository": "land-book/awesome-landing-pages",
      "branch": "main",
      "description": "Referência de padrões de landing pages de alta conversão"
    }
  },
  "agent": {
    "design-verifier": {
      "permission": {
        "bash": "deny",
        "file_edits": "deny"
      }
    },
    "design-critic": {
      "permission": {
        "bash": "deny",
        "file_edits": "deny"
      }
    }
  },
  "permission": {
    "skill": {
      "design-*": "allow"
    }
  }
}
```

### 8.2 Plugin de Bootstrap

**Arquivo:** `.opencode/plugins/design-harness.js`

**Função:** Carrega automaticamente o contexto do harness ao iniciar o OpenCode.

**Responsabilidades:**
1. Registrar path de skills do harness
2. Carregar skill de entrada (`design-entry`) como system prompt
3. Inicializar UI UX Pro Max (`uipro init --ai opencode`)
4. Registrar skills externas: Taste Skill + Emil Skills
5. Configurar MCP servers (Refero, SVGL, SearXNG)

**Implementação:**
```javascript
import path from 'path';
import fs from 'fs';
import { fileURLToPath } from 'url';

const __dirname = path.dirname(fileURLToPath(import.meta.url));

const extractFrontmatter = (content) => {
  const match = content.match(/^---\n([\s\S]*?)\n---\n([\s\S]*)$/);
  if (!match) return { frontmatter: {}, content };
  const frontmatter = {};
  for (const line of match[1].split('\n')) {
    const idx = line.indexOf(':');
    if (idx > 0) {
      frontmatter[line.slice(0, idx).trim()] = line.slice(idx + 1).trim();
    }
  }
  return { frontmatter, content: match[2] };
};

export const DesignHarnessPlugin = async ({ directory }) => {
  const skillsDir = path.resolve(__dirname, '../skills');
  const bootstrapPath = path.join(skillsDir, 'design-entry', 'SKILL.md');

  const getBootstrap = () => {
    if (!fs.existsSync(bootstrapPath)) return null;
    const { content } = extractFrontmatter(fs.readFileSync(bootstrapPath, 'utf8'));
    return `<EXTREMELY_IMPORTANT>
You have Design Harness loaded. The design-entry skill is ALREADY LOADED.
Do NOT use the skill tool to load "design-entry" again.

${content}
</EXTREMELY_IMPORTANT>`;
  };

  return {
    config: async (config) => {
      config.skills = config.skills || {};
      config.skills.paths = config.skills.paths || [];
      if (!config.skills.paths.includes(skillsDir)) {
        config.skills.paths.push(skillsDir);
      }
    },
    'experimental.chat.system.transform': async (_input, output) => {
      const bootstrap = getBootstrap();
      if (bootstrap) {
        (output.system ||= []).push(bootstrap);
      }

      // Design system discovery
      const dsDir = path.resolve(__dirname, '../design-systems');
      if (fs.existsSync(dsDir)) {
        const systems = fs.readdirSync(dsDir).filter(f =>
          fs.statSync(path.join(dsDir, f)).isDirectory()
        );
        if (systems.length > 0) {
          const systemsInfo = `\n<DESIGN_SYSTEMS_AVAILABLE>
The following design systems are available for reuse:
${systems.map(s => `- ${s} (.opencode/design-systems/${s}/MASTER.md)`).join('\n')}
Check if any match the current project before generating a new one.
</DESIGN_SYSTEMS_AVAILABLE>`;
          (output.system ||= []).push(systemsInfo);
        }
      }
    },
  };
};
```

### 8.3 `AGENTS.md`

**Arquivo:** `AGENTS.md`

```markdown
# OpenCode Design Harness

Este projeto usa o Design Harness para criação de interfaces de alta qualidade.

## Estrutura de saída

- `./output/pages/<slug>/` — landing pages HTML
- `./output/apps/<name>/` — apps Next.js
- `./output/design-systems/<name>/` — design systems
- `./output/wireframes/` — wireframes e explorações
- `./output/design-md/` — DESIGN.md exportados

## Comandos rápidos

- "Crie uma landing page para [produto]" → fluxo completo
- "Gere um design system para [marca]" → design-system-gen
- "Explore 3 layouts para [seção]" → design-wireframe
- "Otimize a animação de [componente]" → design-motion
- "Verifique acessibilidade" → design-a11y
- "Audite performance" → design-perf

## Referências

- DESIGN.md de marcas: `.opencode/references/design-md/`
- Anti-patterns: `.opencode/references/anti-patterns.json`
- Design Spells: https://designspells.com
- Refero: https://styles.refero.design
- SearXNG: https://searxng.org (pesquisa na web)
```

### 8.4 `anti-patterns.json`

**Arquivo:** `.opencode/references/anti-patterns.json`

**Nota:** Este é o single source of truth para regras anti-slop. As regras listadas em Secao 6.1 (design-verifier), Secao 6.2 (design-critic) e Secao 12 (Anti-Patterns) devem referenciar este arquivo, nao duplicar as regras.

```json
{
  "version": "1.0",
  "source": "impeccable.style + taste-skill + anthropic-frontend-design",
  "rules": [
    {
      "id": "gradient-text",
      "severity": "critical",
      "description": "Text with gradient background (bg-clip-text text-transparent bg-gradient)",
      "pattern": "bg-clip-text text-transparent bg-gradient",
      "suggestion": "Use solid color from design system tokens"
    },
    {
      "id": "side-stripe-border",
      "severity": "warning",
      "description": "Colored side border on cards (border-[rltb]-N border-{color})",
      "pattern": null,
      "type": "file",
      "check": "(content) => { const hasSideBorder = /border-[rltb]-\\d+/.test(content); const hasColorBorder = /border-(red|blue|green|yellow|purple|pink|orange|indigo|teal|cyan|rose|amber|emerald|fuchsia|violet|lime|sky|)-/.test(content); return hasSideBorder && hasColorBorder; }",
      "suggestion": "Use elevation (shadow) instead of colored borders"
    },
    {
      "id": "ai-color-palette",
      "severity": "critical",
      "description": "Generic AI color palette (purple-pink-orange gradients)",
      "pattern": "from-purple-600 via-pink-500 to-orange-400",
      "suggestion": "Use brand-aligned palette from design system"
    },
    {
      "id": "ghost-card",
      "severity": "warning",
      "description": "Transparent card with subtle border",
      "pattern": "bg-transparent border border-gray",
      "suggestion": "Use solid background with shadow for elevation"
    },
    {
      "id": "over-rounding",
      "severity": "warning",
      "description": "Excessive border-radius on large containers",
      "pattern": "rounded-3xl",
      "suggestion": "Use rounded-lg or rounded-xl for containers"
    },
    {
      "id": "purple-pink-gradient",
      "severity": "critical",
      "description": "Generic purple-to-pink gradient",
      "pattern": "from-purple-400 to-pink-400",
      "suggestion": "Use brand colors from design system"
    },
    {
      "id": "emoji-as-icon",
      "severity": "warning",
      "description": "Emoji used as functional icon instead of SVG",
      "pattern": "[\\u{1F300}-\\u{1F9FF}]|[\\u{2600}-\\u{26FF}]|[\\u{2700}-\\u{27BF}]",
      "type": "regex",
      "suggestion": "Use Heroicons or Lucide SVG icons"
    },
    {
      "id": "inter-default",
      "severity": "info",
      "description": "Inter used as default font without brand justification",
      "pattern": "font-family:\\s*Inter",
      "suggestion": "Choose font based on brand personality"
    },
    {
      "id": "blue-purple-bg",
      "severity": "warning",
      "description": "Generic blue-purple gradient background",
      "pattern": "bg-gradient-to-br from-blue-900 to-purple-900",
      "suggestion": "Use solid background or brand-aligned gradient"
    },
    {
      "id": "decorative-stats",
      "severity": "warning",
      "description": "Decorative numbers without context or source",
      "pattern": "\\d{2,3}%\\s*(uptime|faster|better|growth)",
      "suggestion": "Add source citation or remove decorative stats"
    },
    {
      "id": "excessive-shadow",
      "severity": "warning",
      "description": "Heavy shadow without visual hierarchy",
      "pattern": "shadow-2xl|shadow-xl",
      "suggestion": "Use shadow-sm or shadow-md with clear hierarchy"
    },
    {
      "id": "no-hover-state",
      "severity": "warning",
      "description": "Clickable element without hover transition",
      "pattern": null,
      "type": "file",
      "check": "(content) => { const hasClickable = /cursor-pointer|role=\\\"button\\\"|<button/.test(content); const hasHover = /hover:/.test(content); return hasClickable && !hasHover; }",
      "suggestion": "Add hover state with 150-300ms transition"
    },
    {
      "id": "linear-easing",
      "severity": "warning",
      "description": "Linear easing on UI animations",
      "pattern": "transition.*linear|animation.*linear",
      "suggestion": "Use ease-out for enter, ease-in for exit"
    },
    {
      "id": "ease-in-enter",
      "severity": "warning",
      "description": "Ease-in on enter animations",
      "pattern": "animation.*ease-in.*fadeIn|animate.*ease-in",
      "suggestion": "Use ease-out for enter animations"
    },
    {
      "id": "missing-reduced-motion",
      "severity": "critical",
      "description": "Animations without prefers-reduced-motion media query",
      "pattern": "animation|transition(?!.*prefers-reduced-motion)",
      "type": "file",
      "suggestion": "Add @media (prefers-reduced-motion: reduce) query"
    },
    {
      "id": "tiny-touch-target",
      "severity": "critical",
      "description": "Touch target smaller than 44px on mobile",
      "pattern": null,
      "type": "file",
      "check": "(content) => { const smallHeights = /min-height:\\s*[1-3]\\d{0,1}px|height:\\s*[1-3]\\d{0,1}px/.test(content); const smallTailwind = /h-[1-9]|h-1[0-3]/.test(content); return smallHeights || smallTailwind; }",
      "suggestion": "Ensure minimum 44px touch targets on mobile (h-11 = 44px in Tailwind)"
    },
    {
      "id": "low-contrast",
      "severity": "critical",
      "description": "Text color with contrast ratio below 4.5:1 — requires visual audit (design-critic), not deterministic regex",
      "pattern": null,
      "type": "visual",
      "suggestion": "Use design-critic visual audit to verify contrast against actual background"
    },
    {
      "id": "missing-alt",
      "severity": "critical",
      "description": "Image without alt attribute",
      "pattern": "<img[^>]*(?!alt=)>",
      "suggestion": "Add descriptive alt text to all informative images"
    },
    {
      "id": "missing-viewport",
      "severity": "critical",
      "description": "Missing viewport meta tag",
      "pattern": null,
      "type": "file",
      "check": "(content) => !content.includes('name=\\\"viewport\\\"')",
      "suggestion": "Add <meta name=\"viewport\" content=\"width=device-width, initial-scale=1\">"
    },
    {
      "id": "blocking-js",
      "severity": "warning",
      "description": "Render-blocking script in head without async/defer",
      "pattern": "<script src=\"[^\"]*\"(?![^>]*(?:async|defer))>",
      "suggestion": "Add async or defer attribute to external scripts"
    },
    {
      "id": "cream-serif-cluster",
      "severity": "warning",
      "description": "Generic AI cluster: cream background (#F4F1EA range) + serif display + terracotta accent",
      "pattern": null,
      "type": "file",
      "check": "(content) => { const hasCream = /#[Ff][4-5][Aa][0-2][Ee][Aa][0-2]|cream|ivory|beige/.test(content); const hasSerif = /serif/.test(content); const hasTerracotta = /terracotta|#C24|#[Bb][0-4][Aa][0-5]/.test(content); return hasCream && hasSerif && hasTerracotta; }",
      "suggestion": "Derive palette from the product's world, not from AI defaults"
    },
    {
      "id": "dark-acid-cluster",
      "severity": "warning",
      "description": "Generic AI cluster: near-black background + acid green or vermilion accent",
      "pattern": null,
      "type": "file",
      "check": "(content) => { const hasDark = /#0a0a0a|#111111|#0d0d0d|#000000/.test(content); const hasAcid = /[3-5][Aa][0-9][Aa]f|lime|acid-green|neon-green/.test(content); return hasDark && hasAcid; }",
      "suggestion": "Choose accent color from brand personality, not from AI cluster defaults"
    },
    {
      "id": "broadsheet-cluster",
      "severity": "warning",
      "description": "Generic AI cluster: newspaper-style layout with hairline rules, zero border-radius, dense columns",
      "pattern": null,
      "type": "file",
      "check": "(content) => { const hasZeroRadius = /border-radius:\\s*0|rounded-none/.test(content); const hasHairline = /border-bottom:\\s*1px|hairline|divide-y/.test(content); const hasDense = /columns-[2-4]|grid-cols-[2-4]|dense/.test(content); return hasZeroRadius && hasHairline && hasDense; }",
      "suggestion": "Use intentional layout structure, not broadsheet default"
    }
  ]
}
```

---

## 9. Fluxos de Uso

### 9.1 Landing Page do Zero

```
User: "Crie uma landing page para um SaaS de analytics estilo Linear"

1. design-entry parseia o brief
   - Ground it in the subject: analytics SaaS, audiencia de devs, funcao de conversao
   - Produto: SaaS analytics
   - Estilo: Linear (carrega DESIGN.md de references/design-md/linear/)
   - Output: landing page HTML
   - Signature element: definir o que torna a pagina memoravel

2. Pass 1 — Planejar: cores (4-6 hex), tipo (2+ roles), layout (ASCII wireframe)
3. Pass 2 — Criticar: verificar se o plano e unico ou generico
4. SearXNG MCP: pesquisar referencias visuais
   - Query: "Linear analytics landing page design 2026"
   - Extrair tendencias atuais de design
   - Buscar conteudo real para copy
5. design-system-gen executa UI UX Pro MAX
   - Input: "analytics SaaS dashboard"
   - BM25 match: Soft UI Evolution + Swiss Modernism 2.0
   - Output: MASTER.md + tokens CSS

5. Taste Skill ativa com dials:
    - VARIANCE: 7 (moderno, assimétrico)
    - MOTION: 4 (subtil, hover + scroll)
    - DENSITY: 5 (balanceado)

6. design-landing constrói a página
    - 9 seções de conversão
    - Design system aplicado
    - Anti-slop rules ativas

7. Emil Skills adicionam motion
    - Scroll reveal com ease-out 500ms
    - Hover states com spring
    - prefers-reduced-motion

8. design-verifier valida checklist (25 itens)
9. design-critic audita anti-slop (45+ regras)
10. audit-slop executa detecção determinística
11. audit-vitals verifica LCP/CLS/INP
12. Preview em :8289
```

### 9.2 App Next.js

```
User: "Crie um dashboard Next.js para monitoramento de servidores"

1. design-entry parseia o brief
   - Produto: dashboard monitoramento
   - Estilo: data-dense, dark mode
   - Output: app Next.js

2. design-system-gen gera design system
   - BM25 match: Real-Time Monitoring dashboard style
   - Paleta: dark com accent verde (estilo Vercel/Linear)
   - Tipografia: JetBrains Mono + Geist Sans

3. Taste Skill com dials:
   - VARIANCE: 5 (clean, funcional)
   - MOTION: 3 (mínimo, foco em dados)
   - DENSITY: 8 (data-dense)

4. design-nextjs constrói o app
   - Next.js 15, App Router, TypeScript
   - shadcn/ui para componentes base
   - Framer Motion para transições
   - Server Components padrão

5. Emil Skills: micro-interações em charts e tables
6. Verificação completa e preview
```

### 9.3 Iteração Visual

```
User: "A hero section está muito genérica, melhore"

1. design-entry detecta intenção de refinamento
2. Carrega Taste Skill (anti-slop) + Emil Skills (motion)
3. Aplica comandos de vocabulário:
   - /polish → refinamento geral
   - /typeset → melhorar hierarquia tipográfica
   - /colorize → ajustar paleta
   - /animate → adicionar motion intencional
4. 3 variações geradas
5. Verificação e preview
```

### 9.4 Redesign de Projeto Existente

```
User: "Redesigne o dashboard atual para parecer mais profissional"

1. design-entry detecta intenção de redesign
2. Taste Skill `redesign-existing-projects` ativa
3. Audit da UI atual:
   - Identificar anti-patterns
   - Extrair design tokens existentes
   - Mapear componentes
4. Geração de design system melhorado
5. Aplicação gradual com verificação por componente
6. Preview comparativo antes/depois
```

### 9.5 Wireframe Rápido

```
User: "Explore 3 opções de layout para a hero section"

1. design-entry detecta intenção de exploração
2. Roteamento para design-wireframe
3. Gera 3 variações em output/wireframes/<project>/
4. Preview para comparação lado a lado
5. **Seleção:** Usuário escolhe variação favorita (ex: "usei a opção 2")
6. **Continuação:** design-entry carrega a variação selecionada como base para Phase 3, preservando layout e hierarquia escolhidos.
   - Extrair estrutura de seções do wireframe selecionado.
   - Aplicar design system gerado na Phase 1.
   - Manter posição de CTA e fluxo de navegação do wireframe.
```

### 9.6 Auditar Acessibilidade

```
User: "Verifique a acessibilidade da página"

1. design-entry roteia para design-a11y
2. Checklist WCAG 2.1 AA executado
3. Relatório de issues com severidade
4. Sugestões de correção aplicáveis
```

### 9.7 Auditar Performance

```
User: "Audite a performance da landing page"

1. design-entry roteia para design-perf
2. audit-vitals executa checks de LCP/CLS/INP
3. Relatório com issues e sugestões
4. Aplicação de otimizações
```

---

## 10. Design System Reutilizável

Design systems gerados são persistidos em `output/design-systems/<name>/` e auto-descobertos em sessões futuras via `.opencode/design-systems/<name>/`.

**Estrutura:**
```
output/design-systems/
├── saas-analytics/          # Sistema do SaaS analytics
│   ├── MASTER.md            # Source of truth
│   ├── tokens/
│   │   ├── colors.css       # oklch variables
│   │   ├── typography.css   # font scale
│   │   ├── spacing.css      # spacing scale
│   │   ├── shadows.css      # elevation
│   │   └── borders.css      # radius, borders
│   ├── components/
│   │   ├── buttons.css      # button variants
│   │   ├── forms.css        # input styles
│   │   └── cards.css        # card styles
│   └── pages/
│       ├── landing.md       # overrides para landing
│       └── dashboard.md     # overrides para dashboard
└── brand-marketing/         # Sistema de marketing
    ├── MASTER.md
    └── tokens/
```

**Hierarquia de retrieval:**
1. Verificar `design-systems/<project>/pages/<page>.md` (overrides específicos)
2. Se existir, aplicar overrides sobre o MASTER
3. Se não, usar `MASTER.md` exclusivamente

**Export DESIGN.md (Google Stitch format):**
```
/impeccable document
```
Gera `DESIGN.md` portátil compatível com Google Stitch, Cursor, Claude Code, Codex, Lovable.

---

## 11. Checklist de Qualidade

Antes de qualquer entrega, os verificadores validam 25 itens:

| # | Categoria | Item | Severidade | Determinístico |
|---|-----------|------|------------|----------------|
| 1 | HTML | Tags HTML válidas (tags fechadas, atributos com aspas) | critical | Sim (regex/htmllint) |
| 2 | HTML | Meta tags essenciais (viewport, description, title, OG) | critical | Sim (regex) |
| 3 | Conversão | CTA primary acima da dobra | critical | Nao (requer layout awareness) |
| 4 | Conversão | Copy formula aplicada (Problem → Solution → CTA) | warning | Nao (semantico) |
| 5 | Conversão | Social proof contextualizado | warning | Nao (semantico) |
| 6 | A11y | Contraste WCAG AA (4.5:1 normal, 3:1 grande) | critical | Nao (requer calculo de cor) |
| 7 | A11y | Keyboard navigation completa | critical | Nao (requer teste interativo) |
| 8 | A11y | Alt text em imagens informativas | critical | Sim (regex) |
| 9 | A11y | Focus indicators visíveis | warning | Nao (requer inspecao CSS) |
| 10 | Perf | CSS critical inline | warning | Sim (regex) |
| 11 | Perf | Imagens com dimensões explícitas | critical | Sim (regex) |
| 12 | Perf | Sem JS blocking | warning | Sim (regex) |
| 13 | Perf | Total < 50KB (sem imagens) | info | Sim (file size) |
| 14 | Design | Design system aplicado consistentemente | critical | Nao (semantico) |
| 15 | Design | Sem gradientes excessivos | warning | Sim (audit-slop) |
| 16 | Design | Sem emoji como ícones | warning | Sim (audit-slop) |
| 17 | Design | Sem cards com borda lateral colorida | warning | Sim (audit-slop) |
| 18 | Design | Sem backgrounds blue-purple genéricos | warning | Sim (audit-slop) |
| 19 | Design | Sem fontes overused como padrão | info | Sim (audit-slop) |
| 20 | Design | SVGs de ícones (Heroicons/Lucide) | warning | Nao (semantico) |
| 21 | Motion | Easing correto (ease-out para enter) | warning | Sim (audit-slop) |
| 22 | Motion | Durações dentro dos limites | info | Nao (semantico) |
| 23 | Motion | prefers-reduced-motion respeitado | critical | Sim (audit-slop) |
| 24 | Responsivo | Breakpoints funcionais (375/768/1024/1440px) | critical | Nao (requer render) |
| 25 | Responsivo | Touch targets >= 44px mobile | critical | Nao (requer inspecao CSS) |

**Severidades:**
- **critical:** bloqueia entrega, deve ser corrigido antes de prosseguir
- **warning:** deve ser corrigido, mas não bloqueia preview
- **info:** recomendação para melhoria futura

---

## 12. Anti-Patterns (Slop List)

**Nota:** As regras abaixo sao um resumo das regras definidas em `anti-patterns.json` (Secao 8.4). Ver o arquivo JSON para patterns completos e sugestoes de correcao.

| Regra | Descrição | Padrão de Detecção |
|-------|-----------|-------------------|
| `gradient-text` | Texto com gradiente | `bg-clip-text text-transparent bg-gradient-to-r` |
| `side-stripe-border` | Borda lateral colorida em cards | `"type": "file"` — verificar border-[rltb] + border-{cor} no arquivo |
| `ai-color-palette` | Paleta genérica de IA | `from-purple-600 via-pink-500 to-orange-400` |
| `ghost-card` | Card com fundo transparente + borda sutil | `bg-transparent border border-gray-200` |
| `over-rounding` | Border-radius excessivo | `rounded-3xl` em containers grandes |
| `purple-pink-gradient` | Gradientes purple/pink | `from-purple-400 to-pink-400` |
| `emoji-as-icon` | Emoji como ícone funcional | `<span>🚀</span>` em vez de SVG |
| `inter-default` | Inter como fonte padrão sem justificativa | `font-family: Inter` sem contexto de marca |
| `blue-purple-bg` | Background blue-purple genérico | `bg-gradient-to-br from-blue-900 to-purple-900` |
| `decorative-stats` | Números decorativos sem contexto | `99.9% uptime` sem fonte |
| `excessive-shadow` | Shadow pesado sem hierarquia | `shadow-2xl` em todos os cards |
| `no-hover-state` | Elemento clicável sem hover | `"type": "file"` — verificar cursor-pointer sem hover: no arquivo |
| `linear-easing` | Easing linear em UI | `transition: all 0.3s linear` |
| `ease-in-enter` | Ease-in para enter animation | `animation: fadeIn ease-in` |
| `missing-reduced-motion` | Sem prefers-reduced-motion | `"type": "file"` — verificar arquivo inteiro por `prefers-reduced-motion` |
| `tiny-touch-target` | Touch target < 44px | `"type": "file"` — verificar alturas < 44px em elementos clicaveis |
| `low-contrast` | Contraste < 4.5:1 | `"type": "visual"` — auditado pelo design-critic |
| `missing-alt` | Imagem sem alt text | `<img src="...">` sem `alt` |
| `missing-viewport` | Sem meta viewport | `"type": "file"` — verificar se `<meta name="viewport">` existe |
| `blocking-js` | Script blocking no head | `<script src="...">` sem async/defer |
| `cream-serif-cluster` | Cluster generico cream+serif+terracotta | `"type": "file"` — verificar cream bg + serif + terracotta no arquivo |
| `dark-acid-cluster` | Cluster generico dark+acid green | Fundo preto/near-black + accent verde acido ou vermilion |
| `broadsheet-cluster` | Cluster generico broadsheet | Hairline rules + zero radius + colunas densas + serif body |

---

## 13. Instalação e Setup

### 13.1 Pré-requisitos

- Node.js 18+
- OpenCode instalado e configurado

### 13.2 Instalação de Skills Externas

```bash
# UI UX Pro Max
npm install -g ui-ux-pro-max-cli
uipro init --ai opencode

# Taste Skill
npx skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend"

# Emil Skills
npx skills add emilkowalski/skills

# Impeccable (opcional, para detector)
npx impeccable install

# SearXNG MCP (pesquisa na web)
# Configurar em opencode.json (ver secao 8.1)
# ou instalar localmente:
# docker run -d -p 8080:8080 searxng/searxng
```

### 13.3 Setup do Harness

```bash
# 1. Clonar DESIGN.md references
git clone https://github.com/VoltAgent/awesome-design-md.git
cp -r awesome-design-md/designs/* .opencode/references/design-md/

# 2. Criar estrutura de output
mkdir -p output/{pages,apps,design-systems,wireframes,design-md}

# 3. Configurar opencode.json
# (ver seção 8.1)

# 4. Verificar instalação
ls .opencode/skills/
ls .opencode/agents/
ls .opencode/tools/
```

### 13.4 Comandos Disponíveis

| Comando | Skill | Descrição |
|---------|-------|-----------|
| "Crie uma landing page para [produto]" | design-entry | Iniciar fluxo completo de design |
| "Gere um design system para [marca]" | design-system-gen | Gerar design system completo |
| "Explore 3 layouts para [seção]" | design-wireframe | Explorar layouts rapidamente |
| "Otimize a animação de [componente]" | design-motion | Adicionar/refinar motion |
| "Verifique acessibilidade" | design-a11y | Auditar WCAG 2.1 AA |
| "Audite performance" | design-perf | Verificar Core Web Vitals |
| "Redesigne para parecer mais profissional" | design-entry (redesign) | Melhorar projeto existente |
| `/polish` | taste-skill | Refinamento visual geral |
| `/typeset` | taste-skill | Melhorar hierarquia tipográfica |
| `/colorize` | taste-skill | Ajustar paleta de cores |
| `/animate` | design-motion | Adicionar motion intencional |
| `/design audit` | design-verifier | Verificar qualidade completa |
| `/design detect` | design-critic | Detectar anti-slop |
| `/design preview` | preview tool | Iniciar server local |
| "Prepare handoff para [projeto]" | design-handoff | Documentar design para devs |
| "Otimize para conversão" | design-convert | CRO: CTA, copy, social proof |

### 13.5 Matriz de Dependências

| Dependência       | Tipo      | Obrigatório | Fallback               |
|-------------------|-----------|-------------|------------------------|
| Node.js 18+       | Runtime   | Sim         | —                      |
| UI UX Pro Max     | CLI       | Não         | Conhecimento interno   |
| Taste Skill       | Skill     | Não         | Regras inline          |
| Emil Skills       | Skill     | Não         | Regras inline          |
| Refero MCP        | MCP       | Não         | references/design-md/  |
| SVGL MCP          | MCP       | Não         | Placeholders rotulados |
| SearXNG MCP       | MCP       | Não         | Conhecimento interno   |
| Unsplash MCP      | MCP       | Não         | Placeholders rotulados |
| Standby.Design    | MCP       | Não         | UI UX Pro Max          |
| htmllint          | CLI       | Não         | Regex básico           |

---

## 14. Referências e Fontes

| Recurso | Link | Uso no Harness |
|---------|------|----------------|
| **UI UX Pro Max** | [github.com/nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) | Motor de design system |
| **Taste Skill** | [github.com/Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) | Anti-slop, qualidade visual |
| **Awesome DESIGN.md** | [github.com/VoltAgent/awesome-design-md](https://github.com/VoltAgent/awesome-design-md) | 73 referências de marca |
| **Emil Skills** | [github.com/emilkowalski/skills](https://github.com/emilkowalski/skills) | Motion design |
| **Impeccable** | [impeccable.style](https://impeccable.style) | 45 regras anti-slop, vocabulário |
| **Refero** | [styles.refero.design](https://styles.refero.design) | 2000+ design systems (MCP) |
| **Design Spells** | [designspells.com](https://designspells.com) | Micro-interações |
| **SVGL** | [svgl.app](https://svgl.app) | Logos SVG (MCP) |
| **KITTL** | [kittl.com](https://www.kittl.com) | Assets gráficos |
| **Cult UI** | [cult-ui.com](https://www.cult-ui.com) | Componentes curados |
| **Untitled UI** | [untitledui.com](https://untitledui.com) | UI kits |
| **SearXNG** | [searxng.org](https://searxng.org) | Pesquisa na web (MCP server) |
| **Anthropic frontend-design** | [github.com/anthropics/skills](https://github.com/anthropics/skills) | Framework filosofico (integrado em design-entry + design-critic) |
| **OpenDesign** | [github.com/manalkaff/opendesign](https://github.com/manalkaff/opendesign) | Padrão de referência |
| **Google Stitch** | [stitch.withgoogle.com](https://stitch.withgoogle.com) | Especificação DESIGN.md |
| **OpenCode Docs** | [opencode.ai/docs](https://opencode.ai/docs) | Skills, Agents, Plugins, MCP, Tools |
| **Unsplash MCP** | [github.com/hellokaton/unsplash-mcp-server](https://github.com/hellokaton/unsplash-mcp-server) | Imagens stock (MCP) |
| **Standby.Design** | [github.com/KarstenKreh/Standby.Design](https://github.com/KarstenKreh/Standby.Design) | Paletas OKLCH + tokens (MCP) |
| **CXL Institute** | cxlinstitute.com | Padrões de conversão |
| **WebAIM** | webaim.org | WCAG 2.1 AA guidelines |
| **Google Web Vitals** | web.dev/vitals | Métricas LCP, CLS, INP |

---

## 15. Resumo Técnico

### Componentes do Harness

| Tipo | Quantidade | Nomes |
|------|-----------|-------|
| **Skills externas** | 4 + 1 integrada | UI UX Pro Max, Taste Skill, Awesome DESIGN.md, Emil Skills, Anthropic frontend-design (integrada) |
| **Skills internas** | 10 | design-entry, design-system-gen, design-wireframe, design-nextjs, design-landing, design-motion, design-a11y, design-perf, design-handoff, design-convert |
| **Agentes** | 2 | design-verifier, design-critic |
| **Tools** | 3 | preview.js, audit-slop.js, audit-vitals.js |
| **MCP Servers** | 5 | Refero, SVGL, SearXNG, Unsplash, Standby.Design |
| **Referências externas** | 10 | Refero, Impeccable, Design Spells, SVGL, KITTL, Cult UI, Untitled UI, SearXNG, Unsplash, Standby.Design |
| **Regras anti-slop** | 48+ | Impeccable + Taste Skill + cluster awareness (3 clusters) |
| **Itens de checklist** | 25 | HTML, Conversão, A11y, Perf, Design, Motion, Responsivo |
| **Marcas de referência** | 73 | Awesome DESIGN.md collection |

### Fluxo em 5 Fases

1. **Design System Generation** — 2-pass (planejar → criticar) + UI UX Pro Max → MASTER.md + tokens
2. **Visual References** — DESIGN.md + Refero + SearXNG (pesquisa web) + Taste Skill + dials + signature element
3. **Construction** — design-nextjs ou design-landing com Emil motion + auto-critica (regra Chanel)
4. **Verification** — a11y + perf + verifier (25) + critic (48+ clusters) + audit-slop + loop correção (max 3 iterações)
5. **Delivery** — handoff docs + preview :8289 + DESIGN.md export

### Performance Targets

| Métrica | Target |
|---------|--------|
| LCP | < 2.5s |
| CLS | < 0.1 |
| INP | < 200ms |
| HTML + CSS (sem imagens) | < 50KB |
| JS blocking | zero |
| Lighthouse score | 95+ |

### Acessibilidade

| Requisito | Target |
|-----------|--------|
| Contraste (texto normal) | 4.5:1 |
| Contraste (texto grande) | 3:1 |
| Touch targets mobile | >= 44px |
| Body copy | >= 16px |
| Hero headlines desktop | >= 48px |
| Hero headlines mobile | >= 32px |
| Keyboard navigation | completa |
| prefers-reduced-motion | sempre respeitado |

---

*Spec atualizada em 2026-07-04. Versão 1.1.*
