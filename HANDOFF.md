# Handoff · Facial Premium Design System (versão 1.0.0 · estado em 2026-09-29)

Desenvolvido por **Edegar Junior**. Ponto de retomada; atualizar conforme avançar.

## Concluído

### Showcase local
- `index.html`: showcase self-contained, tema claro e escuro com toggle (chave `fp-theme`), clique para copiar, copiar e baixar SVG de logos e ícones, download PNG dos gradientes, tabela de aplicação no GreatPages.
- **Publicação:** repositório https://github.com/Eddie-FacialAcademy/facial-premium-design-system e showcase https://eddie-facialacademy.github.io/facial-premium-design-system/ (GitHub Pages, branch `main`).

### Pacote portátil (`design-system/`)
- `silka.css` · `facial-premium-design-system.css` · `facial-premium-design-tokens.json` · `copy-deck.facial-premium.json` · `Button.tsx` · documentação `.md`.
- O CSS de colar no site já inclui os componentes do roadmap (formulário, feedback, sobreposições, estrutura, avançados) com prefixo `fp-`.

### Marca
- Derivado do molde Facial Academy, com identidade própria.
- **Logo oficial** dos SVGs em `_FA - Assets\Facial Premium\_SVG`: 4 composições (horizontal, compacto, vertical centralizado, vertical à esquerda) mais o ícone isolado. Ícone com o gradiente oficial `#3A2259 → #59378C → #74529C → #C6B7DA`; texto do logo branco no escuro e grafite `#1D1D1B` no claro.
- **Paleta sóbria (9):** Ameixa `#3A2259`, Roxo Premium `#59378C` (predominante), Roxo médio `#74529C`, Lilás `#C6B7DA`, Petróleo `#00717F` (acento exclusivo), Névoa `#B8C7CF`, Areia `#E3DCD2`, Grafite `#1D1D1B`, Branco `#FFFFFF`.
- **Tipografia:** Silka (títulos 500, eyebrow 600, numeral 700, corpo 300); Poppins de fallback.

### Acessibilidade medida (2 níveis, nos 2 temas)
- **Nível 1, texto:** ≥ 4.5:1.
- **Nível 2, botão contra o fundo:** ≥ 3:1 (WCAG 1.4.11).
- CTA escuro `#8561B3`: texto branco 4.8:1 e 4.1:1 contra o fundo `#0C0912` (o `#59378C` dava 2.2:1 e reprovava). CTA claro `#59378C`: texto branco 8.9:1.
- Acento: escuro `#2EC5CF` com texto `#06292D` (7.3:1); claro `#00717F` com texto branco (5.7:1) e 5.5:1 contra o fundo `#FAFAFA`.

### Copy da rede
- `copy-deck.facial-premium.json` com landing, microcopy e conteúdo de exemplo da área do membro. Regras: "rede" e "membro"; desconto sempre com "até" e com a condição.

## Aplicação no GreatPages

Página: https://lp.facialacademy.com.br/rede-facial-premium
1. Colar `silka.css` e `facial-premium-design-system.css` no código personalizado do `<head>`.
2. Fixar o tema da página com `document.documentElement.dataset.theme='light'` (ou `'dark'`).
3. Classes `fp-` nos blocos de HTML personalizado; valores da tabela de cores por tema nos elementos nativos do editor.

## Próximo
- **Aplicar na página ao vivo** do GreatPages seguindo `design-system/DESIGN-SYSTEM.md`.
- **Depoimentos e números de economia:** pendente. Só publicar com nome, cidade e fala real do membro, e número com fonte.
- `Button.tsx` fica guardado para uma migração futura para Framer ou React.

## Arquivos-chave
- Showcase: `index.html`
- Pacote portátil: `design-system/`
- Docs: `README.md`, `HANDOFF.md`, `design-system/DESIGN-SYSTEM.md`
