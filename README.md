# JwtAuthentication

A full-stack project demonstrating JWT-based authentication using ASP.NET Core (C#) for the backend and React (TypeScript, Vite) for the frontend.

## Project Structure

- **JwtAuthentication.Server/**: ASP.NET Core Web API server for authentication and user management.
- **JwtAuthentication.DAL/**: Data access layer (Entity Framework Core) for database operations.
- **jwtauthentication.client/**: React frontend (TypeScript, Vite) for user interface.

## Prerequisites

- [.NET 8 SDK](https://dotnet.microsoft.com/download)
- [Node.js & npm](https://nodejs.org/)

## Getting Started

### 1. Backend Setup

1. Navigate to the server directory:
   ```sh
   cd JwtAuthentication.Server
   ```
2. Restore dependencies and run migrations:
   ```sh
   dotnet restore
   dotnet ef database update
   ```
3. Run the server:
   ```sh
   dotnet run
   ```

### 2. Frontend Setup

1. Navigate to the client directory:
   ```sh
   cd jwtauthentication.client
   ```
2. Install dependencies:
   ```sh
   npm install
   ```
3. Start the development server:
   ```sh
   npm run dev
   ```

The frontend will be available at [http://localhost:5173](http://localhost:5173) by default.

## Features

- User registration and login
- JWT authentication
- Protected routes on frontend
- Entity Framework Core migrations

## Useful Commands

- **Backend:**
  - Run: `dotnet run` (in `JwtAuthentication.Server`)
  - Migrate DB: `dotnet ef database update`
- **Frontend:**
  - Start: `npm run dev` (in `jwtauthentication.client`)

## Demo

Live demo: https://jwtauthentication.paweldywan.com/

## License

MIT License
