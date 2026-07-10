# Documentação de Análise da API - ReqRes

## 1. Cenário A: Listar Utilizadores da Página 2
* **Verbo HTTP:** GET
* **URL Completa:** https://reqres.in/api/users?page=2
* **Body da Requisição:** Nenhum
* **Status Code Esperado:** 200 OK
* **Resposta da API (Exemplo do JSON):**
```json
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
            "avatar": "[https://reqres.in/img/faces/7-image.jpg](https://reqres.in/img/faces/7-image.jpg)"
        },
        {
            "id": 8,
            "email": "lindsay.ferguson@reqres.in",
            "first_name": "Lindsay",
            "last_name": "Ferguson",
            "avatar": "[https://reqres.in/img/faces/8-image.jpg](https://reqres.in/img/faces/8-image.jpg)"
        }
    ],
    "support": {
        "url": "[https://reqres.in/#support-heading](https://reqres.in/#support-heading)",
        "text": "To keep ReqRes free, contributions towards server costs are appreciated!"
    }
# Pesquisa: Diferença entre API, LIB e SDK

Embora esses três termos sejam fundamentais no desenvolvimento de software e frequentemente usados juntos, eles representam conceitos e escopos completamente diferentes. A principal diferença reside no **tamanho (escopo)** e na **função** que cada um exerce no ecossistema de desenvolvimento.

---

## 1. API (Application Programming Interface)
Uma API (Interface de Programação de Aplicações) é um conjunto de regras, protocolos e definições que permite que duas aplicações de software diferentes se comuniquem entre si. 

* **O que é:** É o "mensageiro" ou o "contrato". Ela não é a implementação do código em si, mas sim a definição de como você pode interagir com esse código.
* **Como funciona:** Você (o desenvolvedor) envia uma requisição estruturada de uma forma específica, e a API devolve uma resposta (geralmente em JSON ou XML) sem que você precise saber como o sistema processou essa informação.
* **Controle:** O sistema remoto dita as regras. Se você não enviar a requisição exatamente como a API exige, ela falha.
* **Exemplos:** ReqRes, Google Maps API, Stripe API.

## 2. LIB (Library / Biblioteca)
Uma Biblioteca é uma coleção de código pré-escrito e reutilizável que os desenvolvedores podem importar para seus próprios projetos para realizar tarefas específicas e comuns, evitando "reinventar a roda".

* **O que é:** É um conjunto de funções e blocos de código focados em resolver um problema específico (como fazer cálculos matemáticos, manipular datas ou criar interfaces visuais).
* **Como funciona:** O seu código "chama" a biblioteca quando precisa dela. 
* **Controle:** **Você está no controle.** Você decide quando, onde e como vai usar os recursos da biblioteca dentro do fluxo do seu programa.
* **Exemplos:** React (interfaces), Axios (requisições HTTP), NumPy (matemática em Python).

## 3. SDK (Software Development Kit)
Um SDK (Kit de Desenvolvimento de Software) é uma caixa de ferramentas completa fornecida por um fabricante de plataforma para permitir que você crie aplicativos especificamente para aquele ambiente.

* **O que é:** É o pacote mais abrangente de todos. Um SDK geralmente **contém** bibliotecas (LIBs) e APIs, mas vai muito além, incluindo compiladores, depuradores (debuggers), documentação e exemplos de código.
* **Como funciona:** Ele fornece tudo o que você precisa para começar e terminar um projeto para uma plataforma específica.
* **Controle:** Ele define as ferramentas base que você vai usar para construir a aplicação inteira.
* **Exemplos:** Android SDK (apps Android), iOS SDK (apps Apple), AWS SDK (serviços Amazon).

---

## O Resumo das Diferenças

Um não substitui o outro; eles se complementam. 

| Característica | API | LIB (Biblioteca) | SDK |
| :--- | :--- | :--- | :--- |
| **Definição Base** | Ponte de comunicação entre sistemas. | Código pré-escrito para funções específicas. | Kit completo de ferramentas para criar software. |
| **O que contém?** | Regras, rotas e protocolos. | Classes, métodos e funções prontas para uso. | APIs, Bibliotecas, compiladores e documentação. |
| **Quem chama quem?** | Seu código faz uma requisição para a API. | Seu código chama as funções da Biblioteca. | Você usa o SDK para construir o seu código. |
| **Nível de Escopo** | Específico (Comunicação). | Específico (Execução de tarefa). | Amplo (Construção completa). |

---

# Exemplo Prático: Criando uma Biblioteca (LIB)

Para demonstrar o conceito de uma LIB na prática, criamos a `coffin-clock-js`. É uma biblioteca JavaScript leve desenvolvida especificamente para o projeto [Coffin Clock](https://coffin-clock-project-0.vercel.app/), focada em gerenciar contagens regressivas e manipulação de temas sombrios.

## 1. O Código da Biblioteca (`coffin-clock-js.js`)

Este é o arquivo da biblioteca. Ele contém a lógica pesada que foi abstraída para facilitar o uso.

```javascript
/**
 * ⚰️ Coffin Clock Library
 * Biblioteca leve para gerenciamento de tempo de vida e contagem regressiva.
 */

export class CoffinTimer {
  constructor({ targetDate, onTick, onTimeUp }) {
    this.targetDate = new Date(targetDate).getTime();
    this.onTick = onTick;
    this.onTimeUp = onTimeUp;
    this.intervalId = null;
    this.timeModifier = 0; // Para adicionar ou subtrair tempo dinamicamente
  }

  _calculateTimeLeft() {
    const now = new Date().getTime();
    const distance = (this.targetDate + this.timeModifier) - now;

    if (distance <= 0) {
      return null;
    }

    return {
      days: Math.floor(distance / (1000 * 60 * 60 * 24)),
      hours: Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)),
      minutes: Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60)),
      seconds: Math.floor((distance % (1000 * 60)) / 1000),
      totalDistance: distance
    };
  }

  start() {
    if (this.intervalId) return; // Evita múltiplos intervalos

    this.intervalId = setInterval(() => {
      const timeLeft = this._calculateTimeLeft();

      if (!timeLeft) {
        this.stop();
        if (this.onTimeUp) this.onTimeUp();
      } else {
        if (this.onTick) this.onTick(timeLeft);
      }
    }, 1000);
  }

  stop() {
    clearInterval(this.intervalId);
    this.intervalId = null;
  }

  addTime(seconds) {
    this.timeModifier += seconds * 1000;
  }

  subtractTime(seconds) {
    this.timeModifier -= seconds * 1000;
  }
}

export const TimeFormatter = {
  toDigitalClock(timeLeft) {
    if (!timeLeft) return "00:00:00:00";
    
    const pad = (num) => String(num).padStart(2, '0');
    return `${pad(timeLeft.days)}:${pad(timeLeft.hours)}:${pad(timeLeft.minutes)}:${pad(timeLeft.seconds)}`;
  },

  getLifePercentage(startDateStr, targetDateStr) {
    const start = new Date(startDateStr).getTime();
    const end = new Date(targetDateStr).getTime();
    const now = new Date().getTime();

    if (now >= end) return 100;
    if (now <= start) return 0;

    const totalDuration = end - start;
    const timePassed = now - start;

    return ((timePassed / totalDuration) * 100).toFixed(2);
  }
};

export const ThemeManager = {
  setTheme(themeName) {
    const root = document.documentElement;
    if (themeName === 'dark-abyss') {
      root.style.setProperty('--bg-color', '#0a0a0a');
      root.style.setProperty('--text-color', '#d3d3d3');
      root.style.setProperty('--font-family', '"Courier New", Courier, monospace');
    }
  },

  setHighlightColor(hexColor) {
    document.documentElement.style.setProperty('--highlight-color', hexColor);
  }
};
}
