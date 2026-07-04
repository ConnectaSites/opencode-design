# OpenCode Design Harness — Landing Pages

Plano para um harness eficiente no OpenCode, seguindo o padrão de trabalho do OpenDesign, para construção de landing pages de alta qualidade.

---

## Visão Geral

O harness é um conjunto integrado de **skills**, **agentes**, **plugins**, **MCP servers** e **custom tools** que transformam o OpenCode em um agente de design especializado em landing pages. A arquitetura segue o mesmo padrão do [OpenDesign](https://github.com/manalkaff/opendesign): uma skill de entrada que roteia para skills especializadas, um plugin que bootstraps o contexto, e um verificador que valida a saída.

---

## 1. Arquitetura do Harness

```
.opencode/
├── opencode.json              # Config principal do projeto
├── plugins/
│   └── landing-harness.js     # Plugin de bootstrap
├── skills/
│   ├── landing-page/          # Skill de entrada (front door)
│   │   └── SKILL.md
│   ├── landing-wireframe/     # Wireframes rápidos
│   │   └── SKILL.md
│   ├── landing-convert/       # Otimização de conversão
│   │   └── SKILL.md
│   ├── landing-brand/         # Extração de design system da marca
│   │   └── SKILL.md
│   ├── landing-a11y/          # Acessibilidade
│   │   └── SKILL.md
│   ├── landing-performance/   # Otimização de performance
│   │   └── SKILL.md
│   └── landing-handoff/       # Handoff para desenvolvimento
│       └── SKILL.md
├── agents/
│   └── landing-verifier.md    # Agente verificador
└── tools/
    ├── preview.js             # Server de preview local
    └── audit-lcp.js           # Tool de auditoria LCP/CLS
```

### Fluxo de Trabalho

```
User request
    │
    ▼
┌───────────────────────┐
│  landing-page skill   │  ← Entrada única (front door)
│  (roteamento central) │
└──────────┬────────────┘
           │
  1. Scan design systems
  2. Intake estruturado
  3. Coleta de contexto
  4. Roteamento para skill especializada
           │
    ┌──────┴──────┐
    ▼             ▼
 Wireframe   Landing-Convert
 Brand       Landing-A11y
    │             │
    └──────┬──────┘
           ▼
  Construção da página
           │
           ▼
┌───────────────────────┐
│  landing-verifier     │  ← Subagente verificador
│  (validação isolada)  │
└──────────┬────────────┘
           ▼
   Preview + Handoff
```

---

## 2. Skills

### 2.1 `landing-page` — Skill de Entrada

**Função:** Front door que estabelece o papel, fluxo de trabalho e regras de qualidade. Roteia para skills especializadas conforme o tipo de tarefa.

**Arquivo:** `.opencode/skills/landing-page/SKILL.md`

```yaml
---
name: landing-page
description: Use when building, refining, or auditing a landing page — SaaS, product, event, lead-gen, or marketing pages. Establishes the designer role, workflow, and quality rules, and routes to specialist skills.
---
```

**Conteúdo da skill (estrutura):**

```markdown
Você é um senior conversion designer especializado em landing pages.
Produz páginas HTML otimizadas para conversão, performance e acessibilidade.

## Workflow em cada tarefa

1. **Verificar design systems existentes.** Scan `./landing-output/design-systems/*/`.
   - Nenhum → perguntar se importar do codebase, criar do zero, ou usar padrão.
   - Um → carregar automaticamente, anunciar escolha.
   - Múltiplos → inferir pelo tipo de tarefa, ou perguntar.

2. **Intake estruturado.** Formulário de ~8-10 perguntas:
   - Objetivo da página (lead gen, demo, download, compra)
   - Público-alvo
   - Tom de voz (formal, casual, técnico, inspirador)
   - Seções desejadas (hero, features, social proof, pricing, FAQ, CTA)
   - Nível de fidelidade (wireframe, mid-fi, hi-fi)
   - Restrições técnicas (framework, bundle size, sem JS)
   - Referências visuais (URLs, screenshots, design system)
   - Métrica de sucesso principal (CTR, sign-ups, downloads)

3. **Coletar contexto.** Ler design system, codebase, brand guidelines.

4. **Planejar.** Todo list com escolhas estéticas explícitas.

5. **Construir.** Sobr `./landing-output/pages/<slug>/`. Iterar.

6. **Verificar.** Fork do subagente `landing-verifier`.

7. **Resumir.** Apenas caveats e próximos passos.

## Regras anti-slop

- Sem gradientes excessivos
- Sem emoji como ícones (a menos que a marca use)
- Sem cards com borda colorida lateral
- Sem fontes overused como padrão (Inter, Roboto, Arial)
- Sem backgrounds blue-purple genéricos
- Sem dados, stats ou ícones decorativos desnecessários

## Regras de escala

- Touch targets: mínimo 44px mobile
- Body copy: mínimo 16px
- Headlines hero: mínimo 48px desktop, 32px mobile

## Aesthetic padrão (sem marca definida)

- 1-3 fontes máximo
- Temperatura definida: warm, cool, ou neutral
- 0-2 accent colors em oklch
- Anunciar escolha no plano, manter consistência
```

### 2.2 `landing-wireframe` — Wireframes Rápidos

**Função:** Explorar o espaço de design rapidamente — muitas ideias rústicas, não uma direção polida.

```yaml
---
name: landing-wireframe
description: Use when exploring landing page layout options quickly — multiple rough wireframes, not polished output.
---
```

**Diretrizes-chave:**
- Produzir 3-5 variações em dimensões significativas: layout, hierarquia, posição de CTA
- HTML + CSS inline, sem assets externos
- Placeholders claramente rotulados para imagens e ícones
- Focar em estrutura e fluxo, não em polimento visual
- Cada variação em arquivo separado: `wireframe-01.html`, etc.

### 2.3 `landing-convert` — Otimização de Conversão

**Função:** Aplicar padrões comprovados de conversão: copywriting, CTA placement, social proof, urgência.

```yaml
---
name: landing-convert
description: Use when optimizing a landing page for conversion — CTA placement, copywriting, social proof, form design, or A/B test variants.
---
```

**Princípios aplicados:**
- **Above the fold:** headline + subheadline + CTA primary visíveis sem scroll
- **CTA hierarchy:** 1 primary CTA (cor accent), secundários muted
- **Social proof:** logos de clientes, depoimentos, números — sempre com contexto
- **Copy formula:** Problem → Agitation → Solution → Proof → CTA
- **Form design:** mínimo de campos, labels claros, inline validation
- **Urgência:** quando genuína, nunca fabricada
- **Variações A/B:** testar headline, CTA copy, cor do botão, posição do form

### 2.4 `landing-brand` — Extração de Design System

**Função:** Extrair ou criar um design system reutilizável a partir de um codebase, brand guide, ou inputs do usuário.

```yaml
---
name: landing-brand
description: Use when creating or extracting a design system from an existing brand, codebase, or product for landing page use.
---
```

**Output:** `./landing-output/design-systems/<name>/` contendo:
- `tokens/colors.css` — variáveis CSS de cores em oklch
- `tokens/typography.css` — scale tipográfica, font families
- `tokens/spacing.css` — scale de espaçamento
- `tokens/shadows.css` — elevation tokens
- `tokens/borders.css` — radius e border styles
- `components/buttons.css` — button variants
- `components/forms.css` — input, select, textarea styles
- `SKILL.md` — documentação do sistema como skill portátil

### 2.5 `landing-a11y` — Acessibilidade

**Função:** Auditar e corrigir acessibilidade: WCAG 2.1 AA compliance, keyboard navigation, screen reader support.

```yaml
---
name: landing-a11y
description: Use when auditing or fixing landing page accessibility — WCAG compliance, keyboard nav, screen reader support, or color contrast.
---
```

**Checklist automático:**
- Contraste mínimo 4.5:1 (texto normal), 3:1 (texto grande)
- Todos os elementos interativos acessíveis por teclado
- Alt text descritivo em todas as imagens
- ARIA labels em ícones funcionais
- Skip links para navegação
- Focus indicators visíveis
- Sem dependência exclusiva de cor para transmitir informação
- `lang` attribute no `<html>`
- Sem auto-play de mídia

### 2.6 `landing-performance` — Performance

**Função:** Garantir que a landing page atinja métricas de performance aceitáveis: LCP < 2.5s, CLS < 0.1, INP < 200ms.

```yaml
---
name: landing-performance
description: Use when optimizing landing page performance — LCP, CLS, INP, bundle size, or Core Web Vitals.
---
```

**Diretrizes:**
- Inline critical CSS, defer o resto
- Imagens: `loading="lazy"`, `width`/`height` explícitos para evitar CLS
- Fontes: `font-display: swap`, preconnect para font origins
- JS: mínimo possível, async/defer, sem blocking
- Target: < 50KB total (HTML + CSS inline) sem imagens
- Sem dependências externas não essenciais

### 2.7 `landing-handoff` — Handoff para Desenvolvimento

**Função:** Preparar o design final para implementação: documentação, tokens, componentes, instruções claras.

```yaml
---
name: landing-handoff
description: Use when handing off a finished landing page design to a developer or coding agent for implementation.
---
```

**Output:**
- `handoff.md` — resumo do design, decisões, tokens, breakpoints
- `components/` — CSS modularizado por componente
- `tokens/` — variáveis CSS extraídas
- `notes/` — caveats, dependências, instruções de deploy

---

## 3. Plugin de Bootstrap

**Arquivo:** `.opencode/plugins/landing-harness.js`

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

export const LandingHarnessPlugin = async ({ directory }) => {
  const skillsDir = path.resolve(__dirname, '../skills');
  const bootstrapPath = path.join(skillsDir, 'landing-page', 'SKILL.md');

  const getBootstrap = () => {
    if (!fs.existsSync(bootstrapPath)) return null;
    const { content } = extractFrontmatter(fs.readFileSync(bootstrapPath, 'utf8'));
    return `<EXTREMELY_IMPORTANT>
You have Landing Harness loaded. The landing-page entry-point skill is ALREADY LOADED.
Do NOT use the skill tool to load "landing-page" again.

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
    },
  };
};
```

---

## 4. Agente Verificador

**Arquivo:** `.opencode/agents/landing-verifier.md`

```yaml
---
name: landing-verifier
description: Verifies landing page output against the design brief and quality checklist.
mode: subagent
color: red
---
```

```markdown
Você é um verificador de qualidade para landing pages.
Sua função é carregar a saída HTML em um contexto limpo e validá-la.

## Checklist de verificação

### Estrutura
- [ ] HTML válido (tags fechadas, atributos com aspas)
- [ ] Meta tags essenciais (viewport, description, title)
- [ ] Sem erros de console (JS, CSS)

### Conversão
- [ ] CTA primary visível acima da dobra
- [ ] Copy segue a fórmula Problem → Solution → CTA
- [ ] Social proof presente e contextualizado
- [ ] Formulário com mínimo de campos

### Acessibilidade
- [ ] Contraste WCAG AA em todos os textos
- [ ] Elementos interativos acessíveis por teclado
- [ ] Alt text em imagens informativas
- [ ] Focus indicators visíveis

### Performance
- [ ] CSS critical inline
- [ ] Imagens com dimensões explícitas
- [ ] Sem JS blocking
- [ ] Total < 50KB (sem imagens)

### Design
- [ ] Design system aplicado consistentemente
- [ ] Sem itens da anti-slop list
- [ ] Placeholders rotulados (sem SVGs complexos)
- [ ] Breakpoints responsivos funcionais

## Comportamento

- Se tudo passar: ficar silencioso.
- Se algo falhar: acordar o builder com lista específica de issues.
- Nunca refazer o trabalho — apenas reportar.
```

---

## 5. Custom Tools

### 5.1 `preview.js` — Server de Preview Local

**Arquivo:** `.opencode/tools/preview.js`

```javascript
import { tool } from "@opencode-ai/plugin";
import { spawn } from "child_process";
import path from "path";

export default tool({
  description: "Start a local preview server for landing pages in ./landing-output/ on port 8289.",
  args: {
    page: tool.schema.string().optional().describe("Specific page slug to preview. If omitted, serves the root directory."),
  },
  async execute(args) {
    const outputDir = path.resolve(process.cwd(), "landing-output");
    const port = 8289;

    const server = spawn("python3", ["-m", "http.server", String(port), "--directory", outputDir], {
      detached: true,
      stdio: "ignore",
    });

    server.unref();
    const url = args.page
      ? `http://localhost:${port}/pages/${args.page}/`
      : `http://localhost:${port}/`;

    return `Preview server started at ${url}`;
  },
});
```

### 5.2 `audit-lcp.js` — Auditoria de Métricas

**Arquivo:** `.opencode/tools/audit-lcp.js`

```javascript
import { tool } from "@opencode-ai/plugin";

export default tool({
  description: "Audit a landing page HTML file for Core Web Vitals risks: LCP candidates, CLS risks, render-blocking resources.",
  args: {
    file: tool.schema.string().describe("Path to the HTML file to audit."),
  },
  async execute(args) {
    const fs = await import("fs");
    const content = fs.readFileSync(args.file, "utf8");

    const issues = [];

    // Check for missing viewport meta
    if (!content.includes('name="viewport"')) {
      issues.push("MISSING: viewport meta tag");
    }

    // Check for images without dimensions (CLS risk)
    const imgTags = content.match(/<img[^>]*>/g) || [];
    for (const img of imgTags) {
      if (!img.includes("width=") || !img.includes("height=")) {
        issues.push("CLS RISK: img without explicit width/height");
      }
    }

    // Check for external fonts without swap
    if (content.includes('@import') && !content.includes('font-display: swap')) {
      issues.push("LCP RISK: external fonts without font-display: swap");
    }

    // Check for inline scripts
    if (content.match(/<script[^>]*>(?![\s]*<\/script>)/)) {
      issues.push("INP RISK: inline script detected");
    }

    // Estimate size
    const sizeKB = (new Blob([content]).size / 1024).toFixed(1);
    if (parseFloat(sizeKB) > 50) {
      issues.push(`SIZE WARNING: HTML is ${sizeKB}KB (target < 50KB without images)`);
    }

    if (issues.length === 0) {
      return `Audit passed. File size: ${sizeKB}KB. No critical issues found.`;
    }

    return `Audit found ${issues.length} issue(s):\n${issues.join("\n")}\n\nFile size: ${sizeKB}KB`;
  },
});
```

---

## 6. MCP Servers

Configuração recomendada em `.opencode/opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": ["landing-harness"],
  "mcp": {
    "unsplash": {
      "type": "remote",
      "url": "https://mcp.unsplash.com",
      "enabled": true,
      "description": "Buscar imagens de stock para hero sections e ilustrações"
    },
    "color-harmony": {
      "type": "local",
      "command": ["npx", "-y", "@mcp/color-tools"],
      "enabled": true,
      "description": "Gerar paletas harmoniosas em oklch a partir de cores de marca"
    }
  },
  "references": {
    "landing-patterns": {
      "repository": "land-book/awesome-landing-pages",
      "branch": "main",
      "description": "Referência de padrões de landing pages de alta conversão"
    }
  }
}
```

---

## 7. Configuração Principal

**Arquivo:** `.opencode/opencode.json`

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "anthropic/claude-sonnet-4-5",
  "plugin": ["landing-harness"],
  "instructions": [
    "AGENTS.md"
  ],
  "mcp": {
    "unsplash": {
      "type": "remote",
      "url": "https://mcp.unsplash.com",
      "enabled": true
    }
  },
  "agent": {
    "landing-verifier": {
      "permission": {
        "bash": "deny",
        "file_edits": "deny"
      }
    }
  },
  "permission": {
    "skill": {
      "landing-*": "allow"
    }
  }
}
```

---

## 8. AGENTS.md

**Arquivo:** `AGENTS.md`

```markdown
# Landing Page Harness

Este projeto usa o Landing Harness para construção de landing pages de alta qualidade.

## Estrutura de saída

- `./landing-output/pages/<slug>/` — páginas geradas
- `./landing-output/design-systems/<name>/` — design systems
- `./landing-output/mockups/` — wireframes e rascunhos

## Comandos

- `opencode run "landing page para [produto]"` — iniciar fluxo
- Tool `preview` — server local em :8289
- Tool `audit_lcp` — auditoria de performance

## Convenções

- HTML como medium de output
- CSS inline para critical path
- oklch para cores
- Placeholders rotulados para assets ausentes
- Nomes de arquivos descritivos, sem versionamento manual
```

---

## 9. Fluxo de Uso

### 9.1 Criar uma Landing Page do Zero

```
User: "Crie uma landing page para um SaaS de analytics"

1. Skill `landing-page` carrega automaticamente (via plugin)
2. Scan de design systems → nenhum encontrado
3. Intake: 8 perguntas estruturadas
   - Objetivo: lead gen
   - Público: CTOs de startups
   - Tom: técnico mas acessível
   - Seções: hero, features, pricing, CTA
   - Fidelidade: hi-fi
   - Sem framework específico
   - Sem referência visual
   - Métrica: sign-ups
4. Roteamento para `landing-convert` (foco em conversão)
5. Construção de `./landing-output/pages/saas-analytics/index.html`
6. Verificação automática via subagente
7. Preview em http://localhost:8289
```

### 9.2 Wireframe Rápido

```
User: "Explore 3 opções de layout para a hero section"

1. Skill `landing-page` detecta intenção de exploração
2. Roteamento para `landing-wireframe`
3. Gera 3 variações em `./landing-output/mockups/hero-exploration/`
4. Preview para comparação lado a lado
```

### 9.3 Otimizar Página Existente

```
User: "Otimize essa landing page para conversão"

1. Skill `landing-page` carrega design system existente
2. Roteamento para `landing-convert`
3. Auditoria com checklist de conversão
4. Aplicação de melhorias: CTA, copy, social proof
5. Verificação e preview
```

### 9.4 Auditar Acessibilidade

```
User: "Verifique a acessibilidade da página"

1. Skill `landing-page` roteia para `landing-a11y`
2. Checklist WCAG 2.1 AA executado
3. Relatório de issues com severidade
4. Sugestões de correção aplicáveis
```

---

## 10. Design System Reutilizável

Design systems criados por `landing-brand` são persistidos em
`./landing-output/design-systems/<name>/` e auto-descobertos em
sessões futuras. Múltiplos sistemas são suportados:

```
landing-output/
└── design-systems/
    ├── marketing/           # Sistema de marketing
    │   ├── tokens/
    │   │   ├── colors.css
    │   │   ├── typography.css
    │   │   ├── spacing.css
    │   │   └── shadows.css
    │   ├── components/
    │   │   ├── buttons.css
    │   │   └── forms.css
    │   └── SKILL.md
    └── product/             # Sistema do produto
        ├── tokens/
        └── SKILL.md
```

A skill `landing-page` infere qual sistema usar pelo tipo de tarefa:
- Páginas de marketing → `marketing/`
- Páginas do produto → `product/`
- Ambíguo → pergunta ao usuário

---

## 11. Checklist de Qualidade

Antes de qualquer entrega, o verificador valida:

| Categoria | Item | Status |
|---|---|---|
| **HTML** | Tags válidas, sem erros | |
| **HTML** | Meta tags essenciais presentes | |
| **Conversão** | CTA acima da dobra | |
| **Conversão** | Copy formula aplicada | |
| **Conversão** | Social proof contextualizado | |
| **Acessibilidade** | Contraste WCAG AA | |
| **Acessibilidade** | Keyboard navigation | |
| **Acessibilidade** | Alt text em imagens | |
| **Performance** | CSS critical inline | |
| **Performance** | Imagens com dimensões | |
| **Performance** | Total < 50KB (sem imagens) | |
| **Design** | Design system consistente | |
| **Design** | Sem anti-slop patterns | |
| **Design** | Placeholders rotulados | |
| **Responsivo** | Breakpoints funcionais | |
| **Responsivo** | Touch targets >= 44px | |

---

## 12. Referências e Fontes

- **OpenDesign** ([manalkaff/opendesign](https://github.com/manalkaff/opendesign)) — padrão de skills, plugin, e workflow deste harness
- **OpenCode Docs** — [Skills](https://opencode.ai/docs/skills/), [Agents](https://opencode.ai/docs/agents/), [Plugins](https://opencode.ai/docs/plugins/), [MCP](https://opencode.ai/docs/mcp-servers/), [Custom Tools](https://opencode.ai/docs/custom-tools/)
- **CXL Institute** — padrões de conversão e copywriting
- **WebAIM** — WCAG 2.1 AA guidelines
- **Google Web Vitals** — métricas LCP, CLS, INP

## 13: Skills

- nextlevelbuilder/ui-ux-pro-max-skill (https://github.com/nextlevelbuilder/ui-ux-pro-max-skill)
- VoltAgent/awesome-design-md (https://github.com/VoltAgent/awesome-design-md)
- Leonxlnx/taste-skill (https://github.com/Leonxlnx/taste-skill)
- emilkowalski/skills (https://github.com/emilkowalski/skills/)

## 14: Links Úteis

- Refero — UI/UX Design (https://styles.refero.design)
- Impeccable Style (https://impeccable.style)
- KITTL (https://www.kittl.com)
- designspells.com (https://designspells.com)
- SVGL (https://svgl.app)
- Cult Ui (https://www.cult-ui.com)
- Untitled UI (https://www.untitledui.com)