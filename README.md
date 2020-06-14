# QA School - API

Este repositório é utilizado nos cursos de API da QA School.

## SETUP :hammer_and_wrench:

> Pré-requisitos:

- Instalar o Docker + Docker-Compose ([encontre instruções aqui](https://github.com/qaschoolbr/setup))

### Clonar Repositório :octocat:

```bash
git clone https://github.com/qaschoolbr/api.git
```

Caso utilize o HUB basta rodar `hub clone qaschoolbr/postman`

### Instanciar a API :whale:

Execute o comando abaixo para subir a stack e aguarde o download da imagem `qaschool/api`:

```bash
docker-compose up -d
```

![Pull](images/pull.png)

Quando a imagem for baixada, o container será instanciado:

![Created](images/created.png)

### Verificar Log :memo:

Execute o comando abaixo para verificar o log em tempo real:

```bash
docker-compose logs -f
```

![Log](images/log.png)

Quando o log exibir **Welcome Back**, basta usar a combinação de teclas <kbd>CTRL</kbd> + <kbd>C</kbd> para sair do log.

## API no Ar :rocket:

Acesse o painel via [localhost:1337](http://localhost:1337) para conferir se está tudo OK mesmo.

---

## AUTH :lock:

Todos os endpoints requerem autenticação. Para obter o token de acesso, é preciso requisitá-lo da seguinte forma:

- Auth (/auth/local)

      - URL: localhost:1337/auth/local
      - HEADER: application/json
      - BODY (raw:json): { "identifier": "qaschool", "password": "qaschool" }

## ENDPOINTS :link:

Basicamente, ele consiste dos seguintes endpoints:

- Category (/categories)

      - GET /categories
      - GET /categories/count
      - GET /categories/:id
      - POST /categories
      - PUT /categories/:id
      - DELETE /categories/:id

- Class (/classes)

      - GET /classes
      - GET /classes/count
      - GET /classes/:id
      - POST /classes
      - PUT /classes/:id
      - DELETE /classes/:id

- Course (/courses)

      - GET /courses
      - GET /courses/count
      - GET /courses/:id
      - POST /courses
      - PUT /courses/:id
      - DELETE /courses/:id

- Student (/students)

      - GET /students
      - GET /students/count
      - GET /students/:id
      - POST /students
      - PUT /students/:id
      - DELETE /students/:id

### ATRIBUTOS :pencil:

- Category (/categories)

    O endpoint /categories contém os seguintes atributos:

        - name: string, required, unique
        - courses: array[/courses({ids})], optional

- Class (/classes)

    O endpoint /classes contém os seguintes atributos:

        - name: string, required
        - seats: integer, required, default[100]
        - start: date, required
        - end: date, optional
        - banner: file[image], optional
        - published: boolean, required, default[false]
        - price: decimal, required
        - uid: uid, required
        - course: integer[/courses({id})], optional
        - teachers: array[/users-permissions_user({ids})], optional
        - students: array[/students({ids})], optional

- Course (/courses)

    O endpoint /courses contém os seguintes atributos:

        - name: string, required, unique
        - description: richtext, optional
        - paid: boolean, required, default[true]
        - uid: uid, required
        - users: array[/users-permissions_user({ids})], optional
        - category: array[/categories({ids})], optional
        - classes: array[/classes({ids})], optional

- Student (/students)

    O endpoint /students contém os seguintes atributos:

        - first_name: string, required
        - last_name: string, required
        - email: string, required, unique
        - avatar: file[image], optional
        - phone: string, optional
        - active: boolean, required, default[true]
        - document: file[files], optional
        - classes: array[/classes({ids})], optional

### Banco de Dados :file_cabinet:

Os dados da API estão contidos em um arquivo SQLite localizado no diretório `.tmp/data.db`.
