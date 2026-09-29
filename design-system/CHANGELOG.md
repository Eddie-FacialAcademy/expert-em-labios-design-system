# Changelog: Expert em Lábios 2026 Design System

Todas as mudanças relevantes deste design system são registradas aqui.
O formato segue [Keep a Changelog](https://keepachangelog.com/pt-BR/1.1.0/) e o
versionamento segue [SemVer](https://semver.org/lang/pt-BR/):

- **MAJOR**: muda ou remove um token/API público (quebra compatibilidade).
- **MINOR**: adiciona de forma retrocompatível (novo componente/token/variante).
- **PATCH**: correções que não mudam a API (bug, contraste, ajuste fino).

---

## [Não lançado]

_Nada pendente no momento._

## [1.1.0] · 2026-09-29
### Alterado
- **Nomes de cor organizados em duas camadas.** Cores da marca (`--brand-*`) levam o nome real da cor nesta marca; tokens de uso têm nomes neutros e iguais em todos os DS do grupo (`--primary`, `--accent`, `--highlight`, `--support`, `--glow`), para o código continuar portável entre marcas. Valores não mudaram: comparação de cor computada em todos os elementos do showcase, antes e depois, nos dois temas, deu zero diferença.
- Tokens de uso: `--roxo-bright` → `--primary-bright`, `--lilas-soft` → `--accent-soft`, `--gold-deep` → `--highlight-deep`, `--gold-line` → `--highlight-line`, `--rose-line` → `--support-line`, `--gold-ink` → `--highlight-ink`, `--rose-ink` → `--support-ink`, `--roxo2` → `--primary`, `--lilas` → `--accent`, `--peach` → `--glow`, `--roxo` → `--primary-deep`, `--gold` → `--highlight`, `--rose` → `--support`.
- Cores da marca: `--brand-amarelo` → `--brand-dourado`, `--brand-vermelho` → `--brand-rosa`, `--brand-amarelado` → `--brand-pessego`, `--brand-roxo` → `--brand-azul`, `--brand-lilas` → `--brand-azul-gelo`.
- JSON de tokens: chaves renomeadas igual aos tokens (camelCase) e mapa de/para em `$deprecated`.
- Variantes de botão `el-gold` e `el-gold-o` viraram `el-highlight` e `el-highlight-o`; os nomes antigos continuam valendo no CSS de colar no site.
- Nomes exibidos no showcase ligados à cor real: acentos compartilhados do grupo como **Dourado claro**, **Rosa claro** e **Pêssego** (antes "Amarelo claro", "Vermelho claro" e "Amarelado", com a mesma cor chamada de formas diferentes entre DS); rótulos de gradiente gerados a partir das cores de cada gradiente.
- Documentação técnica: seção 13 virou "Relação com o molde", só com valores deste DS (a tabela anterior repetia valores de outra marca e desatualizava).
### Descontinuado
- Os nomes antigos listados acima continuam funcionando como apelidos no CSS de colar no site e saem na 2.0. Use os nomes novos em código novo.

## [1.0.3] · 2026-09-29
### Corrigido
- `--brand-navy` presente também no showcase (antes só no CSS e no JSON).
- Tabela de acessibilidade do showcase com valores medidos nos dois temas (antes repetia números do molde que não eram desta paleta) e linha nova "CTA contra o fundo" (nível 2).
### Alterado
- Seletor de design systems inclui a Facial Premium, na ordem única usada em todos os DS.
- Versão alinhada em todos os arquivos: tokens, CSS, copy-deck e documentação estavam presos em uma versão anterior ao CHANGELOG.
- Documentação sem travessão e sem "&", com valores de cor, contraste e classe conferidos contra o CSS e o JSON; referências a versões e arquivos inexistentes corrigidas.

## [1.0.2] · 2026-08-28
### Corrigido
- Swatch de preto absoluto removido das cores de marca (o escuro da marca é
  o navy da tinta `#0F1730`); o branco `#FFFFFF` permanece por ser a cor do
  texto no arquivo da versão para fundo escuro.

## [1.0.1] · 2026-08-28
### Corrigido
- Marca refeita com as duas artes oficiais do logo escrito (fundo escuro e
  fundo claro), cores fixas do arquivo: saíram o logo da Facial Class, o
  símbolo de +, a versão monocromática e o ícone (a marca não tem ícone).
  O showcase troca a versão por tema; composições exibidas sobre o fundo
  correto.

## [1.0.0] · 2026-08-28

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
