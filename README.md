# 🏦 Vex Pay (Fintech Simulation)
# ⚠️ Projeto em construção conforme andamento dos estudos.


Projeto de estudo avançado simulando a arquitetura de uma plataforma de processamento de pagamentos moderna, inspirada em sistemas utilizados por fintechs e bancos digitais.

O objetivo deste projeto é aprofundar conhecimentos em:

- Arquitetura distribuída
- Event-Driven Architecture
- Apache Kafka
- Consistência eventual
- Idempotência
- Double Entry Accounting (Ledger contábil)
- Padrões como Outbox e SAGA
- Concorrência e integridade financeira
- Resiliência e reprocessamento de eventos

---

# 🎯 Objetivo do Projeto

Simular um ecossistema de processamento de pagamentos contendo:

- Recebimento de transações
- Análise antifraude
- Escrituração contábil (Ledger imutável)
- Liquidação financeira (Settlement)
- Comunicação assíncrona entre serviços via Kafka
- Garantias de idempotência e integridade de dados

Este projeto não tem finalidade comercial, sendo exclusivamente voltado para meu (Jonathan) estudo de arquitetura backend de alto nível.

---

# 🧱 Arquitetura

A aplicação segue o modelo de microserviços com comunicação orientada a eventos.

## Serviços

- **payment-service**
    - Recebe requisições de pagamento
    - Aplica idempotência
    - Publica eventos via Outbox Pattern

- **antifraud-service**
    - Consome eventos de pagamento
    - Executa regras de risco
    - Publica aprovação ou rejeição

- **ledger-service**
    - Responsável pelo registro contábil
    - Implementa modelo Double Entry
    - Nunca altera saldo diretamente

- **settlement-service**
    - Simula liquidação financeira (D+X)
    - Atualiza disponibilidade de valores

---

# 🔄 Fluxo Simplificado

1. Cliente cria pagamento
2. Evento `payment.requested` é publicado
3. Antifraude decide aprovação ou rejeição
4. Ledger cria lançamentos contábeis
5. Settlement agenda liquidação futura

Tudo ocorre de forma assíncrona via Kafka.

---

# 🛠️ Stack Tecnológica

- Java 25
- Spring Boot 4
- Spring Kafka
- PostgreSQL
- Redis
- Docker Compose
- Flyway
- Testcontainers
- k6 (teste de carga)

---

# 🐳 Infraestrutura Local

A pasta `infra/` contém:

- Docker Compose com:
    - Kafka
    - PostgreSQL
    - Redis
- Configuração para múltiplos bancos (um por serviço)

Para subir o ambiente:

```bash
cd infra
docker compose up -d
```

# ⚠️ Projeto em construção conforme andamento dos estudos.