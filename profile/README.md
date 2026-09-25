# RH Connect

Plataforma web responsiva para preparação de candidatos para entrevistas de emprego, desenvolvida como projeto acadêmico no SENAC-DF.

O projeto reúne um **Front-end React/Vite**, uma **API NestJS com PostgreSQL/Prisma** e um **serviço Python/Flask para processamento de entrevistas com IA**.

> Este README apresenta uma visão geral do projeto. Detalhes técnicos aprofundados, gaps de segurança e roadmap interno estão documentados separadamente para a equipe do projeto.

---

## 1. Visão geral

O RH Connect tem como objetivo oferecer um ambiente de preparação para entrevistas, permitindo que candidatos pratiquem respostas, recebam avaliação e acompanhem seu desenvolvimento.

O projeto está **em desenvolvimento ativo**, como parte de um trabalho acadêmico. Partes do sistema já possuem integração real entre Front-end, Back-end e serviço de IA; outras áreas ainda estão em evolução e não devem ser consideradas produção-ready.

---

## 2. Arquitetura

O sistema é organizado em três camadas principais:

```text
                         RH CONNECT
                             │
              ┌──────────────┴──────────────┐
              │                             │
         Front-end                       Back-end
        React + Vite                   NestJS + Prisma
              │                             │
              │                         PostgreSQL
              │                             │
              │                 ┌───────────┴───────────┐
              │                 │                       │
              │              Auth/API              Serviço de IA
              │                                         │
              │                                      Flask
              │                                         │
              │                              Parser de vaga + Groq
              │
              └────────────── HTTP ────────────────────┘
```

**Front-end** — interface do candidato, avaliador e administrador, com navegação por rotas e fluxos de entrevista.

**Back-end** — API HTTP em NestJS, responsável por autenticação, persistência e orquestração da comunicação com o serviço de IA.

**Serviço de IA** — API Flask independente para extração de contexto de vagas, geração de perguntas e avaliação de respostas, acessível apenas através do Back-end NestJS.

---

## 3. Stack principal

### Front-end
React 18 · Vite 6 · TypeScript · React Router 7 · Tailwind CSS 4 · Radix UI · Material UI · React Hook Form · Recharts

### Back-end
Node.js · NestJS 11 · TypeScript · Prisma 6 · PostgreSQL · Passport/JWT · Swagger/OpenAPI · Jest

### IA
Python · Flask · Groq · serviço próprio de parsing de vagas

### Ferramentas do projeto
pnpm · Git/GitHub · GitHub Actions

---

## 4. Perfis de acesso

O sistema possui três perfis principais:

- **Candidato** — cadastro, onboarding, criação e acompanhamento de entrevistas, materiais de desenvolvimento e relatórios.
- **Avaliador** — convite e ativação por administrador, fila e revisão de entrevistas.
- **Administrador** — gestão de candidatos, avaliadores, entrevistas, atribuições, critérios e configurações.

Algumas dessas áreas ainda estão em fase de integração com o Back-end e não representam necessariamente uma camada totalmente persistida.

---

## 5. Fluxo de entrevista

```text
Nova entrevista
↓
URL/contexto da vaga
↓
Consentimento
↓
Escolha do modo de avaliação
↓
Preparação
↓
Perguntas e respostas
↓
Revisão
↓
Envio
↓
Resultado/status/relatório
```

A geração de perguntas e a avaliação por IA já possuem integração real com o serviço Python/Groq. Outras etapas do fluxo (avaliação humana, atribuições, relatórios) ainda estão em desenvolvimento.

---

## 6. Integração com a Cachola

O projeto possui integração com recursos externos de aprendizagem, com catálogo persistido no Back-end e consumido pelo Front-end.

---

## 7. Estrutura do repositório

```text
rh-connect/
├── apps/
│   ├── web/                         # Front-end React/Vite
│   └── api/                         # Back-end NestJS
│       └── prisma/                  # Schema, migrations e seeds
│
├── services/
│   └── interview-ai-python/         # Serviço Flask + parser + Groq
│
├── packages/
│   ├── config/
│   ├── types/
│   ├── ui/
│   └── validation/
│
├── docs/
├── guidelines/
├── .github/workflows/
├── package.json
├── pnpm-workspace.yaml
└── README.md
```

---

## 8. Requisitos locais

- Node.js compatível com o ambiente do projeto;
- pnpm;
- PostgreSQL;
- Python para o serviço de IA;
- uma chave própria da API Groq para executar a avaliação/geração por IA (não incluída no repositório).

A configuração exata de cada serviço é feita através dos arquivos `.env.example` correspondentes, que **não contêm valores reais** — apenas os nomes das variáveis esperadas.

