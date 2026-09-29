# Implementação · Facial Premium Design System

Documentação técnica de **como cada item é implementado**. Canal atual: a página da rede no GreatPages (https://lp.facialacademy.com.br/rede-facial-premium). Os mesmos arquivos servem para qualquer outro projeto via tokens. Em caso de divergência, **`facial-premium-design-tokens.json` e `facial-premium-design-system.css` são a fonte da verdade**; o showcase (`index.html`) é a referência visual.

- **Sem etapa de build.** O showcase é um único `index.html` self-contained (CSS em `<style>`, SVGs em `<defs><symbol>`, JS em `<script>`, Silka embutida em base64). Abre direto no navegador, sem dependência de rede.
- **Molde:** Facial Academy. Mesma arquitetura; mudam paleta, logo, prefixo de classe (`fp-`), chave de tema e copy. Ver a seção 13.

---

## 1. Arquitetura e arquivos

```
Facial Premium - Design System/
├── index.html                               # Showcase self-contained (referência visual)
├── README.md · HANDOFF.md                   # Visão geral e retomada
└── design-system/                           # PACOTE consumível
    ├── silka.css                            # @font-face Silka 300 a 700 (woff2 base64)
    ├── facial-premium-design-system.css     # CSS DE COLAR: tokens, reset, foco, movimento, tipografia, botões e componentes fp-
    ├── facial-premium-design-tokens.json    # Tokens legíveis por máquina
    ├── copy-deck.facial-premium.json        # Textos canônicos da rede
    ├── Button.tsx                           # Code Component Framer/React (migração futura, fora do GreatPages)
    ├── DESIGN-SYSTEM.md                     # Spec, aplicação e prompt para IA
    ├── THEME.md                             # Mecânica claro e escuro, tema fixo por página
    ├── CONTRIBUTING.md                      # Governança
    ├── CHANGELOG.md                         # Histórico
    ├── IMPLEMENTACAO.md                     # Este documento
    ├── voz-e-tom.md                         # Guia de copy
    └── glossario-marca.md                   # Vocabulário da rede
```

**Duas camadas de classe:**
- **CSS do pacote** usa classes com prefixo **`fp-`** (`.fp-btn`, `.fp-fill`, `.fp-h1`, `.fp-alert`, `.fp-dtbl`...). Estados ficam sem prefixo (`is-error`, `is-success`, `is-sel`, `is-active`, `is-out`, `is-today`, `is-range`, `active`). É o que se usa nos blocos de HTML personalizado do GreatPages.
- **Showcase** (`index.html`) usa classes curtas próprias (`.b`, `.alert`, `.dtbl`, `.cmdk`...) no `<style>` interno. Todos esses componentes já têm equivalente `fp-` no CSS do pacote; os snippets abaixo usam os nomes do pacote.

---

## 2. Tokens e tema

### 2.1 Mecânica de tema

Três camadas, nesta ordem de precedência:
1. **Padrão = escuro.** O bloco `:root` define o tema escuro.
2. **Claro pelo sistema** via `@media (prefers-color-scheme: light)` em `:root:not([data-theme="dark"])`.
3. **Tema fixado** via `[data-theme="light"]` (ou `"dark"`) no `<html>`, que vence o sistema.

`color-scheme` é declarado em cada tema (controles nativos acompanham).

**No GreatPages:** cada página fixa o tema no código personalizado do `<head>`:
```html
<script>document.documentElement.dataset.theme='light';</script>  <!-- ou 'dark' -->
```

**No showcase:** um init anti-flash lê `localStorage['fp-theme']` antes da pintura, e o toggle (`#themeToggle`, com `aria-pressed`) alterna `data-theme` e grava a escolha. Um listener de `matchMedia('(prefers-color-scheme: light)')` só reage se o usuário não fixou preferência. Código completo em `THEME.md`.

### 2.2 Cores institucionais (base imutável)

| Token | Hex | Papel |
|---|---|---|
| `--brand-ameixa` | `#3A2259` | base do gradiente do logo |
| `--brand-roxo` | `#59378C` | Roxo Premium, predominante |
| `--brand-roxo-medio` | `#74529C` | meio do gradiente do logo |
| `--brand-lilas` | `#C6B7DA` | topo do gradiente do logo |
| `--brand-petroleo` | `#00717F` | acento exclusivo do Premium |
| `--brand-nevoa` | `#B8C7CF` | neutro frio de apoio |
| `--brand-areia` | `#E3DCD2` | neutro quente de apoio |
| `--brand-branco` | `#FFFFFF` | |
| `--brand-grafite` | `#1D1D1B` | texto do logo no claro |

Os `--brand-*` **não** mudam entre temas; os tokens de tema abaixo derivam deles.

### 2.3 Tokens de tema

| Token | Escuro | Claro | Uso |
|---|---|---|---|
| `--bg` | `#0C0912` | `#FAFAFA` | fundo da página |
| `--bg2` | `#15101D` | `#F4F2F7` | fundo alternativo, app shell |
| `--card` | `#1C1528` | `#FBFAFC` | superfície de cartão e controle |
| `--card2` | `#241B33` | `#EEEAF3` | superfície elevada, hover |
| `--line` | `rgba(198,183,218,.14)` | `rgba(89,55,140,.16)` | bordas e divisores |
| `--txt` | `#F9F8FD` | `#1F1A26` (16.3:1) | texto principal |
| `--mut` | `#C4BDCF` | `#5E5670` (6.6:1) | texto secundário |
| `--legal-mut` | `#8F80AE` | `#5E5670` | texto legal e rodapé |
| `--primary-deep` | `#3A2259` | `#3A2259` | roxo profundo (gradiente) |
| `--primary` | `#59378C` | `#59378C` | primária (seleção, dia selecionado) |
| `--primary-bright` | `#8561B3` | `#8561B3` | roxo claro (base do CTA escuro) |
| `--accent` | `#C6B7DA` | `#59378C` (8.6:1) | **accent interativo** (links, ativo, foco) |
| `--accent-soft` | `#D6CBE5` | `#6A4A9E` | hover do accent |
| `--logo` | `#FFFFFF` | `#1D1D1B` | cor do texto do logo SVG |
| `--highlight` | `#2EC5CF` | `#00717F` | acento Petróleo (preenchimento) |
| `--highlight-deep` | `#22A9B3` | `#005C67` | hover do acento |
| `--highlight-on` | `#06292D` (7.3:1) | `#FFFFFF` (5.7:1) | texto sobre o acento |
| `--highlight-ink` | `#2EC5CF` (9.4:1) | `#00717F` (5.5:1) | acento como texto e borda |
| `--highlight-line` | `rgba(46,197,207,.42)` | `rgba(0,113,127,.55)` | borda suave do acento |
| `--support` / `--support-ink` | `#B8C7CF` / `#B8C7CF` | `#B8C7CF` / `#4A5A63` (6.9:1) | Névoa preenchimento / texto |
| `--support-line` | `rgba(184,199,207,.42)` | `rgba(74,90,99,.50)` | borda da Névoa |
| `--glow` | `#E3DCD2` | `#E3DCD2` | Areia (apoio) |

Contrastes do claro medidos contra `#FAFAFA`; os do escuro contra `#0C0912`, salvo `--highlight-on` (medido sobre o `--highlight` do tema).

#### CTA: token por tema (contraste de componente)

O **CTA** muda de tom entre os temas por **WCAG 1.4.11** (*Non-text Contrast*, ≥ 3:1 do botão contra o fundo). No escuro, `#59378C` dava 2.2:1 contra `#0C0912`; o CTA escuro é `#8561B3` (4.1:1; texto branco 4.8:1). No claro o CTA é `#59378C` (texto branco 8.9:1).

| Token | Escuro | Claro | Uso |
|---|---|---|---|
| `--cta-grad` | `linear-gradient(120deg,#8561B3,#7956A3)` | `linear-gradient(120deg,#59378C,#3A2259)` | fundo do `.fp-fill` |
| `--cta-solid` | `#8561B3` | `#59378C` | fundo do `.fp-solid` |
| `--cta-solid-h` | `#7956A3` | `#8561B3` | hover do sólido |
| `--cta-ink` | `#fff` | `#fff` | texto sobre o CTA |

> **Regra:** os botões fill e solid consomem **`--cta-*`**, nunca `--primary` ou `--primary-bright` direto. O `--primary #59378C` segue como primária para seleção.

**Semânticas** (sempre com ícone ou rótulo, nunca cor sozinha):

| Token | Escuro | Claro |
|---|---|---|
| `--success` / `--success-bg` | `#45C08A` / `rgba(69,192,138,.14)` | `#147A45` / `rgba(31,138,91,.10)` |
| `--warning` / `--warning-bg` | `#E8B53D` / `rgba(232,181,61,.14)` | `#8A5A00` / `rgba(138,90,0,.10)` |
| `--danger` / `--danger-bg` | `#FF7D93` / `rgba(255,125,147,.14)` | `#BE2C45` / `rgba(199,47,73,.10)` |
| `--info` / `--info-bg` | `#C6B7DA` / `rgba(198,183,218,.14)` | `#4B2F78` / `rgba(75,47,120,.10)` |
| `--row-sel` | `rgba(198,183,218,.16)` | `rgba(89,55,140,.10)` |
| `--focus-ring` | `#C6B7DA` | `#59378C` |

### 2.4 Escalas e fundações (iguais nos dois temas, salvo sombra)

```
/* Raio */            --radius-sm:8px  --radius-md:14px  --radius-lg:18px  --radius-pill:30px
/* Espaçamento */     --space-1:4  -2:8  -3:12  -4:16  -6:24  -8:32  -12:48 (px)
/* Movimento */       --motion-fast:.15s  --motion:.2s  --motion-slow:.4s  --ease:cubic-bezier(.2,.8,.2,1)
/* Foco */            --focus:0 0 0 2px var(--bg), 0 0 0 4px var(--focus-ring)
/* z-index */         --z-base:0  --z-raised:10  --z-sticky:40  --z-overlay:100  --z-toast:1000
/* Opacidade */       --opacity-disabled:.45  --opacity-muted:.66  --opacity-hover:.08  --opacity-overlay:.58
/* Borda */           --bw-hair:1px  --bw-1:1px  --bw-2:2px
/* Blur */            --blur-sm:6px  --blur-md:12px  --blur-lg:20px
/* Breakpoints */     --bp-phone:390px  --bp-tablet:810px  --bp-desktop:1200px
/* Tamanhos */        --size-icon-sm:16  --size-icon:20  --size-icon-lg:24  --control-h:44  --touch-min:44 (px)
/* Proporção */       --ar-square:1/1  --ar-photo:4/3  --ar-wide:16/9
/* Code (escuro nos 2 temas) */ --code-bg:#07060A  --code-txt:#D6CBE5  --code-comment:#9A8BB8  --code-key:#2EC5CF
/* Componentes */     --row-h:46px  --row-h-compact:38px  --side-w:248px  --cal-cell:38px
```

**Elevação (sombra em camadas; preta no escuro, com matiz roxo no claro):**
```
--elev-1 a --elev-4                            (cada nível mais difuso)
--elev-3 escuro: 0 4px 12px rgba(0,0,0,.45), 0 16px 36px rgba(0,0,0,.55)
--elev-raised:var(--elev-1)  --elev-overlay:var(--elev-3)  --elev-modal:var(--elev-4)
--sh / --sh-strong: rgba(89,55,140,.40/.50) escuro · .18/.26 claro  (brilho do botão fill)
```
**Regra:** use o papel (`--elev-raised/overlay/modal`), não o número.

### 2.5 Formato do `facial-premium-design-tokens.json`

JSON próprio (sem `$value/$type`), com os temas separados dentro de cada categoria:
```
{ $meta, breakpoints, color:{brand,dark,light}, elevation:{roles,dark,light},
  radius, foundations:{opacity,borderWidth,blur,breakpoint,size,aspectRatio},
  space, zIndex, motion, focus, focusRing, typography:{fontFamily,weights,styles{...}},
  components:{button,statusColors,prefix,library,stateClasses}, icons, gradients, accessibility }
```
Consuma gerando suas variáveis. **Regra de ouro:** componente lê token, nunca hex solto.

---

## 3. Fundamentos (reset, foco, movimento, tipografia, ícones, logo)

### 3.1 Reset e base
```css
*{margin:0;padding:0;box-sizing:border-box}
html{scroll-behavior:smooth}
body{font-family:var(--font-sans);background:var(--bg);color:var(--txt);line-height:1.5;
     -webkit-font-smoothing:antialiased;font-variant-numeric:tabular-nums}
img,svg,video{display:block;max-width:100%}
a{color:var(--accent);text-decoration:none}
```
> **Atenção no GreatPages:** o reset é global (`*`, `body`, `a`). Ao colar o CSS na página, confira se os elementos nativos do editor continuam com a aparência esperada.

### 3.2 Foco visível (obrigatório)
```css
a:focus-visible,button:focus-visible,.fp-btn:focus-visible,[tabindex]:focus-visible{
  outline:2px solid var(--accent);outline-offset:2px;box-shadow:var(--focus);border-radius:6px}
@media (forced-colors: active){
  a:focus-visible,button:focus-visible,.fp-btn:focus-visible{outline:2px solid Highlight!important;outline-offset:2px}}
```
Componentes que removem `outline` repõem com `box-shadow:var(--focus)`.

### 3.3 Movimento reduzido
```css
@media (prefers-reduced-motion: reduce){
  html{scroll-behavior:auto}
  *,*::before,*::after{transition-duration:.01ms!important;animation-duration:.01ms!important}}
```
(Ao medir contraste por script, desative as transições antes, senão o valor lido pode ser o intermediário da troca de tema.)

### 3.4 Tipografia
- Pilha: `'Silka','Poppins',system-ui,-apple-system,'Segoe UI',Roboto,sans-serif`. Silka é a base de todos os design systems do grupo, embutida em `silka.css` (pesos 300, 400, 500, 600 e 700, woff2 base64). Sem Silka: Poppins, depois `system-ui`.
- Escala fluida com `clamp()` por papel: `.fp-eyebrow`, `.fp-h1` a `.fp-h6`, `.fp-lead`, `.fp-body`, `.fp-small`, `.fp-legal`, `.fp-num`, `.fp-hl` (destaque em `--accent`). Ex.: `.fp-h1{font-size:clamp(34px,6vw,60px);font-weight:500;letter-spacing:-.025em;line-height:1.03}`. Corpo mínimo **16px** no celular.
- Valores por breakpoint (Desktop 1200 / Tablet 810 / Phone 390) na tabela do `DESIGN-SYSTEM.md`, para os elementos nativos do editor.

### 3.5 Ícones
- Biblioteca **Phosphor**, peso **Thin** (traço 1 na grade 24). No showcase, definidos uma vez em `<svg><defs><symbol id="ph-...">` e referenciados por `<use href="#ph-..."/>`.
- Cor por `currentColor`. Ícone decorativo leva `aria-hidden="true"` e nada focável dentro dele; ícone que informa estado vem **com texto**.

### 3.6 Logo
- Fonte: SVGs oficiais em `_FA - Assets\Facial Premium\_SVG` (versões colorida, mono branca e mono grafite).
- No showcase, os lockups são `<symbol>`: `logo-hor` (horizontal), `logo-compact` (compacto), `logo-vert` (vertical centralizado, arquivo v2), `logo-stack` (vertical à esquerda, arquivo v3), `logo-icon` (ícone isolado). O texto do logo usa `currentColor` com `--logo` (branco no escuro, `#1D1D1B` no claro); o ícone mantém o gradiente oficial `#3A2259 → #59378C → #74529C → #C6B7DA`.
- No CSS do pacote: `.fp-logo{color:var(--logo)}` num SVG com `fill="currentColor"` no texto.
- Mínimo: ícone 24px, horizontal 140px. Não recolorir o gradiente nem recompor o logotipo em Silka.

### 3.7 Gradientes
Só cores da paleta. Classes: `fp-grad-primary` (`#59378C → #3A2259`), `fp-grad-acento` (ameixa, roxo e petróleo), `fp-grad-spectral` (ameixa, roxo, lilás, névoa, areia), `fp-grad-mesh` (radiais sobre `#0C0912`) e `fp-grad-spot` (radial no topo). Sem cônico, blob ou halo. Uso: fundo de seção ou de imagem, nunca texto pequeno.

---

## 4. Botões (componente central)

Classe base **`.fp-btn`**. Composição: `.fp-btn` + variante (`.fp-fill` / `.fp-solid` / `.fp-outline` / `.fp-ghost` / `.fp-acc` / `.fp-acc-o`) + tamanho opcional (`.fp-sm` / `.fp-lg`). Ícone interno: `.fp-ico`.

```css
.fp-btn{display:inline-flex;align-items:center;justify-content:center;gap:9px;
  font-family:inherit;font-size:15px;font-weight:600;border:none;cursor:pointer;text-decoration:none;
  border-radius:var(--radius-pill);transition:.2s var(--ease);white-space:nowrap;min-height:44px;max-width:100%;padding:14px 26px}
```

### 4.1 Tamanhos
| Classe | font-size | padding | gap | ícone |
|---|---|---|---|---|
| `.fp-sm` | 13px | 10px 18px | 7px | 15px |
| md (padrão) | 15px | 14px 26px | 9px | 18px |
| `.fp-lg` | 16px | 17px 32px | 9px | 19px |

### 4.2 Variantes e estados
```css
/* Preenchido (gradiente do CTA com brilho) */
.fp-btn.fp-fill{background:var(--cta-grad);color:var(--cta-ink);box-shadow:0 10px 30px var(--sh)}
.fp-btn.fp-fill:hover{transform:translateY(-2px);box-shadow:0 16px 38px var(--sh-strong)}

/* Sólido (CTA) */
.fp-btn.fp-solid{background:var(--cta-solid);color:var(--cta-ink)}
.fp-btn.fp-solid:hover{background:var(--cta-solid-h)}

/* Contorno */
.fp-btn.fp-outline{background:transparent;color:var(--txt);border:1px solid var(--line)}
.fp-btn.fp-outline:hover{border-color:var(--accent);color:var(--accent)}

/* Texto (ghost) */
.fp-btn.fp-ghost{background:transparent;color:var(--accent);padding:10px 14px;border-radius:var(--radius-sm)}
.fp-btn.fp-ghost:hover{color:var(--accent-soft);text-decoration:underline;text-underline-offset:3px}

/* Acento Petróleo e acento contorno */
.fp-btn.fp-highlight{background:var(--highlight);color:var(--highlight-on);border:1px solid var(--highlight-ink)}
.fp-btn.fp-highlight:hover{background:var(--highlight-deep)}
.fp-btn.fp-highlight-o{background:transparent;color:var(--highlight-ink);border:1px solid var(--highlight-line)}
.fp-btn.fp-highlight-o:hover{border-color:var(--highlight-ink)}
```
Contraste do acento: escuro `#2EC5CF` com texto `#06292D` (7.3:1; hover `#22A9B3` 5.4:1); claro `#00717F` com texto branco (5.7:1; hover `#005C67` 7.7:1) e 5.5:1 contra o fundo.

### 4.3 Estados globais (microinteração)
```css
.fp-btn:active{transform:translateY(0) scale(.985);transition-duration:var(--motion-fast)}
.fp-btn:disabled,.fp-btn[aria-disabled="true"]{opacity:.42;pointer-events:none;box-shadow:none;transform:none}
@media(max-width:560px){.fp-btn{white-space:normal;text-align:center}}
```
Resumo: `transition:.2s var(--ease)`; `fp-fill` sobe 2px no hover e o brilho cresce (`--sh` → `--sh-strong`); `:active` faz `scale(.985)` em `.15s`. O brilho vive só no botão. Alvo de toque mínimo 44px.

**Destino:** todo botão de CTA aponta para um destino real (âncora existente na página, formulário ou contato com a consultora). Use `<a class="fp-btn" href="...">` para navegar e `<button>` para ação.

### 4.4 `Button.tsx` (migração futura)
Code Component para Framer ou React, com Property Controls. **Não é usado no GreatPages.**
```
label:string="Quero ser membro" · variant:"fill|solid|outline|ghost|acc|acc-o"=fill ·
size:"sm|md|lg"=md · showIcon:boolean=true · iconPosition:"left|right"=right ·
link:string · newTab:boolean · disabled:boolean · style:CSSProperties
```
Mapeia 1:1 para as variantes e tamanhos acima, lendo as mesmas variáveis CSS com fallback para as cores da marca.

---

## 5. Componentes

Todos estão no `facial-premium-design-system.css`. Acessibilidade consolidada na seção 8.

### 5.1 Chip, badge, status
```css
.fp-chip{background:var(--card);border:1px solid var(--line);color:var(--txt);padding:9px 16px;border-radius:var(--radius-pill)}
.fp-badge{color:var(--highlight-ink);border:1px solid var(--highlight-line);font-size:10.5px;padding:4px 10px;border-radius:20px}
.fp-status{padding:9px 15px;border-radius:var(--radius-pill);border:1px solid currentColor}
.fp-status.is-success{color:var(--success);background:var(--success-bg)}
.fp-status.is-warning{color:var(--warning);background:var(--warning-bg)}
.fp-status.is-danger {color:var(--danger);background:var(--danger-bg)}
.fp-status.is-info   {color:var(--info);background:var(--info-bg)}
```
Status compacto de tabela: `.fp-st` com ponto `.fp-st i` (`.fp-ok` / `.fp-warn` / `.fp-off`).

### 5.2 Formulário
```css
.fp-input,.fp-textarea,.fp-select{font:inherit;font-size:15px;color:var(--txt);background:var(--card);
  border:var(--bw-1) solid var(--line);border-radius:var(--radius-md);padding:0 14px;min-height:var(--control-h);width:100%;outline:none}
.fp-input:focus,.fp-textarea:focus,.fp-select:focus{border-color:var(--accent);box-shadow:var(--focus)}
.fp-input.is-error{border-color:var(--danger)}  .fp-input.is-success{border-color:var(--success)}
.fp-input:disabled{opacity:var(--opacity-disabled);cursor:not-allowed}
.fp-input[readonly]{background:var(--card2);color:var(--mut)}
```
- Estrutura: `.fp-form-grid` > `.fp-field` > `.fp-field-lbl` (com `.fp-req` para obrigatório) + controle + `.fp-field-help` (`.fp-err` / `.fp-ok`). Select com `.fp-select-wrap` e seta `.fp-car`.
- **Checkbox e radio** (`.fp-check`): input com `appearance:none`, 20px; `:checked` pinta `var(--accent)` e desenha a marca via `::after`. Rótulo com `min-height:44px`.
- **Toggle** (`.fp-toggle`): trilho 42x24, bolinha de 20px que desliza de `left:2px` para `20px` em `.2s`; `:checked` pinta o trilho de `--accent`.
- Campos do cadastro na página: Nome, E-mail, Telefone, CNPJ. Mensagens de validação no `copy-deck.facial-premium.json` (ex.: "CNPJ inválido. Confira os 14 números."), sempre o que houve e como resolver.

### 5.3 Feedback
```css
.fp-alert{display:flex;gap:11px;padding:13px 16px;border-radius:var(--radius-md);border:var(--bw-1) solid var(--line);background:var(--card)}
.fp-alert.fp-ok{background:var(--success-bg);border-color:var(--success)}   /* idem fp-info, fp-warn, fp-err */
.fp-toast{border-radius:var(--radius-pill);background:var(--card2);box-shadow:var(--elev-overlay)}
.fp-spinner{width:28px;height:28px;border-radius:50%;border:3px solid var(--line);border-top-color:var(--accent);animation:spin .7s linear infinite}
.fp-skel{background:linear-gradient(90deg,var(--card) 25%,var(--card2) 37%,var(--card) 63%);background-size:400% 100%;animation:shimmer 1.4s ease infinite}
.fp-empty{border:1px dashed var(--line);border-radius:var(--radius-lg);text-align:center;padding:30px 20px}
```
Alert: ícone mais `<b>Título.</b> corpo` (ex.: "Pedido enviado. A confirmação chega por e-mail."). Spinner com `role="status" aria-label="Carregando"`. Estado vazio: "Nenhum pedido ainda. Faça o primeiro no marketplace."

### 5.4 Sobreposições
```css
.fp-modal-scrim{position:absolute;inset:0;background:radial-gradient(...rgba(198,183,218,.30)...),rgba(58,34,89,.55);
                backdrop-filter:blur(var(--blur-sm))}                      /* véu com matiz da marca */
.fp-modal{width:min(380px,100%);background:var(--card);border:var(--bw-1) solid var(--line);
          border-radius:var(--radius-lg);box-shadow:var(--elev-modal);padding:22px}   /* .fp-m-row alinha botões à direita */
.fp-tip .fp-bub{background:var(--card2);border:var(--bw-1) solid var(--line);border-radius:var(--radius-sm);box-shadow:var(--elev-overlay)}
.fp-pop{width:240px;background:var(--card);border:var(--bw-1) solid var(--line);border-radius:var(--radius-md);box-shadow:var(--elev-overlay)}
```
Confirmação destrutiva de exemplo: "Cancelar pedido?" com "Cancelar pedido" e "Manter pedido".

### 5.5 Estrutura
```css
.fp-tabs{display:flex;gap:4px;border-bottom:var(--bw-1) solid var(--line)}
.fp-tab{color:var(--mut);border-bottom:2px solid transparent;padding:10px 14px;margin-bottom:-1px}
.fp-tab.active{color:var(--accent);border-bottom-color:var(--accent)}
.fp-acc summary svg{transition:transform .2s var(--ease)}              /* acordeão: seta */
.fp-acc details[open] summary svg{transform:rotate(180deg)}           /* gira 180° ao abrir */
.fp-av{width:40px;height:40px;border-radius:50%;background:var(--card2);border:var(--bw-1) solid var(--line)}
.fp-av .fp-dot{background:var(--success);border:2px solid var(--bg)}   /* presença */
.fp-av-stack .fp-av{margin-left:-12px;border:2px solid var(--bg)}      /* empilhado */
.fp-crumb a:hover{color:var(--accent)}  .fp-crumb .fp-cur{color:var(--txt);font-weight:500}
.fp-pg{min-width:40px;height:40px;border-radius:var(--radius-sm);border:var(--bw-1) solid var(--line)}
.fp-pg.active{border-color:var(--accent);color:var(--accent);font-weight:600}
```
O acordeão `.fp-acc` usa `<details>/<summary>` nativo (abre e fecha sem JS, acessível); corpo em `.fp-acc-body`. **Não confundir** com o botão de acento `.fp-btn.fp-highlight`: o seletor do botão sempre inclui `.fp-btn`. Uso típico na página: perguntas frequentes ("Preciso mudar a marca da clínica?", "Existe compra mínima?").

### 5.6 Cartão
```css
.fp-card{background:var(--card);border:1px solid var(--line);border-radius:var(--radius-lg);padding:var(--space-6)}
.fp-cardv{background:var(--card);border:var(--bw-1) solid var(--line);border-radius:var(--radius-lg);padding:18px;overflow:hidden}
.fp-cardv.fp-inter:hover{transform:translateY(-3px);box-shadow:var(--elev-overlay)}   /* sobe 3px, sem brilho */
.fp-cardv-media .fp-media{height:92px;background:linear-gradient(120deg,var(--highlight),var(--support))}
.fp-card-h .fp-thumb{width:54px;height:54px;border-radius:var(--radius-md)}           /* cartão horizontal */
```

### 5.7 Avançados (área do membro)

**Tabela de dados (`.fp-dtbl`)** dentro de `.fp-dtable-wrap` > `.fp-dtbl-x{overflow-x:auto}`:
- Cabeçalho fixo: `thead th{position:sticky;top:0;background:var(--card2)}`, caixa alta 10.5px.
- Ordenação: botão `.fp-ths` no `th`; estado em `aria-sort="ascending|descending"`; a seta gira.
- Linha: hover `var(--card2)`; selecionada `tr.is-sel{background:var(--row-sel)}`; seleção na coluna `.fp-col-ck`; densidade `.fp-dtbl.fp-compact` (46 → 38px).
- Barra `.fp-dtable-tools` e rodapé `.fp-dtable-foot`. Conteúdo de exemplo: "Pedidos da clínica" (Item, Categoria, Qtd., Estado).

**Paleta de comandos (`.fp-cmdk`)** sobre `.fp-cmdk-scrim`:
- `width:min(520px,100%)`, campo `.fp-cmdk-in`, lista `.fp-cmdk-list{max-height:262px;overflow-y:auto}`, grupos `.fp-cmdk-grp`.
- Item `.fp-cmdk-item`; ativo `.is-active{background:var(--row-sel)}` com ícone em `--accent` e `.fp-kbd`. Rodapé `.fp-cmdk-foot`.

**App shell (`.fp-appshell`)**: `grid-template-columns:var(--side-w) 1fr`, `min-width:660px`.
- Lateral `.fp-appside` (`.fp-ab-brand`, `.fp-navgroup-lbl`, itens, `.fp-side-foot`); barra `.fp-appbar`; conteúdo `.fp-appbody`.
- Item `.fp-navitem`; ativo `.is-active` com faixa de 3px em `--accent` via `::before`. Navegação de exemplo: Início, Pedidos, Marketplace, Notas fiscais, Consultora, Conta.

**Seletor de data (`.fp-dpick` e `.fp-cal`)**: campo `.fp-dpick-field`, calendário `width:296px`, grade `.fp-cal-grid{grid-template-columns:repeat(7,1fr)}`.
- Dia `.fp-cal-day`. Estados: `.is-out` · `.is-today` (anel `--accent`) · `.is-range` (`--row-sel`) · `.is-sel{background:var(--primary);color:#fff}` (branco 8.9:1).

**Utilitários:** `.fp-kbd` (tecla), `.fp-sr-only` (texto só para leitor de tela), `.fp-soon` (bloco "em breve").

---

## 6. Comportamentos (JavaScript do showcase)

O CSS do pacote não depende de JS. Os comportamentos abaixo existem no `index.html`, em JS puro, sem dependências; para a página do GreatPages, só replique o que precisar.

- **Tema:** init anti-flash e toggle `#themeToggle` (ver 2.1). Chave `localStorage['fp-theme']`.
- **Scrollspy:** `IntersectionObserver({rootMargin:"-78px 0px -68% 0px",threshold:0})` em cada `<section>` com id; marca `.active` no link do menu e no grupo. Seção nova = link no menu e `<section id>`.
- **Menu:** clique no grupo alterna `.open` (com `aria-expanded`); um grupo aberto por vez.
- **Menu mobile:** botão alterna `.nav-open` (com `aria-expanded` e `aria-controls`); fecha com Escape, clique fora ou clique em item.
- **Clique para copiar:** `navigator.clipboard.writeText()` com fallback; aviso em notificação que some em cerca de 1,5 s.
- **Tabela:** checkbox da linha aplica `is-sel`; controles de densidade e "selecionar todos".
- **Paleta de comandos:** lista com id `cmdk-list-fp`.
- **Download:** SVG a partir do `<symbol>`; PNG dos gradientes renderizado em `<canvas>`.

---

## 7. Microinterações

- **Tempo e curva:** `--motion-fast .15s · --motion .2s · --motion-slow .4s`; curva única `--ease:cubic-bezier(.2,.8,.2,1)` (desaceleração, sem quique).
- **O que anima:** `transform, box-shadow, border-color, background, color, opacity`. Nunca layout ou texto de leitura.
- **`@keyframes`:** `spin` (spinner, `.7s linear infinite`) e `shimmer` (esqueleto, `1.4s ease infinite`).
- **Catálogo:** botão fill sobe 2px com brilho e encolhe no clique; cartão `.fp-inter` sobe 3px com sombra; acordeão gira a seta 180°; toggle desliza; aba, item de navegação, paginação e dia trocam fundo ou cor; linha da tabela destaca no hover; seta de ordenação gira.
- **Movimento reduzido:** tudo cai para `.01ms` (ver 3.3).

---

## 8. Acessibilidade

- **Contraste WCAG 2.1 AA em 2 níveis**, nos 2 temas:
  - **Nível 1, texto:** normal ≥ 4.5:1; grande ≥ 3:1 (WCAG 1.4.3).
  - **Nível 2, componente:** o botão ou controle contra o fundo da página ≥ 3:1 (WCAG 1.4.11).
- **Valores medidos (contra o `--bg` do tema):**

| Par | Escuro | Claro |
|---|---|---|
| Texto principal | `#F9F8FD` 18.7:1 | `#1F1A26` 16.3:1 |
| Texto secundário | `#C4BDCF` 10.8:1 | `#5E5670` 6.6:1 |
| Texto legal | `#8F80AE` 5.5:1 | `#5E5670` 6.6:1 |
| Link | `#C6B7DA` 10.5:1 | `#59378C` 8.6:1 |
| CTA contra o fundo | `#8561B3` 4.1:1 | `#59378C` 8.6:1 |
| Texto branco no CTA | 4.8:1 | 8.9:1 |
| Acento contra o fundo | `#2EC5CF` 9.4:1 | `#00717F` 5.5:1 |
| Texto sobre o acento (`--highlight-on`) | `#06292D` 7.3:1 | `#FFFFFF` 5.7:1 |
| Névoa como texto | `#B8C7CF` | `#4A5A63` 6.9:1 |

- **Foco visível:** outline 2px `--accent` mais `box-shadow:var(--focus)`; guarda para `forced-colors` (`Highlight`).
- **Cor nunca sozinha:** todo estado vem com ícone ou texto.
- **Alvos de toque:** `--touch-min:44px` em botões, `.fp-check`, `.fp-toggle`; controles densos (paginação 40, dia 38) compensam com espaçamento.
- **Movimento:** respeita `prefers-reduced-motion`.
- **Semântica e ARIA:** `aria-pressed` (toggle de tema), `aria-expanded` e `aria-haspopup` (menu), `aria-controls` (menu mobile), `aria-sort` (tabela), `role="status"` (spinner), `role="dialog"` e `aria-modal` (modal, paleta), `aria-current="page"` (navegação), `aria-hidden` (ícones decorativos, sem nada focável dentro), `aria-label` (controles sem texto).
- **HTML nativo primeiro:** `<details>/<summary>`, `<table>` semântica, `<button>` e `<a href>` corretos.

---

## 9. Responsividade

- Breakpoints de referência: Phone 390 / Tablet 810 / Desktop 1200.
- Tipografia fluida com `clamp()` nas classes `fp-`. Grades como `.fp-form-grid` usam `auto-fit`.
- Celular: botões podem quebrar linha (`white-space:normal` abaixo de 560px); tabela e app shell têm rolagem horizontal própria (`.fp-dtbl-x`).
- Conferir ausência de rolagem horizontal da página de 320px a 1440px.

---

## 10. Aplicação

**A) GreatPages (canal atual)**
1. Código personalizado do `<head>` da página: colar `silka.css` e depois `facial-premium-design-system.css`.
2. Fixar o tema: `<script>document.documentElement.dataset.theme='light';</script>` (ou `'dark'`).
3. Blocos de HTML personalizado: classes `fp-`.
```html
<section class="fp-card">
  <p class="fp-eyebrow">Como fazer parte da rede</p>
  <h2 class="fp-h2">Adesão com uma consultora</h2>
  <a class="fp-btn fp-fill" href="#cadastro">Quero ser membro</a>
</section>
```
`#cadastro` é âncora de exemplo: aponte para o id real do formulário na página, nunca para uma âncora que não existe.
4. Elementos nativos do editor: valores da tabela de cores por tema (`DESIGN-SYSTEM.md`) e da escala tipográfica.

**B) Tokens (qualquer projeto)**: importe `facial-premium-design-tokens.json` e gere CSS vars, JS ou tema de Tailwind. Componente consome token, nunca hex.

**C) Migração futura**: `Button.tsx` como Code Component para Framer ou React.

---

## 11. Publicação e infraestrutura

- **Repositório:** https://github.com/Eddie-FacialAcademy/facial-premium-design-system (público, branch `main`).
- **Showcase:** https://eddie-facialacademy.github.io/facial-premium-design-system/ (GitHub Pages a partir da raiz de `main`; de 1 a 3 minutos após o push). Localmente, o `index.html` abre com duplo clique.
- **Página da rede:** GreatPages, em https://lp.facialacademy.com.br/rede-facial-premium .

---

## 12. Governança e versionamento

- **SemVer:** MAJOR (quebra token ou API), MINOR (adição retrocompatível), PATCH (bug, contraste, ajuste). Toda mudança visível entra no `CHANGELOG.md` na mesma alteração.
- **Arquitetura de tokens:** `primitive → semantic/intent → component`; o semântico **nunca sugere valor** (`--btn-bg`, não `--roxo-500`).
- **Regra dos 3 usos:** só vira padrão oficial o que tem 3 ou mais usos reais.
- **Critério de pronto:** design (todos os estados e variantes), acessibilidade (teclado, foco, semântica, contraste nos 2 níveis), código (consome tokens), doc (quando usar, quando não usar, exemplo).
- **Depreciação:** marcar `deprecated`, manter por pelo menos 1 MINOR com caminho de migração, remover só numa MAJOR.

---

## 13. Relação com o molde

**Molde:** Facial Academy. Mesma arquitetura, JS, componentes, escalas e semânticas; o que é próprio da Facial Premium está abaixo.

Valores lidos do CSS e do showcase desta versão. Esta seção não repete valores de outras marcas: cada DS documenta só os próprios, para não desatualizar.

| Aspecto | Facial Premium |
|---|---|
| Arquivos | `facial-premium-design-system.css` · `facial-premium-design-tokens.json` · `copy-deck.facial-premium.json` |
| Prefixo de classe (CSS de colar no site) | `fp-*` |
| Chave de tema | `localStorage['fp-theme']` |
| id da paleta de comandos | `cmdk-list-fp` |
| Token primário | `--primary` `#59378C` |
| Destaque interativo (links, foco de campo) | `--accent` `#C6B7DA` escuro · `#59378C` claro |
| CTA (degradê) | `#8561B3 → #7956A3` escuro · `#59378C → #3A2259` claro |
| `--info` | `#C6B7DA` escuro · `#4B2F78` claro |
| Foco (`--focus-ring`) | `#C6B7DA` escuro · `#59378C` claro |
| Sombra (matiz) | `rgba(89,55,140,…)` |
| Logo na navegação | `24px` de altura |

> Trocar de marca = trocar a linha de import (`facial-premium-design-system.css`) e o prefixo de classe (`fp-`). O resto do código é igual entre os DS do mesmo molde.

---

## 14. Seções do showcase

Marca e logo · Cores · Gradientes · Tipografia · Ícones · Botões e componentes · Feedback e sobreposições · Estrutura e navegação · Componentes avançados · Acessibilidade e contraste · Fundamentos do sistema · Princípios e processo · Voz e tom · Tokens para copiar (com a tabela de aplicação no GreatPages).

Cada seção tem `id="nav-..."` (alvo do scrollspy) e a maioria dos valores e códigos é clicável para copiar.
