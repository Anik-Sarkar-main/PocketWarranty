# Overview

My Bills & Warranty is a digital receipt and warranty management application designed to help users store, organize, and track their purchase receipts and warranties. The application provides features such as bill storage with image capture, warranty expiry tracking, reminder notifications, and the ability to share bill details. It's built as a Progressive Web App (PWA) with offline capabilities and push notifications.

# User Preferences

Preferred communication style: Simple, everyday language.

# System Architecture

## Frontend Architecture

The client-side is built using **React with TypeScript** and follows a modern single-page application (SPA) pattern. The UI leverages **shadcn/ui** components for a consistent design system built on top of **Radix UI primitives** and **Tailwind CSS** for styling. The application uses **Wouter** for client-side routing instead of React Router, providing a lightweight navigation solution.

State management is handled through **TanStack Query (React Query)** for server state management and caching, while local component state is managed using React's built-in hooks. Form validation and handling is implemented using **React Hook Form** with **Zod** schema validation.

The application supports PWA features including service workers for offline functionality, push notifications for warranty reminders, and installable app capabilities through the manifest.json configuration.

## Backend Architecture

The server is built using **Express.js** with TypeScript in an ESM module format. The architecture follows a simple REST API pattern with route-based organization. The server implements middleware for request logging, JSON parsing, and error handling.

Currently, the application uses an **in-memory storage** implementation for development purposes, but the architecture is designed with a storage abstraction layer (IStorage interface) that can be easily swapped for database persistence. The storage interface defines methods for user and bill management operations.

## Authentication System

Authentication is handled through **Firebase Authentication**, supporting multiple providers including Google OAuth and email/password authentication. The client-side authentication state is managed through a custom `useAuth` hook that provides login, registration, and logout functionality. Firebase users are synchronized with the application's internal user management system.

## File Storage and Image Handling

The application integrates with **Firebase Storage** for handling bill image uploads. Users can capture photos directly through the camera interface or upload existing images. Images are processed on the client-side using HTML5 Canvas API before being uploaded to Firebase Storage.

## Database Schema

The application defines a PostgreSQL-compatible schema using **Drizzle ORM**, even though it currently uses in-memory storage. The schema includes:

- **Users table**: Stores user profiles with Firebase UID integration
- **Bills table**: Stores bill/receipt information with foreign key relationships to users
- Support for UUID primary keys and automatic timestamp management
- Category-based organization for bills with predefined categories

## Real-time Features and Notifications

The application implements a notification system for warranty expiry reminders using:

- Service worker for background processing
- Browser Notification API for push notifications
- Scheduled reminders at 5, 3, 2, and 1 days before warranty expiry
- Background sync capabilities for offline functionality

# External Dependencies

## Core Technologies
- **React 18** with TypeScript for frontend development
- **Express.js** for backend API server
- **Vite** for build tooling and development server
- **Tailwind CSS** for utility-first styling
- **Node.js** runtime environment

## UI Component Libraries
- **Radix UI** primitives for accessible, unstyled components
- **shadcn/ui** for pre-built component implementations
- **Lucide React** for iconography
- **Class Variance Authority** for component variant management

## State Management and Data Fetching
- **TanStack Query** for server state management and caching
- **React Hook Form** for form state management
- **Zod** for runtime type validation and schema definition

## Authentication and Storage
- **Firebase Authentication** for user authentication
- **Firebase Storage** for file/image storage
- **Firebase SDK** for client-side integration

## Database and ORM
- **Drizzle ORM** for type-safe database operations
- **Drizzle Kit** for database migrations and management
- **@neondatabase/serverless** as the PostgreSQL client
- **PostgreSQL** as the target database (configured but not yet implemented)

## Development and Build Tools
- **TypeScript** for type safety
- **ESBuild** for server-side bundling
- **PostCSS** with Autoprefixer for CSS processing
- **@replit/vite-plugin-runtime-error-modal** for development error handling
- **@replit/vite-plugin-cartographer** for Replit integration

## Utility Libraries
- **date-fns** for date manipulation and formatting
- **clsx** and **tailwind-merge** for conditional class handling
- **nanoid** for unique ID generation
- **wouter** for lightweight client-side routing