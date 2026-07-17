# Documentação de Análise da API - ReqRes

## 1. Cenário A: Listar Utilizadores da Página 2
[cite_start]**Verbo HTTP:** GET [cite: 33]
[cite_start]**URL Completa:** https://reqres.in/api/users?page=2 [cite: 34]
[cite_start]**Body da Requisição:** Nenhum [cite: 35]
[cite_start]**Status Code Esperado:** 200 OK [cite: 36]
[cite_start]**Resposta da API (Exemplo do JSON):** [cite: 37]
{
  "page": 2,
  "per_page": 6,
  "total": 12,
  "total_pages": 2,
  "data": [
    {
      "id": 7,
      "email": "michael.lawson@reqres.in",
      "first_name": "Michael",
      "last_name": "Lawson",
      "avatar": "https://reqres.in/img/faces/7-image.jpg"
    }
  ],
  "support": {
    "url": "https://reqres.in/#support-heading",
    "text": "To keep ReqRes free, contributions towards server costs are appreciated!"
  }
}

## 2. Cenário B: Criar Novo Utilizador
[cite_start]**Verbo HTTP:** POST [cite: 33]
[cite_start]**URL Completa:** https://reqres.in/api/users [cite: 34]
[cite_start]**Body da Requisição:** [cite: 35]
{
    "name": "[Seu Nome]",
    "job": "Desenvolvedor Full-Stack"
}
[cite_start]**Status Code Esperado:** 201 Created [cite: 36]
[cite_start]**Resposta da API (Exemplo do JSON):** [cite: 37]
{
    "name": "[Seu Nome]",
    "job": "Desenvolvedor Full-Stack",
    "id": "789",
    "createdAt": "2026-07-03T23:09:34.000Z"
}

## 3. Cenário C: Utilizador Inexistente
[cite_start]**Verbo HTTP:** GET [cite: 33]
[cite_start]**URL Completa:** https://reqres.in/api/users/23 [cite: 34]
[cite_start]**Body da Requisição:** Nenhum [cite: 35]
[cite_start]**Status Code Esperado:** 404 Not Found [cite: 36]
[cite_start]**Resposta da API (Exemplo do JSON):** [cite: 37]
{}
SDK
/**
 * @file tactical-library-sdk.ts
 * @description SDK Oficial da Biblioteca Tática do Sensei para Valorant.
 * Proporciona acesso tipado, busca avançada e filtros inteligentes para sistemas táticos.
 * 
 * @license MIT
 */

// --- TYPES & INTERFACES ---

export type TacticalCategory = 'mira' | 'posicionamento' | 'economia' | 'utilitarias' | 'gameSense';

export type TacticalDifficulty = 'Iniciante' | 'Intermediário' | 'Avançado';

export interface LibraryItem {
  id: string;
  title: string;
  alias: string;
  category: TacticalCategory;
  categoryLabel: string;
  difficulty: TacticalDifficulty;
  description: string;
  howToApply: string;
  proTip: string;
}

export interface SDKConfig {
  defaultDifficulty?: TacticalDifficulty;
  language?: 'pt-BR' | 'en';
}

// --- STATIC DATABASE (CORE DATA) ---

const DEFAULT_ITEMS: LibraryItem[] = [
  {
    id: "crosshair-placement",
    title: "Crosshair Placement",
    alias: "Posicionamento de Mira",
    category: "mira",
    categoryLabel: "Mira & Mecânica",
    difficulty: "Iniciante",
    description: "A arte de manter a mira constantemente na altura da cabeça do oponente, antecipando onde ele estará ao abrir o ângulo. Isso minimiza a necessidade de correções bruscas de flick, resultando em abates muito mais velozes e consistentes.",
    howToApply: "Mantenha a mira na linha do queixo do oponente (use referências visuais no cenário, como caixas e linhas horizontais nas paredes) e afaste-a levemente da parede ao andar para dar tempo de reação caso o inimigo abra correndo.",
    proTip: "No aquecimento, ande pelos mapas mirando apenas nos pontos em que a cabeça do inimigo apareceria. Desative o hábito de mirar no chão."
  },
  {
    id: "counter-strafing",
    title: "Counter-Strafing",
    alias: "Parada Brusca",
    category: "mira",
    categoryLabel: "Mira & Mecânica",
    difficulty: "Avançado",
    description: "Técnica de movimentação usada para zerar a imprecisão de movimento instantaneamente. Consiste em pressionar a tecla oposta à direção do seu movimento (por exemplo, soltar 'A' e dar um toque rápido em 'D') logo antes de atirar.",
    howToApply: "Quando estiver se movendo para a esquerda (A), solte a tecla e toque rapidamente no 'D'. No momento exato em que a velocidade do agente chega a zero, faça o disparo. Se feito corretamente, a bala irá perfeitamente reta.",
    proTip: "Treine no estande de tiro com o indicador de erro de movimento ativado na mira para entender o timing exato da precisão."
  },
  {
    id: "spray-control",
    title: "Spray Transfer & Control",
    alias: "Controle de Recuo",
    category: "mira",
    categoryLabel: "Mira & Mecânica",
    difficulty: "Intermediário",
    description: "Habilidade de compensar o recuo da arma movendo o mouse no padrão inverso ao disparo contínuo, ou transferir esse disparo para um segundo inimigo durante a mesma rajada de balas.",
    howToApply: "Com a Vandal ou Phantom, as primeiras 3 balas são altamente precisas. Do 4º disparo em diante, puxe o mouse para baixo de forma constante. A partir do 9º, a arma começa a oscilar lateralmente.",
    proTip: "Evite disparar mais de 5 a 6 balas por rajada em médias e longas distâncias. Prefira rajadas curtas (bursts) ou tiros únicos (tapping)."
  },
  {
    id: "default-play",
    title: "Default",
    alias: "Estrutura Padrão",
    category: "gameSense",
    categoryLabel: "Táticas & Mindset",
    difficulty: "Intermediário",
    description: "Uma estratégia de início de round em que a equipe se espalha pelo mapa para obter informações, controlar áreas importantes, gastar utilitários inimigos e punir avanços agressivos dos defensores, sem comprometer-se com nenhum bomb site específico.",
    howToApply: "Distribua os jogadores em um padrão como 1-3-1 ou 2-1-2. Segure os ângulos passivamente, espere os utilitários de contenção inimigos (como smokes e barreiras) expirarem e só então decida qual site atacar com base nas brechas identificadas.",
    proTip: "Fazer 'Default' é a melhor solução contra defensores que jogam avançando agressivamente para conseguir abates fáceis."
  },
  {
    id: "clutch-mindset",
    title: "Clutch Isolation",
    alias: "Isolamento em Desvantagem",
    category: "gameSense",
    categoryLabel: "Táticas & Mindset",
    difficulty: "Avançado",
    description: "Abordagem mental e tática quando você é o último sobrevivente contra múltiplos inimigos. Em vez de lutar contra todos de uma vez, o objetivo é isolar cada confronto em duelos individuais de 1v1 usando cobertura e movimentação inteligente.",
    howToApply: "Não se desespere. Use passos falsos ou silêncio total para confundir a localização dos adversários. Faça o plant/defuse de forma a forçá-los a vir até você individualmente e use utilitárias para bloquear linhas de visão indesejadas.",
    proTip: "Inimigos em vantagem numérica tendem a ficar gananciosos e buscar o abate correndo individualmente. Use essa impaciência a seu favor."
  },
  {
    id: "lurk",
    title: "Lurking",
    alias: "Jogo Furtivo",
    category: "posicionamento",
    categoryLabel: "Posicionamento",
    difficulty: "Avançado",
    description: "Jogar longe do foco principal da sua equipe para coletar informações na retaguarda inimiga, cortar as rotas de rotação dos defensores ou pegar inimigos flanqueando desprevenidos.",
    howToApply: "Enquanto sua equipe faz barulho ou executa uma entrada em um bomb site, esgueire-se silenciosamente pelo lado oposto ou pelo meio. Escute os passos das rotações rápidas e elimine os inimigos que estão correndo de costas.",
    proTip: "Um bom lurker não é aquele que se esconde o round inteiro, mas sim o que sabe exatamente quando agir para quebrar a defesa por trás."
  },
  {
    id: "off-angle",
    title: "Off-Angle",
    alias: "Ângulo Incomum",
    category: "posicionamento",
    categoryLabel: "Posicionamento",
    difficulty: "Intermediário",
    description: "Posicionar-se em um local onde o inimigo não espera que você esteja ao abrir a mira (pré-aim). Ao contrário dos ângulos comuns de cobertura (onde os inimigos já abrem atirando), o off-angle pega o oponente de surpresa no meio do movimento.",
    howToApply: "Fique de pé em espaços abertos ou locais planos, ligeiramente afastado das paredes habituais de pixel. Garanta que você consiga pelo menos um abate antes de recuar para uma posição segura de cobertura.",
    proTip: "Excelente para agentes de mobilidade como Jett (com dash) ou Chamber (com teletransporte), que conseguem atirar de locais expostos e escapar instantaneamente."
  },
  {
    id: "one-way-smoke",
    title: "One-Way Smokes",
    alias: "Smokes de Sentido Único",
    category: "utilitarias",
    categoryLabel: "Utilidades",
    difficulty: "Intermediário",
    description: "Smokes posicionadas em superfícies elevadas (como caixas ou quinas) que cobrem a linha de visão do inimigo ao nível dos olhos dele, mas deixam os pés dele visíveis para você de longe, permitindo abates sem que ele consiga te ver.",
    howToApply: "Coloque a fumaça de forma que ela fique travada em uma quina de parede ou caixa alta. Afaste-se do pixel e olhe por baixo da fumaça para observar as pernas do inimigo avançando.",
    proTip: "Use de forma consistente em gargalos de entrada (choke points) como a Main da Ascent ou a B do Bind com controladores como Omen ou Cypher."
  },
  {
    id: "economy-buy",
    title: "Thrifty & Eco Management",
    alias: "Gestão Econômica",
    category: "economia",
    categoryLabel: "Gestão de Economia",
    difficulty: "Iniciante",
    description: "O controle rigoroso dos créditos da equipe. Dividido em: Full Buy (compra completa de rifles/escudo/utilitárias), Force Buy (comprar tudo o que puder mesmo sem dinheiro suficiente para rifles), Semi-Buy (compra parcial mantendo dinheiro para o próximo round) e Eco (gastar quase nada para economizar).",
    howToApply: "Abra o menu de compras (B) e observe o campo 'Compra Mínima Próx. Round'. Esse valor deve ser mantido acima de 3900 créditos para garantir que você compre Vandal/Phantom + Escudo Pesado no round seguinte.",
    proTip: "Nunca compre individualmente se sua equipe estiver fazendo Eco. Economizar juntos garante rounds armados com chance real de vitória."
  }
];

// --- CORE CLASS IMPLEMENTATION ---

export class SenseiTacticalSDK {
  private items: LibraryItem[];
  private config: SDKConfig;

  constructor(config: SDKConfig = {}) {
    this.items = [...DEFAULT_ITEMS];
    this.config = {
      language: 'pt-BR',
      ...config
    };
  }

  /**
   * Retorna todas as táticas cadastradas na biblioteca.
   */
  public getAll(): LibraryItem[] {
    return this.items;
  }

  /**
   * Busca uma tática específica pelo seu ID identificador único.
   */
  public getById(id: string): LibraryItem | undefined {
    return this.items.find(item => item.id === id);
  }

  /**
   * Filtra os itens por uma ou mais categorias táticas.
   */
  public getByCategory(category: TacticalCategory): LibraryItem[] {
    return this.items.filter(item => item.category === category);
  }

  /**
   * Filtra as táticas por complexidade / dificuldade.
   */
  public getByDifficulty(difficulty: TacticalDifficulty): LibraryItem[] {
    return this.items.filter(item => item.difficulty === difficulty);
  }

  /**
   * Motor de pesquisa inteligente. Busca correspondências no Título, Alias, 
   * Descrição ou Dicas, retornando os melhores resultados ordenados.
   */
  public search(query: string): LibraryItem[] {
    if (!query || query.trim() === '') {
      return this.items;
    }

    const cleanQuery = query.toLowerCase().trim();

    return this.items
      .map(item => {
        let score = 0;
        
        // Atribui relevâncias diferentes com base no campo encontrado
        if (item.title.toLowerCase() === cleanQuery) score += 100;
        else if (item.title.toLowerCase().includes(cleanQuery)) score += 40;
        
        if (item.alias.toLowerCase().includes(cleanQuery)) score += 30;
        if (item.description.toLowerCase().includes(cleanQuery)) score += 15;
        if (item.howToApply.toLowerCase().includes(cleanQuery)) score += 10;
        if (item.proTip.toLowerCase().includes(cleanQuery)) score += 5;

        return { item, score };
      })
      .filter(match => match.score > 0)
      .sort((a, b) => b.score - a.score)
      .map(match => match.item);
  }

  /**
   * Obtém apenas a Pro Tip (Dica de mestre) de uma tática por ID.
   */
  public getProTip(id: string): string | null {
    const item = this.getById(id);
    return item ? item.proTip : null;
  }

  /**
   * Retorna táticas recomendadas com base nas fraquezas informadas.
   * @param weaknesses Array de strings contendo as fraquezas detectadas.
   */
  public getRecommendedTactics(weaknesses: string[]): LibraryItem[] {
    const recommendations: LibraryItem[] = [];
    const weakString = weaknesses.join(" ").toLowerCase();

    // Mapeamentos semânticos inteligentes baseados nas fraquezas escritas pelo Coach
    if (weakString.includes("mira") || weakString.includes("precisão") || weakString.includes("headshot")) {
      recommendations.push(...this.getByCategory("mira"));
    }
    if (weakString.includes("posicionamento") || weakString.includes("morre") || weakString.includes("pixel")) {
      recommendations.push(...this.getByCategory("posicionamento"));
    }
    if (weakString.includes("economia") || weakString.includes("crédito") || weakString.includes("eco")) {
      recommendations.push(...this.getByCategory("economia"));
    }
    if (weakString.includes("utilitarias") || weakString.includes("smoke") || weakString.includes("flash")) {
      recommendations.push(...this.getByCategory("utilitarias"));
    }
    if (weakString.includes("game sense") || weakString.includes("decisão") || weakString.includes("clutch")) {
      recommendations.push(...this.getByCategory("gameSense"));
    }

    // Retorna únicos
    return Array.from(new Set(recommendations)).slice(0, 3);
  }
}
EXEMPLO DE USSO
import { SenseiTacticalSDK } from "./tactical-library-sdk";

// 1. Inicializa o SDK do Sensei
const sensei = new SenseiTacticalSDK();

// 2. Busca uma tática específica
const tacticalInfo = sensei.getById("counter-strafing");
console.log(`[${tacticalInfo?.difficulty}] ${tacticalInfo?.title} - Como fazer: ${tacticalInfo?.howToApply}`);

// 3. Realiza busca textual avançada
const searchResults = sensei.search("smoke");
console.log("Resultados da busca por 'smoke':", searchResults.map(item => item.title));

// 4. Gera recomendações táticas baseadas na análise de fraquezas de um jogador
const playerWeaknesses = ["Baixa taxa de headshot", "Gastando créditos incorretamente nos rounds de eco"];
const dynamicRecommendations = sensei.getRecommendedTactics(playerWeaknesses);

console.log("Táticas recomendadas para o seu treino:");
dynamicRecommendations.forEach(tactic => {
  console.log(`- ${tactic.title} (Categoria: ${tactic.categoryLabel})`);
});
