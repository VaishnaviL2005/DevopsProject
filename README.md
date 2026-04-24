# Dev Forum

Dev Forum is an online platform where software developers can showcase their portfolios, bid on projects, and connect with recruiters to get hired.

<img alt='screenshot' src='https://mir-s3-cdn-cf.behance.net/project_modules/fs_webp/508a45121098563.68c131f10f6fb.png' />

## Stack

- Next.js 14 (App Router)
- Shadcn/UI
- Tailwind CSS
- Prisma/Postgres
- Docker (for containerized setup)

---

# Setup & Installation

## Option 1: Docker Setup (Recommended)

> Prerequisite: Install Docker Desktop (Windows/Mac) or Docker Engine (Linux)

### Clone the repository

```cmd
git clone https://github.com/saifulshihab/dev-forum.git
cd dev-forum
````

### Configure environment file

```cmd
cp .env.example .env
```

Open `.env` and set all required values.

Example:

```env
NEXTAUTH_URL=http://localhost:3000
DATABASE_URL=postgresql://postgres:admin123@host.docker.internal:5433/devforum?schema=public
```

### Start PostgreSQL in Docker

```cmd
docker run --name devforum-postgres ^
-e POSTGRES_USER=postgres ^
-e POSTGRES_PASSWORD=admin123 ^
-e POSTGRES_DB=devforum ^
-p 5433:5432 ^
-d postgres:15
```

### Build Docker image

```cmd
docker build -t devforum-app .
```

### Run application container

```cmd
docker run --name devforum-app -p 3000:3000 --env-file .env devforum-app
```

### Access Application

```text
http://localhost:3000
```

This setup runs:

- PostgreSQL database inside Docker
- Dev Forum application inside Docker

Docker provides a portable runtime environment for the application. 
Some initial project setup steps such as Prisma generation may require local Node.js.

---

## Option 2: Manual Local Setup

### Clone the repository

```cmd
git clone https://github.com/saifulshihab/dev-forum.git
cd dev-forum
```

### Install dependencies

```cmd
npm install
```

### Environment variables

Copy `.env.example` to `.env`

```cmd
cp .env.example .env
```

Open `.env` and set all necessary values.

### Database setup with Prisma

Generate Prisma client:

```cmd
npx prisma generate
```

Run migrations:

```cmd
npx prisma migrate deploy
```

or for development:

```cmd
npx prisma migrate dev
```

### Build / Start application

Development mode:

```cmd
npm run dev
```

Production build:

```cmd
npm run build
npm start
```

---

## Live

```
```
