# Docker MySQL Basic

Este repositório detalha a execução de um container Docker, com My SQL 8, e os comandos basicos para criar e listar banco de dados, assim como a exposição de porta para conexão ocm DBeaver.

Sistma utilizado: Linux Debian 12 - Bookworm

## O Projeto

- Criar um container, com exposição de portas e volume tipo **`bind`**
- Se basear na documentação: **`https://hub.docker.com/_/mysql`**
- Mapear o caminho: **`/var/lib/mysql`**
- No prompt do MySQL: 
   - **`show databases;`**
   - **`create database NOME-ALUNO;`**
   - ```bash
         CREATE TABLE alunos (
         id INT AUTO_INCREMENT PRIMARY KEY,
         nome VARCHAR(50),
         idade INT
         );
      ```
### Desenvolvimento do projeto

- `mkdir -p /caminho/para/diretorio/mysql-data`

   `docker run --name mysql-container \
   -p 3306:3306 \
   -v /caminho/para/diretorio/mysql-data:/var/lib/mysql \
   -e MYSQL_ROOT_PASSWORD=a_senha_super_secreta \
   -d mysql:latest`

   No comando acima, Temos o nome do container(--name), a porta(-p),
   o volume em bind(-v), o mapeamento do caminho(/caminho/para/diretorio/       mysql-data:/var/lib/mysql), a senha do MySQL(MYSQL_ROOT_PASSWORD), a versão do mysql(-d).

Após tudo feito, no terminal:

- `docker exec -it mysql-container bash`

- `no prompt: mysql -u root -p`

- Colocar a senha super secreta.

- ´>mysql`

Executar os comandos:

Mostrar os bancos de dados:

```bash
SHOW DATABASES;
```
Criar um banco de dados e usa-lo:

```bash
CREATE DATABASE NOME_ALUNO;
USE NOME_ALUNO;
```
Criar a tabela alumos dentro do banco de dados:

```bash
CREATE TABLE alunos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(50),
    idade INT
);

```
Mostrar as tabelas:

```bash
SHOW TABLES;
```

Caso queira ver os arquivos criados no volume bind escolhido:

```bash
cd /caminho/para/diretorio/mysql-data
ls -la
```

Caso haja problemas de permissionamento de usuário, adicione ao seu código a flag:

`-u $(id -u):$(id -g)`


## Conexão com DBeaver

**Cheque se as potas estão devidamente abertas no Docker**:
   - `docker ps`
   Veja se aparece no docker id:

   - `0.0.0.0:3306->3306/tcp, :::3306->3306/tcp, 33060/tcp   mysql-container`

**Conexão com DBeaver**:

   - Em nova conexão, escolha: MySQL

   - Server host:

   ```bash
      localhost
   ```

   - Database:

   ```bash
   NOME_ALUNO
   ```

   - Username: root

   - Password: a senha super secreta

   #### Teste a conexão, caso peça para instalar um jdbc driver, faça-o.

   #### Conecte apertando o botão Finish.

**Visualize seu banco de dados no DBeaver comnforme a imagem a seguir**

![Mysql docker dbeaver](https://github.com/user-attachments/assets/38a6c1af-2ec6-4cdb-b6f9-5553db0ae5e3)
