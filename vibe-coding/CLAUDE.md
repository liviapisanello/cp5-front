# CLAUDE.md — Madrugada Hacker

Landing page de um hackathon universitário (fictício) na Avenida Paulista que acontece **das 19h às 7h**. Feita para a atividade de Front-end sobre vibe coding com autonomia: descrever → gerar → ver no navegador → refinar, em ciclos curtos. A IA executa, mas as decisões são minhas.

Antes de gerar ou alterar qualquer coisa nesta página, siga este arquivo.

---

## 1. Conceito

**Rolar a página é atravessar a noite.** O topo é céu estrelado com lua. A programação esquenta de azul (noite) para roxo e rosa (madrugada) e depois amarelo (amanhecer). A inscrição já começa a clarear, e o rodapé termina com o sol nascendo e um "Bom dia, hacker.". Um relógio fixo no canto converte a rolagem em horário: o topo é 19:00 e o fim é 07:00.

A estética é **pôster de festa + terminal**: títulos condensados enormes em caixa alta, cantos retos, sombras duras deslocadas, fonte pixel para dados e alguns elementos levemente tortos (crachás, ingresso, selo de data).

O que **não** fazer, porque deixa a cara de "template gerado":

- eyebrows do tipo `// sobre o evento` em cima de cada título;
- cantos `rounded-2xl` em tudo, glow suave em tudo, cards idênticos em grade;
- Inter, Space Grotesk, JetBrains Mono e outras fontes "padrão de IA";
- hero centralizado com selo + título + subtítulo + 2 botões, todos no mesmo eixo.

---

## 2. Stack

| Item     | Escolha                                                                      |
| -------- | ---------------------------------------------------------------------------- |
| Marcação | HTML5 semântico, arquivo único `index.html`                                  |
| Estilo   | Tailwind CSS v4 via `@tailwindcss/browser@4.1.13` (CDN, versão fixada)       |
| Fontes   | Google Fonts: Big Shoulders Display, Atkinson Hyperlegible Next, VT323       |
| Ícones   | Formas em CSS (lua, sol), caracteres (✦ ☾ ☀) e um SVG inline (pino de local) |
| JS       | Vanilla, inline no fim do `<body>`, sem dependências                         |
| Build    | Nenhum. Basta abrir `index.html` no navegador                                |

Biblioteca de componentes: não usar. A estética depende de cantos retos e sombras duras, e os temas prontos (DaisyUI, Flowbite) puxam para o visual arredondado.

> O Tailwind pelo navegador serve para protótipo e aula. Em produção, o certo é gerar o CSS com o CLI ou com o Vite.

---

## 3. Tokens

Ficam em `@theme`. Prefixo `hk-` para não colidir com a paleta padrão do Tailwind.

### Cores

| Token        | Hex       | Papel                                                                |
| ------------ | --------- | -------------------------------------------------------------------- |
| `hk-bg`      | `#0B0F1A` | Céu da noite, fundo base                                             |
| `hk-surface` | `#121828` | Crachás e faixa de seção _(derivado do fundo)_                       |
| `hk-white`   | `#F8FAFC` | Texto; botão primário; opacidades para hierarquia                    |
| `hk-blue`    | `#3B82F6` | **Noite** (19h–23h59); mentoria                                      |
| `hk-purple`  | `#8B5CF6` | **Madrugada**; palestras; sombra do botão primário; seleção de opção |
| `hk-pink`    | `#EC4899` | Ponto alto da madrugada (Insomnia Mode); host do CTF; **erros**      |
| `hk-cyan`    | `#22D3EE` | **Foco e interação**; segundos da contagem; links no hover           |
| `hk-yellow`  | `#FBBF24` | **Lua, amanhecer e destaque**: data, marcos, premiação, sol          |

### Tipografia

| Token          | Fonte                              | Uso                                                                                          |
| -------------- | ---------------------------------- | -------------------------------------------------------------------------------------------- |
| `font-display` | Big Shoulders Display 700–900      | Títulos (sempre caixa alta), botões, nomes nos crachás                                       |
| `font-sans`    | Atkinson Hyperlegible Next 400/700 | Texto corrido e formulário. Escolhida pela legibilidade, já que o display é muito condensado |
| `font-pixel`   | VT323                              | Horários, contagem, navegação, tags, erros, números do ingresso                              |

Tamanhos: `h1` usa `clamp(4.25rem, 17vw, 12.5rem)`; `h2` `text-5xl → sm:text-7xl`; títulos de atividade `text-2xl → sm:text-3xl`. VT323 nunca abaixo de `text-base` (16px), porque fica ilegível.

### Forma

- **Cantos retos** em botões, campos, cards e crachás. Só lua, sol, furo do crachá e recortes do ingresso são redondos.
- **Sombra dura** `shadow-[Npx_Npx_0_cor]` no lugar de glow em elementos interativos ou de destaque (botão primário, contagem, crachá host, ingresso, campo em foco).
- Rotação sutil (−2° a 2°) só em: selo de data, faixa de rolagem, crachás e ingresso.

---

## 4. Regras de cor

1. **Cor = hora da noite.** Azul → roxo → rosa → amarelo, nessa ordem, de cima para baixo. Uma seção não usa a cor de uma fase posterior como protagonista (por exemplo, nada amarelo dominante na fase "Noite").
2. **Amarelo é lua e sol.** Fora isso, só para marcos (abertura, code freeze, premiação), data do evento e vagas. Nunca como texto corrido.
3. **Ciano = foco/interação.** Todo foco visível usa ciano.
4. **Rosa = ponto alto ou erro.** Erro sempre vem com texto (`> mensagem` em fonte pixel).
5. Gradiente de texto oficial: `purple → pink → yellow` (`text-gradient`), usado no máximo uma vez por seção.
6. Hex fora da paleta só para dado real: cores das linhas do metrô.

### Mapa de tags (programação)

| Tag                  | Classe                    |
| -------------------- | ------------------------- |
| Recepção / Pausa     | `tag-neutral`             |
| Marco / Code freeze  | `tag-yellow` (preenchida) |
| Palestras / Banca    | `tag-purple`              |
| Hacking / ponto alto | `tag-pink`                |
| Mentoria             | `tag-blue`                |
| Desafio              | `tag-cyan`                |

---

## 5. Componentes e variações

Ficam em `@layer components` ou `@utility`, no padrão **base + modificador**.

| Componente            | Classes                                          | Variações                                                                                                            |
| --------------------- | ------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------- |
| Título                | `.title`                                         | tamanho definido no uso; `text-gradient` ou `text-outline` em uma palavra                                            |
| Botão                 | `.btn`                                           | `.btn-primary` (branco, sombra roxa que vira rosa no hover e "afunda" no clique), `.btn-outline`                     |
| Tag                   | `.tag`                                           | `-neutral`, `-yellow`, `-purple`, `-pink`, `-blue`, `-cyan`                                                          |
| Fase da programação   | `.phase` + `.phase-head`                         | três fases com gradiente e ícone próprios (lua azul, estrelas, sol nascendo); título fixo (`sticky`) no desktop      |
| Atividade             | `.slot` + `.slot-time` + `.slot-title`           | cor do horário segue a fase; `.slot-hot` para o ponto alto (barra rosa à esquerda)                                   |
| Crachá                | `.badge` + `.badge-strip`                        | **palestrante** (faixa roxa), **mentora** (azul), **banca** (amarela), **host** (`.badge-host`: borda e sombra rosa) |
| Contagem              | bloco com sombra ciano                           | segundos em ciano; textos de estado "acontecendo agora" e "edição encerrada"                                         |
| Ingresso de premiação | bloco amarelo girado                             | recortes laterais + linha pontilhada                                                                                 |
| Campo                 | `.field-label` / `.field-input` / `.field-error` | foco (borda e sombra ciano) e erro (`aria-invalid`, rosa)                                                            |
| Opção                 | `.choice`                                        | marcada via `has-checked:` (roxo + sombra)                                                                           |
| Faixa                 | marquee `animate-marquee`                        | para com `motion-reduce`                                                                                             |
| Céu                   | `bg-stars`, `moon`                               | —                                                                                                                    |

**Regra:** padrão com significado que se repete 3 vezes ou mais vira componente. Layout continua inline.

---

## 6. Estrutura

1. Header fixo (fundo aparece após rolar; menu hambúrguer abaixo de `md`)
2. Hero: selo de data, título gigante, texto, CTAs, **contagem**
3. Faixa rolando com os nomes das atividades
4. Sobre: frase-manifesto grande + texto + números em grade com bordas
5. **Programação**: Noite / Madrugada / Amanhecer
6. **Crachás** (6 pessoas)
7. Local (metrô) + ingresso de premiação
8. **Inscrição** (o fundo começa a clarear)
9. FAQ (`<details name="faq">`)
10. Rodapé com nascer do sol

Relógio fixo de rolagem (`#relogio-scroll`): aparece a partir de `sm` e é `aria-hidden`.

---

## 7. Comportamento

- **Contagem:** de `2026-11-21T19:00:00-03:00` até `2026-11-22T07:00:00-03:00`, sempre com fuso explícito. O intervalo é limpo ao zerar.
- **Relógio de rolagem:** `19:00 + progresso × 12h`. Ícone ☾ em ciano antes das 5h e ☀ em amarelo depois.
- **Formulário:** `novalidate` + validação própria. Valida no envio e, depois disso, a cada mudança. O foco vai para o primeiro campo inválido. Campos obrigatórios: nome com sobrenome, e-mail, instituição, semestre, papel no time, **18+** e regulamento. O sucesso é simulado e não há envio real.

---

## 8. Acessibilidade

- Link "Pular para o conteúdo"; landmarks `header/nav/main/footer`.
- Contagem `aria-hidden` + texto `sr-only` com a data. Nada de `aria-live` na contagem.
- Lua, estrelas, sol, faixa e relógio de rolagem: `aria-hidden`.
- Erros ligados por `aria-describedby` e `aria-invalid`.
- `motion-reduce:animate-none` na faixa e em animações contínuas.
- Parágrafos em no mínimo `text-hk-white/70`; legendas curtas podem ir até `/50`.

---

## 9. Regras do projeto

- ✅ Mobile-first. Testar em **390px** e **1440px**, sem scroll horizontal. O `body` tem `overflow-x-clip` por causa dos elementos rotacionados.
- ✅ Só tokens `hk-*` (exceto as cores do metrô).
- ✅ Textos em pt-BR, com tom de conversa ("Pega sua vaga", "Traga café"). Nomes das atividades em inglês, como na programação oficial.
- ✅ Pessoas, endereço exato e valores são **fictícios**, e o rodapé avisa isso.
- ❌ Sem eyebrows `// seção` e sem fontes "padrão de IA" (ver seção 1).
- ❌ Sem fotos de rostos para pessoas fictícias. Usar iniciais.
- ❌ Sem número de endereço na Paulista.
- ❌ Sem framework JS, bundler ou biblioteca de animação.

### Checklist de cada ciclo

1. Abri em 390px e 1440px? Algo vazou para os lados?
2. Tab percorre tudo com foco ciano visível?
3. Envio vazio mostra os 7 erros e foca "Nome"? Envio válido mostra sucesso? "Fazer outra inscrição" limpa tudo?
4. Contagem e relógio de rolagem fazem sentido (topo 19:00, fim 07:00)?
5. Prêmios somam R$ 15 mil (8 + 4 + 2 + 1)?
