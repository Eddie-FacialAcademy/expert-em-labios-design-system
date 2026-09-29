# Handoff: Expert em Lábios 2026 Design System (Versão 1.0.3 · estado em 2026-09-29)

Desenvolvido por **Edegar Junior**. Ponto de retomada; atualizar conforme avançar.

## ✅ Concluído

### Design system online (GitHub Pages)
- **URL pública:** https://eddie-facialacademy.github.io/expert-em-labios-design-system/
- Repo público `expert-em-labios-design-system` (conta `Eddie-FacialAcademy`), branch `main`, `index.html` na raiz.
- `index.html`: showcase self-contained, dark/light automático + toggle (chave `el-theme`), click-to-copy, **copiar/baixar SVG** de logos, **download PNG** dos gradientes, menu "Design systems" entre as marcas e favicon do 26 (badge de gelo, o único claro da fileira).

### Marca
- Curso da **Facial Class**, derivado do molde **Facial Academy** (mesma arquitetura, seções e JS).
- Paleta extraída do **gradiente do 26**: azul gelo `#B3E3FB` e azul `#6B99E6`. Derivadas: azul claro `#9CD4F5`, azul texto `#2C4FA3`, azul CTA claro `#1D3E8F`, azul profundo `#16306F`, navy da tinta `#0F1730`, fundos escuros navy-azulados `#0A0E1D` a `#1F2547`. Apoio herdado: amarelo `#FFE4A4`, vermelho claro `#FFB1BD`, amarelado `#FFCA9B`.
- **Logo:** o logo escrito "Expert em LÁBIOS 26", em DUAS versões oficiais com cores fixas do arquivo: fundo escuro (`experte em labios 2026 2.svg`, texto branco + 26 em gradiente) e fundo claro (`experte em lábio 26.svg`, texto azul + 26 branco). **Sem monocromático, sem ícone, sem vertical, sem o logo da Facial Class.** Não recolorir; o showcase troca a versão por tema. Fonte: `34 - Expert em Lábios 2026/_assets` (esses 2 arquivos; o restante da pasta é legado).
- **CTA de gelo (assinatura da marca no escuro):** gradiente `#B3E3FB → #6B99E6` com tinta navy `#0F1730`; no claro, `#1D3E8F → #2C4FA3` com branco.
- **Domínio:** preenchimento labial expert (avaliação, proporção, agulha e cânula, naturalidade, casos). Glossário em `design-system/glossario-marca.md`.

### Acessibilidade (medida, não estimada)
- 40 pares de contraste medidos antes do build, 0 falhas; varredura renderizada nos 2 temas.
- Anel de foco em 2 camadas: `--focus-ring` escuro `#B3E3FB`, claro `#2C4FA3` (presente também no bloco `prefers-color-scheme` do pacote); guard forced-colors com `outline !important`.

### Pacote portátil (`design-system/`)
- `silka.css` · `expert-em-labios-design-system.css` (prefixo `el-`) · `expert-em-labios-design-tokens.json` · `Button.tsx` · `THEME.md` · `DESIGN-SYSTEM.md` · `IMPLEMENTACAO.md` · `CHANGELOG.md` · `CONTRIBUTING.md` · `copy-deck.expert-em-labios.json` · `glossario-marca.md` · `voz-e-tom.md`.

## 📌 Próximos passos possíveis
- Landing/página da marca no Framer (subir Color Styles e Text Styles a partir dos tokens).

## Como publicar mudanças
Editar → `git add/commit/push` na `main` (credencial no Cofre do Windows; `.git` em `AppData\Local\gitdirs\expert-em-labios-design-system`; line-endings LF via `.gitattributes`). O GitHub Pages atualiza sozinho em ~1 minuto.
