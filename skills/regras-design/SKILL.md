---
name: regras-design
description: "Regras de design visual e de texto que evitam a cara de interface gerada por IA e garantem robustez: cores sólidas sem gradiente, sem emoji nem travessão, tipografia e espaçamento com números, movimento, estados de tela e de controle, dados extremos, texto de ação e checklist de entrega. Use ao criar ou repaginar tela, seção, componente, formulário, card, landing page ou texto de tela, e ao revisar uma UI antes de entregar. Dispensável em ajuste pontual de uma propriedade CSS ou em correção que não muda nada visível."
---

# Regras de Design e Escrita

Aplicar em todo projeto de interface (site, sistema web, landing page, painel).
Objetivo: layout bonito, coeso, que aguenta dado real e que não pareça gerado por IA.

> **Como usar:** ler antes de desenhar/implementar UI nova ou repaginar UI existente.
> Passar o **checklist da seção 10 antes de entregar** qualquer tela. Para formulário,
> tabela, lista ou qualquer tela com dado do usuário, seguir também
> [reference/robustez.md](reference/robustez.md). A marca do projeto (cores/tipografia
> definidas no design system local) sempre prevalece; estas regras preenchem as
> lacunas e barram os vícios de "cara de IA".
>
> **Composição:** a direção visual mais profunda vem de dois plugins com papéis
> distintos. O `ui-ux-pro-max` decide o que é **correto** (paletas, pares de fonte,
> tokens, escalas, acessibilidade, movimento); o `frontend-design` decide o que é
> **distintivo** (direção estética, tipografia com personalidade, fugir do templated).
> A voz e o método de copy de venda ficam na skill de marca do projeto (ex.
> `copy-nymbus`). Estas regras são o piso comum e valem sobre os dois: se qualquer um
> deles sugerir gradiente, emoji na UI, travessão-conector, glass ou efeito de
> espetáculo, ignore. Em conflito, a marca e o design system do projeto ganham de todos.

## 1. Cores

- Usar apenas cores sólidas da marca. Gradientes são proibidos em fundos, botões, cards, textos e ícones.
- Definir uma paleta fechada de 4 a 6 valores em variáveis CSS (primária, secundária, fundo, superfície, texto, borda). Nenhum hex solto no meio do código.
- Cor tem função, não enfeite: uma cor de destaque para ação principal, neutros para o resto. Se tudo é destaque, nada é.
- Não usar as paletas que viraram assinatura de IA: fundo creme (#F4F1EA) com serifada grande e acento terracota (#D97757), preto com verde ácido, roxo/azul neon em degradê.
- Contraste mínimo AA (4.5:1 para texto normal, 3:1 para texto grande e ícones).
- Texto secundário sobre fundo colorido usa um tom derivado do próprio fundo, nunca cinza genérico.
- Sombras: no máximo dois níveis, sempre neutras, sutis e com deslocamento. Nada de glow colorido, halo, spotlight radial atrás do hero ou brilho atrás de card.

## 2. Texto e pontuação

- Não usar travessão (—) nem meia-risca (–) no meio da frase. Substituir por vírgula, dois pontos, ponto final, parênteses ou quebra de parágrafo.
- Não usar as construções típicas de IA:
  - "Não é apenas X, é Y", e a cadência de efeito repetida seção após seção ("X. Sem Y.", "Menos X. Mais Y.")
  - listas de três adjetivos em sequência ("rápido, moderno e intuitivo")
  - "no mundo de hoje", "na era digital", "revolucione", "transforme", "eleve"
  - frases que abrem com "Seja bem-vindo ao futuro de..."
- Frases curtas, voz ativa, tempo presente. Escrever como se estivesse explicando para o cliente por telefone.
- Ser específico em vez de esperto. "Emite NFC-e em 2 cliques" vale mais que "Solução completa e inovadora".
- Sentence case em títulos, botões e labels. Nada de Caixa Alta Em Toda Palavra e nada de CAPS LOCK como recurso de ênfase.
- Nomear as coisas pelo que o usuário reconhece, não pelo nome técnico interno. "Notificações", não "webhook config".
- Título não repete o parágrafo de introdução, e o mesmo texto não aparece duas vezes no mesmo card.
- Sem conteúdo de rascunho na entrega: nada de Lorem ipsum, "Empresa X", números inventados ("+10.000 clientes") ou depoimentos fictícios.

## 3. Copy da primeira dobra

- Proibidas pílulas e badges genéricas: "AI-Powered", "New", "Launch", "v2.0", "Beta", "Powered by IA".
  - Se houver badge, ela precisa carregar informação real: "Integrado à SEFAZ SP", "Homologado NFC-e", "Suporte 7h às 19h".
- A headline diz o que o produto faz e para quem, em uma frase. O subtítulo resolve a dúvida imediata seguinte.
- CTA descreve a ação real: "Falar com o suporte", "Agendar demonstração", "Baixar o instalador". Nunca "Comece agora", "Saiba mais", "Clique aqui".
- Página não é montada no template "número gigante + rótulo pequeno + faixa de estatísticas + destaque". Número grande só quando o número é o assunto.

## 4. Ícones e emojis

- Sempre usar biblioteca de ícones (Lucide, Phosphor, Heroicons, Font Awesome). Uma biblioteca só por projeto.
- Manter tamanho, espessura de traço e estilo (outline ou fill) consistentes em toda a interface.
- Emoji na UI é proibido: menus, botões, títulos, cards, tabelas, documentação.
- Emoji permitido só onde é linguagem natural da conversa: mensagens de chat, respostas de bot, WhatsApp, e-mail informal.
- Ícone acompanha texto. Ícone sozinho só com tooltip ou aria-label.
- Proibido o "ícone dentro de quadradinho arredondado em cima do título" como abertura de card. Ícone vai em linha com o texto ou não vai.
- Nada de ilustração de hero montada com formas SVG primitivas (círculos, blobs, linhas soltas).

## 5. Tipografia

- No máximo duas famílias: uma para títulos, uma para texto. Uma terceira só se houver dado tabular ou código.
- Fonte monoespaçada só para código e dado. Nunca como fantasia de "produto técnico".
- Escala definida e reaproveitada (ex.: 12 / 14 / 16 / 20 / 24 / 32 / 48). Nada de tamanho inventado por seção. Passo entre níveis de pelo menos 1.25 em landing e 1.125 a 1.2 em sistema; sistema usa escala fixa em rem, sem `clamp`.
- Hierarquia por tamanho e peso, não por cor aleatória.
- Corpo de texto entre 16 e 18px, altura de linha de 1.5 a 1.6, largura máxima de 65 a 75 caracteres por linha.
- Título tem mais espaço acima do que abaixo: ele pertence ao conteúdo que vem depois.
- Pisos: texto funcional (botão, label, célula) nunca abaixo de 11px; campo de formulário com 16px no mínimo (abaixo disso o iOS dá zoom); sem texto justificado; sem parágrafo em caixa alta; números tabulares (`font-variant-numeric: tabular-nums`) em tabela e valor monetário.

## 6. Layout e composição

- Espaçamento em escala de 4 ou 8px. Sem valores avulsos.
- Ritmo: elementos de um mesmo grupo bem próximos, grupos diferentes bem separados. O mesmo espaçamento em tudo apaga a hierarquia.
- Respiro mínimo de 12 a 16px dentro de qualquer container com borda ou fundo, e de 16px na borda da tela no celular.
- Um valor de raio de borda para todo o sistema (ou dois: um para card, um para input).
- Agrupar primeiro por espaço; card só quando o grupo precisa de fronteira. Card dentro de card, nunca.
- Evitar o padrão repetido de "três cards com ícone, título curto e parágrafo genérico". Se usar cards, o conteúdo precisa ser diferente entre si e útil.
- Numeração 01 / 02 / 03 e divisórias só quando o conteúdo realmente for uma sequência. Eyebrow (texto pequeno em caixa alta acima do título) é proibido.
- Borda colorida grossa em um lado só de card, alerta ou item de lista é proibida. Status se mostra com ícone, texto ou fundo sutil.
- Alinhamento consistente: definir o grid e respeitar. Nada de seção centralizada seguida de seção à esquerda sem motivo.
- Evitar clichês visuais de IA: glassmorphism, blobs animados no fundo, mockup de dashboard falso no hero, foto de banco de imagens com "pessoa apontando para tela".
- Ponto pulsando, cursor piscando e letreiro rolando só onde há dado ao vivo de verdade.

## 7. Movimento

- Animação só quando comunica algo: mudança de estado, carregamento, feedback de ação.
- Nada de fade-in em toda seção ao rolar a página.
- Durações: 100 a 150ms para feedback de clique, 150 a 300ms para mudança de estado, 300 a 500ms para painel ou modal abrindo. A saída é mais rápida que a entrada.
- Curva de saída suave (`cubic-bezier(0.16, 1, 0.3, 1)`). Efeito de mola ou elástico (bounce) é proibido.
- Animar só `transform` e `opacity`, nunca `width`, `height` ou `margin`.
- Conteúdo visível por padrão: animação de entrada nunca deixa o conteúdo escondido se o JavaScript falhar.
- Respeitar `prefers-reduced-motion` reduzindo o deslocamento, mas mantendo o feedback de estado.

## 8. Estados, robustez e qualidade mínima

- Toda tela tem os quatro estados prontos: carregando, vazio, erro e sucesso.
- Todo controle interativo tem: normal, hover, foco, pressionado, desabilitado, carregando e erro.
- Tela vazia é convite para agir, com o botão da ação principal, e distingue o motivo: primeiro uso, busca sem resultado, filtro aplicado, sem permissão (explicar por quê) ou falha.
- Erro explica o que aconteceu e o que fazer, sem pedir desculpas e sem termo técnico. Erro de envio preserva tudo que o usuário digitou.
- Botão de envio fica desabilitado e mostra carregamento enquanto processa: duplo envio é impossível.
- Um componente com erro não derruba a tela inteira.
- A tela aguenta dado real: texto muito longo, campo vazio, número grande e lista enorme. Roteiro e técnicas em [reference/robustez.md](reference/robustez.md).
- Moeda, data e número no padrão do usuário (`Intl`, pt-BR por padrão).
- Responsivo até 360px de largura. Imagem com proporção reservada (sem a tela pular ao carregar).
- Foco de teclado visível. Alvo de toque mínimo de 44x44px.
- Formulário com label visível (placeholder não substitui label), formato exigido mostrado antes do envio, mensagem de erro junto ao campo e validação em linguagem simples.

## 9. Ação e decisão

- Inline primeiro: editar, confirmar e dar feedback no próprio lugar sempre que couber. Modal quando a tarefa precisa de foco isolado (confirmação destrutiva, formulário longo, fluxo de etapas). Nunca modal só por hábito.
- No máximo 4 opções visíveis por ponto de decisão: 1 primária, 1 ou 2 secundárias, o resto em menu.
- O nome da ação se mantém do botão até a confirmação: quem clica em "Salvar" vê "Salvo".
- Ação destrutiva nomeia o objeto e a consequência ("Excluir o pedido 1042? Os itens voltam para o estoque."). O botão repete a ação ("Excluir pedido"), nunca "OK" ou "Sim". Quando der, oferecer desfazer em vez de pedir confirmação.

## 10. Checklist antes de entregar

1. Existe algum gradiente, glow, halo ou glass na tela? Remover.
2. Existe travessão no meio de alguma frase? Trocar a pontuação.
3. Existe badge, eyebrow ou palavra genérica na primeira dobra? Trocar por informação real ou tirar.
4. Existe emoji fora de contexto de chat? Trocar por ícone da biblioteca.
5. Todas as cores saem das variáveis da marca?
6. A headline explica o produto para quem nunca ouviu falar dele?
7. Tem algum texto de rascunho, número inventado ou imagem genérica?
8. Tem card dentro de card, borda grossa de um lado só ou ícone em quadradinho em cima de título?
9. A tela resiste ao teste de dados extremos de [reference/robustez.md](reference/robustez.md)?
10. Todo controle tem foco, desabilitado e carregando? O botão de envio impede duplo clique?
11. Ação destrutiva diz o que vai acontecer e o botão repete a ação?
12. Se eu tirar um elemento decorativo, a tela fica pior ou melhor? Se ficar melhor, tirar.
