# CineExpress API

A backend API for a cinema platform, enabling movie session management, ticket purchasing, and payment processing. Built as the final project of the Back-End with JS module at Kenzie Academy Brasil by a team of 6 developers.

## Technologies

- Node.js
- TypeScript
- Express
- PostgreSQL
- TypeORM
- Jest
- Docker

## Features

- User registration with admin and employee roles
- JWT authentication with role-based access control
- Cinema and room management
- Movie listing and session scheduling
- Ticket purchasing with seat selection
- Payment info management
- Soft delete for users

## Getting Started

**Requirements:** Docker and Docker Compose

1. Clone the repository and create your `.env` file

2. Fill in the `.env` variables:

```dotenv
HOST=docker_db
POSTGRES_PASSWORD=yourpassword
POSTGRES_DB=cineexpress
POSTGRES_USER=cineexpress_user
SECRET_KEY=yoursecretkey
PGPORT=5432
PORT=3000
```

3. Start the application:

```bash
docker compose up --build
```

The API will be available at `http://localhost:3000`. Migrations run automatically on startup.

## API Endpoints

### Users

**POST** `/users` — Create user

```json
// Request
{
  "name": "Thiago",
  "email": "thiago@mail.com",
  "isAdm": true,
  "isEmployee": false,
  "contact": "99999999999",
  "birthDate": "2000/01/01",
  "password": "1234"
}

// Response 201
{
  "id": "f1719800-2e5a-4270-88de-64380f73dd3d",
  "name": "Thiago",
  "email": "thiago@mail.com",
  "isAdm": true,
  "isEmployee": false,
  "isActive": true,
  "createdAt": "2022-10-29T00:41:28.717Z",
  "updatedAt": "2022-10-29T00:41:28.717Z"
}
```

**POST** `/login` — Authenticate user

```json
// Request
{ "email": "thiago@mail.com", "password": "1234" }

// Response 200
{ "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..." }
```

**GET** `/users` — List all users — Admin required

**GET** `/users/:id` — Get user by id — Admin or Employee required

**PATCH** `/users/:id` — Update user — Auth required

**DELETE** `/users/:id` — Soft delete user — Admin required

### Movies

**POST** `/movies` — Create movie — Auth required

```json
// Request
{
  "name": "Jason 5",
  "gender": "Horror",
  "avaliation": "4.3",
  "duration": "2:00",
  "onDisplay": true,
  "cinema": "1"
}

// Response 201
{
  "id": 4,
  "name": "Jason 5",
  "gender": "Horror",
  "avaliation": "4.3",
  "duration": "2:00",
  "onDisplay": true,
  "cinema": { "id": 1, "name": "Cine Express" }
}
```

**GET** `/movies` — List all movies — Auth required

**GET** `/movies/:id` — Get movie by id — Auth required

**PATCH** `/movies/:id` — Update movie — Employee required

**DELETE** `/movies/:id` — Delete movie — Admin required

### Sessions

**POST** `/sessions` — Create session — Auth required

```json
// Request
{ "day": "2022/11/12", "hour": "13:00", "room_id": "1", "movie_id": "1" }

// Response 201
{
  "id": 4,
  "day": "2022-11-15",
  "hour": "19:00:00",
  "room": { "id": 1, "capacity": 100 },
  "movie": { "id": 1, "name": "A Família Adams", "onDisplay": true }
}
```

**GET** `/sessions` — List all sessions — Auth required

**GET** `/sessions/movie/:movieId` — List sessions by movie — Auth required

**PATCH** `/sessions/:id` — Update session — Employee required

**DELETE** `/sessions/:id` — Delete session — Admin required

### Tickets

**POST** `/tickets` — Purchase ticket — Auth required

```json
// Request
{ "chair": "5", "session": 2, "user": "1597a7b4-24e5-4856-a52c-70576459de11" }

// Response 201
{
  "id": "d1eaa744-85d5-4eef-8f38-53a92320e786",
  "chair": "5",
  "price": 15,
  "session": { "id": 2, "day": "2022-11-10", "hour": "15:00:00" }
}
```

**GET** `/tickets` — List all tickets — Employee required

**GET** `/tickets/:id` — Get ticket by id — Auth required

### Cinema

**POST** `/cinema` — Create cinema — Auth required

**GET** `/cinema` — List all cinemas — Auth required

**PATCH** `/cinema/:id` — Update cinema — Employee required

### Rooms

**POST** `/rooms` — Create room (30–100 seats) — Auth required

**GET** `/rooms` — List all rooms — Auth required

**GET** `/rooms/:id` — Get room by id — Auth required

**PATCH** `/rooms/:id` — Update room — Admin and Employee required

### Payments

**POST** `/paymentInfo` — Add payment info — Auth required

**GET** `/paymentInfo` — List user payment info — Auth required

**GET** `/paymentInfo/:id` — Get payment info by id — Auth required

**PATCH** `/paymentInfo/:id` — Update payment info — Auth required

**DELETE** `/paymentInfo/:id` — Delete payment info — Auth required

## Team

- [Thiago A. Scherer](https://www.linkedin.com/in/thiago-araujo-scherer/) — Scrum Master
- [Larissa Sato](https://www.linkedin.com/in/larissa-sato-51a835222/) — Tech Lead
- [Amon Fanticelli](https://www.linkedin.com/in/amon-fanticelli/) — Product Owner
- [Ricardo Martins](https://www.linkedin.com/in/ormartins02/) — Developer
- [Leandro Junges](https://www.linkedin.com/in/leandro-junges/) — Developer
- [João Victor](https://www.linkedin.com/in/joao-victor-lemos/) — Developer
