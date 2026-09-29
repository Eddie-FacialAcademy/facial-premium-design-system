# Contribuindo · Facial Premium Design System

Este guia descreve **como o sistema evolui** sem virar uma colcha de retalhos.
Vale para o CSS e os tokens aplicados na página da rede no GreatPages e para o
`Button.tsx` guardado para uma migração futura.

## Princípios inegociáveis

1. **Token primeiro.** Nunca use hex, raio ou sombra solto: consuma os tokens. O
   token semântico **nunca sugere valor** (`--btn-bg`, não `--roxo-500`); o de
   componente referencia o semântico, nunca o primitivo direto.
2. **Paridade claro e escuro, WCAG AA em dois níveis.** O contraste vale nos
   **dois** temas em **dois níveis**: **(1) texto** ≥ 4.5:1 (texto grande ≥ 3:1);
   **(2) componente, botão e estados** (inclusive foco) contra o fundo ≥ 3:1
   (WCAG 1.4.11, Non-text Contrast). Cor nunca comunica sozinha: sempre com ícone
   ou texto.
3. **Marca sóbria.** O roxo fica em marca, CTA e destaques; os neutros carregam a
   interface. O Petróleo é acento, não fundo. O gradiente é fundo de seção ou de
   imagem, nunca decoração de texto pequeno.
4. **Acessibilidade desde o início.** Foco visível em tudo que é focável,
   navegação por teclado e semântica HTML correta entram na criação, não numa
   auditoria depois.

## Quando algo vira padrão: regra dos 3 usos

Só promovemos a **componente ou token oficial** o que tem **3 ou mais usos reais**
distintos. Antes disso, é um padrão local. Isso evita inchar o sistema com peças
de uso único.

## Critério de pronto

Um componente só fecha quando tem **os quatro**:

- **Design:** todos os estados, variantes e tamanhos.
- **Acessibilidade:** teclado, foco e semântica, mais contraste nos **dois níveis**
  nos dois temas. O CTA preenchido e o botão de acento não fecham sem passar o
  nível 2.
- **Código:** implementação no `facial-premium-design-system.css`, com prefixo
  `fp-`, consumindo tokens.
- **Doc:** quando usar, quando não usar e exemplo, com copy da rede (ver
  `voz-e-tom.md`).

## Versionamento (SemVer) e CHANGELOG

Siga o [SemVer](https://semver.org/lang/pt-BR/): **MAJOR** quebra, **MINOR**
adiciona de forma retrocompatível, **PATCH** corrige. **Toda** mudança visível
entra no `CHANGELOG.md` na mesma alteração.

## Depreciação

Nada some de repente. Marque como `deprecated`, mantenha por **pelo menos um
MINOR** com aviso e caminho de migração, e só remova numa **MAJOR**.

## Fluxo

1. **Proponha** o problema ou uso (não a solução pronta).
2. **Revise** com quem mantém o sistema (cabe ao sistema ou é caso local?).
3. **Implemente** consumindo tokens e cumpra o critério de pronto.
4. **Documente** e atualize o `CHANGELOG.md`.
5. **Teste nos dois temas** e aplique na página do GreatPages com o tema que ela fixa.

## Linguagem

Documentação e textos de interface inclusivos: evite "só", "simplesmente",
"fácil", "óbvio". O que é óbvio para quem criou raramente é para quem chega depois.
