# Projeto Docker - Lista de Tarefas

## Integrantes do Grupo

* **Carlos Eduardo Barbosa** — RA: **2411335**
* **Gustavo Alves de Morais Souza** — RA: **2411264**
* **Gabriel Lucas Modesto Rodrigues** — RA: **2120900**
* **Wagdo Braga Gomes Junior** — RA: **2411093**
* **Aliny de Jesus Costa** — RA: **2421298**

---

## Objetivo do Projeto

Este projeto tem como objetivo aplicar conceitos de **Arquitetura de Sistemas Distribuídos** por meio da **conteinerização de aplicações utilizando Docker**.

A aplicação foi dividida em três serviços independentes:

* **Frontend** → Interface da aplicação
* **Backend** → API responsável pela lógica de negócio
* **Banco de Dados PostgreSQL** → Persistência dos dados

Todos os serviços se comunicam através de uma **rede Docker customizada**, permitindo isolamento, escalabilidade e comunicação entre containers.

---

## Tecnologias Utilizadas

* **Docker**
* **Node.js**
* **Express**
* **React**
* **Vite**
* **PostgreSQL**
* **Nginx**

---

## Estrutura do Projeto

```text
tarefas-docker-main/
│
├── backend/
│   ├── Dockerfile
│   ├── package.json
│   ├── package-lock.json
│   ├── .env
│   └── src/
│
├── frontend/
│   ├── Dockerfile
│   ├── package.json
│   ├── package-lock.json
│   ├── public/
│   └── src/
│
└── README.md
```

---

## Criação da Rede Docker

Criar a rede customizada:

```bash
docker network create tarefas-net
```

---

## Build das Imagens

### Backend

```bash
cd backend
docker build -t backend-image .
```

### Frontend

```bash
cd ../frontend
docker build -t frontend-image .
```

---

## Execução do Banco de Dados (PostgreSQL)

```bash
docker run -d --name postgres --network tarefas-net -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -e POSTGRES_DB=tarefasdb -p 5432:5432 postgres
```

Container criado:

**Nome:** `postgres`

---

## Execução do Backend

Entrar na pasta backend:

```bash
cd backend
```

Executar:

```bash
docker run -d --name backend --network tarefas-net -p 3001:3001 --env-file .env backend-image
```

Container criado:

**Nome:** `backend`

---

## Execução do Frontend

Entrar na pasta frontend:

```bash
cd frontend
```

Executar:

```bash
docker run -d --name frontend --network tarefas-net -p 3000:80 frontend-image
```

Container criado:

**Nome:** `frontend`

---

## Containers Utilizados

| Serviço    | Nome do Container | Porta |
| ---------- | ----------------- | ----- |
| Frontend   | frontend          | 3000  |
| Backend    | backend           | 3001  |
| PostgreSQL | postgres          | 5432  |

---

## Acesso ao Sistema

Frontend:

```text
http://localhost:3000
```

Backend:

```text
http://localhost:3001
```

---

## Resultado

O projeto foi conteinerizado com sucesso, atendendo aos seguintes requisitos:

✅ Dockerfile funcional para Backend
✅ Dockerfile funcional para Frontend
✅ Container PostgreSQL configurado
✅ Rede Docker customizada criada
✅ Comunicação entre serviços funcionando corretamente
✅ Documentação completa de execução
