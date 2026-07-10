Documentação de Análise da API - ReqRes
Feito por: João

Cenário A: Ver a lista de utilizadores da página 2

Verbo HTTP usado: GET
Link (URL) que testei: https://reqres.in/api/users?page=2
Corpo (Body) enviado: Nenhum. Como era só para ler a lista, não precisei enviar nenhuma informação em JSON para o servidor.
Status Code esperado: 200 OK (deu tudo certo!)
Resposta que recebi da API:

(Nota: Colei aqui só o primeiro utilizador para o texto não ficar gigante, mas quando cliquei no botão, a API me devolveu os 6 utilizadores dessa página certinho).

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
]
}

Cenário B: Criar um utilizador novo com o meu nome

Verbo HTTP usado: POST (mudei o verbo porque agora a ideia era eu enviar os meus dados para lá).
Link (URL) que testei: https://reqres.in/api/users
Corpo (Body) enviado: Sim. Dessa vez escrevi os meus dados num JSON e enviei assim:
{
"name": "João",
"job": "Desenvolvedor Front-end"
}
Status Code esperado: 201 Created (que significa que o perfil foi criado com sucesso).
Resposta que recebi da API:

(Nota: A API não só confirmou os dados que enviei, mas também já gerou um ID e a data de criação).

{
"name": "João",
"job": "Desenvolvedor Front-end",
"id": "789",
"createdAt": "2026-07-03T10:15:30.000Z"
}

Cenário C: Procurar um utilizador que não existe

Verbo HTTP usado: GET (voltei para o GET porque era só uma tentativa de busca).
Link (URL) que testei: https://reqres.in/api/users/23
Corpo (Body) enviado: Nenhum.
Status Code esperado: 404 Not Found (Deu erro de propósito! Como o utilizador 23 não existe no banco deles, esse é o erro certo).
Resposta que recebi da API:

(Nota: O sistema me respondeu com isso vazio, o que faz sentido já que não encontrou nada).

{}
______________________________________________________________________________________________________________________________________________________________________________________________________________
Aula 2

# Pesquisa Técnica: Diferenças entre API, SDK e Biblioteca (Lib)
Estudo de Caso Aplicado: Ecossistema Aurora Cycle

Para compreender como o aplicativo de saúde feminina Aurora Cycle funciona no nível da engenharia de software, é fundamental diferenciar três pilares de integração tecnológica: Bibliotecas (Libs), SDKs (Software Development Kits) e APIs (Application Programming Interfaces). Embora operem de forma integrada, eles pertencem a camadas totalmente diferentes.

---

## 1. Biblioteca (Library / Lib)

Uma biblioteca é um conjunto de códigos, funções ou classes pré-escritas que os desenvolvedores importam para resolver um problema específico e isolado. Ela não dita a estrutura do projeto; o desenvolvedor detém o controle e a chama apenas quando necessário.

Como analogia prática, imagine uma ferramenta específica dentro de uma maleta, como uma chave de fenda.



### Aplicação no Aurora Cycle

No Frontend Web: Na nossa Landing Page, os scripts gráficos em WebGL que geram o efeito visual de aurora boreal na tela atuam como uma biblioteca isolada de renderização.

No Aplicativo Mobile: No app em Flutter, utilizamos bibliotecas específicas como o share_plus (utilizado unicamente para abrir a folha de compartilhamento nativa do sistema operacional ao exportar o histórico em CSV) e pacotes de criptografia específicos para realizar o hash de chaves de segurança.

---

## 2. SDK (Software Development Kit)

Um SDK é um Kit de Desenvolvimento de Software completo. É um pacote robusto e abrangente que inclui documentação, compiladores, emuladores, guias de estilo e, na maioria das vezes, uma coleção de várias bibliotecas e APIs integradas. O SDK dita o ecossistema e as regras sob as quais o software será construído.

Como analogia prática, funciona como uma oficina mecânica de fábrica inteira, com todas as ferramentas e o manual de engenharia da montadora inclusos.



### Aplicação no Aurora Cycle

O Aurora Cycle é inteiramente desenvolvido utilizando o Flutter SDK. Não usamos o Flutter apenas para uma função isolada; o SDK dele controla todo o ciclo de vida do software, dita a arquitetura de gerenciamento de estado, renderiza as interfaces a 60fps constantes por meio do motor gráfico Impeller e compila o código-fonte nativo para as plataformas Android e iOS.

---

## 3. API (Application Programming Interface)

Uma API é uma interface ou contrato de comunicação. Ela estabelece uma ponte para que dois softwares, ou partes distintas de um mesmo sistema, conversem entre si de forma padronizada. A API define quais dados podem ser solicitados e quais serão devolvidos, omitindo a complexidade interna de como o tratamento foi feito.

Como analogia prática, pense no garçom de um restaurante. Você escolhe o pedido no menu (requisição), o garçom leva o pedido à cozinha (API) e traz o prato pronto (resposta) sem que você precise saber como o chef preparou a comida.



### Aplicação no Aurora Cycle

Como o Aurora Cycle foi concebido sob a premissa de Zero Backend / Zero Cloud, nossa arquitetura rejeita APIs web tradicionais (como endpoints REST externos) para mitigar o risco de vazamento de dados. Em vez disso, consumimos APIs locais e nativas do hardware:

Local Authentication API (Biometria): O app solicita ao sistema operacional (iOS/Android) que valide a identidade da usuária. O hardware de segurança executa a checagem e retorna a resposta via API local (true para sucesso ou false para falha).

Drift / SQLCipher API: O núcleo do aplicativo se comunica com a camada de dados através das APIs de consulta do banco criptografado local, processando dados sensíveis diretamente no chip do dispositivo.

---

## Resumo das Diferenças

Em relação ao escopo, a biblioteca possui foco estrito em solucionar uma única microtarefa, enquanto o SDK oferece um ecossistema completo de desenvolvimento e a API atua como o meio de comunicação e contrato entre sistemas.

No quesito controle, você gerencia a biblioteca e decide quando invocá-la. Por outro lado, o SDK dita o padrão que seu código deve seguir, e a API determina o formato exato das requisições e respostas.

No contexto prático do projeto, as bibliotecas controlam o efeito WebGL e pacotes de animação, o SDK do Flutter estrutura e compila o aplicativo, e as APIs do sistema tratam as requisições locais de biometria e o banco SQLCipher.
