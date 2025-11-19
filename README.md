# Plataforma de Upskilling/Reskilling - Futuro do Trabalho 2030+

## Descrição do Problema

O futuro do trabalho está sendo transformado por tecnologias como IA, automação, análise de dados e ambientes
híbridos/remotos. Ao mesmo tempo, cresce a necessidade de:

- **Requalificação (reskilling)** de profissionais cujas atividades correm risco de automação
- **Aperfeiçoamento (upskilling)** contínuo para acompanhar as novas demandas do mercado
- **Educação permanente**, conectada às competências do futuro (tecnológicas e humanas)

O Futuro do Trabalho exige o uso de soluções inovadoras para ajudar as pessoas a se prepararem para carreiras de 2030+.

## Solução Proposta

Desenvolver uma API RESTful para uma plataforma de Upskilling/Reskilling voltada ao futuro do trabalho (2030+),
permitindo que pessoas:

- Se cadastrem na plataforma
- Acessem trilhas de aprendizagem focadas em competências do futuro
- Se inscrevam nessas trilhas para se requalificar profissionalmente

Por meio dessa plataforma inovadora (ODS-9), as pessoas terão acesso à um ensino de qualidade (ODS-4) de forma mais
acessível e igualitária para o futuro (ODS-10), permitindo que elas prosperem no competitivo mercado de 2030+ (ODS-8).

## Tecnologias e Versões

- **Java**: 17 ou superior
- **Spring Boot**: 3.x
- **Banco de Dados**: Oracle Database
- **Documentação**: Swagger/OpenAPI 3.0

### Principais Dependências

```xml
<dependencies>
    <dependency>
        <groupId>org.springdoc</groupId>
        <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
        <version>2.8.14</version>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-security</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-validation</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>com.oracle.database.jdbc</groupId>
        <artifactId>ojdbc11</artifactId>
        <version>23.4.0.24.05</version>
    </dependency>
</dependencies>
```

## Instalação e Configuração

### Pré-requisitos

- Java 17+ instalado
- Maven 3.6+
- Oracle Database

### Passo a Passo

1. **Clone o repositório do projeto**

2. **Instale as dependências**
   ```bash
   mvn clean install
   ```

3. **Configuração do Banco de Dados Oracle**

   Edite o arquivo `application.properties` com suas credenciais:

   ```properties
   spring.datasource.url=jdbc:oracle:thin:@oracle.fiap.com.br:1521/orcl
   spring.datasource.username=SEU_USUARIO
   spring.datasource.password=SUA_SENHA
   
   spring.jpa.hibernate.ddl-auto=update
   spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.OracleDialect
   ```
   Caso você não tenha as tabelas previamente criadas, altere a property `spring. jpa.hibernate. ddl-auto` de
   `update` para `create` durante a primeira
   execução. Após isso, retorne para a versão original para não perder os dados persistidos caso venha a reiniciar o
   projeto.


4. **Execute a aplicação**

   ```bash
   mvn spring-boot:run
   ```

   Ou usando o wrapper do Maven:
   ```bash
   ./mvnw spring-boot:run
   ```

5. **Acesse a aplicação**
    - API: http://localhost:8080
    - Documentação Swagger: http://localhost:8080/swagger-ui.html
    - API Docs: http://localhost:8080/api-docs

## Autenticação

A API utiliza autenticação Basic Auth com as seguintes credenciais padrão:

- **Usuário**: `admin`
- **Senha**: `fiap`

## Endpoints da API

### Usuários (`/user`)

| Método | Endpoint     | Descrição               |
|--------|--------------|-------------------------|
| POST   | `/user`      | Cria um novo usuário    |
| GET    | `/user/{id}` | Busca usuário por ID    |
| GET    | `/user`      | Lista todos os usuários |
| PUT    | `/user/{id}` | Atualiza usuário por ID |
| DELETE | `/user/{id}` | Exclui usuário por ID   |

### Trilhas (`/trail`)

| Método | Endpoint      | Descrição              |
|--------|---------------|------------------------|
| POST   | `/trail`      | Cria uma nova trilha   |
| GET    | `/trail/{id}` | Busca trilha por ID    |
| GET    | `/trail`      | Lista todas as trilhas |
| PUT    | `/trail/{id}` | Atualiza trilha por ID |
| DELETE | `/trail/{id}` | Exclui trilha por ID   |

### Atribuições (`/assignment`)

| Método | Endpoint                      | Descrição                     |
|--------|-------------------------------|-------------------------------|
| POST   | `/assignment`                 | Cria uma nova atribuição      |
| PUT    | `/assignment/{id}`            | Atualiza atribuição por ID    |
| GET    | `/assignment/user/{userId}`   | Busca atribuições por usuário |
| GET    | `/assignment/trail/{trailId}` | Busca atribuições por trilha  |

## Modelos de Dados

### User

```json
{
  "id": 1,
  "name": "João Silva",
  "email": "joao.silva@email.com",
  "birthDate": "1990-01-15",
  "field": "Tecnologia"
}
```

### Trail

```json
{
  "id": 1,
  "name": "Desenvolvimento Backend Java",
  "field": "Tecnologia",
  "description": "Trilha completa para desenvolvimento backend com Java e Spring Boot"
}
```

### AssignmentDTO

```json
{
  "id": 1,
  "userId": 1,
  "trailId": 1,
  "status": "ACTIVE"
}
```

**Status disponíveis**: `ACTIVE`, `COMPLETED`, `CANCELED`

## Exemplos de Requisições

### 1. Criar Usuário

**URL**: `POST http://localhost:8080/user`

**Headers**:

- `Content-Type: application/json`
- `Authorization: Basic YWRtaW46ZmlhcA==`

**Payload**:

```json
{
  "name": "João Silva",
  "email": "joao.silva@email.com",
  "birthDate": "1990-01-15",
  "field": "Tecnologia"
}
```

### 2. Criar Trilha

**URL**: `POST http://localhost:8080/trail`

**Headers**:

- `Content-Type: application/json`
- `Authorization: Basic YWRtaW46ZmlhcA==`

**Payload**:

```json
{
  "name": "Desenvolvimento Backend com Java",
  "field": "Tecnologia",
  "description": "Trilha completa para formação em desenvolvimento backend com Java, Spring Boot e APIs REST"
}
```

### 3. Criar Atribuição

**URL**: `POST http://localhost:8080/assignment`

**Headers**:

- `Content-Type: application/json`
- `Authorization: Basic YWRtaW46ZmlhcA==`

**Payload**:

```json
{
  "userId": 1,
  "trailId": 1,
  "status": "ACTIVE"
}
```

**Caso não seja definido o `status` no payload, o padrão será `"ACTIVE"`**

### 4. Atualizar Usuário

**URL**: `PUT http://localhost:8080/user/1`

**Headers**:

- `Content-Type: application/json`
- `Authorization: Basic YWRtaW46ZmlhcA==`

**Payload**:

```json
{
  "id": 1,
  "name": "João Silva Santos",
  "email": "joao.silva@email.com",
  "birthDate": "1990-01-15",
  "field": "Desenvolvimento de Software"
}
```

### 5. Atualizar Atribuição

**ATENÇÃO! Este método não permite a alteração do Id da Trilha e/ou Usuário.**

**URL**: `PUT http://localhost:8080/assignment/1`

**Headers**:

- `Content-Type: application/json`
- `Authorization: Basic YWRtaW46ZmlhcA==`

**Payload**:

```json
{
  "id": 1,
  "status": "COMPLETED"
}
```

## Testando com Postman

### Configuração Básica

1. **Baixe e instale o Postman**
2. **Configure a autenticação**:
    - Vá para a aba "Authorization"
    - Selecione "Basic Auth"
    - Username: `admin`
    - Password: `fiap`

3. **Configure os headers**:
    - `Content-Type: application/json`

### Coleção de Exemplos

**Criar um usuário**:

```http
curl -X POST "http://localhost:8080/user" \
  -H "Authorization: Basic YWRtaW46ZmlhcA==" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Maria Oliveira",
    "email": "maria.oliveira@email.com",
    "birthDate": "1985-05-20",
    "field": "Ciência de Dados"
  }'
```

**Buscar usuário por ID**:

```http
curl -X GET "http://localhost:8080/user/1" \
  -H "Authorization: Basic YWRtaW46ZmlhcA=="
```

**Listar todas as trilhas**:

```http
curl -X GET "http://localhost:8080/trail" \
  -H "Authorization: Basic YWRtaW46ZmlhcA=="
```

**Buscar atribuições de um usuário**:

```http
curl -X GET "http://localhost:8080/assignment/user/1" \
  -H "Authorization: Basic YWRtaW46ZmlhcA=="
```

**Buscar usuários de uma trilha**:

```http
curl -X GET "http://localhost:8080/assignment/trail/1" \
  -H "Authorization: Basic YWRtaW46ZmlhcA=="
```

## Estrutura do Projeto

```
src/
├── main/
│   ├── java/
│   │   └── com/
│   │       └── platform/
│   │           ├── controller/     # Interfaces das APIs
│   │           ├── service/        # Lógica de negócio
│   │           ├── repository/     # Camada de dados
│   │           ├── model/          # Entidades JPA (User, Trail, Assignment)
│   │           ├── dto/            # DTOs (AssignmentDTO)
│   │           └── config/         # Configurações
│   └── resources/
│       └── application.properties  # Configurações da aplicação
```

## Validações

### User

- **name**: Máximo 100 caracteres
- **email**: Máximo 100 caracteres
- **birthDate**: Data no passado ou presente
- **field**: Máximo 100 caracteres

### Trail

- **name**: Máximo 100 caracteres
- **field**: Máximo 100 caracteres
- **description**: Máximo 500 caracteres

### Assignment

- **status**: Valores aceitos: ACTIVE, COMPLETED, CANCELED

## Troubleshooting

### Problemas Comuns

1. **Erro de conexão com o Oracle**:
    - Verifique se o Oracle está rodando
    - Confirme as credenciais no `application.properties`
    - Teste a conexão com um cliente SQL

2. **Erro de autenticação**:
    - Use as credenciais corretas: usuário `admin`, senha `fiap`
    - Certifique-se de incluir o header `Authorization`

3. **Erro de validação**:
    - Verifique os limites de caracteres nos campos
    - Para status, use apenas: ACTIVE, COMPLETED, CANCELED

4. **Porta em uso**:
    - Altere a porta no `application.properties`: `server.port=8081`

## Colaboradores

- Mateus Leme RM 557803
- Heloísa Fleury Jardim RM 556378
- Stephany Borzi Marques RM 557351