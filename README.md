# ProductAPI

API RESTful desenvolvida em C# com .NET 10 e Entity Framework Core, utilizando Oracle Database como banco de dados e Swagger para documentação e testes dos endpoints.

## Integrantes

* **Mohamed Afif RM 554445**
* **Lucca Cardinale RM 556668**


---

## 1. Sobre o projeto

O **ProductAPI** é uma API RESTful desenvolvida como projeto da disciplina **C# Software Development**.

O projeto tem como objetivo disponibilizar operações básicas de gerenciamento de produtos, permitindo cadastrar, consultar, atualizar e excluir produtos por meio de requisições HTTP.

A API foi desenvolvida utilizando conceitos de desenvolvimento de APIs RESTful, Entity Framework Core, banco de dados Oracle, versionamento de endpoints e documentação através do Swagger.

### Problema que o projeto resolve

O sistema permite centralizar o gerenciamento de produtos de forma simples, possibilitando que aplicações clientes consultem e alterem informações de produtos através de uma API.

### Público-alvo

A API pode ser utilizada por sistemas que necessitem realizar operações básicas de cadastro e gerenciamento de produtos, como sistemas de estoque, aplicações comerciais ou sistemas administrativos.

---

## 2. Tecnologias utilizadas

* **C#**
* **.NET 10**
* **ASP.NET Core Web API**
* **Entity Framework Core**
* **Oracle Database**
* **Oracle.EntityFrameworkCore**
* **Swagger / Swashbuckle**
* **Visual Studio**
* **Oracle SQL Developer**

---

## 3. Banco de dados

O banco de dados utilizado no projeto é o **Oracle Database**.

O acesso ao banco é realizado através do **Entity Framework Core**, utilizando o provider:

```text
Oracle.EntityFrameworkCore
```

A aplicação utiliza um `DbContext` para realizar a comunicação entre a API e o banco de dados.

### Entidade

O projeto possui a entidade `Produto`, composta pelos seguintes campos:

| Campo     | Tipo    | Descrição                        |
| --------- | ------- | -------------------------------- |
| Id        | int     | Identificador único do produto   |
| Nome      | string  | Nome do produto                  |
| Descricao | string  | Descrição do produto             |
| Preco     | decimal | Preço do produto                 |
| Estoque   | int     | Quantidade disponível em estoque |

---

## 4. Estrutura do projeto

A estrutura principal do projeto é:

```text
ProductAPI/
│
├── Controllers/
│   └── ProdutosController.cs
│
├── Data/
│   └── AppDbContext.cs
│
├── Models/
│   └── Produto.cs
│
├── Migrations/
│   ├── InitialCreate.cs
│   └── AppDbContextModelSnapshot.cs
│
├── Properties/
│
├── appsettings.json
├── Program.cs
├── ProductAPI.csproj
└── README.md
```

### Controllers

Contém os endpoints da API e as operações HTTP relacionadas aos produtos.

### Data

Contém o `AppDbContext`, responsável pela comunicação da aplicação com o banco de dados através do Entity Framework Core.

### Models

Contém as entidades utilizadas pela aplicação.

### Migrations

Contém o histórico das alterações da estrutura do banco de dados realizadas através do Entity Framework Core.

---

## 5. Entity Framework Core

O projeto utiliza o Entity Framework Core para realizar as operações de persistência dos dados.

O contexto principal da aplicação é:

```text
AppDbContext
```

A entidade `Produto` é disponibilizada através de:

```csharp
public DbSet<Produto> Produtos { get; set; }
```

As operações de criação, consulta, atualização e exclusão dos produtos são realizadas através do Entity Framework Core.

---

## 6. Migration

Foi criada uma Migration inicial para gerar a estrutura necessária no banco de dados Oracle.

Migration utilizada:

```text
InitialCreate
```

Para criar uma nova Migration utilizando o Package Manager Console do Visual Studio:

```powershell
Add-Migration NomeDaMigration
```

Para aplicar a Migration ao banco:

```powershell
Update-Database
```

A Migration permite manter o histórico das alterações realizadas na estrutura do banco através do Entity Framework Core.

---

## 7. Configuração do banco de dados

A conexão com o Oracle é configurada no arquivo:

```text
appsettings.json
```

Exemplo:

```json
{
  "ConnectionStrings": {
    "OracleConnection": "User Id=SEU_USUARIO;Password=SUA_SENHA;Data Source=SEU_SERVIDOR:PORTA/ORCL"
  }
}
```

As informações de usuário e senha não devem ser compartilhadas publicamente no repositório.

Para executar o projeto, cada integrante deve configurar suas próprias credenciais de acesso ao banco Oracle.

---

## 8. Como executar o projeto

### Pré-requisitos

Para executar o projeto localmente, é necessário possuir:

* Visual Studio com suporte ao .NET 10;
* .NET 10 SDK;
* acesso ao banco Oracle;
* Oracle SQL Developer ou ferramenta equivalente;
* acesso ao schema utilizado pela aplicação.

### Passo 1 — Clonar o repositório

Clone o projeto:

```bash
git clone URL_DO_REPOSITORIO
```

Entre na pasta:

```bash
cd ProductAPI
```

### Passo 2 — Configurar o banco

Abra o arquivo:

```text
appsettings.json
```

e configure a connection string com as credenciais do Oracle.

### Passo 3 — Restaurar os pacotes

No Visual Studio, restaure os pacotes NuGet do projeto.

Os principais pacotes utilizados são:

```text
Oracle.EntityFrameworkCore
Microsoft.EntityFrameworkCore.Tools
Microsoft.EntityFrameworkCore.Design
Swashbuckle.AspNetCore
```

### Passo 4 — Aplicar a Migration

No Package Manager Console:

```powershell
Update-Database
```

Isso criará/atualizará as estruturas necessárias no banco Oracle.

### Passo 5 — Executar a API

Execute o projeto pelo Visual Studio utilizando:

```text
Ctrl + F5
```

ou:

```text
F5
```

A aplicação será iniciada localmente.

---

## 9. Swagger

O projeto utiliza o **Swagger** para documentar e testar os endpoints da API.

Após iniciar a aplicação, acesse:

```text
https://localhost:7014/swagger
```

A porta pode variar dependendo da configuração do ambiente.

A interface do Swagger permite visualizar todos os endpoints disponíveis e executar as requisições diretamente pelo navegador.

---

# 10. Endpoints

A API utiliza versionamento através da rota:

```text
/api/v1
```

Os endpoints disponíveis são:

| Método | Rota                    | Descrição                     |
| ------ | ----------------------- | ----------------------------- |
| GET    | `/api/v1/produtos`      | Retorna todos os produtos     |
| GET    | `/api/v1/produtos/{id}` | Retorna um produto pelo ID    |
| POST   | `/api/v1/produtos`      | Cadastra um novo produto      |
| PUT    | `/api/v1/produtos/{id}` | Atualiza um produto existente |
| DELETE | `/api/v1/produtos/{id}` | Remove um produto             |

---

# 11. GET — Listar produtos

### Requisição

```http
GET /api/v1/produtos
```

### Descrição

Retorna todos os produtos cadastrados no banco de dados.

### Status esperado

```text
200 OK
```

### Exemplo de resposta

```json
[
  {
    "id": 1,
    "nome": "Notebook",
    "descricao": "Notebook para estudos",
    "preco": 3500,
    "estoque": 10
  }
]
```

---

# 12. GET — Buscar produto por ID

### Requisição

```http
GET /api/v1/produtos/1
```

### Descrição

Retorna um produto específico utilizando seu identificador.

### Status esperado

```text
200 OK
```

Caso o produto não exista:

```text
404 Not Found
```

---

# 13. POST — Cadastrar produto

### Requisição

```http
POST /api/v1/produtos
```

### Corpo da requisição

```json
{
  "nome": "Notebook",
  "descricao": "Notebook para estudos",
  "preco": 3500.00,
  "estoque": 10
}
```

### Status esperado

```text
201 Created
```

O produto é persistido no banco Oracle através do Entity Framework Core.

---

# 14. PUT — Atualizar produto

### Requisição

```http
PUT /api/v1/produtos/1
```

### Corpo da requisição

```json
{
  "id": 1,
  "nome": "Notebook Dell",
  "descricao": "Notebook atualizado",
  "preco": 4200.00,
  "estoque": 8
}
```

### Status esperado

```text
204 No Content
```

Caso o ID informado não corresponda ao ID enviado no corpo:

```text
400 Bad Request
```

Caso o produto não exista:

```text
404 Not Found
```

---

# 15. DELETE — Remover produto

### Requisição

```http
DELETE /api/v1/produtos/1
```

### Descrição

Remove o produto informado pelo ID.

### Status esperado

```text
204 No Content
```

Caso o produto não exista:

```text
404 Not Found
```

---

# 16. Status HTTP utilizados

A API utiliza códigos HTTP adequados para representar o resultado das operações.

| Código          | Utilização                                    |
| --------------- | --------------------------------------------- |
| 200 OK          | Consulta realizada com sucesso                |
| 201 Created     | Recurso criado com sucesso                    |
| 204 No Content  | Atualização ou exclusão realizada com sucesso |
| 400 Bad Request | Requisição inválida                           |
| 404 Not Found   | Recurso não encontrado                        |

---

# 17. Versionamento da API

Os endpoints utilizam o prefixo:

```text
/api/v1
```

Exemplo:

```text
/api/v1/produtos
```

O versionamento permite que futuras versões da API sejam disponibilizadas sem necessariamente quebrar as aplicações que utilizam a versão anterior.

---

# 18. Evidências de testes

Os testes foram realizados utilizando o Swagger.

## POST — Cadastro de produto

**Endpoint:**

```text
POST /api/v1/produtos
```

**Resultado esperado:**

```text
201 Created
```

![Teste POST](../ProductAPI/docs/images/post-produto.png)

---

## GET — Listagem de produtos

**Endpoint:**

```text
GET /api/v1/produtos
```

**Resultado esperado:**

```text
200 OK
```

![Teste GET](../ProductAPI/docs/images/get-produtos.png)

---

## GET — Busca por ID

**Endpoint:**

```text
GET /api/v1/produtos/{id}
```

**Resultado esperado:**

```text
200 OK
```

![Teste GET por ID](../ProductAPI/docs/images/get-produto-id.png)

---

## PUT — Atualização de produto

**Endpoint:**

```text
PUT /api/v1/produtos/{id}
```

**Resultado esperado:**

```text
204 No Content
```

![Teste PUT](../ProductAPI/docs/images/put-produto.png)

---

## DELETE — Exclusão de produto

**Endpoint:**

```text
DELETE /api/v1/produtos/{id}
```

**Resultado esperado:**

```text
204 No Content
```

![Teste DELETE](../ProductAPI/docs/images/delete-produto.png)

---

## Tratamento de erro — Produto não encontrado

**Endpoint:**

```text
GET /api/v1/produtos/999
```

**Resultado esperado:**

```text
404 Not Found
```

![Teste 404](../ProductAPI/docs/images/get-404.png)

---

# 19. Evidência do banco de dados

O banco Oracle foi utilizado para armazenar os dados dos produtos.

A estrutura e os registros podem ser verificados através do Oracle SQL Developer.

![Oracle SQL Developer](docs/images/oracle-produtos.png)

---

# 20. Fluxo da aplicação

O funcionamento geral do projeto pode ser representado da seguinte forma:

```text
Cliente
   │
   │ HTTP Request
   ▼
Swagger
   │
   ▼
ProdutosController
   │
   ▼
AppDbContext
   │
   ▼
Entity Framework Core
   │
   ▼
Oracle Database
   │
   ▼
Resposta HTTP
   │
   ▼
Swagger
```

O cliente realiza uma requisição HTTP através do Swagger. O `ProdutosController` recebe a requisição e utiliza o `AppDbContext` para realizar as operações através do Entity Framework Core. Os dados são persistidos ou consultados no Oracle Database e o resultado é retornado através de uma resposta HTTP.

---

# 21. Boas práticas utilizadas

O projeto foi desenvolvido buscando manter uma estrutura simples e organizada, separando as responsabilidades entre:

* **Models:** representação das entidades;
* **Data:** configuração e acesso ao banco através do Entity Framework Core;
* **Controllers:** implementação dos endpoints da API;
* **Migrations:** controle da evolução da estrutura do banco.

Também foram utilizados nomes significativos para classes, métodos e propriedades, além de códigos HTTP adequados para representar os resultados das operações.

---

# 22. Conclusão

O projeto **ProductAPI** demonstra a implementação de uma API RESTful utilizando C# e .NET 10, com persistência de dados através do Entity Framework Core e Oracle Database.

A aplicação possui versionamento de endpoints, operações CRUD, tratamento de situações de erro, Migration para gerenciamento da estrutura do banco e documentação/testes através do Swagger.

Dessa forma, o projeto contempla os principais conceitos solicitados na atividade de **C# Software Development**.
