# Tema claro/escuro: Expert em Lábios 2026 Design System

Desenvolvido por **Edegar Junior**.

**Regra:** o **dark é a base**; o **light é a variante**. O site/app **segue automaticamente a aparência do sistema do visitante** (`prefers-color-scheme`). Opcionalmente, um **toggle** deixa o usuário escolher e a escolha é **lembrada** (`localStorage`).

Toda cor é um token com par **Light/Dark**. Componentes consomem tokens (nunca hex solto), então trocam de tema sozinhos.

### Caso especial: CTA theme-aware (`--cta`)

O **CTA** (botão preenchido/sólido) é theme-aware via os tokens **`--cta-grad` / `--cta-solid` / `--cta-solid-h` / `--cta-ink`**. Os botões `.el-btn.el-fill` e `.el-btn.el-solid` consomem **`--cta`**, nunca `--primary` / `--primary-bright` direto.

Diferente da maioria dos tokens (que só invertem Light/Dark), o CTA muda por tema (botão de gelo no escuro, azul profundo no claro) por acessibilidade de **contraste de componente** (WCAG 1.4.11):

- **Dark:** `--cta-grad: linear-gradient(120deg,#B3E3FB,#6B99E6)` · `--cta-solid:#B3E3FB` · `--cta-solid-h:#9CD4F5` · `--cta-ink:#0F1730`. O escuro usa o gelo `#B3E3FB` com tinta navy `#0F1730` (12.9:1); o claro usa `#1D3E8F` com branco.
- **Light:** `--cta-grad: linear-gradient(120deg,#1D3E8F,#2C4FA3)` · `--cta-solid:#1D3E8F` · `--cta-solid-h:#16306F` · `--cta-ink:#fff`.

---

## 1. Web (HTML/CSS): já implementado em `expert-em-labios-design-system.css`

Três camadas, nesta ordem:

```css
/* 1) Base = dark (padrão) */
:root{ --bg:#0A0E1D; --txt:#F7FAFE; /* … todos os tokens dark … */
  /* CTA clareado no dark (a11y de componente, WCAG 1.4.11): */
  --cta-grad:linear-gradient(120deg,#B3E3FB,#6B99E6); --cta-solid:#B3E3FB; --cta-solid-h:#9CD4F5; --cta-ink:#0F1730;
  color-scheme:dark; }

/* 2) Segue o sistema: se o SO está em light e o usuário NÃO escolheu manualmente */
@media (prefers-color-scheme: light){
  :root:not([data-theme="dark"]){ --bg:#FAFAFA; --txt:#131A33; /* … light … */
    --cta-solid:#1D3E8F; --cta-ink:#fff; /* CTA light inalterado */ color-scheme:light; }
}

/* 3) Escolha manual do usuário (toggle) vence o sistema */
[data-theme="light"]{ --bg:#FAFAFA; --txt:#131A33; /* … light … */
  --cta-solid:#1D3E8F; --cta-ink:#fff; /* CTA light inalterado */ color-scheme:light; }
[data-theme="dark"]{ /* herda o :root dark */ }
```

Resultado:
- SO dark + sem escolha → **dark**
- SO light + sem escolha → **light** (automático)
- `data-theme` definido → **vence** o sistema

### Toggle (anti-flash + persistente)
No `<head>`, **antes** da pintura, pra não piscar:
```html
<script>(function(){try{var t=localStorage.getItem('el-theme');
if(t!=='light'&&t!=='dark')t=matchMedia('(prefers-color-scheme: light)').matches?'light':'dark';
document.documentElement.setAttribute('data-theme',t)}catch(e){document.documentElement.setAttribute('data-theme','dark')}})();</script>
```
Botão que alterna e salva:
```js
btn.addEventListener('click',function(){
  var n=document.documentElement.getAttribute('data-theme')==='light'?'dark':'light';
  document.documentElement.setAttribute('data-theme',n);
  localStorage.setItem('el-theme',n);
});
```

> `color-scheme` em cada tema faz scrollbars/controles nativos acompanharem. No light, dourado/rosa como **texto** usam as variantes `-ink`.

> **Acessibilidade em 2 níveis** (vale para os dois temas): **(1) texto ≥ 4.5:1** (AA); **(2) componente/botão vs fundo ≥ 3:1** (WCAG 1.4.11, Non-text Contrast). CTA de gelo no escuro e azul profundo no claro, ambos medidos nos 2 níveis.

---

## 2. Framer: como deve ser feito

1. **Color Styles com Light + Dark** (a subir quando o projeto Framer da marca existir): cada estilo tem valor de Light e de Dark.
2. **Aplique os Color Styles** nos fills/textos das camadas (não use hex solto). Como o estilo carrega os dois valores, a camada troca de tema sozinha.
3. **Ativação por tema do visitante:** o site publicado **segue o `prefers-color-scheme`** do sistema automaticamente quando as cores usam Color Styles com variante Dark. Não precisa de código.
4. **Toggle manual no Framer (opcional):** crie uma Variable de tema (ou use um Component com variantes Light/Dark) ligada a um botão; ela sobrepõe o tema do sistema, equivalente ao `data-theme` da web. Persistência fica por conta do toggle.

> Importante: o que faz o tema funcionar é **tudo usar os Color Styles**. Qualquer cor hardcoded não troca. Mesma regra da web (tokens, nunca hex solto).

---

## 3. Checklist
- [ ] Todas as superfícies/textos usam Color Styles (web: tokens; Framer: Color Styles).
- [ ] `prefers-color-scheme` ativo (web: o `@media`; Framer: Color Styles com Dark).
- [ ] Toggle opcional persiste a escolha (`el-theme`) e sobrepõe o sistema.
- [ ] No light, texto dourado/rosa usa `-ink` (contraste AA).
- [ ] **Texto** ≥ 4.5:1 (AA), nível 1 de acessibilidade.
- [ ] **CTA/componente vs fundo** ≥ 3:1 (WCAG 1.4.11) nos **dois temas**, nível 2; o CTA dark usa o gelo `#B3E3FB` com tinta navy (não `#6B99E6`) para passar.
- [ ] CTA preenchido/sólido consome `--cta` (`--cta-grad`/`--cta-solid`/`--cta-solid-h`/`--cta-ink`), nunca `--primary`/`--primary-bright` direto.
- [ ] Testar nos dois temas (contraste de texto e de componente, e legibilidade).
