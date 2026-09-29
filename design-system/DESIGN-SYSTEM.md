# Facial Premium · Design System

**Versão 1.0.0** · Desenvolvido por **Edegar Junior**.

Design system da **Facial Premium**, a rede de compras de insumos de HOF do Grupo Facial (clínica direto com a indústria, sem atravessador; público: dono de clínica). Escuro por padrão no CSS, claro por troca de tema. Esta pasta é a **fonte da verdade** para aplicar a marca.

Canal: a página da rede vive **só no GreatPages**, em https://lp.facialacademy.com.br/rede-facial-premium .

## Arquivos

| Arquivo | Para quê |
|---|---|
| `silka.css` | **Fonte Silka** (pesos 300 a 700) embutida em woff2/base64. Carregue **antes** do CSS principal. |
| `facial-premium-design-system.css` | **CSS de colar no site.** Tokens (escuro e claro), reset, foco, movimento, tipografia, botões, chips, status e todos os componentes com prefixo `fp-`. |
| `facial-premium-design-tokens.json` | Tokens legíveis por máquina (geração de variáveis, agentes de IA). |
| `Button.tsx` | Code Component para Framer ou React, para uma migração futura. **Não é usado no GreatPages.** |
| `THEME.md` | Como o claro e o escuro são resolvidos e como fixar um tema por página. |
| `DESIGN-SYSTEM.md` | Este documento (spec, aplicação e prompt para IA). |
| `CHANGELOG.md` | Histórico de versões (Keep a Changelog e SemVer). |
| `CONTRIBUTING.md` | Governança: regra dos 3 usos, critério de pronto, SemVer, depreciação. |
| `IMPLEMENTACAO.md` | **Documentação técnica**: arquitetura, tokens, fundamentos, botões, componentes, comportamentos JS, acessibilidade, responsivo e aplicação. |
| `voz-e-tom.md` | Guia de copy da rede (voz, faça e não faça, estrangeirismos, acessibilidade). |
| `glossario-marca.md` | Vocabulário de domínio da rede e palavras proibidas. |
| `copy-deck.facial-premium.json` | Textos canônicos (landing, microcopy, conteúdo de exemplo). |
| `../index.html` | Showcase visual navegável, com clique para copiar. Abrir com duplo clique ou em https://eddie-facialacademy.github.io/facial-premium-design-system/. |

---

## Como aplicar

### 1. GreatPages (canal atual)
1. No código personalizado do `<head>` da página, cole `silka.css` e depois `facial-premium-design-system.css`.
2. Fixe um tema por página:
```html
<script>document.documentElement.dataset.theme='light';</script>  <!-- ou 'dark' -->
```
3. Nos blocos de HTML personalizado, use as classes `fp-`:
```html
<p class="fp-eyebrow">Rede de compras para clínicas de HOF</p>
<h1 class="fp-h1">Compre insumos com <span class="fp-hl">até 40% de desconto.</span></h1>
<p class="fp-legal">Descontos de até 40% variam por produto, indústria e condição comercial vigente.</p>
<a class="fp-btn fp-fill" href="#cadastro">Quero ser membro</a>
<a class="fp-btn fp-outline" href="#como-funciona">Ver como funciona</a>
```
4. Nos elementos nativos do editor, aplique os valores da **tabela de cores por tema** abaixo.

> Os `href` do exemplo precisam apontar para âncoras que existem na página (formulário e seção "Como fazer parte da rede"). Não deixe âncora morta.

Sem a Silka, a pilha cai em **Poppins** e depois `system-ui`, sem quebrar.

### 2. Qualquer outro projeto, via tokens
Importe `facial-premium-design-tokens.json` e gere variáveis no formato que precisar (CSS vars, JS, tema de Tailwind). Regra: **componentes consomem tokens, nunca hex solto.**

### 3. Migração futura
`Button.tsx` fica pronto como Code Component para Framer ou React, com Property Controls e as mesmas variantes do CSS. Hoje não há página fora do GreatPages.

---

## Tabela de cores por tema (elementos nativos do editor)

| Papel | Token | Claro | Escuro |
|---|---|---|---|
| Fundo da página | `--bg` | `#FAFAFA` | `#0C0912` |
| Fundo alternativo de seção | `--bg2` | `#F4F2F7` | `#15101D` |
| Cartão | `--card` | `#FBFAFC` | `#1C1528` |
| Cartão elevado / hover | `--card2` | `#EEEAF3` | `#241B33` |
| Texto principal | `--txt` | `#1F1A26` (16.3:1) | `#F9F8FD` |
| Texto secundário | `--mut` | `#5E5670` (6.6:1) | `#C4BDCF` |
| Texto legal | `--legal-mut` | `#5E5670` | `#8F80AE` |
| Link e destaque | `--lilas` | `#59378C` (8.6:1) | `#C6B7DA` |
| CTA (fundo do botão) | `--cta-solid` | `#59378C` (texto branco 8.9:1) | `#8561B3` (texto branco 4.8:1; 4.1:1 contra o fundo) |
| CTA hover | `--cta-solid-h` | `#8561B3` | `#7956A3` |
| Acento (fundo do botão) | `--acc` | `#00717F` (texto branco 5.7:1; 5.5:1 contra o fundo) | `#2EC5CF` (texto `#06292D` 7.3:1) |
| Acento hover | `--acc-deep` | `#005C67` | `#22A9B3` |
| Texto sobre o acento | `--acc-on` | `#FFFFFF` | `#06292D` |
| Acento como texto | `--acc-ink` | `#00717F` (5.5:1) | `#2EC5CF` (9.4:1) |
| Névoa como texto | `--mist-ink` | `#4A5A63` (6.9:1) | `#B8C7CF` |
| Cor do logo | `--logo` | `#1D1D1B` | `#FFFFFF` |

Contrastes medidos contra o `--bg` do tema, salvo quando indicado.

---

## Fundamentos

### Logo
- Arquivos oficiais: `_FA - Assets\Facial Premium\_SVG`. **4 composições** (horizontal, compacto, vertical centralizado, vertical à esquerda) e o **ícone isolado**.
- O ícone usa o gradiente oficial `#3A2259 → #59378C → #74529C → #C6B7DA`. O texto do logo é **branco no escuro** e **grafite `#1D1D1B` no claro**.
- **Mono branca** sobre roxo, foto ou fundo escuro. **Mono grafite** para aplicação em 1 cor e impressão.
- Não recolorir o gradiente. Não recompor o logotipo digitando em Silka.
- Tamanho mínimo: **ícone 24px**, **horizontal 140px**.

### Cores institucionais (9, não inventar fora disto)
| Nome | Hex | Papel |
|---|---|---|
| Ameixa | `#3A2259` | base do gradiente do logo, fundos profundos |
| Roxo Premium | `#59378C` | **predominante**: marca, CTA, destaques |
| Roxo médio | `#74529C` | meio do gradiente do logo, segunda parada em gradientes de fundo |
| Lilás | `#C6B7DA` | topo do gradiente, links e foco no escuro |
| Petróleo | `#00717F` | **acento exclusivo do Premium** |
| Névoa | `#B8C7CF` | neutro frio de apoio |
| Areia | `#E3DCD2` | neutro quente de apoio |
| Grafite | `#1D1D1B` | texto do logo no claro, impressão |
| Branco | `#FFFFFF` | |

A marca não tem código Pantone; a referência é o hex. **Marca sóbria:** o roxo aparece em marca, CTA e destaques, não em fundos inteiros; os neutros carregam a interface. O gradiente é fundo de seção ou de imagem, nunca decoração de texto pequeno.

### Tema
- **Escuro é o padrão do CSS.** Claro com `data-theme="light"` no `<html>`; sem atributo, segue `prefers-color-scheme`. No GreatPages, fixe um tema por página (ver `THEME.md`).
- No claro, **Petróleo e Névoa como texto** usam as variantes `-ink` (`--acc-ink`, `--mist-ink`). Como preenchimento, o acento usa `--acc` com o texto em `--acc-on`.

### CTA: token por tema (`--cta`)
O CTA consome **`--cta`** em vez de `--roxo2` ou `--roxo-bright` direto, para garantir **contraste de componente** (WCAG 1.4.11). Tokens: `--cta-grad` · `--cta-solid` · `--cta-solid-h` · `--cta-ink`.

| Tema | `--cta-solid` | `--cta-grad` | hover (`--cta-solid-h`) | `--cta-ink` |
|---|---|---|---|---|
| **Escuro** | `#8561B3` | `#8561B3 → #7956A3` | `#7956A3` | `#fff` |
| **Claro** | `#59378C` | `#59378C → #3A2259` | `#8561B3` | `#fff` |

No escuro, o `#59378C` dava 2.2:1 contra o fundo `#0C0912`; por isso o CTA escuro é `#8561B3` (4.1:1 contra o fundo, texto branco 4.8:1).

### Tokens de sistema
- **Raio:** sm 8 · md 14 · lg 18 · pill 30
- **Espaçamento (base 4 e 8):** 4 · 8 · 12 · 16 · 24 · 32 · 48
- **Elevação:** `--elev-1..4` (sombras pretas no escuro; com matiz roxo sutil no claro)
- **Z-index:** base 0 · raised 10 · sticky 40 · overlay 100 · toast 1000
- **Movimento:** fast .15s · base .2s · slow .4s · ease `cubic-bezier(.2,.8,.2,1)`
- **Foco:** `--focus: 0 0 0 2px var(--bg), 0 0 0 4px var(--focus-ring)` (anel `#C6B7DA` no escuro, `#59378C` no claro)
- **Fundações:** opacidade (disabled .45 / muted .66 / hover .08 / overlay .58) · espessura de borda (hair, 1, 2) · blur (sm 6 / md 12 / lg 20) · pontos de quebra (390, 810, 1200) · tamanhos (ícone 16, 20, 24; controle e toque 44px) · proporção (1:1, 4:3, 16:9).
- **Elevação por papel:** `--elev-raised` (=1) · `--elev-overlay` (=3) · `--elev-modal` (=4). Use o papel, não o número.

### Cantos aninhados
Quando um elemento arredondado fica **dentro** de outro, os cantos devem ser **concêntricos**:

```
raio interno = raio externo − padding
```

```css
.card{ --r:24px; --pad:16px; border-radius:var(--r); padding:var(--pad); }
.card > .inner{ border-radius:max(0px, calc(var(--r) - var(--pad))); } /* 24 - 16 = 8 */
```

Pares: cartão grande 24/16 → 8 · médio 16/8 → 8 · pequeno 12/8 → 4 · bloco 8/8 → 0 (reto). Se o padding for maior ou igual ao raio, o interno fica 0. Com borda, externo = interno + espessura. Pill é exceção.

### Tipografia: Silka (escala responsiva)
Silka é a base de todos os design systems do grupo; **Poppins** é o fallback e depois `system-ui`. `tamanho = Desktop / Tablet / Phone (px)`

| Estilo | D / T / P | Peso | Entrelinha |
|---|---|---|---|
| Display / H1 | 60 / 44 / 34 | 500 | 1.03 |
| Heading / H2 | 38 / 32 / 26 | 500 | 1.12 |
| Sub / H3 | 24 / 22 / 20 | 500 | 1.2 |
| Sub / H4 | 20 / 19 / 18 | 500 | 1.25 |
| Sub / H5 | 17 / 16 / 16 | 500 | 1.3 |
| Sub / H6 | 15 / 14 / 14 | 500 | 1.35 |
| Eyebrow | 12 / 12 / 11 | 600 | 1.2 · caixa alta · tracking .18em · cor `--lilas` |
| Lead | 18 / 17 / 16 | 300 | 1.5 · cor `--mut` |
| Body | 16 / 16 / 16 | 300 | 1.65 |
| Body small | 14 / 13 / 13 | 300 | 1.6 |
| Numeral / Preço | 44 / 38 / 32 | 700 | 1 · tabular-nums |
| Legal | 12 / 11 / 11 | 300 | 1.5 · cor `--legal-mut` |

As classes `fp-h1` a `fp-legal` já usam `clamp()` entre Phone e Desktop. Nos elementos nativos do editor, use a coluna Desktop para a tela de computador e a coluna Phone para o celular, onde o editor permitir ajuste por dispositivo. Corpo **≥ 16px no celular** (evita zoom no iOS). **Numerais sempre com `tabular-nums`** (global no `body`). Rótulo de botão: 15px fixo.

### Ícones
Biblioteca **Phosphor**, peso **Thin** (traço de 1pt, `stroke-width:1` na grade 24), cor por `currentColor`. Tamanhos: 16 / 20 / 24 / 32 / 48. Nunca emoji como ícone. O ícone nunca substitui o rótulo.

### Gradientes
Somente cores da paleta. **Sem cônico, blob ou halo**: use malhas (radiais multiponto) e lineares. Classes prontas: `fp-grad-primary`, `fp-grad-acento` (ameixa, roxo e petróleo), `fp-grad-spectral`, `fp-grad-mesh`, `fp-grad-spot`. Uso: fundo de seção ou de imagem.

---

## Componentes

### Botão: `fp-btn`
`class="fp-btn <variante> <tamanho>"`
- **Variantes:** `fp-fill` (gradiente do CTA, primário) · `fp-solid` · `fp-outline` · `fp-ghost` (texto) · `fp-acc` (acento Petróleo) · `fp-acc-o` (acento contorno)
- **Tamanhos:** `fp-sm` · (md = padrão) · `fp-lg`
- **Estados:** hover · `:active` · `:focus-visible` · `:disabled` / `[aria-disabled="true"]`
- **Regras:** altura mínima 44px, raio pill, ícone Phosphor opcional (`<svg class="fp-ico">`). Use `<button>` para ação na página e `<a href>` com destino real para navegação.
- `fp-fill` usa `--cta-grad` e `--cta-ink`; `fp-solid` usa `--cta-solid` (hover `--cta-solid-h`); `fp-acc` usa `--acc`, texto `--acc-on`, borda `--acc-ink` e hover `--acc-deep`.
- Rótulos da rede: "Quero ser membro", "Falar com uma consultora", "Ver como funciona".

### Status: `fp-status is-success | is-warning | is-danger | is-info`
Sempre **ícone e texto**, nunca só cor. Verde, âmbar e vermelho são funcionais e ficam fora da paleta de propósito.

### Demais componentes (todos no CSS, prefixo `fp-`)
- **Base:** `fp-chip` · `fp-badge` (acento) · `fp-card` · `fp-logo` (SVG com `fill="currentColor"`).
- **Formulário:** `fp-form-grid` · `fp-field` · `fp-field-lbl` · `fp-input` · `fp-textarea` · `fp-select` · `fp-check` · `fp-toggle` · `fp-field-help` (`fp-err`, `fp-ok`).
- **Feedback:** `fp-alert` (`fp-ok`, `fp-info`, `fp-warn`, `fp-err`) · `fp-toast` · `fp-spinner` · `fp-skel` · `fp-empty`.
- **Sobreposições:** `fp-modal` e `fp-modal-scrim` · `fp-tip` · `fp-pop`.
- **Estrutura:** `fp-tabs` e `fp-tab` · `fp-acc` (acordeão; não confundir com o botão `fp-btn fp-acc`) · `fp-av` · `fp-crumb` · `fp-pager` e `fp-pg` · `fp-cardv`.
- **Avançados:** `fp-dtbl` · `fp-cmdk` · `fp-appshell` · `fp-dpick` · `fp-cal` · `fp-kbd` · `fp-sr-only`.
- **Estados sem prefixo:** `is-error`, `is-success`, `is-sel`, `is-active`, `is-out`, `is-today`, `is-range`, `active`.

Detalhes de cada um em `IMPLEMENTACAO.md`.

---

## Acessibilidade (obrigatório)
- **Contraste WCAG AA em 2 níveis:**
  - **Nível 1, texto:** ≥ 4.5:1 (texto normal) / ≥ 3:1 (texto grande). No claro, Petróleo e Névoa como texto usam `-ink`.
  - **Nível 2, botão contra o fundo:** ≥ 3:1 (WCAG 1.4.11). CTA escuro `#8561B3` (4.1:1); acento claro `#00717F` (5.5:1); acento escuro `#2EC5CF` (9.4:1).
- **Foco visível:** `outline:2px solid var(--lilas)` e `box-shadow:var(--focus)`; guarda em `@media (forced-colors: active)`.
- **`prefers-reduced-motion`:** transições e animações reduzidas.
- **Toque ≥ 44px.** **Cor nunca sozinha** (estados com ícone e texto).

## Faça e não faça
Faça: consumir tokens · fixar um tema por página no GreatPages · Silka · Phosphor Thin · malhas e lineares da paleta · foco visível · CTA com destino real.
Não faça: hex solto nos componentes · cor fora das 9 institucionais · roxo em fundo inteiro · gradiente em texto pequeno · cônico, blob ou halo · emoji como ícone · Petróleo claro como texto no tema claro (use `-ink`) · recolorir o logo · as palavras proibidas do `glossario-marca.md`.

---

## Processo e versionamento

Veja **`CONTRIBUTING.md`** (princípios, regra dos 3 usos, critério de pronto, SemVer e depreciação) e o **`CHANGELOG.md`**. Arquitetura de tokens: `primitive → semantic/intent → component`, e o token semântico **nunca sugere valor**.

---

## Para agentes de IA

Ao aplicar este design system, **leia `facial-premium-design-tokens.json`** e `copy-deck.facial-premium.json` e siga as regras acima. Prompt sugerido:

> Você vai aplicar o **Facial Premium Design System** (autor: Edegar Junior) na página da rede no GreatPages. Fonte da verdade: `facial-premium-design-tokens.json`, `facial-premium-design-system.css` e `copy-deck.facial-premium.json` desta pasta.
> Regras: (1) só as 9 cores institucionais e seus derivados, com o roxo em marca, CTA e destaques e os neutros na interface; (2) componha com tokens e classes `fp-`, nunca hex solto; (3) fixe um tema por página com `document.documentElement.dataset.theme` e use nos elementos nativos os valores da tabela desse tema; (4) tipografia Silka com a escala por breakpoint, corpo ≥ 16px no celular; (5) ícones Phosphor Thin com `currentColor`; (6) gradientes só malhas e lineares da paleta, como fundo de seção ou de imagem; (7) WCAG AA em 2 níveis, foco visível, `prefers-reduced-motion`, toque ≥ 44px, cor nunca sozinha; (8) copy: "rede" e "membro", nunca a palavra proibida do glossário; desconto sempre "até 40%" com a condição; número só com fonte; sem "e comercial", sem travessão, sem hipérbole; todo CTA com destino real.
> Antes de finalizar, confira contraste no tema escolhido e ausência de rolagem horizontal de 320px a 1440px.
