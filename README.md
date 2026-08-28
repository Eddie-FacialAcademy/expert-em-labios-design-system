# Expert em Lábios 2026 — Design System

Design system do **Expert em Lábios 2026** (curso expert de preenchimento labial da Facial Class, no ecossistema Facial Academy). Paleta em **azul gelo `#B3E3FB`** e **azul `#6B99E6`**, extraída do gradiente do numeral 26 do logo co-brand; tipografia **Silka** (embutida em woff2, headers em **Medium 500**).

Desenvolvido por **Edegar Junior**.

## Entregas

- **index.html** — design system reutilizável (showcase navegável): paleta (institucional + derivada, com o grupo "Gradiente da marca" e a construção do gradiente do 26), temas **dark/light**, tipografia (Silka), **gradientes**, **ícones** (Phosphor Thin, copiar SVG), **logos** (horizontal, vertical, monocromático e ícone; copiar/baixar SVG) e sistema de **botões** com o **CTA de gelo** no tema escuro. Click-to-copy em cores, valores e código; download PNG dos gradientes.
  - 🌐 **Online (para compartilhar):** https://eddie-facialacademy.github.io/expert-em-labios-design-system/ — GitHub Pages (repo público `expert-em-labios-design-system`).

## Design System portátil (`design-system/`)

Pacote para aplicar a marca em **qualquer projeto/ferramenta** (web, React, Framer, agentes de IA).

- **silka.css** — fonte **Silka** (pesos 300–700) embutida em woff2/base64, self-contained; linke antes do CSS principal.
- **expert-em-labios-design-system.css** — drop-in (tokens dark/light, CTA theme-aware: escuro gelo `#B3E3FB` com tinta navy `#0F1730`, claro `#1D3E8F` com branco). Prefixo de classe `el-`.
- **expert-em-labios-design-tokens.json** — tokens legíveis por máquina (Style Dictionary, Framer, IA).
- **Button.tsx** — Code Component Framer/React com Property Controls.
- **DESIGN-SYSTEM.md** — spec completa, 3 formas de aplicar e **prompt pronto para IA**.
- **THEME.md** — como o claro/escuro é configurado e ativado pelo tema do sistema do visitante (web + Framer).

## Notas técnicas

- **Cores:** extraídas do **gradiente do 26** (azul gelo `#B3E3FB`, azul `#6B99E6`) mais o navy `#0F1730` da tinta do CTA e o apoio herdado da família (amarelo claro `#FFE4A4`, vermelho claro `#FFB1BD`, amarelado `#FFCA9B`). Derivadas medidas em WCAG AA nos dois temas (40 pares, 0 falhas).
- **Logo:** co-brand "facialclass + Expert em Lábios 26". Texto nas cores do arquivo: branco sobre escuro, azul `#6B99E6` sobre claro (cor institucional do próprio logo; logos são isentos da exigência de contraste da WCAG). O 26 mantém o gradiente oficial e não se recolore.
- **Tipografia:** Silka (institucional), embutida em base64/woff2; Poppins como fallback, depois system-ui. **Headers em Medium (500)**.
- **Ícones:** biblioteca **Phosphor**, peso **Thin** (stroke 1pt na grade 24), `currentColor`.
- **Tema:** dark por padrão; light via `data-theme="light"`; sem atributo segue `prefers-color-scheme`. Toggle persiste em `el-theme`.
- **Acessibilidade (2 níveis):** (1) texto ≥4.5:1; (2) componente/botão vs fundo ≥3:1 (WCAG 1.4.11). CTA de gelo: tinta navy 12.9:1 e botão vs fundo 14:1.

## Publicação

Repo público `expert-em-labios-design-system` (conta `Eddie-FacialAcademy`), branch `main`, `index.html` na raiz, GitHub Pages. `.git` fora do OneDrive (`AppData\Local\gitdirs\`); line-endings LF (`.gitattributes`). Deploy: editar → `git add/commit/push` (credencial no Cofre do Windows, sem token). Ver `HANDOFF.md`.

## CHANGELOG

- **1.0.0** (2026-08-28) — primeira versão da marca, derivada do molde Facial Academy com paleta do gradiente do 26 (gelo e azul). Histórico completo em `design-system/CHANGELOG.md`.
