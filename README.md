<h1 align="center">Banco de dados do Edellcation</h1>
<h2 align="center">Ponderada semana 3/4</h2>
 
 ## Descrição:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EDELLCATION é uma plataforma de apoio aos funcionários da Dell para que eles tenham um acesso rápido aos seus manuais. A proposta do grupo Dellta é que a plataforma funcione como uma “Netflix” de treinamentos da Dell, onde haveriam suas pendências, o catálogo de manuais e outras funcionalidades como favoritos e filtros de pesquisa. Como o projeto está em período de validação, ainda não é possível determinar como vai funcionar o administrador do site, então foi planejado apenas a questão do principal usuário, o montador.

## SQL Designer

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;O SQL Designer foi a ferramenta de apoio utilizada para a modelagem do banco de dados. Nela foi possível fazer toda a diagramação do banco, criando tabelas, suas colunas e as chaves estrangeiras. Além disso, a ferramenta possui uma função muito útil para a modelagem que é a conversão do diagrama para SQL, com isso é possível gerar o código pronto para que possa ser aplicado no DBeaver.

<p align="center">
<a><img src="assets/bd sqldesigner.png" alt="Diagrama SQL Designer"</a>
</p>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;O diagrama acima foi montado no aplicativo, ele explica como funciona a relação de dados por dentro das funções propostas pela aplicação do grupo Dellta.

### Relações do Banco de Dados:

- **users - manuals:**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;A tabela users é referente aos funcionários, e a tabela manuals é referente aos manuais propostos pela Dell. Existem muitos manuais para muitos funcionários, ou seja uma relação (n,n), então é preciso uma chave auxiliar, que aqui foi chamada de tasks, que seriam as tarefas atribuídas para aquele montador.

- **manuals - hardwares:**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; A tabela hardwares é referente aos produtos que são montados na fábrica da Dell. Existem vários tipos de hardware, mas um manual só pode pertencer a um tipo específico de hardware, gerando uma relação (1,n).

## Aplicação no DBeaver

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;O DBeaver é a ferramenta utilizada para a criação do banco de dados. Como explicado anteriormente, o SQL Designer pode gerar o código que é aplicado em softwares com o DBeaver, então ao aplicar o código gerado do diagrama é possível gerar o seguinte resultado:

```sql
CREATE TABLE manuals (
    id SERIAL PRIMARY KEY,
    title VARCHAR(50) NOT NULL DEFAULT NULL,
    description TEXT NOT NULL DEFAULT NULL,
    link_pdf VARCHAR NOT NULL DEFAULT NULL,
    version INTEGER NOT NULL DEFAULT NULL,
    additional_content VARCHAR DEFAULT NULL,
    id_hardwares INTEGER,
    FOREIGN KEY (id_hardwares) REFERENCES hardwares(id)
);

CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50) NOT NULL DEFAULT NULL,
    function VARCHAR(10) NOT NULL DEFAULT NULL,
    email VARCHAR(15) NOT NULL DEFAULT NULL,
    password VARCHAR NOT NULL DEFAULT NULL
);

CREATE TABLE hardwares (
    id SERIAL PRIMARY KEY,
    name VARCHAR(20) NOT NULL DEFAULT NULL,
    type VARCHAR(15) NOT NULL DEFAULT NULL
);

CREATE TABLE tasks (
    id SERIAL PRIMARY KEY,
    user_progress INTEGER NOT NULL DEFAULT NULL,
    id_manuals INTEGER,
    id_users INTEGER,
    FOREIGN KEY (id_manuals) REFERENCES manuals(id),
    FOREIGN KEY (id_users) REFERENCES users(id)
);
```

<p align="center">
<a><img src="assets/bd dbeaver.png" alt="Diagrama DBeaver"</a>
</p>