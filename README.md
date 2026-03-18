# JwtAuthentication

A full-stack web application demonstrating JWT-based authentication using ASP.NET Core Identity API with React frontend. This project showcases modern authentication patterns, Entity Framework Core with PostgreSQL, and a Single Page Application (SPA) architecture.

## Application URL

Live Application: https://jwtauthentication.paweldywandev.com/

Development: https://localhost:7253

## Overview

JwtAuthentication is a comprehensive authentication solution built on .NET 8 and React. It implements cookie-based authentication with ASP.NET Core Identity API endpoints, providing a secure and scalable foundation for web applications requiring user authentication and authorization. The application uses PostgreSQL for data persistence and includes automatic database seeding for development environments.

## Key Features

- Cookie-based authentication using ASP.NET Core Identity API endpoints
- User registration and login with ASP.NET Core Identity
- Secure password hashing and validation
- Protected API routes with authorization middleware
- Entity Framework Core with PostgreSQL database
- Automatic database migrations and seeding
- Data Protection API with key persistence
- React frontend with TypeScript and Vite
- Bootstrap-based responsive UI with Reactstrap
- React Router for client-side routing
- Development and production environment configurations
- Docker support with Linux containers
- Swagger/OpenAPI documentation
- SPA proxy for seamless development experience

## Architecture

This solution follows a multi-layered architecture pattern:

```
JwtAuthentication/
|
+-- JwtAuthentication.Server/
|   |   (ASP.NET Core Web API - .NET 8)
|   |   Main web server hosting API endpoints
|   |   and serving the React SPA
|   |
|   +-- Controllers/
|   |   +-- UserController.cs
|   |       (Custom user API endpoints)
|   |
|   +-- Program.cs
|   |   (Application entry point, service
|   |    configuration, middleware pipeline)
|   |
|   +-- appsettings.json
|       (Application configuration)
|
+-- JwtAuthentication.DAL/
|   |   (Data Access Layer - .NET 8)
|   |   Entity Framework Core context,
|   |   migrations, and database seeding
|   |
|   +-- JwtAuthenticationContext.cs
|   |   (DbContext with Identity and
|   |    Data Protection integration)
|   |
|   +-- SampleData/
|   |   +-- JwtAuthenticationSeeder.cs
|   |       (Database seeding logic)
|   |
|   +-- Migrations/
|       (EF Core migration files)
|
+-- jwtauthentication.client/
    |   (React SPA - TypeScript + Vite)
    |   Frontend application with
    |   authentication UI
    |
    +-- src/
    |   (React components and pages)
    |
    +-- package.json
    |   (Node.js dependencies and scripts)
    |
    +-- vite.config.ts
        (Vite configuration)
```

### Project Dependencies

```
JwtAuthentication.Server
    |
    +-- References:
        |
        +-- JwtAuthentication.DAL
        |
        +-- jwtauthentication.client (SPA Proxy)
```

## Getting Started

### Prerequisites

- .NET 8 SDK or later
- Node.js 18.x or later with npm
- PostgreSQL 12 or later
- Visual Studio 2022 or Visual Studio Code (optional)
- Docker Desktop (optional, for containerized deployment)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/paweldywandev/JwtAuthentication.git
cd JwtAuthentication
```

2. Configure the database connection:

   Create or edit `JwtAuthentication.Server/appsettings.json` or use User Secrets:
   ```json
   {
     "ConnectionStrings": {
       "DefaultConnection": "Host=localhost;Database=JwtAuthDb;Username=your_username;Password=your_password"
     }
   }
   ```

3. Restore .NET dependencies:
```bash
cd JwtAuthentication.Server
dotnet restore
```

4. Install frontend dependencies:
```bash
cd ../jwtauthentication.client
npm install
```

### Running the Application

#### Option 1: Visual Studio

1. Open `JwtAuthentication.sln` in Visual Studio 2022
2. Set `JwtAuthentication.Server` as the startup project
3. Press F5 to run with debugging

The application will automatically:
- Apply pending database migrations
- Seed the database with sample data
- Start the backend server
- Launch the React development server via SPA Proxy
- Open your browser to https://localhost:7253

#### Option 2: Command Line

1. Start the backend server:
```bash
cd JwtAuthentication.Server
dotnet run
```

2. In a separate terminal, start the frontend development server:
```bash
cd jwtauthentication.client
npm run dev
```

3. Access the application:
   - Frontend: https://localhost:5173 (Vite dev server)
   - Backend API: https://localhost:7253
   - Swagger UI: https://localhost:7253/swagger

#### Option 3: Docker

Build and run using Docker:
```bash
docker build -t jwtauthentication .
docker run -p 8080:8080 -p 8081:8081 jwtauthentication
```

### Default User Credentials

For development and testing, a default user is automatically created:

- Email/Username: `paweldywandev@paweldywandev.com`
- Password: `P@ssw0rd`

**Important:** Change or remove this user in production environments.

### Database Migrations

The application automatically applies pending migrations on startup in development mode. To manually manage migrations:

Create a new migration:
```bash
cd JwtAuthentication.DAL
dotnet ef migrations add MigrationName --startup-project ../JwtAuthentication.Server
```

Apply migrations:
```bash
dotnet ef database update --startup-project ../JwtAuthentication.Server
```

Remove the last migration:
```bash
dotnet ef migrations remove --startup-project ../JwtAuthentication.Server
```

## Technology Stack

### Backend
- **Framework:** ASP.NET Core 8.0 (Web API)
- **Authentication:** ASP.NET Core Identity with Identity API Endpoints
- **ORM:** Entity Framework Core 8.0
- **Database:** PostgreSQL (via Npgsql.EntityFrameworkCore.PostgreSQL 8.0.10)
- **Security:** 
  - ASP.NET Core Data Protection with EF Core key persistence
  - ASP.NET Core Identity with hashed passwords
- **API Documentation:** Swashbuckle (Swagger/OpenAPI)
- **Development Tools:**
  - Entity Framework Core Tools
  - Database Developer Page Exception Filter
  - User Secrets

### Frontend
- **Framework:** React 18.3.1
- **Language:** TypeScript 5.6.3
- **Build Tool:** Vite 5.4.10
- **UI Library:** 
  - Bootstrap 5.3.3
  - Reactstrap 9.2.3
- **Routing:** React Router DOM 6.27.0
- **Code Quality:**
  - ESLint 9.13.0
  - TypeScript ESLint 8.12.2

### Infrastructure
- **Containerization:** Docker with Linux containers
- **Hosting:** ASP.NET Core Kestrel web server
- **SPA Integration:** ASP.NET Core SPA Proxy

## API Documentation

### Authentication Endpoints

The application uses ASP.NET Core Identity API endpoints which are automatically mapped:

#### Register a new user
```
POST /register
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "YourSecurePassword123!"
}
```

#### Login
```
POST /login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "YourSecurePassword123!",
  "useCookies": true
}
```

#### Logout
```
POST /logout
Authorization: Required (authenticated user)

{}
```

### Custom User Endpoints

#### Login (Legacy)
```
GET /api/User/Login?user=username&password=password
```

**Response:**
- 200 OK - Login successful
- 401 Unauthorized - Invalid credentials

#### Get Current User Name
```
GET /api/User/Name
Authorization: Required (authenticated user)
```

**Response:**
- 200 OK - Returns username
- 401 Unauthorized - Not authenticated

### Swagger Documentation

Interactive API documentation is available in development mode at:
```
https://localhost:7253/swagger
```

## Project Configuration

### Backend Configuration

Key configuration in `Program.cs`:

- **Database:** PostgreSQL with EF Core
- **Identity:** Cookie-based authentication, password requirements
- **Data Protection:** Keys persisted to database
- **CORS:** Configured for development SPA proxy
- **Static Files:** Serves React build output
- **Fallback Route:** SPA fallback to index.html

### Frontend Configuration

Vite configuration (`vite.config.ts`) includes:
- HTTPS proxy to backend API
- Development server on port 5173
- React plugin with Fast Refresh
- Build output to `dist/` directory

## Development

### Project Structure Conventions

- **Controllers:** RESTful API controllers in `JwtAuthentication.Server/Controllers/`
- **Data Context:** EF Core DbContext in `JwtAuthentication.DAL/`
- **Migrations:** Database migrations in `JwtAuthentication.DAL/Migrations/`
- **Seeding:** Data seeding logic in `JwtAuthentication.DAL/SampleData/`
- **Frontend:** React components in `jwtauthentication.client/src/`

### Building for Production

Build the entire solution:
```bash
dotnet build JwtAuthentication.sln --configuration Release
```

Build the React frontend:
```bash
cd jwtauthentication.client
npm run build
```

The production build will be output to `jwtauthentication.client/dist/` and is automatically served by the ASP.NET Core server.

### Code Quality

Run frontend linting:
```bash
cd jwtauthentication.client
npm run lint
```

## Contributing

Contributions are welcome! Please follow these guidelines:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/YourFeature`)
3. Commit your changes (`git commit -m 'Add some feature'`)
4. Push to the branch (`git push origin feature/YourFeature`)
5. Open a Pull Request

Please ensure your code:
- Follows existing code style and conventions
- Includes appropriate error handling
- Updates documentation as needed
- Passes all existing tests

## License

This project is licensed under the MIT License. See the LICENSE file for details.

## Author

**Pawel Dywan**

- GitHub: [@paweldywandev](https://github.com/paweldywandev)
- Website: https://paweldywandev.com/

## Acknowledgments

- ASP.NET Core Identity team for the authentication framework
- Entity Framework Core team for the ORM
- React team for the frontend framework
- Vite team for the blazing fast build tool
- PostgreSQL community for the robust database system
- Bootstrap and Reactstrap teams for the UI components

