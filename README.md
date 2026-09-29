# Facial Premium · Design System

Design system da **Facial Premium**, a rede de compras de insumos de HOF (harmonização orofacial) do Grupo Facial. A rede conecta a clínica direto à indústria, sem atravessador; o público é o dono de clínica, a adesão é feita com uma consultora e o membro compra no marketplace da rede.

Cor predominante: **Roxo Premium `#59378C`**. Acento exclusivo da marca: **Petróleo `#00717F`**. Tipografia: **Silka** (embutida em woff2, títulos em Medium 500).

Desenvolvido por **Edegar Junior**. Versão **1.1.0** (2026-09-29).

## Entregas

- **index.html**: showcase navegável do design system. Logo, paleta (institucional e derivada), temas claro e escuro, tipografia Silka, gradientes, ícones (Phosphor Thin, copiar SVG), botões e componentes, acessibilidade, voz e tom, tokens para copiar e a tabela de aplicação no GreatPages. Clique para copiar cores, valores e código; download PNG dos gradientes.
  - **Online (para compartilhar):** https://eddie-facialacademy.github.io/facial-premium-design-system/ (GitHub Pages). Localmente, o `index.html` abre com duplo clique e funciona sem internet.

## Pacote portátil (`design-system/`)

| Arquivo | Uso |
|---|---|
| `silka.css` | Fonte Silka (pesos 300 a 700) embutida em woff2/base64. Carregue antes do CSS principal. |
| `facial-premium-design-system.css` | CSS de colar no site: tokens claro e escuro, reset, foco, movimento, tipografia, botões e todos os componentes com prefixo `fp-`. |
| `facial-premium-design-tokens.json` | Tokens legíveis por máquina (geração de variáveis, agentes de IA). |
| `copy-deck.facial-premium.json` | Textos canônicos da rede (landing, microcopy, conteúdo de exemplo). |
| `Button.tsx` | Code Component para Framer ou React, reservado para uma migração futura. Não é usado no GreatPages. |
| `DESIGN-SYSTEM.md` | Especificação, aplicação no GreatPages e prompt para IA. |
| `THEME.md` | Como o tema claro e o escuro funcionam e como fixar um tema por página. |
| `IMPLEMENTACAO.md` | Documentação técnica de cada token, componente e comportamento. |
| `voz-e-tom.md` e `glossario-marca.md` | Guia de copy e vocabulário da rede. |
| `CHANGELOG.md` e `CONTRIBUTING.md` | Histórico de versões e governança. |

## Onde a marca é aplicada

A página da rede vive **só no GreatPages**: https://lp.facialacademy.com.br/rede-facial-premium . Não existe página da Facial Premium em outra ferramenta. Resumo da aplicação (detalhes em `design-system/DESIGN-SYSTEM.md`):

1. Colar `silka.css` e `facial-premium-design-system.css` no código personalizado do `<head>` da página.
2. Fixar um tema por página: `document.documentElement.dataset.theme='light'` (ou `'dark'`).
3. Usar as classes `fp-` nos blocos de HTML personalizado.
4. Nos elementos nativos do editor, aplicar os valores da tabela de cores por tema.

## Notas técnicas

- **Cores:** 9 institucionais. Ameixa `#3A2259`, Roxo Premium `#59378C`, Roxo médio `#74529C`, Lilás `#C6B7DA`, Petróleo `#00717F`, Névoa `#B8C7CF`, Areia `#E3DCD2`, Grafite `#1D1D1B`, Branco `#FFFFFF`. O roxo aparece em marca, CTA e destaques; os neutros carregam a interface.
- **Tipografia:** Silka é a base de todos os design systems do grupo; Poppins é o fallback e depois `system-ui`. Títulos 500, eyebrow 600, numeral 700, corpo 300.
- **Ícones:** Phosphor, peso Thin (traço de 1pt na grade 24), `currentColor`.
- **Tema:** escuro por padrão no showcase; claro com `data-theme="light"`; sem atributo segue `prefers-color-scheme`. O toggle do showcase grava em `fp-theme`. No GreatPages, cada página fixa o próprio tema.
- **Acessibilidade em 2 níveis:** (1) texto ≥ 4.5:1; (2) botão contra o fundo ≥ 3:1 (WCAG 1.4.11). O CTA do tema escuro é `#8561B3` (texto branco 4.8:1; 4.1:1 contra o fundo `#0C0912`).

## Publicação

- **Repositório:** https://github.com/Eddie-FacialAcademy/facial-premium-design-system (público, branch `main`).
- **Showcase:** https://eddie-facialacademy.github.io/facial-premium-design-system/ (GitHub Pages a partir da raiz de `main`; a atualização leva de 1 a 3 minutos após o push).

## Changelog

Ver `design-system/CHANGELOG.md`. Versão atual: **1.1.0**; a primeira versão publicada foi a 1.0.0.
