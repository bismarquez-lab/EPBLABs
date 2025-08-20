# Overview

This is a file sharing application built for EPB (Escola Particular Brasileira) that allows users to upload, manage, and share educational files. The system features Microsoft Authenticator integration for login, file categorization, GitHub integration for version control, and a modern web interface built with React and shadcn/ui components.

# User Preferences

Preferred communication style: Simple, everyday language.

# System Architecture

## Frontend Architecture
- **Framework**: React with TypeScript using Vite for development and building
- **UI Components**: shadcn/ui component library with Radix UI primitives
- **Styling**: Tailwind CSS with custom design tokens and glass morphism effects
- **State Management**: TanStack React Query for server state and React Context for authentication
- **Routing**: Wouter for client-side routing
- **Forms**: React Hook Form with Zod validation

## Backend Architecture
- **Runtime**: Node.js with Express.js server
- **Database**: PostgreSQL with Drizzle ORM for type-safe database operations
- **Authentication**: JWT-based authentication with bcrypt for password hashing
- **File Storage**: Local file system with multer for file upload handling
- **Session Management**: Express sessions with PostgreSQL session store

## Database Schema (Supabase)
- **Users**: Authentication and profile information with Microsoft ID and optional GitHub integration
- **Files**: File metadata, storage paths, categorization, and GitHub commit tracking
- **Shared Folders**: Organized collections of files for educational content sharing

## Authentication & Authorization
- **Microsoft Authenticator Integration**: Primary authentication method using Azure AD/Microsoft Entra ID
- **MSAL Library**: Uses @azure/msal-react and @azure/msal-browser for secure authentication
- **JWT token-based authentication**: Tokens stored in localStorage for session management
- **Multi-provider support**: Microsoft Authentication, traditional email/password, and GitHub OAuth
- **Protected routes**: All routes requiring valid authentication tokens
- **Automatic account linking**: Microsoft accounts can be linked to existing email accounts

## File Management System
- Multi-part file uploads with size limits (50MB)
- Automatic file categorization and metadata extraction
- User-specific file organization in separate directories
- File versioning through GitHub integration
- Support for various file types with MIME type detection

## External Dependencies

### Database & ORM
- **Supabase**: PostgreSQL database with real-time features and built-in authentication
- **postgres-js**: High-performance PostgreSQL client optimized for Supabase
- **Drizzle ORM**: Type-safe SQL toolkit for database operations

### Authentication & Security
- **bcrypt**: Password hashing and verification
- **jsonwebtoken**: JWT token generation and validation

### File Processing
- **multer**: Multipart file upload middleware
- **file-type detection**: Automatic MIME type identification

### GitHub Integration
- **GitHub API**: Version control integration for file commits
- **GitHub OAuth**: Optional social authentication

### Microsoft Authentication
- **@azure/msal-react**: React integration for Microsoft Authentication Library
- **@azure/msal-browser**: Browser-based Microsoft authentication
- **@azure/msal-node**: Server-side token validation (if needed)

### UI & Styling
- **shadcn/ui**: Pre-built accessible component library
- **Radix UI**: Unstyled accessible UI primitives
- **Tailwind CSS**: Utility-first CSS framework
- **Lucide React**: Icon library

### Development Tools
- **Vite**: Fast development server and build tool
- **TypeScript**: Type safety across the entire stack
- **TanStack React Query**: Server state management and caching

## Microsoft Authentication Setup

### Step 1: Azure App Registration
1. Go to [Azure Portal](https://portal.azure.com) → App registrations
2. Click "New registration"
3. Configure:
   - **Name**: EPB File Sharing System
   - **Account types**: Accounts in any organizational directory and personal Microsoft accounts
   - **Redirect URI**: Single-page application → `http://localhost:5000` (for development)
4. Note the **Application (client) ID**

### Step 2: Configure Permissions
1. In your app registration, go to "API permissions"
2. Add Microsoft Graph permissions:
   - `User.Read` (to read user profile)
   - `profile` (for basic profile information)
   - `email` (for email access)

### Step 3: Environment Configuration
Create a `.env` file based on `.env.example`:
```env
VITE_MICROSOFT_CLIENT_ID="your-client-id-from-azure"
VITE_MICROSOFT_AUTHORITY="https://login.microsoftonline.com/common"
```

### Step 4: Production Setup
For production deployment:
1. Update redirect URI in Azure to your production domain
2. Configure proper CORS settings
3. Consider using a specific tenant instead of "common" for better security

## Supabase Database Setup

### Step 1: Create Supabase Project
1. Go to [Supabase dashboard](https://supabase.com/dashboard/projects)
2. Create a new project if you haven't already
3. Once in the project page, click the "Connect" button on the top toolbar
4. Copy URI value under "Connection string" -> "Transaction pooler"
5. Replace `[YOUR-PASSWORD]` with the database password you set for the project

### Step 2: Configure Environment
Add to your `.env` file:
```env
DATABASE_URL="postgresql://postgres.PROJECT_REF:PASSWORD@aws-0-sa-east-1.pooler.supabase.com:6543/postgres?sslmode=require"
```

### Step 3: Run Database Migration
Execute `npm run db:push` to create the database schema in Supabase.