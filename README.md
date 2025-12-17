# 🧬 Projeto VekRest

O Projeto VekRest foi desenvolvido em 4 módulos, com o objetivo de aplicar tecnologias e padrões de desenvolvimento modernos em um projeto robusto e inter conectado, utilizando Clean Architecture e padrões SOLID.

## 🧩 MÓDULOS DO PROJETO (4 Módulos e 7 Aplicações)
| Aplicação      | Descrição                                          | Módulo | Link                                                                                                 |
|----------------|----------------------------------------------------|--------|------------------------------------------------------------------------------------------------------|
| VekClient      | Aplicação de CRUD de Pessoa                        | 1      | [Repositório VekClient Módulo 1](https://github.com/VekRest/vekrest-vekclient-modulo1)               |
| VekGateway     | Gateway - Centraliza o acesso às outras aplicações | 2      | [Repositório VekGateway Módulo 2](https://github.com/VekRest/vekrest-vekgateway-modulo2)             
| VekSecurity    | Aplicação de Login e Segurança                     | 2.1    | [Repositório VekSecurity Módulo 2.1](https://github.com/VekRest/vekrest-veksecurity-modulo2.1)       |
| VekLambda      | Lambda - Consumer Kafka                            | 3      | [Repositório VekLambda Módulo 3](https://github.com/VekRest/vekrest-veklambda-modulo3)               |
| VekProducer    | Producer - Producer Kafka                          | 4      | [Repositório VekProducer Módulo 4](https://github.com/VekRest/vekrest-vekproducer-modulo4)           |  
| VekConsumer    | Consumer - Consumer Kafka simples                  | 4.1    | [Repositório VekConsumer Módulo 4.1](https://github.com/VekRest/vekrest-vekconsumer-modulo4.1)       |      
| VekConsumerAPI | Consumer REST - Consumer Kafka com API REST        | 4.2    | [Repositório VekConsumerRest Módulo 4.2](https://github.com/VekRest/vekrest-vekconsumerapi-modulo4.2) | 

> Cada módulo é independente, possuindo seu próprio repositório, Dockerfile e docker-compose.yml para facilitar o deploy e testes isolados.

> Porém, todos os módulos podem ser integrados para formar um sistema completo e funcional, como será demonstrado abaixo.

---

# 📦 Instalação e Configuração do Ambiente (Integração de TODOS os Módulos)

### 1️⃣ Clone este repositório
```bash
# Clonar um por um:
git clone https://github.com/VekRest/VekRest.git

# Entre na pasta do projeto
cd VekRest
```

### 2️⃣ Construa os containers
```bash
docker-compose up -d
```

### 3️⃣ Após a finalização do comando, aguarde de 1 a 2 minutos para todas as aplicações iniciarem

### 4️⃣ Execute o seguinte cURL:

```bash
curl --location 'http://localhost:8083/vekrest/vekproducer/v1/client' \
--header 'Content-Type: application/json' \
--data '{
    "name": "Vek",
    "birth": "2023-01-01",
    "address": {
        "cep": "03759040",
        "state": "SP"
    }
}'
```

### 5️⃣ Após retornar status 201, verifique os logs dos Consumers para comprovar o recebimento da mensagem Kafka

### 6️⃣ Para atestar que um cliente foi criado com a requisição anterior, execute o seguinte cURL:

```bash
curl --location 'http://localhost:8080/vekrest/vekclient/v1/client?page=0' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJzaXN0ZW1hIiwiaWF0IjoxNzY0MjU5MDc1LCJleHAiOjQ5MTc4NTkwNzV9.CH6C_uDbqysBFaXhDz0I_19LkHfhxFT9PYe4Y00wV90' \
--data ''
```

> Deve retornar o cliente cadastrado na listagem

---

## 🧩 Tecnologias Utilizadas

- **Spring Boot** → Framework Back-End
- **Java** → Linguagem de programação
- **Maven** → Build
- **Docker** → Containers e virtualização
- **Docker Hub** → Repositório de imagens Docker
- **Kafka** → Mensageria
- **Zookeeper** → Gerenciamento do Kafka
- **MongoDB** → Persistência de dados
- **Redis** → Cache
- **OpenSearch e Graylog** → Logs da Aplicação
- **Swagger** → Documentação da API
- **SonarQube** → Qualidade
- **Github Actions** → CI/CD automatizado
- **.bat** → Scripts para automatizar processos no Windows

---

## Postman Collection

> Link para download da coleção Postman utilizada nos testes da API: [Postman Collection VekRest](https://web.postman.co/workspace/My-Workspace~e702bcc2-18e9-41e7-86d7-21df963c99df/folder/33703402-f59218e7-8804-436c-8866-2693c75b9eb6?action=share&source=copy-link&creator=33703402&ctx=documentation)

---