# Voz e tom (guia de copy do design system)

> Guia da **Facial Premium**. As regras de forma (pontuação, estrangeirismos, acessibilidade) são as mesmas dos design systems do grupo. O vocabulário da rede fica em **`glossario-marca.md`** e **nunca cruza** para outra marca.

## Para que serve
Padroniza a copy da página da rede e da interface: hero, notas de seção, botões, alertas, estados vazios, validação, dicas e o conteúdo de exemplo dos componentes. Fala de **empresa para empresa**: o leitor é o dono de clínica decidindo como comprar insumos.

## Princípio geral
Sóbria, direta, precisa, transparente, de negócio. Sem autoelogio, sem hipérbole, sem "happy talk". A copy diz o que a rede faz, em que condição, e qual é o próximo passo.

## Adjetivos da voz
Sóbria · direta · precisa · transparente · de negócio.

## Faça
- O rótulo do botão diz a **ação** ("Quero ser membro", "Falar com uma consultora", "Ver como funciona"), nunca o genérico ("Enviar", "OK", "Saiba mais").
- No erro, diga **o que houve e o próximo passo** ("Não foi possível enviar. Verifique a conexão e tente de novo.").
- **Número só com fonte ou condição na mesma frase.** "Até 40% de desconto" sempre acompanhado de "varia por produto, indústria e condição comercial vigente".
- Diga o que o membro **não** precisa fazer quando isso tira uma objeção real ("Você não precisa alterar a sua marca.").
- Voz ativa, frases curtas.
- A cor nunca comunica sozinha: acompanhe sempre de ícone e texto.
- pt-BR em tudo. Código em inglês (padrão da indústria).

## Não faça
- **Sem as palavras proibidas** listadas no `glossario-marca.md`, nem em comparação. Use "rede" e "membro".
- **Sem o caractere de "e comercial".** Escreva a palavra "e".
- **Sem travessão** (nem o longo nem o médio) no meio do texto. Use vírgula, dois-pontos, parênteses ou ponto.
- Sem **hipérbole** ("a melhor", "incrível", "revolucionário") e sem os verbos vazios "desbloqueie", "eleve", "transforme", "potencialize".
- Sem **"happy talk"** ("Bem-vindo!", "Que bom te ver!") e sem frase de aquecimento.
- Sem "economize 40%": o desconto é "até" e depende da condição.
- **Não misture domínio** entre marcas (ver "Separação de domínio").

## Estrangeirismos (o que o design system já traduziu)
Regra: **traduza** quando existe equivalente limpo em pt-BR; **mantenha** o que é nome próprio, sigla ou termo de código.

**Traduzir** (decisões já aplicadas):
tabela de dados (data table) · paleta de comandos (command palette) · seletor de data (date picker) · barra de navegação (navbar) · barra lateral (sidebar) · janela modal (modal) · dica (tooltip) · balão (popover) · notificação (toast) · indicador de carregamento (spinner) · esqueleto (skeleton) · caminho de navegação (breadcrumb) · abas (tabs) · acordeão (accordion) · cartão (card) · estado vazio (empty state) · fundo (background) · padrão (default) · estado (status) · ponto de quebra (breakpoint) · malha (mesh) · alerta (alert).

**Manter** (sem tradução): token · hover e link (como estado ou elemento) · avatar · pill (formato de raio) · GreatPages · marketplace · CNPJ · nomes de código (CSS, JSON, SVG, PNG, Code Component) · siglas (WCAG, SemVer) · fontes (Silka, Poppins) · biblioteca de ícones (Phosphor) e seu peso (Thin) · funções de código (`currentColor`, `clamp()`).

## Separação de domínio (rígida)
A Facial Premium só fala do **próprio domínio**: compra de insumos de HOF pela clínica. O vocabulário está em **`glossario-marca.md`** e não aparece em outro design system. Nada de conteúdo educacional, de técnica clínica ou de outras áreas do grupo. Na dúvida, **erre para o neutro**.

- **Neutros (valem em qualquer marca):** corpo de texto, preenchimento de cor, token, cartão, fundo, escala, grade.

## Nomes de marca
Mantidos como são e **por extenso**: "Facial Premium", "Grupo Facial". Não abreviar nem inventar variações.

## Acessibilidade na copy
- Erros dizem **o que houve e como resolver**.
- Rótulos de botão **específicos** (a ação, não o genérico).
- A cor nunca é o único sinal: texto e ícone sempre acompanham.
- Mensagem curta ajuda a caber no alvo de toque e a manter o foco legível.

## Números
Algarismos com função **tabular** em tabelas e listas, para os dígitos alinharem. No design system isso já é global (`font-variant-numeric: tabular-nums`). Percentual, preço e prazo só com a fonte ou a condição junto.

## Depoimentos e prova
Depoimento só com nome, cidade e fala real do membro. Número de economia só com fonte. Enquanto não houver material aprovado: **pendente** (não preencher com texto de exemplo na página ao vivo).

## Microcopy modelo (fonte: `copy-deck.facial-premium.json`)
- **Botão principal:** "Quero ser membro".
- **Botão de contato:** "Falar com uma consultora".
- **Botão secundário:** "Ver como funciona".
- **Estado vazio:** "Nenhum pedido ainda. Faça o primeiro no marketplace."
- **Sucesso:** "Pedido enviado. A confirmação chega por e-mail."
- **Erro:** "Não foi possível enviar. Verifique a conexão e tente de novo."
- **Confirmação destrutiva:** "Cancelar pedido?" com as ações "Cancelar pedido" e "Manter pedido".
- **Condição do desconto:** "Descontos de até 40% variam por produto, indústria e condição comercial vigente."

---
*Domínio e termos da marca: ver `glossario-marca.md`.*
