# Changelog · Facial Premium Design System

Todas as mudanças relevantes deste design system são registradas aqui.
O formato segue [Keep a Changelog](https://keepachangelog.com/pt-BR/1.1.0/) e o
versionamento segue [SemVer](https://semver.org/lang/pt-BR/):

- **MAJOR**: muda ou remove um token ou API pública (quebra compatibilidade).
- **MINOR**: adiciona de forma retrocompatível (novo componente, token ou variante).
- **PATCH**: correções que não mudam a API (bug, contraste, ajuste fino).

---

## [Não lançado]

_Nada pendente no momento._

## [1.0.0] · 2026-09-29

Primeira versão do design system da Facial Premium.

### Adicionado
- **Origem:** derivado do molde Facial Academy (mesma arquitetura de tokens, CSS e showcase), com identidade própria da rede.
- **Logo oficial** a partir dos SVGs de `_FA - Assets\Facial Premium\_SVG`: 4 composições (horizontal, compacto, vertical centralizado, vertical à esquerda) e o ícone isolado, com o gradiente oficial `#3A2259 → #59378C → #74529C → #C6B7DA`.
- **Paleta sóbria de empresa B2B** com 9 cores institucionais e o **Petróleo `#00717F`** como acento exclusivo do Premium. Névoa e Areia como neutros de apoio. O roxo fica em marca, CTA e destaques.
- **Tema claro e escuro** medidos em WCAG AA nos 2 níveis: texto ≥ 4.5:1 e botão contra o fundo ≥ 3:1 (WCAG 1.4.11). CTA escuro `#8561B3`, CTA claro `#59378C`, acento claro `#00717F` com texto branco (`--acc-on`).
- **Componentes do roadmap** (formulário, feedback, sobreposições, estrutura, avançados) incluídos no CSS de colar no site, com prefixo `fp-` e estados sem prefixo (`is-*`, `active`).
- **Copy da rede** em `copy-deck.facial-premium.json`: landing, microcopy e conteúdo de exemplo da área do membro.
- **Aplicação no GreatPages** documentada: CSS no código personalizado do `<head>`, tema fixo por página, classes `fp-` em blocos de HTML personalizado e tabela de cores por tema para os elementos nativos do editor.

[Não lançado]: #não-lançado
[1.0.0]: #100--2026-09-29
