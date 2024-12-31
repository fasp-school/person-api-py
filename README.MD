
# Pesquisa sobre o uso de IA como Assistente de Codigo.

Este é um exercicio proposto para avaliar os impactos da construcao de uma simples API por estudantes com e sem uso de IA como Assistente de Codigo.


## Requisitos de Tecnologia.

<img src="https://www.python.org/static/img/python-logo.png" alt="python" height="50">
<img src="https://fastapi.tiangolo.com/img/logo-margin/logo-teal.png" alt="fastapi" height="50"> 


## História: Cadastrar uma Pessoa.
**Título**: Cadastrar uma Pessoa </br>
**Papel**: Como um Administrador do Sistema </br>
**Objetivo**: Quero cadastrar uma nova pessoa no sistema </br>
**Benefício**: Para que eu possa gerenciar seus dados. </br>


## Critérios de Aceitação

### Campos Obrigatórios:
Os seguintes campos devem ser preenchidos antes que o cadastro seja concluído:

- Nome Completo
- Data de Nascimento
- Endereço de E-mail (deve ser único)
- Número de Contato (deve ser único)

### Campos Opcionais
Os seguintes campos são opcionais:
- Endereço
- Cidade
- País

### Regras de Validação
- Data de Nascimento:
    - Não deve permitir datas futuras.
- Endereço de E-mail:
    - Deve seguir o formato xxx@xxx.xxx.
- Número de Contato:
    - Deve seguir o formato 99.99999.9999.
- Campos Obrigatórios:
    - Qualquer campo obrigatório que estiver ausente deve resultar em erro.
- Verificação de Duplicidade:
    - Endereço de E-mail
    - Número de Contato

- Validação Adicional: 
<br/>O sistema deve garantir que não existam dois cadastros com o mesmo e-mail ou número de contato.

## Requisitos da API
### Método POST: Cadastrar uma Nova Pessoa

#### Requisição:
Aceita um payload JSON contendo os dados da pessoa.

#### Exemplo de Requisição:
```
POST /api/person
Content-Type: application/json

{
  "fullName": "João Silva",
  "dateOfBirth": "1990-05-15",
  "email": "joao.silva@exemplo.com",
  "contactNumber": "99.12345.6789",
  "address": "Rua Principal, 123",
  "city": "Recife",
  "country": "Brasil"
}
```

#### Resposta:
- **201 Created** :
    - O cadastro da pessoa foi realizado com sucesso.
    - Retorna o ID da pessoa cadastrada.
    - Exemplo de Resposta:
        ```
        {
            "id": 1,
            "fullName": "João Silva",
            "dateOfBirth": "1990-05-15",
            "email": "joao.silva@exemplo.com",
            "contactNumber": "99.12345.6789",
            "address": "Rua Principal, 123",
            "city": "São Paulo",
            "country": "Brasil"
        }
        ```

- **400 Bad Request**:
    - Caso algum campo obrigatório esteja ausente ou falhe na validação.
    - Retorna uma mensagem de erro.
    - Exemplo de Resposta:
        ```
        {
            "detail": "Falha na validação: O e-mail é obrigatório."
        }
        ```

- **409 Conflict**:
    - Caso o e-mail ou número de contato já exista no sistema.
    - Retorna uma mensagem de erro.
    - Exemplo de Resposta:
        ```
        {
            "detail": "Entrada duplicada: O e-mail já existe."
        }
        ```

### Método POST: Cadastrar uma Nova Pessoa

#### Cenários:
- **Quando um ID de Pessoa é informado**: 
    - Retorna os detalhes da pessoa especificada.

    #### Exemplo de Requisição:
    ```
    GET /api/person/1
    ```

    #### Exemplo de Resposta:
    - **200 OK**:
        ```
        {
            "id": 1,
            "fullName": "João Silva",
            "dateOfBirth": "1990-05-15",
            "email": "joao.silva@exemplo.com",
            "contactNumber": "99.12345.6789",
            "address": "Rua Principal, 123",
            "city": "São Paulo",
            "country": "Brasil"
        }
        ```
    - **404 Not Found**:
        ```
        {
            "detail": "Pessoa não encontrada"
        }
        ```

- **Quando nenhum ID de Pessoa é informado**: 
    - Retorna a lista de todas as pessoas no sistema.

    #### Exemplo de Requisição:
    ```
    GET /api/person
    ```
    #### Exemplo de Resposta:
    - **200 OK**:
        ```
        [
            {
                "id": 1,
                "fullName": "João Silva",
                "email": "joao.silva@exemplo.com"
            },
            {
                "id": 2,
                "fullName": "Maria Oliveira",
                "email": "maria.oliveira@exemplo.com"
            }
        ]
        ```
    - **204 No Content**:
        ```
        {
            "message": "Nenhuma pessoa encontrada."
        }
        ```

## Armazenamento de Dados

### Armazenamento em Memória:
Os dados das pessoas serão armazenados temporariamente em memória.