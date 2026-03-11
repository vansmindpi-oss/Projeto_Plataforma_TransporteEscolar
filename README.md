# Projeto_Plataforma_TransporteEscolar — VansMind (MVP)

## Objetivo
Documentar a estrutura técnica do MVP: módulos, entidades, permissões, regras e endpoints.

---

## Arquitetura (simples e viável para PI)
- Frontend: web/mobile-first (ex.: React)
- Backend: API (ex.: Node/Express ou FastAPI)
- Banco: PostgreSQL
- Autenticação: login simples + perfis (motorista/responsável/admin)

> MVP sem integrações externas obrigatórias.

---

## Módulos
### Motorista (principal)
- Rotas (CRUD)
- Vagas por rota
- Solicitações (aprovar/recusar)
- Lista do dia
- Check-in/out
- Avisos/ocorrências
- Histórico

### Responsável (mínimo)
- Buscar rota (por escola/bairro/turno)
- Solicitar vaga
- Acompanhar status + check-in/out (sem mapa)

### Admin (mínimo)
- Validar motorista/rota (simulado)
- Relatórios simples (atrasos/ocorrências)

---

## Modelo de dados (entidades)
- Driver (motorista)
- Vehicle (van)
- Route (rota)
- RouteStop (bairros/pontos simplificados)
- Request (solicitação de vaga)
- Student (mínimo/fictício)
- CheckEvent (CHECK_IN / CHECK_OUT)
- Notice (atraso/ocorrência)
- AuditLog (registro de ações)

---

## Permissões (regras)
- Motorista: gerencia apenas suas rotas e eventos
- Responsável: vê apenas registros do(s) aluno(s) associado(s)
- Admin: vê dados agregados e validações

---

## Endpoints (exemplo)
Auth:
- POST /auth/login

Rotas:
- GET /routes (filtros: escola, bairro, turno)
- POST /routes
- PUT /routes/:id
- DELETE /routes/:id

Solicitações:
- POST /requests
- GET /requests?driverId=
- PATCH /requests/:id (aprovar/recusar)

Eventos:
- POST /check-events (check-in/out)
- GET /history?routeId=&date=

Avisos:
- POST /notices
- GET /notices?routeId=&date=

Relatórios:
- GET /reports/summary?from=&to=

---

## Regras críticas (testes obrigatórios)
- não permitir check-out sem check-in
- impedir exceder capacidade de vagas
- garantir que o responsável só acesse o que é dele
- audit log para ações importantes (check-in/out, avisos)

---

## Requisitos não funcionais (MVP)
- UX rápida em celular
- feedback visual (sucesso/erro)
- dados mínimos (privacidade)
- logs básicos (auditoria)
