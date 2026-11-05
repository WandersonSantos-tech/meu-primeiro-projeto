# Aula 10 — JWT + ViaCEP

## Como executar

Use Node.js 18 ou superior (recomendado Node 22).

```bash
cd api
npm install
node src/database/seed.js
npm run dev
```

O arquivo `.env` já está configurado para testes locais e é ignorado pelo Git. **Em produção, altere o JWT_SECRET.**

## Testes no Postman

1. `POST http://localhost:3001/api/auth/login` com JSON `{ "email": "contato@technova.com", "senha": "123456" }` → 200 + token (válido por 8h).
2. `POST http://localhost:3001/api/vagas` sem token → 401.
3. `POST http://localhost:3001/api/vagas` com `Authorization: Bearer SEU_TOKEN` e JSON `{ "titulo": "Vaga Autenticada", "tipo": "remoto", "tecnologias": "Node" }` → 201.
4. `DELETE http://localhost:3001/api/vagas/ID` com token da empresa proprietária → 204.
5. `GET http://localhost:3001/api/cep/01310100` → endereço da Avenida Paulista, São Paulo/SP.
6. `GET http://localhost:3001/api/cep/00000000` → 404.
7. `GET http://localhost:3001/api/cep/123` → 400.

As rotas GET de vagas continuam públicas. O POST usa o ID da empresa do token, ignorando `empresa_id` no corpo. O DELETE só permite excluir vagas da própria empresa. O PUT permanece conforme a Aula 09 (sem autenticação), pois o enunciado exige proteger POST e DELETE.
