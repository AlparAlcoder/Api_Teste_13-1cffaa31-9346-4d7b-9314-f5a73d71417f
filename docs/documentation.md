# Documentação da API FastAPI

Este código é uma aplicação FastAPI que fornece uma API REST para autenticação de usuários e manipulação de dados de usuários.

## Dependências

As dependências necessárias para esta aplicação, além do FastAPI, são:

- SQLAlchemy
- Pydantic
- jose
- passlib
- datetime
- typing

## Funções

### `get_db()`

Esta função cria uma nova sessão de banco de dados e a retorna.

### `get_user(db: Session, username: str)`

Esta função consulta o banco de dados para encontrar um usuário com base no nome de usuário fornecido.

Parâmetros:
- `db`: Uma instância de `Session` do SQLAlchemy.
- `username`: Uma `str` que representa o nome do usuário.

Retorna: 
- A primeira instância de usuário que corresponde ao nome de usuário fornecido.

### `authenticate_user(fake_db, username: str, password: str)`

Esta função autentica um usuário com base no nome de usuário e senha fornecidos.

Parâmetros:
- `fake_db`: Um banco de dados fictício para autenticação.
- `username`: Uma `str` que representa o nome do usuário.
- `password`: Uma `str` que representa a senha do usuário.

Retorna: 
- O usuário se a autenticação for bem-sucedida, `False` caso contrário.

### `create_access_token(data: dict, expires_delta: Optional[timedelta] = None)`

Esta função cria um token de acesso JWT.

Parâmetros:
- `data`: Um `dict` que contém os dados a serem incorporados no token.
- `expires_delta`: Um `timedelta` opcional que representa o tempo até o token expirar.

Retorna: 
- Um token JWT.

### `get_current_user(token: str = Depends(oauth2_scheme))`

Esta função retorna o usuário atual com base no token de acesso fornecido.

Parâmetros:
- `token`: Uma `str` que representa o token de acesso.

Retorna: 
- Os dados do token se o token for válido, caso contrário, lança uma exceção.

## Rotas

### `POST /token`

Esta rota permite que um usuário faça login e obtenha um token de acesso.

Retorna: 
- Um dicionário contendo o token de acesso e o tipo de token.

### `POST /users/`

Esta rota permite que um novo usuário seja criado.

Parâmetros:
- `user`: Uma instância da classe `User` que representa o novo usuário.

Retorna: 
- O novo usuário criado.

### `GET /users/{user_id}`

Esta rota permite que os detalhes de um usuário específico sejam recuperados.

Parâmetros:
- `user_id`: Um `int` que representa o ID do usuário.

Retorna: 
- Os detalhes do usuário se o usuário existir, caso contrário, lança uma exceção.

## Notas importantes

- A chave secreta e o algoritmo usados para criar os tokens JWT são definidos no início do código e são usados em todo o código. Garanta que a chave secreta seja mantida em sigilo e não seja exposta de nenhuma forma.
- Esta aplicação utiliza o esquema de segurança OAuth2 com fluxo de senha, que é um padrão comum para rotas de autenticação de usuário.
- O modelo de usuário Pydantic é usado para validação de dados de entrada.