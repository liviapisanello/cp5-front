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

## Fechando

O que mais me marcou foi que a primeira versão estava tecnicamente certa, mas sem graça. A IA entrega rápido o que é "padrão", e o diferencial só apareceu quando eu parei, olhei e decidi mudar o conceito. Daí para frente, a IA ajudou muito na execução, mas quem dizia o que ficava e o que saía era eu.
