# regras-design

Skill para agentes de código (Claude Code, OpenCode, Cursor e outros) que aplica um conjunto de regras de design visual e de escrita para interfaces web. Evita a "cara de IA" (gradiente, emoji, travessão como conector, card-em-card, ícone em quadradinho) e garante que a tela aguenta dado real: texto longo, número grande, lista enorme, campo vazio.

> Regra de piso para qualquer UI. Não decide a marca do projeto: ela sempre prevalece.

## O que ela faz

Você pede para criar ou repaginar uma tela, seção, componente, formulário, card ou landing page, e o agente aplica 10 blocos de regra antes de entregar:

| Bloco | Cobre |
|---|---|
| 1. Cores | só cores sólidas da marca, sem gradiente, sem glow, contraste mínimo AA |
| 2. Texto e pontuação | sem travessão como conector, sem frases de efeito típicas de IA, frases curtas e específicas |
| 3. Copy da primeira dobra | sem badge genérico ("AI-Powered", "Beta"), CTA com ação real |
| 4. Ícones e emojis | biblioteca de ícones, nunca emoji na UI (exceto chat) |
| 5. Tipografia | escala numérica, pisos de tamanho (11px mínimo funcional, 16px em campo) |
| 6. Layout e composição | espaçamento em escala de 4/8px, sem card dentro de card |
| 7. Movimento | durações numéricas (100-500ms), curva de saída, sem bounce |
| 8. Estados, robustez e qualidade mínima | os 4 estados de tela, os 7 estados de controle, dado extremo |
| 9. Ação e decisão | inline primeiro, no máximo 4 opções, ação destrutiva nomeia a consequência |
| 10. Checklist antes de entregar | 12 perguntas de verificação final |

Para formulário, tabela, lista ou qualquer tela com dado do usuário, a skill também aplica o roteiro de **robustez** (`reference/robustez.md`): teste de extremos (texto de 100+ caracteres, número de R$ 1.284.937,52, lista de 1.000+ itens), técnicas de CSS para não estourar o layout, formatação pt-BR (`Intl.NumberFormat`, `Intl.DateTimeFormat`) e estado vazio por motivo.

### Composição com outras ferramentas

- **`ui-ux-pro-max`** decide o que é correto: paletas, pares de fonte, tokens, escalas, acessibilidade.
- **`frontend-design`** decide o que é distintivo: direção estética, tipografia com personalidade.
- A skill de marca do seu projeto cuida da voz do texto.
- `regras-design` é o piso comum: se qualquer um dos outros sugerir gradiente, emoji na UI ou travessão-conector, ela vence. A marca e o design system do projeto vencem de todos.

## Instalação

Pré-requisito: [Node.js](https://nodejs.org) 18 ou superior (traz o `npx`).

### Com npx (recomendado)

```bash
npx skills add nymbuslab/regras-design
```

O instalador pergunta em quais agentes instalar (Claude Code, OpenCode, Cursor etc.) e se a instalação é só para o projeto atual ou para todos os projetos.

Para instalar direto, sem perguntas:

```bash
# Claude Code, valendo para todos os seus projetos
npx skills add nymbuslab/regras-design -g -a claude-code -y

# Claude Code e OpenCode ao mesmo tempo
npx skills add nymbuslab/regras-design -g -a claude-code -a opencode -y
```

| Opção | Efeito |
|---|---|
| `-g` | instala para o usuário (todos os projetos); sem ela, só no projeto atual |
| `-a <agente>` | escolhe o agente (`claude-code`, `opencode`, `cursor`...); pode repetir |
| `-y` | não faz perguntas |

### Manual

Copie a pasta `skills/regras-design` para a pasta de skills do seu agente:

| Agente | Pasta |
|---|---|
| Claude Code (todos os projetos) | `~/.claude/skills/regras-design/` |
| Claude Code (só um projeto) | `.claude/skills/regras-design/` |
| OpenCode | `~/.config/opencode/skills/regras-design/` (o OpenCode também lê `~/.claude/skills/`) |

```bash
git clone https://github.com/nymbuslab/regras-design.git
cp -r regras-design/skills/regras-design ~/.claude/skills/
```

Feche e abra o agente depois de instalar.

## Como usar

Peça para criar ou repaginar uma tela, seção, componente ou texto de interface. Exemplos:

- "Cria a tela de cadastro de cliente"
- "Repagina o card de plano da landing page"
- "Revisa essa tela antes de eu entregar"

No Claude Code também dá para chamar pelo nome: `/regras-design`.

A skill é dispensável em ajuste pontual de uma propriedade CSS ou em correção que não muda nada visível na tela.

### Exemplo

Pedido: "Cria a seção de destaque (hero) da landing page do meu SaaS de PDV."

Sem a skill, um agente tende a gerar fundo em degradê, um selo "AI-Powered" e um CTA genérico ("Comece agora"). Com a skill:

```markdown
- Fundo sólido, cor da marca (sem gradiente)
- Selo com informação real: "Homologado NFC-e"
- Headline: diz o que o produto resolve e para quem
- CTA: "Agendar demonstração" (ação real, não "Comece agora")
- Sem travessão na copy
```

## Atualizar e remover

```bash
npx skills update regras-design
npx skills remove regras-design
```

## Estrutura

```
skills/regras-design/
├── SKILL.md                roteiro das 10 regras e o checklist final
├── reference/
│   └── robustez.md         roteiro de teste de extremos, CSS, formatação pt-BR, estado vazio
└── evals/
    └── evals.json          3 cenários de teste com critérios de aprovação
```

## Limites

- A skill aplica regras de piso. Se o projeto já tem design system e marca definidos, eles sempre prevalecem.
- Um pedido explícito seu (ex. "quero gradiente aqui") é atendido: a skill protege o que você não especificou, não contraria instrução direta.
- Dependendo do agente, um pedido pequeno pode não acionar a skill automaticamente; chame pelo nome se quiser garantir.

## Licença

[MIT](LICENSE)
