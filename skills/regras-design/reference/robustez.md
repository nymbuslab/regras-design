# Robustez: a tela aguenta dado real?

Referência da seção 8 da `regras-design`. Ler ao criar ou alterar formulário, tabela, lista, card com dado do usuário ou qualquer tela que mostre conteúdo que não foi escrito pelo designer.

O protótipo sempre tem o nome "Maria Silva", três itens e o valor R$ 49,90. O cliente real tem razão social de 120 caracteres, 4.000 produtos e faturamento de R$ 1.284.937,52.

## 1. Roteiro de teste de extremos

Antes de entregar, preencher a tela com cada caso e olhar no desktop e em 360px:

| Caso | Exemplo | O que não pode acontecer |
|---|---|---|
| Texto longo | nome com 100+ caracteres, palavra sem espaço (e-mail, URL, código de barras) | estourar o container, empurrar botão para fora, quebrar o grid |
| Texto mínimo | 1 caractere, campo vazio, campo opcional não preenchido | card colapsar, rótulo órfão, "undefined" / "null" na tela |
| Número grande | R$ 1.284.937,52; quantidade 99.999; percentual negativo | coluna desalinhada, valor cortado, sinal sumindo |
| Lista grande | 1.000+ itens | tela travar, rolagem da página inteira em vez da lista, sem paginação ou busca |
| Lista de um | 1 item só | layout pensado para grid parecer quebrado |
| Sem permissão | usuário sem acesso à ação | botão que falha ao clicar em vez de explicar |
| Rede lenta / falha | servidor demora ou devolve erro | tela branca, botão clicável duas vezes, dado digitado perdido |

## 2. Técnicas de CSS

```css
/* Filho de flex/grid encolhe em vez de estourar */
.item { min-width: 0; }

/* Uma linha com reticências */
.truncar { overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }

/* Várias linhas com reticências */
.limitar-3 { display: -webkit-box; -webkit-line-clamp: 3; -webkit-box-orient: vertical; overflow: hidden; }

/* Palavra enorme sem espaço (e-mail, URL) quebra em vez de vazar */
.quebrar { overflow-wrap: anywhere; }

/* Números alinhados em tabela e valores */
.numero { font-variant-numeric: tabular-nums; text-align: right; }

/* Imagem não faz a tela pular ao carregar */
.thumb { aspect-ratio: 4 / 3; object-fit: cover; }
```

- Container de texto sem largura fixa em px: usar `max-width`, `min-width: 0` e unidades relativas.
- Texto truncado mostra o conteúdo completo no `title` ou em tooltip.
- Menu suspenso, tooltip e popover não podem ficar presos dentro de `overflow: hidden` de um card ou tabela: usar portal, `position: fixed` ou a API `popover`.

## 3. Formatação pt-BR

```js
new Intl.NumberFormat('pt-BR', { style: 'currency', currency: 'BRL' }).format(1284937.52) // R$ 1.284.937,52
new Intl.DateTimeFormat('pt-BR').format(data)                                              // 07/10/2026
new Intl.NumberFormat('pt-BR').format(99999)                                               // 99.999
```

- Plural com regra, não concatenação: `Intl.PluralRules` ou função `n === 1 ? '1 item' : \`${n} itens\``. Nunca "1 itens" nem "item(s)".
- Valor monetário é calculado em centavos (inteiro) e formatado só na exibição.

## 4. Envio e erro

- Ao enviar: botão desabilitado, rótulo de carregamento ("Salvando..."), clique repetido ignorado.
- Ao falhar: o formulário continua preenchido, o erro aparece junto ao campo culpado ou no topo com link para ele, e o botão volta a ficar ativo.
- Erro de um bloco (um gráfico, um card) mostra o erro só naquele bloco; o resto da tela continua funcionando.
- Carregamento acima de ~300ms mostra esqueleto ou indicador; abaixo disso, não pisca indicador nenhum.

## 5. Estado vazio por motivo

| Motivo | Mensagem | Ação |
|---|---|---|
| Primeiro uso | o que vai aparecer aqui | botão de criar o primeiro |
| Busca sem resultado | "Nada encontrado para 'xyz'" | limpar busca |
| Filtro aplicado | quais filtros estão escondendo os itens | limpar filtros |
| Sem permissão | por que não tem acesso e quem pode liberar | nenhuma ação falsa |
| Falha ao carregar | o que deu errado em linguagem simples | tentar de novo |
