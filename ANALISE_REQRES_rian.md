LIBs, APIs e SDKs

LIB (Libraries)
A LIB, ou biblioteca, é um pedaço de código que executa uma tarefa específica. O código é baixado e colocado dentro de um projeto para não ter que começar do nada. O código principal do projeto é quem decide quando e como usar essa biblioteca. 

API (Application Programming Interface)
As APIs, ou interface de programação de aplicações, são responsáveis por fazer que dois sistemas diferentes conversem e troquem dados. Elas fornecem uma interface para acessar recursos característicos de uma plataforma. A API é desenvolvida para que um sistema possa usar as funcionalidades de um outro sistema. Um sistema se comunica com outro sistema compartilhando suas ações, ferramentas, padrões e protocolos, gerando uma conversa de sistema para sistema. 

SDK (Software Development Kit)
O SDK, ou pacote de desenvolvimento de software, é um conjunto de ferramentas e bibliotecas disponibilizados por algum fornecedor para criar softwares em uma plataforma específica. O SDK dá a infraestrutura completa para criar um software, e pode incluir LIBs, APIs e ferramentas.

===

LIB: Registro Imutável de Eventos

const crypto = require('crypto');

/**
 * Biblioteca: Registro Imutável de Eventos (Web3 SDK)
 * Propósito: Capturar logs, gerar provas criptográficas e simular o agrupamento on-chain.
 */
class ImmutableLogLib {
    constructor() {
        this.pendingLogs = []; // Buffer de eventos off-chain
        this.onChainSimulatedLedger = []; // Simulação do Smart Contract (Blockchain)
    }

    /**
     * Motor de Hashing Interno
     * Gera uma "impressão digital" (SHA-256) única para os dados.
     */
    _generateHash(data) {
        // Converte o objeto para string de forma determinística e gera o hash
        const dataString = JSON.stringify(data);
        return crypto.createHash('sha256').update(dataString).digest('hex');
    }

    /**
     * Passo 1: Captura do Evento (Off-chain)
     * Registra o evento, carimba o tempo e gera a assinatura matemática.
     * @param {Object} eventData - Os dados críticos do log.
     * @param {String} priority - 'HIGH', 'MEDIUM', 'LOW' (Filtro de Importância)
     */
    captureEvent(eventData, priority = 'MEDIUM') {
        const payload = {
            ...eventData,
            timestamp: new Date().toISOString()
        };
        
        const hash = this._generateHash(payload);
        const logEntry = { payload, hash, priority };
        
        this.pendingLogs.push(logEntry);
        
        return {
            status: "Evento capturado off-chain",
            hashGerado: hash,
            dados: payload
        };
    }

    /**
     * Passo 2: O Agrupamento (Batching) para Redução de Custos
     * Pega todos os logs pendentes e gera uma Raiz Mestra (simulando Merkle Root)
     * para enviar à Blockchain pagando apenas 1 taxa de rede.
     */
    commitBatchToBlockchain() {
        if (this.pendingLogs.length === 0) {
            return { status: "Nenhum evento pendente para registro." };
        }

        // Agrupa todos os hashes pendentes em uma única string
        const allPendingHashes = this.pendingLogs.map(log => log.hash).join('');
        
        // Gera o Hash Mestre (Merkle Root simplificada)
        const masterHash = this._generateHash(allPendingHashes);
        
        // Simula o registro na Blockchain (On-chain)
        const transactionReceipt = {
            txId: '0x' + crypto.randomBytes(16).toString('hex'),
            masterHash: masterHash,
            logsCount: this.pendingLogs.length,
            timestamp: new Date().toISOString()
        };

        this.onChainSimulatedLedger.push(transactionReceipt);
        this.pendingLogs = []; // Limpa o buffer após o registro bem-sucedido
        
        return {
            status: "Lote registrado na Blockchain com sucesso!",
            recibo: transactionReceipt
        };
    }

    /**
     * Passo 3: O Portal de Verificação ("Não Confie, Verifique")
     * Valida se um dado específico corresponde ao hash guardado.
     * @param {Object} originalPayload - O dado que o auditor está verificando.
     * @param {String} expectedHash - O hash original gerado no momento do evento.
     */
    verifyIntegrity(originalPayload, expectedHash) {
        const testHash = this._generateHash(originalPayload);
        const isValid = testHash === expectedHash;

        return {
            isValid: isValid,
            message: isValid 
                ? "SUCESSO: Prova de integridade válida. O dado não foi alterado."
                : "ALERTA: Integridade corrompida. O dado foi modificado."
        };
    }
}

module.exports = ImmutableLogLib;

===

ANALISE_REQRES_Rian

* **Verbo HTTP:** [Ex: GET, POST, PUT, DELETE]
* **URL Completa:** [Cole a URL testada aqui]
* **Body da Requisição:** [Teve que enviar algum JSON? Se não, escreva "Nenhum"]
* **Status Code Esperado:** [Ex: 200 OK, 201 Created, 404 Not Found]
* **Resposta da API (Exemplo do JSON):**

Cenário A: Buscar a lista de utilizadores da página 2
GET
https://reqres.in/api/users?page=2
Nenhum 
200 ok

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
        },
        {
            "id": 8,
            "email": "lindsay.ferguson@reqres.in",
            "first_name": "Lindsay",
            "last_name": "Ferguson",
            "avatar": "https://reqres.in/img/faces/8-image.jpg"
        },
        {
            "id": 9,
            "email": "tobias.funke@reqres.in",
            "first_name": "Tobias",
            "last_name": "Funke",
            "avatar": "https://reqres.in/img/faces/9-image.jpg"
        },
        {
            "id": 10,
            "email": "byron.fields@reqres.in",
            "first_name": "Byron",
            "last_name": "Fields",
            "avatar": "https://reqres.in/img/faces/10-image.jpg"
        },
        {
            "id": 11,
            "email": "george.edwards@reqres.in",
            "first_name": "George",
            "last_name": "Edwards",
            "avatar": "https://reqres.in/img/faces/11-image.jpg"
        },
        {
            "id": 12,
            "email": "rachel.howell@reqres.in",
            "first_name": "Rachel",
            "last_name": "Howell",
            "avatar": "https://reqres.in/img/faces/12-image.jpg"
        }
    ],
    "support": {
        "url": "https://benhowdle.im/first-cto-playbook?utm_source=reqres&utm_medium=json&utm_campaign=referral",
        "text": "Become a better CTO. A playbook of painful stories and practical advice from a two-time startup CTO."
    },
    "_meta": {
        "powered_by": "ReqRes",
        "docs_url": "https://app.reqres.in/documentation",
        "upgrade_url": "https://app.reqres.in/upgrade",
        "example_url": "https://app.reqres.in/examples/notes-app",
        "variant": "v1_a",
        "message": "Your data persists here. Add auth, logs, and custom schemas to build a real backend.",
        "cta": {
            "label": "See example app",
            "url": "https://app.reqres.in/examples/notes-app"
        },
        "context": "legacy_success"
    }
}

Cenário B Criar Novo Usuário

POST
https://reqres.in/api/users
JSON {
    "name": "Rian",
    "job": "Advogado"
}
201 Created

{
    "name": "Rian",
    "job": "Advogado",
    "id": "847",
    "createdAt": "2026-07-03T23:35:22.901Z",
    "_meta": {
        "powered_by": "ReqRes",
        "docs_url": "https://app.reqres.in/documentation",
        "upgrade_url": "https://app.reqres.in/upgrade",
        "example_url": "https://app.reqres.in/examples/notes-app",
        "variant": "v1_a",
        "message": "Your data persists here. Add auth, logs, and custom schemas to build a real backend.",
        "cta": {
            "label": "See example app",
            "url": "https://app.reqres.in/examples/notes-app"
        },
        "context": "legacy_success"
    }
}

Cenário C: Tentar procurar um utilizador que não existe (ex: utilizador com ID 23) e capturar o
erro devolvido pela API.

GET
https://reqres.in/api/users/123
Nenhum
404 Not Found

{}
