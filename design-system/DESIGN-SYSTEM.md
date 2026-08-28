# Expert em Lábios 2026 — Design System

**Versão 1.0.0** · Desenvolvido por **Edegar Junior**.

Sistema de design portátil para web (HTML/CSS, React, Framer). Dark por padrão, light por troca de tema. Esta pasta é a **fonte da verdade** para aplicar a marca em qualquer projeto.

## Arquivos

| Arquivo | Para quê |
|---|---|
| `silka.css` | **Fonte Silka** (pesos 300–700) embutida em woff2/base64, self-contained. Linke **antes** do CSS principal. |
| `expert-em-labios-design-system.css` | **Drop-in.** Tokens (dark/light) + reset + foco + motion + tipografia + botões + chips/badges/status. Basta linkar. |
| `expert-em-labios-design-tokens.json` | Tokens legíveis por máquina (Style Dictionary, Framer, plugins, agentes de IA). |
| `Button.tsx` | Code Component Framer/React do botão, com Property Controls. |
| `THEME.md` | Como o claro/escuro é configurado e **ativado pelo tema do sistema** do visitante (web + Framer). |
| `DESIGN-SYSTEM.md` | Este documento (spec + como usar + prompt para IA). |
| `CHANGELOG.md` | Histórico de versões (Keep a Changelog + SemVer). |
| `CONTRIBUTING.md` | Governança: como o sistema evolui (regra das 3 equipes, gate de pronto, SemVer, depreciação). |
| `IMPLEMENTACAO.md` | **Documentação técnica de implementação**: arquitetura (sem build), tokens e theming, fundamentos, botões e todos os estados/microinterações, componentes, comportamentos JS, acessibilidade, responsivo, consumo/Framer, deploy/infra e diferenças por marca. |
| `voz-e-tom.md` | **Guia de copy generalista** (voz, faça/não faça, estrangeirismos, separação de domínio, acessibilidade). Vale para todas as marcas. |
| `glossario-marca.md` | **Glossário de domínio desta marca** (termos exclusivos, regras de produto). Não cruza para outro DS. |
| `copy-deck.expert-em-labios.json` | Deck de copy do produto (hero, notas, microcopy, demos) usado no showcase. Fonte canônica das strings. |
| `../index.html` | Showcase visual navegável (todas as cores, gradientes, tipografia, ícones e componentes ao vivo, com click-to-copy). |

---

## Como aplicar (3 caminhos)

### 1. HTML/CSS — drop-in
```html
<html lang="pt-BR">  <!-- dark por padrão; sem data-theme segue o sistema -->
<head>
  <link rel="stylesheet" href="silka.css">            <!-- fonte Silka -->
  <link rel="stylesheet" href="expert-em-labios-design-system.css">
</head>
<body>
  <h1 class="el-h1">Pare de injetar <span class="el-hl">no escuro.</span></h1>
  <button class="el-btn el-fill">Assinar <svg class="el-ico">…</svg></button>
</body>
```
A fonte **Silka** vem em `silka.css` (woff2 embutido, self-contained) — linke antes do CSS principal. Sem ela, cai em **Poppins** (fallback) e, por fim, `system-ui` — sem quebrar.

### 2. Qualquer stack — via tokens
Importe `expert-em-labios-design-tokens.json` e gere variáveis no seu formato (CSS vars, JS, Tailwind theme, etc.). Regra de ouro: **componentes consomem tokens, nunca hex solto.**

### 3. Framer
- Crie cada cor como **Color Style** com valor **Light** e **Dark** (tabela na seção 02 · Cores do index.html, com click-to-copy).
- Crie os **Text Styles** com **3 breakpoints (L/M/S)** — ver **"Framer — Text Styles responsivos"** na seção Tipografia (mecânica + valores exatos).
- Importe o botão via `Button.tsx` (Code Component) ou recrie com as variantes.
- Ícones: biblioteca **Phosphor**, peso **Thin**.

---

## Fundamentos

### Cores institucionais (base — não inventar fora disto)
`#6B99E6` azul · `#B3E3FB` azul gelo · `#0F1730` navy · `#FFE4A4` amarelo · `#FFB1BD` vermelho · `#FFCA9B` amarelado · `#FFFFFF` branco · `#000000` preto.

### Tema
- **Dark é o padrão.** Light ativa com `data-theme="light"` no `<html>`; sem atributo, segue `prefers-color-scheme`.
- Toggle (persistente + anti-flash): coloque no `<head>`, antes da pintura:
```html
<script>(function(){try{var t=localStorage.getItem('el-theme');if(t!=='light'&&t!=='dark')t=matchMedia('(prefers-color-scheme: light)').matches?'light':'dark';document.documentElement.setAttribute('data-theme',t)}catch(e){document.documentElement.setAttribute('data-theme','dark')}})();</script>
```
No light, **dourado e rosa como texto** usam variantes `-ink` (`--gold-ink`, `--rose-ink`); como preenchimento mantêm a cor institucional. A marca (`--logo`) usa as cores do arquivo: branca no dark e azul `#6B99E6` no light.

### CTA — token theme-aware (`--cta`)
O CTA (botão preenchido/sólido) consome o token **`--cta`** em vez de `--roxo2`/`--roxo-bright` direto, para garantir **contraste de componente** (WCAG 1.4.11, ver Acessibilidade nível 2). Tokens: `--cta-grad` · `--cta-solid` · `--cta-solid-h` · `--cta-ink`.

| Tema | `--cta-solid` | `--cta-grad` | hover (`--cta-solid-h`) | `--cta-ink` |
|---|---|---|---|---|
| **Escuro** | `#B3E3FB` (gelo, tinta navy) | `#B3E3FB → #6B99E6` | `#9CD4F5` | `#0F1730` |
| **Claro** | `#1D3E8F` | `#1D3E8F → #2C4FA3` | `#16306F` | `#fff` |

No **tema escuro** o CTA é o botão de gelo: gradiente da marca com tinta navy (12.9:1). No **tema claro** o CTA usa azul profundo `#1D3E8F` com branco.

### Tokens de sistema
- **Raio:** sm 8 · md 14 · lg 18 · pill 30
- **Espaçamento (base 4/8):** 4 · 8 · 12 · 16 · 24 · 32 · 48
- **Elevação:** `--elev-1..4` (sombras azuis sutis no light, mais densas no dark)
- **Z-index:** base 0 · raised 10 · sticky 40 · overlay 100 · toast 1000
- **Motion:** fast .15s · base .2s · slow .4s · ease `cubic-bezier(.2,.8,.2,1)`
- **Foco:** `--focus: 0 0 0 2px var(--bg), 0 0 0 4px var(--focus-ring)`
- **Foundations:** opacidade (disabled .45 / muted .66 / hover .08 / overlay .58) · border-width (hair/1/2) · blur (sm 6 / md 12 / lg 20) · breakpoints (390/810/1200) · sizing (ícone 16/20/24, control/touch 44px) · aspect-ratio (1:1 / 4:3 / 16:9).
- **Elevação semântica:** `--elev-raised` (=1) · `--elev-overlay` (=3) · `--elev-modal` (=4); use o papel, não o número. Sombras em **camadas**: pretas no dark; com matiz da marca no light.

### Cantos aninhados (nested corners)
Quando um elemento arredondado fica **dentro** de outro, os cantos devem ser **concêntricos** (mesmo centro de arco):

```
raio interno = raio externo − padding
```

Mantém o espaçamento uniforme inclusive nos cantos. Mesmo raio nos dois → o gap "estufa" nos cantos (efeito errado).

```css
.card{ --r:24px; --pad:16px; border-radius:var(--r); padding:var(--pad); }
.card > .inner{ border-radius:max(0px, calc(var(--r) - var(--pad))); } /* 24 - 16 = 8 */
```

Pares: card grande 24/16→8 · médio 16/8→8 · pequeno 12/8→4 · tile 8/8→0 (reto).

Regras: **padding ≥ raio** → interno 0 (reto); **borda/stroke** inverte (externo = interno + largura); **aninhamento profundo** subtrai o padding de cada nível; **pill** é exceção; com **corner smoothing/squircle** a fórmula vira aproximação (iguale o smoothing em pai e filho).

### Tipografia — Silka (escala responsiva)
`size = Desktop / Tablet / Phone (px)`

| Estilo | D / T / P | Peso | LH |
|---|---|---|---|
| Display / H1 | 60 / 44 / 34 | 500 | 1.03 |
| Heading / H2 | 38 / 32 / 26 | 500 | 1.12 |
| Sub / H3 | 24 / 22 / 20 | 500 | 1.2 |
| Sub / H4 | 20 / 19 / 18 | 500 | 1.25 |
| Sub / H5 | 17 / 16 / 16 | 500 | 1.3 |
| Sub / H6 | 15 / 14 / 14 | 500 | 1.35 |
| Eyebrow | 12 / 12 / 11 | 600 | 1.2 · UPPERCASE · tracking .18em · cor lilás |
| Lead | 18 / 17 / 16 | 300 | 1.5 · cor muted |
| Body | 16 / 16 / 16 | 300 | 1.65 |
| Body small | 14 / 13 / 13 | 300 | 1.6 |
| Numeral / Preço | 44 / 38 / 32 | 700 | 1 · tabular-nums |
| Legal | 12 / 11 / 11 | 300 | 1.5 |

No CSS use `clamp()` entre Phone e Desktop. Body **≥16px no mobile** (evita zoom no iOS). **Numerais sempre com `tabular-nums`** — ativado globalmente no `body` (dígitos de largura fixa, não encavalam: preços, stats, tabelas, contadores).

#### Framer — Text Styles responsivos (L / M / S, desktop-first)

O Expert em Lábios 2026 usa **3 breakpoints: L · M · S** (desktop-first). No editor: **L = Desktop ≥1200 (primário), M = Tablet 810–1199, S = Mobile 390–809**. Você edita o L e ele herda pra baixo; sobrescreve M/S onde precisar. **Tipografia não auto-escala** — os 3 tamanhos precisam existir no estilo.

**Editar à mão no editor (CONFIÁVEL — recomendado):** abra o estilo → painel *Breakpoints* → defina os 3 tamanhos. O Framer seta os `Min Width` certos (1200/810/390) sozinho e é WYSIWYG. O slot **S é a base** e seu Min Width fica **travado/cinza**; com só 3 tiers o Framer mostra o S como base — para o S exibir **390** explicitamente, existe um 4º tier (ver workaround).

> **⚠️ BUG da Server API `framer-api` (confirmado jun/2026, v0.1.14).** `TextStyle.setAttributes({ breakpoints })` **emparelha o `fontSize` com o `minWidth` errado — deslocado em 1 posição**. Lendo de volta (`style.breakpoints`) os dados parecem certos, mas o **editor renderiza os tamanhos rotacionados** (sintoma clássico: "o maior cai no M", "o S puxa o tamanho do L"). O objeto de Text Style **não** tem `getAttributes()` — leia pela propriedade `style.breakpoints` + o topo (`style.fontSize`/`style.minWidth` = tier primário).

**Mapa observado do bug** (como o editor exibe o que a API gravou):

| Slot | `fontSize` vem de | `minWidth` vem de |
|---|---|---|
| **L** | primário (topo) | `bp[0].minWidth` (maior) |
| **M** | `bp[0].fontSize` | `bp[1].minWidth` |
| **S** | `bp[1].fontSize` | `bp[2].minWidth` |
| **XS** | `bp[2].fontSize` | `0` |

(`bp[…]` = breakpoints ordenados do **maior pro menor** minWidth; o Framer reordena sozinho.)

**Workaround via API (pré-compensação)** — desloca os tamanhos de propósito pra cancelar o bug. Para exibir **L=1200/L, M=810/M, S=390/S**:

```js
await style.setAttributes({
  minWidth: 0, fontSize: `${L}px`, lineHeight, letterSpacing,   // primário → vira o L
  breakpoints: [
    { minWidth: 1200, fontSize: `${M}px`, lineHeight, letterSpacing },  // → vira o M
    { minWidth: 810,  fontSize: `${S}px`, lineHeight, letterSpacing },  // → vira o S
    { minWidth: 390,  fontSize: `${S}px`, lineHeight, letterSpacing },  // → vira XS@0 (dup do S, inofensivo)
  ],
})
```

Resultado no editor: **L 1200/L · M 810/M · S 390/S · XS 0/S**. O XS@0 é duplicata do S — pode apagar no editor. (Script de referência no workspace do molde (Facial Academy): `framer-api/facial-bp-precomp.ts`.) Editar à mão depois é seguro — o editor normaliza.

Valores oficiais (px) para subir no projeto Expert em Lábios 2026:

| Estilo | L (1200) | M (810) | S (390) | LH |
|---|---|---|---|---|
| Display H1 | 60 | 44 | 34 | 1.03 |
| Heading H2 | 38 | 32 | 26 | 1.12 |
| Sub H3 | 24 | 22 | 20 | 1.2 |
| Sub H4 | 20 | 19 | 18 | 1.25 |
| Sub H5 | 17 | 16 | 16 | 1.3 |
| Sub H6 | 15 | 14 | 14 | 1.35 |
| Eyebrow | 12 | 12 | 11 | 1.2 |
| Lead | 18 | 17 | 16 | 1.5 |
| Body | 16 | 16 | 16 | 1.65 |
| Body Small | 14 | 13 | 13 | 1.6 |
| Numeral | 44 | 38 | 32 | 1.0 |
| Legal | 12 | 11 | 11 | 1.5 |

**Botão Label** = 15px fixo (sem breakpoints, não escala).

### Ícones
Biblioteca **Phosphor**, peso **Thin** (traço de **1pt** / `stroke-width:1` na grade 24), cor por `currentColor`. Tamanhos: 16 / 20 / 24 / 32 / 48. Nunca emoji como ícone.

### Gradientes
Somente cores do brand. **Não usar conic, blob nem halo** — preferir **meshes** (radiais multiponto) e lineares. Variantes light sobre base branca. Biblioteca completa na seção 03 · Gradientes do index.html.

---

## Componentes

### Botão — `el-btn`
`class="el-btn <variante> <tamanho>"`
- **Variantes:** `el-fill` (gradiente do CTA, primário) · `el-solid` · `el-outline` · `el-ghost` (texto) · `el-gold` · `el-gold-o`
- **Tamanhos:** `el-sm` · (md = padrão) · `el-lg`
- **Estados:** hover · `:active` · `:focus-visible` · `:disabled` / `[aria-disabled]`
- **Regras:** altura mínima 44px, raio pill, ícone Phosphor opcional (`<svg class="el-ico">`). Use `<button>` (não `<a>` sem href) para ser focável.
- **CTA (preenchido/sólido) consome o token `--cta`, nunca `--roxo2`/`--roxo-bright` direto.** `.el-btn.el-fill` usa `--cta-grad` + `--cta-ink`; `.el-btn.el-solid` usa `--cta-solid` (hover `--cta-solid-h`). O `--cta` é **theme-aware** (ver "CTA — token theme-aware" nos Fundamentos): no escuro o roxo é **mais claro** para o botão passar contraste de componente (WCAG 1.4.11, ≥3:1 vs fundo); no claro fica `#6B99E6` (inalterado).

### Status / feedback — `el-status is-success|is-warning|is-danger|is-info`
Sempre **ícone + texto**, nunca só cor. Verde/âmbar/vermelho saem da paleta de propósito (são funcionais).

### Outros
`el-chip` · `el-badge` (dourado) · `el-card` · `el-logo` (em SVG com `fill="currentColor"`).

---

## Acessibilidade (obrigatório)
- **Contraste WCAG AA em 2 níveis:**
  - **Nível 1 — texto:** ≥4.5:1 (texto normal) / ≥3:1 (texto grande). No light, dourado/rosa como texto = `-ink`.
O CTA escuro usa o gelo `#B3E3FB` com tinta navy `#0F1730` (12.9:1); nada foi "clareado", a marca nasceu assim.
- **Foco visível:** `outline:2px solid var(--lilas)` + `box-shadow var(--focus)`; guard `@media (forced-colors: active)`.
- **`prefers-reduced-motion`:** reduzir transições/animações.
- **Toque ≥44px.** **Cor nunca sozinha** (estados com ícone+texto).

## Faça / Não faça
✅ Consumir tokens · dark+light em paridade · Silka · Phosphor Thin · meshes do brand · foco visível.
🚫 Hex solto nos componentes · cor fora das institucionais (gelo, azul, navy e apoio) · conic/blob/halo · emoji como ícone · texto dourado claro no light (usar `-ink`) · botão `<a>` sem href.

---

## Processo & versionamento

O sistema evolui sob governança: veja **`CONTRIBUTING.md`** (princípios, regra das 3 equipes, gate de "pronto", SemVer e depreciação) e o **`CHANGELOG.md`** (histórico de versões). Regra de ouro dos tokens: `primitive → semantic/intent → component`, e o token semântico **nunca sugere valor**.

---

## Para agentes de IA (Claude e outros)

Ao aplicar este design system em um projeto, **leia `expert-em-labios-design-tokens.json`** e siga as regras acima. Prompt sugerido:

> Você vai aplicar o **Expert em Lábios 2026 Design System** (autor: Edegar Junior). Fonte da verdade: `expert-em-labios-design-tokens.json` + `expert-em-labios-design-system.css` desta pasta.
> Regras inegociáveis: (1) só use as cores institucionais (azul gelo `#B3E3FB`, azul `#6B99E6`, navy `#0F1730` e o apoio) e seus derivados — nada de hex fora da paleta; (2) componha tudo com os tokens (nunca hex solto); (3) entregue **dark e light** com paridade, dark por padrão e light via `data-theme="light"`; (4) tipografia **Silka** com a escala responsiva por breakpoint (Desktop/Tablet/Phone) usando `clamp()`, body ≥16px no mobile; (5) ícones **Phosphor peso Thin** com `currentColor`; (6) gradientes **só meshes/lineares do brand — sem conic/blob/halo**; (7) acessibilidade WCAG AA: foco visível, `prefers-reduced-motion`, toque ≥44px, cor nunca sozinha; (8) botão = `<button>` com as variantes `el-*`.
> Antes de finalizar, verifique contraste nos dois temas e ausência de scroll horizontal de 320px a 1440px.
