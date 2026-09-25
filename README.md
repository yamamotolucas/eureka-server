<div align="center">

# 🧭 Eureka Discovery Server (`eureka-server`)

<p align="center">
  <b>Servidor central de Service Discovery e Registro de Instâncias do ecossistema Barbearia.</b>
</p>

<!-- Badges de Tecnologias -->
<p align="center">
  <img src="https://img.shields.io/badge/Java-17-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white" alt="Java 17" />
  <img src="https://img.shields.io/badge/Spring_Boot-4.0.5-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white" alt="Spring Boot 4" />
  <img src="https://img.shields.io/badge/Spring_Cloud-2025.1.1-6DB33F?style=for-the-badge&logo=spring&logoColor=white" alt="Spring Cloud" />
  <img src="https://img.shields.io/badge/Netflix_Eureka_Server-Spring_Cloud-brightgreen?style=for-the-badge&logo=spring&logoColor=white" alt="Eureka Server" />
</p>

</div>

---

## 📌 Visão Geral

O **`eureka-server`** é o serviço responsável pelo registro central e resolução de nomes de toda a arquitetura de microsserviços. Em vez de hardcodar IPs e portas fixas entre as aplicações, cada serviço (`api-gateway`, `identity-ms`, `booking-ms`) registra-se dinamicamente neste servidor durante o boot.

O serviço opera como o ponto focal de Service Discovery, permitindo que o **API Gateway** e as comunicações via **OpenFeign** realizem chamadas com balanceamento de carga no cliente (*Client-Side Load Balancing*) utilizando o protocolo `lb://`.

---

## ✨ Funcionalidades Principais

- 📍 **Service Registry Central:** Catálogo unificado com o endereço, IP e porta de cada nó ativo na rede.
- 💓 **Monitoramento de Heartbeats:** Rastreamento contínuo da disponibilidade dos serviços através de renovações periódicas.
- 🔀 **Resolução de Rotas Dinâmicas:** Resolução de instâncias para o `api-gateway` e clientes `feign-client`.
- 📊 **Dashboard Visual:** Interface web integrada para monitoramento de instâncias registradas, uso de memória e status geral.
- 🛡️ **Autonomia Operacional:** Configurado em modo *standalone* com auto-preservação desativada para respostas rápidas em ambiente local.

---

## 🏗️ Estrutura Arquitetural

O serviço adota uma estrutura limpa e minimalista dedicada exclusivamente à infraestrutura de descoberta:

```text
eureka-server/
├── src/
│   ├── main/
│   │   ├── java/br/com/eureka_server/
│   │   │   └── EurekaServerApplication.java   # Entrypoint anotado com @EnableEurekaServer
│   │   └── resources/
│   │       └── application.properties         # Configurações de porta e comportamento standalone
│   └── test/
│       └── java/br/com/eureka_server/         
│
└── pom.xml
```

---

## ⚙️ Variáveis de Ambiente Esperadas

As configurações principais gerenciadas no `application.properties` aceitam as seguintes variáveis de ambiente:

| Variável | Descrição | Valor Padrão / Exemplo |
| :--- | :--- | :--- |
| `SERVER_PORT` | Porta de execução do servidor Eureka | `8081` |
| `EUREKA_CLIENT_SERVICEURL_DEFAULTZONE` | URL da zona padrão para comunicação e clientes Eureka | `http://localhost:8081/eureka` |

---
## ⚠️ Observações de Execução no Ecossistema

> **Atenção:** Este microsserviço integra uma arquitetura distribuída. Para o seu funcionamento pleno (comunicação entre serviços, descoberta de rotas e persistência de dados), é indispensável que o **`eureka-server`**, uma instância ativa do **MySQL** e os demais microsserviços dependentes estejam em execução.
>
> Para executar ou clonar o ecossistema completo com todas as dependências e submódulos configurados, acesse o repositório central:  
> 🔗 [**barbearia-network-main**](https://github.com/yamamotolucas/barbearia-network-main)
