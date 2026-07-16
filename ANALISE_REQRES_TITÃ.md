# Documentação de Análise da API - ReqRes....

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
