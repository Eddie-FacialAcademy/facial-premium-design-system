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

## [1.1.0] · 2026-09-29
### Alterado
- **Nomes de cor organizados em duas camadas.** Cores da marca (`--brand-*`) levam o nome real da cor nesta marca; tokens de uso têm nomes neutros e iguais em todos os DS do grupo (`--primary`, `--accent`, `--highlight`, `--support`, `--glow`), para o código continuar portável entre marcas. Valores não mudaram: comparação de cor computada em todos os elementos do showcase, antes e depois, nos dois temas, deu zero diferença.
- Tokens de uso: `--roxo-bright` → `--primary-bright`, `--lilas-soft` → `--accent-soft`, `--gold-deep` → `--highlight-deep`, `--gold-line` → `--highlight-line`, `--rose-line` → `--support-line`, `--mist-line` → `--support-line`, `--gold-ink` → `--highlight-ink`, `--rose-ink` → `--support-ink`, `--acc-deep` → `--highlight-deep`, `--acc-line` → `--highlight-line`, `--mist-ink` → `--support-ink`, `--acc-ink` → `--highlight-ink`, `--acc-on` → `--highlight-on`, `--roxo2` → `--primary`, `--lilas` → `--accent`, `--peach` → `--glow`, `--roxo` → `--primary-deep`, `--gold` → `--highlight`, `--rose` → `--support`, `--mist` → `--support`, `--sand` → `--glow`, `--acc` → `--highlight`.
- JSON de tokens: chaves renomeadas igual aos tokens (camelCase) e mapa de/para em `$deprecated`.
- Botão de acento `fp-btn fp-acc` virou `fp-btn fp-highlight` (e `fp-acc-o` virou `fp-highlight-o`). O nome antigo colidia com o acordeão `.fp-acc`, cujas regras atingiam o botão; por isso não há apelido para ele.
- Nomes exibidos no showcase ligados à cor real: acentos compartilhados do grupo como **Dourado claro**, **Rosa claro** e **Pêssego** (antes "Amarelo claro", "Vermelho claro" e "Amarelado", com a mesma cor chamada de formas diferentes entre DS); rótulos de gradiente gerados a partir das cores de cada gradiente.
- Documentação técnica: seção 13 virou "Relação com o molde", só com valores deste DS (a tabela anterior repetia valores de outra marca e desatualizava).
### Descontinuado
- Os nomes antigos listados acima continuam funcionando como apelidos no CSS de colar no site e saem na 2.0. Use os nomes novos em código novo.

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
