# Tema claro e escuro · Facial Premium Design System

Desenvolvido por **Edegar Junior**.

**Regra:** o **escuro é a base** do CSS; o **claro é a variante**. Sem nenhuma indicação, o CSS segue a aparência do sistema do visitante (`prefers-color-scheme`). Na página da rede no GreatPages, **cada página fixa o próprio tema** (ver seção 2).

Toda cor é um token com par Claro e Escuro. Componentes consomem tokens, nunca hex solto, então trocam de tema sozinhos.

### Casos especiais: CTA (`--cta`) e acento (`--acc`)

O **CTA** (botão preenchido ou sólido) usa os tokens **`--cta-grad` / `--cta-solid` / `--cta-solid-h` / `--cta-ink`**. Os botões `.fp-btn.fp-fill` e `.fp-btn.fp-solid` consomem `--cta`, nunca `--roxo2` ou `--roxo-bright` direto. No tema **escuro** o CTA é clareado por contraste de componente (WCAG 1.4.11):

- **Escuro:** `--cta-grad: linear-gradient(120deg,#8561B3,#7956A3)` · `--cta-solid:#8561B3` · `--cta-solid-h:#7956A3` · `--cta-ink:#fff`. Texto branco 4.8:1; botão 4.1:1 contra o fundo `#0C0912`. O `#59378C` dava 2.2:1 contra esse fundo e reprovava.
- **Claro:** `--cta-grad: linear-gradient(120deg,#59378C,#3A2259)` · `--cta-solid:#59378C` · `--cta-solid-h:#8561B3` · `--cta-ink:#fff`. Texto branco 8.9:1.

O **acento Petróleo** muda de tom entre os temas e tem um token próprio para o texto sobre ele (`--acc-on`), usado por `.fp-btn.fp-acc`:

- **Escuro:** `--acc:#2EC5CF` · `--acc-deep:#22A9B3` (hover) · `--acc-on:#06292D` (texto 7.3:1) · `--acc-ink:#2EC5CF` (acento como texto, 9.4:1 no fundo).
- **Claro:** `--acc:#00717F` · `--acc-deep:#005C67` (hover) · `--acc-on:#FFFFFF` (texto 5.7:1; botão 5.5:1 contra `#FAFAFA`) · `--acc-ink:#00717F` (acento como texto, 5.5:1).

---

## 1. Como o CSS resolve o tema (`facial-premium-design-system.css`)

Três camadas, nesta ordem:

```css
/* 1) Base = escuro (padrão) */
:root{ --bg:#0C0912; --txt:#F9F8FD; /* ... todos os tokens do escuro ... */
  --acc:#2EC5CF; --acc-deep:#22A9B3; --acc-on:#06292D;
  --cta-grad:linear-gradient(120deg,#8561B3,#7956A3); --cta-solid:#8561B3; --cta-solid-h:#7956A3; --cta-ink:#fff;
  color-scheme:dark; }

/* 2) Segue o sistema: SO em claro e página sem data-theme="dark" */
@media (prefers-color-scheme: light){
  :root:not([data-theme="dark"]){ --bg:#FAFAFA; --txt:#1F1A26; /* ... claro ... */
    --acc:#00717F; --acc-deep:#005C67; --acc-on:#FFFFFF;
    --cta-solid:#59378C; --cta-ink:#fff; color-scheme:light; }
}

/* 3) Tema fixado na página (ou escolhido no toggle) vence o sistema */
[data-theme="light"]{ --bg:#FAFAFA; --txt:#1F1A26; /* ... claro ... */
  --acc:#00717F; --acc-deep:#005C67; --acc-on:#FFFFFF;
  --cta-solid:#59378C; --cta-ink:#fff; color-scheme:light; }
[data-theme="dark"]{ /* herda o :root escuro */ }
```

Resultado:
- SO escuro e sem `data-theme` → **escuro**
- SO claro e sem `data-theme` → **claro**
- `data-theme` definido → **vence** o sistema

> `color-scheme` em cada tema faz barras de rolagem e controles nativos acompanharem. No claro, Petróleo e Névoa **como texto** usam as variantes `-ink` (`--acc-ink`, `--mist-ink #4A5A63`).

---

## 2. GreatPages: um tema fixo por página

A página da rede vive no GreatPages (https://lp.facialacademy.com.br/rede-facial-premium). Lá o tema não depende do visitante: cada página escolhe o seu.

1. No código personalizado do `<head>` da página, carregue `silka.css` e `facial-premium-design-system.css` (colados inline ou por link, conforme o que a página aceitar).
2. Logo depois, fixe o tema:
```html
<script>document.documentElement.dataset.theme='light';</script>
<!-- ou 'dark' -->
```
3. Nos blocos de HTML personalizado, use as classes `fp-`: elas leem os tokens do tema fixado.
4. Nos elementos nativos do editor (que não leem as variáveis CSS), aplique à mão os valores da tabela de cores do tema escolhido (seção "Tokens para copiar" do `index.html` e seção 2.3 do `IMPLEMENTACAO.md`).

> O que garante a consistência é tudo usar os valores do **mesmo** tema. Misturar um bloco nativo pintado com a cor do escuro numa página fixada em claro quebra o contraste.

---

## 3. Toggle do showcase (referência)

O `index.html` tem um toggle com anti-flash e escolha lembrada em `localStorage` (chave `fp-theme`). Serve para quem quiser oferecer escolha de tema num projeto próprio; a página do GreatPages não usa.

No `<head>`, **antes** da pintura:
```html
<script>(function(){try{var t=localStorage.getItem('fp-theme');
if(t!=='light'&&t!=='dark')t=matchMedia('(prefers-color-scheme: light)').matches?'light':'dark';
document.documentElement.setAttribute('data-theme',t)}catch(e){document.documentElement.setAttribute('data-theme','dark')}})();</script>
```
Botão que alterna e salva:
```js
btn.addEventListener('click',function(){
  var n=document.documentElement.getAttribute('data-theme')==='light'?'dark':'light';
  document.documentElement.setAttribute('data-theme',n);
  localStorage.setItem('fp-theme',n);
});
```

> **Acessibilidade em 2 níveis** (vale para os dois temas): **(1) texto ≥ 4.5:1**; **(2) botão contra o fundo ≥ 3:1** (WCAG 1.4.11).

---

## 4. Checklist
- [ ] A página do GreatPages fixa um tema com `document.documentElement.dataset.theme`.
- [ ] Blocos de HTML personalizado usam classes `fp-` (tokens, nunca hex solto).
- [ ] Elementos nativos do editor usam os valores da tabela do **mesmo** tema.
- [ ] No claro, Petróleo e Névoa como texto usam `-ink`.
- [ ] Botão de acento usa `--acc-on` para o texto (escuro `#06292D`, claro `#FFFFFF`).
- [ ] **Texto** ≥ 4.5:1 (nível 1).
- [ ] **CTA e componentes contra o fundo** ≥ 3:1 nos **dois temas** (nível 2); CTA escuro usa `#8561B3`.
- [ ] CTA preenchido ou sólido consome `--cta-*`, nunca `--roxo2` ou `--roxo-bright` direto.
- [ ] Conferir no tema escolhido: contraste de texto, de componente e legibilidade.
