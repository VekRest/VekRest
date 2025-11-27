# 🧬 Projeto VekRest

O Projeto VekRest foi desenvolvido em 4 módulos, com o objetivo de aplicar tecnologias e padrões de desenvolvimento modernos em um projeto robusto e inter conectado, utilizando Clean Architecture e padrões SOLID.

## 🧩 MÓDULOS DO PROJETO
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
> Porém, todos os módulos podem ser integrados para formar um sistema completo e funcional.

---

## ⚙️ Objetivo

Módulo 1
Crie uma API REST utilizando Spring Boot (versão 3+).
A API deve conter um CRUD de Pessoa (Criar, Ler, Atualizar e Deletar), com os seguintes requisitos:

O retorno do serviço deve ser paginado, mostrando 10 itens por página.

Apenas pessoas com o atributo ativo = true devem ser retornadas.

Utilize o banco de dados da sua escolha e crie uma tabela com o seguinte padrão:

ID NOME DT_NASCIMENTO ATIVO
Os logs da aplicação devem ser enviados ao Graylog.

No seu docker-compose, adicione todas as imagens utilizadas (banco de dados, Graylog, aplicação, etc.).

Módulo 2
Crie uma API REST de Login com controle de acesso por usuário e senha.
Requisitos:

Ao enviar um usuário e senha válidos, o sistema deve retornar, através do endpoint /login, um token de autenticação (Bearer Token).

Crie um API Gateway e garanta que sua aplicação de Login só possa ser acessada através de uma rota no Gateway.

O container da aplicação de Login não deve expor sua porta diretamente (configure o Docker adequadamente).

Inclua o Dockerfile necessário para a construção da aplicação.

Módulo 3
Crie uma função Lambda que escute um tópico Kafka e exiba no console a mensagem recebida, por exemplo:

A mensagem chegou: <mensagem>
Em seguida:

Gere uma imagem Docker dessa aplicação.

Publique a imagem no DockerHub através de uma GitHub Action configurada no repositório.

Módulo 4
Crie três aplicações Spring Boot com Kafka:

1 produtor

2 consumidores

Requisitos:

Garanta que uma mensagem enviada pelo produtor seja consumida pelas duas aplicações.

Configure corretamente o Group ID no Kafka.

Garanta resiliência com três brokers Kafka.

Configure cinco partições para garantir redundância e melhor paralelismo na leitura das mensagens.

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

## 📜 Licença
> Este projeto é distribuído sob a licença GPL-3.0. Consulte o arquivo [LICENCE](LICENSE.txt)
para mais detalhes.

---

# 📦 Instalação e Configuração do Ambiente (Integração de TODOS os Módulos)

## 1° Método (Clonando todos as aplicações individualmente)

> Aplicação Gateway principal para integração de todos os módulos:  [VekGateway](https://github.com/VekRest/vekrest-vekgateway-modulo2)
> Nesta aplicação, descomente as últimas linhas do docker-compose.yml para subir todas as aplicações juntas.

### 1️⃣ Clone todos os repositórios das aplicações do projeto
```bash
# Clonar um por um:
git clone <repositório_da_aplicação>
````

### 2️⃣ Construa os containers de cada aplicação individualmente
```bash
# Dentro da pasta de cada aplicação, rode:
mvn clean package -DskipTests

# Depois, construa a imagem Docker de cada aplicação:
docker build -t vekrest/<aplicação>:latest .

# Descomente as últimas linhas do docker-compose.yml da aplicação VekGateway para subir todas as aplicações juntas
docker-compose up -d
```

### 3️⃣ Verifique se todas as aplicações subiram corretamente no Docker Desktop e acompanhe os Logs

---

## 2° Método (Clonando apenas o repositório do Gateway e construindo containers do Docker Hub)

### 1️⃣ Clone o repositório do Gateway
```bash
git clone https://github.com/VekRest/vekrest-vekgateway-modulo2.git

cd vekrest-vekgateway-modulo2
````

### 2️⃣ Construa os containers de cada aplicação a partir do Docker Hub
```bash
# Dentro da pasta da aplicação VekGateway, rode:
docker-compose -f docker-compose-full.yml up -d
```

### 3️⃣ Verifique se todas as aplicações subiram corretamente no Docker Desktop e acompanhe os Logs

---

## Postman Collection

> Link para download da coleção Postman utilizada nos testes da API: [Postman Collection VekRest](https://web.postman.co/workspace/My-Workspace~e702bcc2-18e9-41e7-86d7-21df963c99df/folder/33703402-f59218e7-8804-436c-8866-2693c75b9eb6?action=share&source=copy-link&creator=33703402&ctx=documentation)

---

## ✍️ Autor

<div align="center">

| [<img src="https://avatars.githubusercontent.com/u/98980071" width=115><br><sub>Victor Cardoso</sub>](https://github.com/vek03)
| :---: |

</div>

---
