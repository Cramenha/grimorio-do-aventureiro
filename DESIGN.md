# DESIGN.md — Grimório do Aventureiro

Direção trocada a pedido do usuário em 05/11/2026: continua o **Material Design 3** (m3.material.io) como sistema (papéis de cor, escala tonal de superfícies, escala tipográfica, state layers), mas a referência visual deixa de ser foundryvtt.com e passa a ser o site oficial **baldursgate3.game**. Cores, fontes, bordas e cantos abaixo foram medidos nos estilos computados do site, no navegador, nesta data. O print de conferência está em `assets/bg3-website.png`. A versão anterior (Foundry) está no histórico do git.

> **Estado:** aplicado no `style.css` em 05/11/2026 (tokens dos dois temas, fontes via `@fontsource/alegreya` e `@fontsource/gothic-a1`, cantos retos, moldura, botões). Contraste dos pares de texto conferido nos dois temas; o mais justo é `primary` claro sobre `surface-container-highest` claro, com 4,84:1.

## Identidade

App de ficha de D&D 4e com a estrutura de um produto M3 (tokens, superfícies por tom, componentes com estado) e a atmosfera do site do BG3: noite, metal velho e pergaminho iluminado à vela. O site do BG3 é preto, com texto branco, e todo o calor vem de um único metal (bronze e dourado) em fios finos, títulos e botões. O mood vem daí. Os pixels não vêm (ver "O que NÃO fazer").

## Personalidade

Sóbrio, solene e preciso. O ouro marca o que se pode tocar e o que é título, e nunca preenche áreas grandes. As molduras são finas e retas, de joalheria, não grossas.

## Paleta M3 (sementes medidas em baldursgate3.game)

M3 gera a escala tonal (0–100) a partir das sementes. Aqui ficam as sementes, os valores medidos e os papéis. "Medido" quer dizer que o valor aparece nos estilos computados do site; "derivado" quer dizer que é um tom da escala M3 calculado a partir de uma semente.

- **Seed `primary`** = bronze dourado **`#C19976`** (medido: `rgb(193,153,118)`, a cor mais usada do site depois do branco; links, texto dos botões, títulos de seção). Papéis: `primary` (ação, link, foco, título de quadro), `on-primary` = **`#1D1003`** (medido: o marrom quase preto usado sobre o dourado), `primary-container` (fundo de destaque suave, tom escuro derivado), `on-primary-container`.
- **Destaque claro** = **`#FBCEA0`** (medido, `rgb(251,206,160)`): hover e realce do `primary`, ícone ativo. É um tom da mesma semente, não uma quarta cor.
- **Seed `secondary`** = bronze das molduras **`#B1906A`** (medido: borda dos quadros). Vira `outline`. Os bronzes mais escuros **`#896D51`** e **`#785F42`** (medidos) viram `outline-variant` e divisores.
- **Seed `neutral`** = preto **`#000000`** (medido: fundo do `body`). M3 precisa de degraus de superfície, então `surface-container-lowest → highest` são tons derivados com leve matiz marrom (do quase preto ao marrom-carvão), nunca cinza azulado. No site esses degraus vêm de pinturas escuras atrás do conteúdo. Aqui vêm do tom, sem imagem.
- **`on-surface`** = **`#FFFFFF`** (medido). **`on-surface-variant`** = branco a ~70% sobre o fundo (medido: o site usa `rgba(255,255,255,.6–.8)` no corpo de texto). Em token, fica um cinza quente sólido equivalente, não transparência, para o contraste ser previsível.
- **Seed `tertiary`** = vermelho-sangue `#8E1B1B`, só para o selo de poder "encontro" (regra de D&D 4e, ver Motivos). O site do BG3 não tem esse vermelho. É informação de jogo, não marca.
- **`error`** = vermelho M3 padrão (`#B3261E` claro / `#F2B8B5` escuro), separado do `tertiary`.
- Cap do antislop (R-29): núcleo = primary (bronze dourado) + secondary (bronze das molduras, só borda) + tertiary (selo de poder) + error. Os neutros não contam.
- **Contraste conferido:** `#C19976` sobre `#000` dá cerca de 8:1 (AA e AAA). `#785F42` não passa como texto: só borda e divisor.

## Temas claro e escuro

- **Escuro** (padrão do sistema e do site do BG3): é o descrito acima.
- **Claro**: o site não tem. Fica derivado das mesmas sementes nos tons claros do M3: superfícies de pergaminho claro, texto em tinta marrom-escura e `primary` num bronze escuro que passe AA sobre o pergaminho (conferir na aplicação dos tokens). Serve para impressão e para quem prefere.
- Botão ☀/☾ e `tema.js` continuam como estão. Tokens em `:root` (escuro) e `:root[data-tema="claro"]`. Cor nova entra nos dois blocos, nada de cor fixa fora deles.
- Selos de poder no claro: verde e vermelho viram containers claros, e o "diário" continua escuro, porque preto é a cor da regra.
- Scrim de modal: preto translúcido nos dois temas.
- O manual (`manual/manual.html`) usa os mesmos tokens. O PDF do pacote sai no claro.

## Tipografia (escala M3: Display/Headline/Title/Body/Label, cada um L/M/S)

O site usa **Quadraat Offc Pro** (serifada humanista; Demibold em caixa-alta nos títulos, Regular no corpo), que é licenciada e não pode ser embarcada. Na interface miúda usa **Gothic A1**, que é aberta. O app precisa funcionar offline, então as fontes vêm do `@fontsource` (pacote em `VENDOR` no `server.js`), nunca de CDN.

- **Display, Headline e Title**: **Alegreya**, 700, caixa-alta nos títulos de quadro e de seção. É a serifada humanista aberta mais próxima da Quadraat: mesmo traço caligráfico, boa em tamanho grande e pequeno. Substitui a Cinzel. Pacote: `@fontsource/alegreya`.
- **Body**: **Alegreya** 400. O site do BG3 lê o corpo em serifada, e a Alegreya foi desenhada para texto longo, que é o caso do compêndio. Substitui a Signika.
- **Label** (rótulos em caixa-alta, chips, cabeçalhos de tabela, células numéricas pequenas): **Gothic A1** 600, a mesma fonte do site. Pacote: `@fontsource/gothic-a1`.
- Tamanhos pela escala M3 (Display L 57/M 45/S 36, Headline L 32/M 28/S 24, Title L 22/M 16/S 14, Body L 16/M 14/S 12, Label L 14/M 12/S 11), em `rem`.
- **Tracking:** o site usa `letter-spacing: normal` nos títulos. Caixa-alta em Alegreya pede um pouco de ar, então fica +0.04em em Title e Headline e +0.08em em Label. Não usar os 0.14em espaçados da Cinzel.
- **Números** de placar (defesas, PV, atributos): Alegreya 700 com algarismos alinhados (`font-variant-numeric: lining-nums tabular-nums`), para colunas de valores ficarem retas.

## Forma (shape scale M3 ajustada ao BG3)

O site do BG3 tem `border-radius: 0` em tudo: quadros, botões e cartões. A shape scale do M3 continua como token, mas com valores retos:

`none 0` (quadros, folhas, cartões, modais, botões) · `extra-small 2px` (campo de texto, chip, célula numérica: só para não serrilhar) · `full` (o oval do valor de atributo e os selos de status de poder, as duas exceções registradas).

Não usar 8/12/16/28px. Botão comum não é pílula.

## Molduras e elevação

- **Superfície**: hierarquia pelo tom (`surface-container-lowest → highest`), como manda o M3.
- **Moldura de quadro** (o motivo de identidade do BG3): fio de 1px em `outline-variant` (bronze escuro) com **cantos marcados** por um L de 2px × 14px em `outline` (bronze claro), feito com gradientes CSS sobre a própria borda (sem SVG nem imagem). Só nos contêineres de primeiro nível (quadro da ficha, modal, cartão da tela inicial), nunca em botão, campo, chip ou cartão aninhado. A versão Foundry tinha tirado a moldura de cantos do tema "pergaminho". Ela volta aqui de forma mais leve: fio de 1px e canto pequeno, sem SVG pesado nem textura.
- **Botão** (medido no site): retangular, fundo escuro translúcido (`rgba(0,0,0,.35)` → token `surface-container-low`), borda 1px `outline`, texto `primary` em caixa-alta. O botão principal de cada tela (um por tela) é o preenchido em `primary` com texto `on-primary`.
- **Sombra** (M3 elevation) só em flutuantes de verdade: modal, janela de anotação arrastável, menu.
- **Sem imagem de fundo pintada** no app: o site usa arte do jogo, que não é nossa (ver "O que NÃO fazer"). A profundidade vem dos degraus de superfície e de um vinheta escura opcional no `body`.

## Motivos de identidade (o que muda, o que fica)

- **Fica**: o selo de poder por tipo (verde/vermelho/preto para à vontade/encontro/diário), porque é regra do jogo. Fica também o d20 como ícone de marca, agora em bronze em vez de âmbar em brasa.
- **Muda**: o acento sai do âmbar/laranja da Foundry e vai para o bronze dourado do BG3. Os cantos saem de 12/16px e ficam retos. As fontes passam de Cinzel + Signika para Alegreya + Gothic A1.
- **Entra**: a moldura de 1px com cantos marcados, nos contêineres de primeiro nível.
- **Continua do M3**: state layer em todo elemento interativo, com overlay de 8% (hover), 10% (focus/pressed) e 16% (dragged) da cor do conteúdo, e foco visível de 2px em `primary`.

## Aba Ficha: arranjo do Character Builder (decisão de 05/11/2026)

- **Arranjo**: a aba Ficha segue a página 1 da ficha em PDF do Character Builder. Coluna 1: Iniciativa, Atributos, Pontos de vida, Perícias. Coluna 2: Defesas, Pontos de ação, Características raciais, Características de classe, Idiomas. Coluna 3: Deslocamento, Sentidos, Ataques, Talentos. Embaixo ficam os textos da página 2 (traços, maneirismos e aparência, companheiros). Quem vem do PDF acha cada campo onde já procura. Não reordenar sem esse motivo.
- **Colunas do CB**: defesas, iniciativa, deslocamento, perícias e ataques mostram a decomposição do CB (10 + ½ nível, atributo, classe, talento, aprimoramento, outros), com zero em branco como no PDF. Os bônus situacionais do CB (Special Movement, Conditional Bonuses) aparecem como texto no quadro correspondente.
- **Vocabulário da ficha do D&D Beyond**, redesenhado nos tokens daqui: quadro com título em caixa-alta centralizado numa faixa `surface-container-highest` (o equivalente da faixa preta do CB), caixa de atributo com o modificador grande e o valor num oval (`full`) e caixas de valor com o rótulo em cima. Com a direção BG3, a faixa de título ganha um fio inferior em `outline` e o título em `primary`. Os quadros seguem a regra de moldura acima.

## Mood / dials (antislop)

- **ENERGY 2** (Balanced): fundo quase preto e calmo, com o ouro pontuando título e ação. O site do BG3 é ENERGY 3 por causa da arte, e o app fica um degrau abaixo porque é ferramenta de leitura longa.
- **RHYTHM 2**: toda tela usa o mesmo sistema de superfícies e molduras. A variação vem do conteúdo (ficha vs. grimório vs. bloco de criatura).
- **MOTION 2**: state layer e transições curtas de hover/foco. Sem parallax, sem scroll-reveal e sem as partículas e brilhos animados do site. Respeitar `prefers-reduced-motion`.

## O que NÃO fazer aqui (colisão com antislop, decisão registrada)

- **Não copiar o site do BG3 (R-30)**: nada de logo, arte de personagem, imagem de fundo pintada, ornamentos SVG do site nem fonte Quadraat. O que vem de lá são as sementes de cor medidas, o mood (preto + metal + serifada) e a geometria (cantos retos, fio de 1px). O app é ferramenta de D&D 4e, não fã-site do BG3.
- **Ouro em tudo (R-13 / excesso de acento)**: dourado só em título de quadro, ação, link e foco. Texto corrido fica em `on-surface`. Fundo de área grande nunca é dourado.
- **Glow**: o site tem brilhos de luz nas imagens. Aqui, no máximo um realce `#FBCEA0` pontual (hover do botão principal), nunca em card, borda e ícone ao mesmo tempo.
- **Ornamento em tudo**: canto marcado só no contêiner de primeiro nível (ver Molduras). Moldura dentro de moldura não.
- **Pílula**: só o oval de atributo e os selos de status. Botões e chips são retos.
- **Transparência como cor de texto**: o site usa branco a 60–80%. Nos tokens vira cor sólida equivalente, para o contraste ser verificável nos dois temas.
