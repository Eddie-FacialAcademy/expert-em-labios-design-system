# Changelog — Expert em Lábios 2026 Design System

Todas as mudanças relevantes deste design system são registradas aqui.
O formato segue [Keep a Changelog](https://keepachangelog.com/pt-BR/1.1.0/) e o
versionamento segue [SemVer](https://semver.org/lang/pt-BR/):

- **MAJOR** — muda ou remove um token/API público (quebra compatibilidade).
- **MINOR** — adiciona de forma retrocompatível (novo componente/token/variante).
- **PATCH** — correções que não mudam a API (bug, contraste, ajuste fino).

---

## [Não lançado]

_Nada pendente no momento._

## [1.0.2] — 2026-08-28
### Corrigido
- Swatch de preto absoluto removido das cores de marca (o escuro da marca é
  o navy da tinta `#0F1730`); o branco `#FFFFFF` permanece por ser a cor do
  texto no arquivo da versão para fundo escuro.

## [1.0.1] — 2026-08-28
### Corrigido
- Marca refeita com as duas artes oficiais do logo escrito (fundo escuro e
  fundo claro), cores fixas do arquivo: saíram o logo da Facial Class, o
  símbolo de +, a versão monocromática e o ícone (a marca não tem ícone).
  O showcase troca a versão por tema; composições exibidas sobre o fundo
  correto.

## [1.0.0] — 2026-08-28

Primeira versão do Expert em Lábios 2026, curso da Facial Class, derivada do
molde Facial Academy. Paleta extraída do gradiente do numeral 26 do logo
(azul gelo `#B3E3FB`, azul `#6B99E6`) com derivadas medidas em WCAG AA nos
dois temas (40 pares, 0 falhas).

### Marca
- Logo co-brand "facialclass + Expert em Lábios 26" nas composições
  horizontal, vertical, monocromática e o ícone (numeral 26); texto segue o
  tema por `currentColor` com as cores do arquivo (branco no escuro, azul
  `#6B99E6` no claro, cor institucional do próprio logo), 26 mantém o
  gradiente oficial.
- Favicon com o 26 em navy sobre badge de gelo `#B3E3FB` (o único badge claro
  da fileira, distintivo na barra de abas).

### Fundações
- Tema escuro com fundos navy-azulados (`#0A0E1D` a `#1F2547`) e tema claro
  off-white com cartões frios; paridade e contraste **WCAG AA** medidos.
- **CTA de gelo no escuro:** gradiente da marca `#B3E3FB → #6B99E6` com tinta
  navy `#0F1730` (12.9:1 e 6.2:1); claro `#1D3E8F → #2C4FA3` com texto branco.
- Anel de foco em duas camadas (`--focus-ring` escuro `#B3E3FB`, claro
  `#2C4FA3`), presente também no bloco `prefers-color-scheme` do pacote;
  guard de alto contraste com `outline` `!important`.
- Prefixo de classe `el-`; tema em `localStorage` na chave `el-theme`.
- Seção Cores com o grupo "Gradiente da marca": construção do gradiente do 26
  e dos derivados de CTA, com receita CSS.

### Produto
- Copy de demonstração no domínio do curso: lábios, avaliação, proporção,
  técnica com agulha e cânula, naturalidade e casos (ver
  `glossario-marca.md`).

### Navegação do showcase
- Menu "Design systems" com as marcas do ecossistema e scrollspy por
  categorias, herdados do molde.
