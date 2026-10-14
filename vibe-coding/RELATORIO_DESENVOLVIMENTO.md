# Relatório de desenvolvimento — Madrugada Hacker

## Como começou

A atividade pedia para desenvolver com o Claude seguindo o ciclo de descrever, gerar, olhar no navegador e ajustar. Então foi o que eu fiz.

No primeiro pedido, falei pouco: uma landing page de hackathon universitário na Avenida Paulista, com contagem regressiva, programação, palestrantes e formulário de inscrição. Usando HTML, Tailwind e a paleta que eu já tinha escolhido (fundo bem escuro, branco, roxo, rosa, azul, ciano e amarelo).

## A primeira versão (e por que eu mudei quase tudo)

A primeira versão funcionava. Tinha contagem, programação em abas, cards e formulário validando certinho. Mas quando abri no navegador, a sensação foi de "já vi isso mil vezes". Hero centralizado, tudo arredondado, um brilho roxo no fundo, `// SOBRE O EVENTO` em cima de cada título e aquelas fontes que todo site gerado por IA usa.

Não estava ruim. Só não tinha personalidade nenhuma.

Aí tive a ideia que mudou o projeto: em vez de um hackathon genérico de dois dias, seria uma **Madrugada Hacker**, das 19h às 7h. Montei a programação com nomes como _Midnight Debugging_, _Insomnia Mode_, _Coffee & Commit_ e _Sunrise Demo Day_ e pedi para refazer a página inteira em cima disso.

## O que mudou com o tema novo

- **Fontes:** troquei tudo. Ficou a Big Shoulders Display nos títulos (condensada, com cara de pôster de festa), a VT323 nos horários e na contagem (pixel, cara de terminal antigo) e a Atkinson Hyperlegible no texto corrido, porque com um título tão apertado o resto precisava ser fácil de ler.
- **Sem eyebrows:** tirei os `// alguma coisa` de cima dos títulos. Os próprios títulos passaram a carregar a seção ("Quem vai virar a noite com você", "Saiu às 7h? O metrô já abriu.").
- **Cores com significado:** a programação virou três blocos, _Noite_, _Madrugada_ e _Amanhecer_, que vão do azul para o roxo e o rosa e terminam no amarelo. O fim da página tem um sol nascendo. Gostei porque a paleta deixou de ser enfeite e passou a contar o horário.
- **Cantos retos e sombra dura** no lugar de tudo arredondado e com brilho.
- **Sem abas:** como agora é uma noite só, as abas da programação perderam o sentido.

## Sugestões da IA que eu não aceitei

- **React + Vite logo no começo.** A atividade é de HTML e Tailwind.
- **DaisyUI.** Considerei, mas os temas dele são todos arredondadinhos, exatamente o visual que eu queria evitar.
- **Vermelho para os erros do formulário.** Não está na paleta. Usei rosa, sempre com uma mensagem escrita junto.
- **Fotos aleatórias para os palestrantes.** As pessoas são inventadas, e colocar rosto de gente real em nome inventado é estranho. Ficaram as iniciais.
- **Um endereço com número na Paulista.** O evento é fictício e eu não queria associá-lo a um prédio de verdade. Deixei só as estações de metrô.
- **Biblioteca de animação ao rolar.** Achei dependência demais por pouco efeito. A única animação contínua é a faixa com os nomes das atividades, e ela para para quem prefere menos movimento.

## Sugestões que aceitei

- Fixar a versão do Tailwind no CDN, para nada quebrar do nada.
- Organizar os componentes como "classe base + variação" (`.btn` + `.btn-primary`).
- Mandar o foco para o primeiro campo com erro quando o formulário não passa.
- Os crachás levemente tortos, alternando o ângulo. A ideia foi da IA quando pedi que os cards de palestrante "parecessem crachá de evento", e ficou bem melhor do que eu imaginava.

## Decisões que fomos ajustando juntos

- **Relógio de rolagem:** eu queria que desse para "sentir" a noite passando. A IA sugeriu um relógio fixo no canto que vai de 19:00 a 07:00 conforme a rolagem. Aceitei, mas pedi para escondê-lo no celular, porque ali atrapalhava.
- **Insomnia Mode como ponto alto:** decidimos destacar só essa atividade, com uma barra rosa e a tag "★ ponto alto". Se tudo fosse destaque, nada seria.
- **Checkbox de 18+:** como o evento atravessa a madrugada, fazia sentido. Entrou no formulário e no FAQ.
- **Premiação como ingresso:** o card amarelo com recortes nas laterais foi uma mistura de ideia minha (ficar diferente do resto) com a execução da IA.

## Ajustes que só apareceram olhando no navegador

- No celular, a lua ficava em cima do selo de data. Mudei a lua de lugar.
- Os acentos em letra maiúscula (À, Ê, Ô) encostavam na linha de cima por causa do espaçamento muito apertado. Aumentei um pouco.
- Os crachás e o ingresso, por estarem girados, encostavam na borda da tela no celular. Coloquei uma trava para não gerar rolagem lateral.
- Antes, ainda na primeira versão, o logo tinha um espaço estranho no meio e as opções do formulário ficavam espremidas no celular.

## Componentes que planejei

- **Botão:** primário (branco com sombra roxa que vira rosa no hover e "afunda" no clique) e contorno.
- **Tag:** neutra, amarela preenchida (marcos), roxa, rosa, azul e ciano, cada uma ligada a um tipo de atividade.
- **Bloco de fase:** Noite, Madrugada e Amanhecer, cada uma com sua cor e seu ícone (lua, estrelas, sol).
- **Atividade:** normal e "ponto alto".
- **Crachá:** palestrante (faixa roxa), mentora (azul), banca (amarela) e host do CTF (borda e sombra rosa).
- **Contagem:** contando, "acontecendo agora" e "edição encerrada".
- **Campo do formulário:** normal, em foco (ciano) e com erro (rosa + mensagem).
- **Opção de escolha:** normal e marcada.
- **Ingresso de premiação**, **faixa animada** e **céu com lua e estrelas**, que aparecem uma vez só, mas têm regra própria.

---

# Registro de prompts

## 1. Briefing

> Na pasta `vibe-coding`, desenvolva uma landing page para um hackathon universitário na Avenida Paulista. A atividade propõe utilizar IA no desenvolvimento de interfaces sem perder a autonomia do desenvolvedor, seguindo ciclos curtos de descrição, geração de código, visualização no navegador e refinamento.
>
> A página deve conter contagem regressiva, programação completa, cards de palestrantes e formulário de inscrição. Utilize HTML e Tailwind CSS, preferencialmente em um único arquivo que possa ser aberto diretamente no navegador, sem configuração complexa. Bibliotecas externas são permitidas, mas só devem ser utilizadas quando realmente fizerem sentido.
>
> A identidade visual inicial deve utilizar fundo escuro `#0B0F1A`, branco `#F8FAFC`, roxo `#8B5CF6`, rosa `#EC4899`, azul `#3B82F6`, ciano `#22D3EE` e amarelo `#FBBF24`. Distribua as cores de maneira equilibrada, utilizando gradientes principalmente nos destaques.
>
> Quero uma página moderna, responsiva e adequada ao público universitário, com hierarquia visual clara e componentes consistentes. Evite uma composição genérica. Mantenha o código organizado e documente as principais decisões no `CLAUDE.md`.

A IA sugeriu React e Vite, mas recusei essa abordagem por não corresponder às restrições da atividade. Reforcei o uso de HTML e Tailwind via CDN e optei por não utilizar DaisyUI, preferindo criar componentes próprios com classes reutilizáveis, como `.btn`, `.btn-primary` e `.btn-secondary`.

## 2. Componentes e conteúdo

> Desenvolva os componentes da página com estilos consistentes e variações bem definidas. O formulário deve conter nome, e-mail, instituição de ensino e informações sobre participação em equipe, com validação em português e mensagens de erro abaixo dos campos. Não quero os balões padrão do navegador, nem integração com backend: após uma inscrição válida, basta exibir uma mensagem de sucesso.
>
> Crie seis palestrantes fictícios, representados por suas iniciais, sem fotografias ou avatares externos. Organize a programação por horários e mantenha os elementos visuais coerentes com a paleta definida.
>
> Os estados de erro, foco e sucesso devem ser claros e acessíveis. Não introduza cores fora da identidade visual sem necessidade, e mantenha os componentes adaptáveis a telas pequenas.

A IA utilizou vermelho nos erros do formulário, então pedi para substituí-lo pelo rosa da paleta, sempre acompanhado de uma mensagem explicativa. Também preferi as iniciais dos palestrantes às fotos sugeridas, buscando uma solução mais consistente e simples de manter.

## 3. Mudança de direção visual para Madrugada Hacker

> A página está funcional, mas visualmente parece muito genérica, como um template produzido por IA. Quero mudar a direção criativa para uma experiência chamada **Madrugada Hacker**, com programação das 19h às 7h. Não quero apenas trocar o título: repense a composição, a tipografia, a hierarquia visual e a maneira como as seções se conectam.
>
> Preserve a paleta original, mas utilize as cores de acordo com o conceito de uma noite dedicada à tecnologia, programação e desafios. Troque a fonte atual por uma combinação mais coerente com o tema, sem prejudicar a legibilidade. Remova os rótulos repetitivos, como “// SOBRE O EVENTO”, e evite clichês visuais comuns em landing pages geradas por IA.
>
> Organize a programação como uma narrativa que começa com o credenciamento, passa pelas palestras e pelo desenvolvimento dos projetos, ganha destaque nos desafios da madrugada e termina com as apresentações ao amanhecer.
>
> Utilize esta programação como referência:
>
> - 19h — Credenciamento & Cyber Welcome.
> - 20h — The Hack Begins.
> - 21h — Tech Talks: O Futuro é Agora.
> - 22h — Code Rush.
> - 00h — Midnight Debugging.
> - 02h — Madrugada Hacker: Insomnia Mode, com desafio surpresa de programação e mini CTF.
> - 03h30 — Coffee & Commit.
> - 05h — Final Commit.
> - 06h — Sunrise Demo Day.
> - 07h — The Last Level, com premiação e encerramento.
>
> Quero uma identidade própria, com atmosfera noturna, elementos tecnológicos e uma transição visual que remeta à chegada do amanhecer. Mantenha a contagem regressiva, os palestrantes e o formulário, mas faça com que todos os componentes pareçam pertencer ao mesmo universo visual.

Essa foi a principal mudança do projeto. A programação passou a contribuir para a identidade visual, e não apenas cumprir a função de informar horários. Percebi que uma boa IDV depende da relação entre cores, tipografia, composição, conteúdo e conceito, e não somente de uma paleta bonita.

## 4. Elementos temáticos

> Refine a identidade da Madrugada Hacker com elementos que remetam à experiência presencial do evento. Transforme os cards de palestrantes em crachás, como cartões presos a um cordão, com variações para palestrantes, mentoras, banca avaliadora e host. Utilize pequenas inclinações e detalhes gráficos quando fizer sentido, mantendo a leitura e a consistência entre os componentes.
>
> Quero também transmitir a passagem da noite durante a navegação. Sugira uma solução visual, como um relógio que acompanhe o período das 19h às 7h, sem competir com o conteúdo. Se o elemento ocupar espaço demais no celular, limite sua exibição a telas maiores.
>
> Mantenha apenas animações que contribuam para a experiência. A faixa com os nomes das atividades pode ter movimento, mas deve respeitar a preferência do usuário por movimento reduzido.
>
> Como o evento é fictício, não apresente um endereço completo como se fosse real. Mantenha referências às estações de metrô próximas e inclua no formulário uma confirmação de que o participante tem 18 anos ou mais.

A IA sugeriu rotações leves para os crachás e um relógio fixo para reforçar a temática. Aproveitei essas ideias com restrições de responsividade. Também preferi evitar bibliotecas de animação desnecessárias, priorizando efeitos com função visual clara.

## 5. Revisão crítica no navegador

> Revise a página considerando o resultado visual em diferentes tamanhos de tela. No celular, as opções de “já tem time?” estão espremidas, a lua se sobrepõe à data e os crachás inclinados ficam muito próximos das bordas, podendo provocar rolagem horizontal.
>
> Corrija também o espaçamento do logo e a altura de linha da tipografia, pois os acentos em letras maiúsculas estão encostando na linha superior. Preserve a identidade visual e a hierarquia dos elementos, sem simplesmente reduzir todos os tamanhos.
>
> Verifique os breakpoints, os espaçamentos, os elementos decorativos e o comportamento dos componentes. Garanta que o formulário continue legível e utilizável, que os elementos interativos funcionem e que a animação respeite a preferência por movimento reduzido.
>
> Faça correções pontuais nos problemas identificados, sem reformular partes que já estão funcionando. Ao concluir, diferencie o que foi efetivamente verificado daquilo que ainda precisa de testes.

A visualização no navegador foi essencial para identificar problemas que não estavam claros apenas pela descrição. Em vez de pedir mudanças genéricas, passei a apontar os elementos específicos, explicar o que estava errado e delimitar o resultado esperado. Isso tornou os pedidos mais objetivos e ajudou a preservar as decisões visuais já estabelecidas.

## Fechando

O que mais me marcou foi que a primeira versão estava tecnicamente certa, mas sem graça. A IA entrega rápido o que é "padrão", e o diferencial só apareceu quando eu parei, olhei e decidi mudar o conceito. Daí para frente, a IA ajudou muito na execução, mas quem dizia o que ficava e o que saía era eu.
