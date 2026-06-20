# DSMeta

Sistema de relatório de vendas com notificação por SMS, desenvolvido durante o curso **Semana Spring React**, da escola [DevSuperior](https://github.com/devsuperior), ministrado pelo professor [Nélio Alves](https://github.com/nelioalves) (UFU).

## Sobre o projeto

O DSMeta é uma aplicação para acompanhamento de desempenho de vendas, com um diferencial em relação aos demais projetos da mesma linha: a integração com a API de SMS da [Twilio](https://www.twilio.com/), usada para enviar ao vendedor uma notificação com os dados de uma venda (nome do vendedor, valor vendido e data).

### Modelo de domínio

- **Sale** (`tb_sales`) — `seller_name`, `visited` (visitas realizadas), `deals` (negócios fechados), `amount` (valor vendido), `date`

## Arquitetura

O backend segue a arquitetura em camadas padrão dos projetos da DevSuperior:

- **Repository** — acesso a dados via Spring Data JPA.
- **Service** — regras de negócio, incluindo o envio de notificações via Twilio.
- **Controller** — endpoints REST, comunicação via DTO em JSON.
- **Config** — configuração de segurança HTTP (`HttpSecurity`) e CORS.

```
Frontend (React + TypeScript) → Controller (REST/JSON) → Service → Repository (JPA) → Banco de dados
                                        ↑                      ↓
                                  Config (Security + CORS)   Twilio (SMS)
```

## Integração com Twilio

O backend utiliza o SDK oficial da Twilio para envio de SMS:

```xml
<dependency>
    <groupId>com.twilio.sdk</groupId>
    <artifactId>twilio</artifactId>
    <version>8.31.1</version>
</dependency>
```

As credenciais da Twilio (SID, token, números de telefone) são configuradas via variáveis de ambiente, mantendo dados sensíveis fora do código-fonte.

## Tecnologias

**Backend**
- Java
- Spring Boot
- Spring Data JPA
- Maven
- Twilio SDK (envio de SMS)

**Frontend**
- React
- TypeScript
- Vite
- React Datepicker
- React Toastify (notificações)
- Axios

## Conceitos aplicados

- Arquitetura em camadas (Controller / Service / Repository)
- Padrão DTO
- Configuração de segurança HTTP e CORS
- Integração com API externa (Twilio)
- Variáveis de ambiente para credenciais sensíveis

## Como executar

### Backend
```bash
cd backend
./mvnw spring-boot:run
```

> É necessário configurar as credenciais da Twilio (`TWILIO_SID`, `TWILIO_KEY`, etc.) como variáveis de ambiente para que o envio de SMS funcione. Sem essas credenciais, o restante da aplicação ainda funciona normalmente.

### Frontend
```bash
cd frontend
npm install
npm run dev
```

## Contexto

Este projeto foi desenvolvido durante minha jornada de transição de carreira da fisioterapia para o desenvolvimento de software, como parte da formação prática oferecida pela DevSuperior.
