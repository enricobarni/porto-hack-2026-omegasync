# OmegaSync — Porto Hack Santos 2026

Motor de decisão sobre o comportamento do importador após a DUIMP, com foco no
**Cenário C** (retirada via retroporto) e **Cenário B** (falta de fluxo de caixa).

Hackathon: [Porto Hack Santos 2026](https://portohacksantos.com.br) · Realização: ABTRA ·
Trilha Hack.

## O problema

Desde maio de 2026, o Porto de Santos permite desembaraço "sobre águas", possibilitando
retirada direta da carga sem passar por recinto alfandegado. A ABTRA — que representa
terminais e recintos alfandegados — não sabe quanto do seu volume é estruturalmente perdido
para esse novo fluxo, quanto é retível, e o que oferecer no lugar da armazenagem.

## O que o OmegaSync faz

Transforma em motor executável a "Máquina de Decisão do Importador" (fluxograma oficial da
ABTRA), respondendo três perguntas por carga:

1. **O que essa carga deveria fazer?** — ponto de indiferença entre retirada direta e
   retroporto, calculado com tarifa pública
2. **Dá para executar?** — testa a janela de 48h úteis contra o perfil da carga
3. **Quanto custa não fazer?** — valor em reais deixado na mesa

E, agregando várias cargas, mostra ao operador de terminal/recinto quanto do volume é
estruturalmente perdido, quanto é retível, e onde agir.

## Arquitetura

Toda a lógica de decisão vive isolada em `/lib/engine`. Isso é decisão deliberada: qualquer
integrante do time consegue explicar e defender qualquer parte do código, e a lógica de
negócio nunca se mistura com apresentação.

## Stack

- Next.js + React
- TypeScript
- Function calling com [Resolv ONE] para a camada de explicação (agente)

TypeScript foi escolhido no lugar de Python porque é a linguagem que o time já domina — o
motor de decisão é lógica condicional e aritmética, sem necessidade de recursos exclusivos de
outra linguagem.

## Como rodar localmente

```bash
npm install
npm run dev
```

Abra http://localhost:3000

## Duas camadas do motor

- **Camada 1 — regra pública:** cobre os 6 cenários, com fórmulas baseadas em tarifas e
  normas públicas (ver FONTES.md). Não depende de pesquisa de campo.
- **Camada 2 — calibração de campo:** ajusta os filtros de B e C com dados reais de entrevistas
  realizadas na pesquisa do hackathon. Só B e C são calibrados — os demais cenários (A, D, E, F)
  não exigem calibração por natureza (ver seção correspondente na pesquisa).

A interface sinaliza claramente qual ramo é calibrado e qual é só modelo teórico.

## Time

Time OmegaSync — [nomes dos integrantes]

## Licença

MIT — ver LICENSE