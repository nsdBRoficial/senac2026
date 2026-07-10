# Pesquisa: LIB vs SDK vs API — e aplicação no projeto do jogo 2D (Cavaleiro Solo)

## 1. Definições

### LIB (Biblioteca / Library)
Uma **lib** é um conjunto de código reutilizável (funções, classes, rotinas) que resolve um problema específico e é *incorporado diretamente* dentro do seu programa. Ela não roda sozinha — precisa ser importada/linkada ao seu código para funcionar.

- Exemplos: `Pygame` (Python), `Box2D` (física), `TMXLib` (leitura de mapas Tiled), `Newtonsoft.Json` (C#).
- Você chama as funções da lib de dentro do seu código; ela não tem "vida própria".

### SDK (Software Development Kit)
Um **SDK** é um pacote maior e mais completo que geralmente inclui **várias libs, ferramentas, documentação, exemplos, compiladores e até um ambiente de execução/testes**. É tudo que você precisa para desenvolver para uma plataforma específica.

- Exemplos: `Unity SDK`, `Android SDK`, `Godot Engine` (em partes), `Steamworks SDK`.
- Um SDK pode conter uma ou mais libs e ainda expor APIs para você usar.

### API (Application Programming Interface)
Uma **API** é um **contrato/interface** de comunicação entre dois sistemas: define quais funções, métodos ou endpoints estão disponíveis, quais dados enviar e quais dados esperar de volta. A API pode ser local (parte de uma lib) ou remota (via internet, como uma API REST).

- Exemplos: API do Steam (conquistas, ranking online), API REST de um leaderboard online, API de física exposta pela sua própria engine.
- A API é a "porta de entrada"; a implementação por trás dela pode ser uma lib, um serviço web, etc.

## 2. Diferença resumida

| Característica | LIB | SDK | API |
|---|---|---|---|
| O que é | Código pronto reutilizável | Kit completo de ferramentas | Contrato de comunicação |
| Roda sozinho? | Não, é embutido no código | Não, mas fornece ferramentas para criar o app | Não, é só a interface |
| Escopo | Específico (ex: física, som) | Amplo (plataforma inteira) | Pode ser pequeno (uma função) ou grande (um serviço inteiro) |
| Exemplo prático | `pygame.mixer` para tocar som | Unity SDK para criar o jogo inteiro | Endpoint para salvar pontuação online |
| Analogia | Uma peça de LEGO pronta | A caixa completa de LEGO com manual e peças | O encaixe padrão entre as peças |

**Resumindo com uma analogia simples:**
- A **API** é a tomada elétrica (o padrão de encaixe).
- A **lib** é o fio com o plugue já pronto que você compra e conecta.
- O **SDK** é a caixa de ferramentas completa que vem com vários fios, manuais e até o multímetro para você trabalhar.

## 3. Aplicando ao projeto: Jogo 2D — Cavaleiro Solo

Pensando no produto inicial do grupo (o jogo do cavaleiro), dá pra planejar a arquitetura em três camadas, usando exatamente esses três conceitos:

### a) LIB que podemos criar
Uma biblioteca própria, reutilizável em outros jogos do grupo no futuro. Sugestão:

**`knight-core` (ou `cavaleiro-lib`)** — biblioteca com as funcionalidades centrais do personagem:
- `MovimentoController` — controla andar, correr, pular
- `CombateSystem` — ataque, dano, combo, invencibilidade temporária
- `AnimacaoManager` — troca de sprites conforme estado (idle, andando, atacando, morrendo)
- `ColisaoHelper` — detecção de colisão com inimigos/cenário

Essa lib seria importada dentro do jogo principal (feito em Pygame, Godot ou Unity), sem depender de rede ou de outras ferramentas externas.

### b) SDK que usaríamos
O grupo não vai criar um SDK do zero (isso é trabalho de meses/anos), mas vai **usar** um SDK existente como base do projeto:
- **Godot Engine** ou **Unity** → já trazem editor de cena, engine de física, sistema de áudio, tudo junto.
- Dentro desse SDK, nossa lib (`knight-core`) seria "plugada" como um módulo extra.

### c) API que o jogo pode expor/consumir
Se o jogo tiver features online (ranking, conquistas, salvar progresso na nuvem), aí entra API:
- Consumir uma **API REST** própria (ex: Node.js + banco de dados) para salvar recordes de tempo/fases.
- Ou usar a **API do Steam** (se for publicado lá) para conquistas e estatísticas.

## 4. Proposta de próximos passos para o grupo

1. Cada integrante edita sua parte do documento explicando LIB, SDK e API com suas próprias palavras/exemplos.
2. Definir qual engine/SDK será a base do jogo (Godot, Unity, Pygame etc).
3. Prototipar a lib `knight-core` com pelo menos: movimento, ataque básico e animação.
4. Deixar em aberto a decisão sobre API online (pode ficar para uma versão futura do jogo).

---
*Documento de apoio para pesquisa em grupo — pode ser editado e expandido por cada integrante.*
