Let me search through the codebase to understand the platform API and web structure.


Search files...
Let me try a different approach by looking at the directory structure first.


Ran tool
I can see there are two main directories: `exto-platform-web` and `exto-platform-api`. Let me examine each one to give you a high-level overview.

Let's look at the API structure first:


Ran tool
Now let's look at the web structure:



Ran tool
Based on the directory structures, I can provide you with a high-level overview of both the platform API and web components:

### Platform API (exto-platform-api)
This is a Node.js/TypeScript-based backend service with the following key characteristics:

1. **Architecture**:
   - Uses a monorepo structure with NX workspace
   - Contains multiple apps and libraries in the `apps/` and `libs/` directories
   - Includes worker processes for background tasks

2. **Key Technologies**:
   - TypeScript-based development
   - MongoDB as the database (evident from migration files and MongoDB configs)
   - Swagger for API documentation
   - Jest for testing
   - Docker support for containerization

3. **Development Features**:
   - Comprehensive testing setup (Jest, MongoDB test config)
   - Code quality tools (ESLint, Prettier)
   - Git hooks and pre-commit checks
   - Migration support for database changes
   - CI/CD integration (Azure pipelines)

### Platform Web (exto-platform-web)
This is an Angular-based frontend application with the following characteristics:

1. **Architecture**:
   - Angular-based SPA (Single Page Application)
   - Nginx configuration for serving the application
   - Proxy configuration for development

2. **Key Technologies**:
   - Angular framework
   - TypeScript
   - Karma and Protractor for testing
   - Docker support for containerization

3. **Development Features**:
   - Modern development tooling (ESLint, Prettier)
   - CI/CD integration (Azure pipelines, Bitbucket pipelines)
   - Internationalization support (`.lingua` file)
   - Development and production Docker configurations
   - Build automation scripts

### Integration
The two components work together as a full-stack application:
- The web frontend communicates with the API backend
- The API provides the necessary endpoints and business logic
- Both components have their own containerization setup for deployment
- They share similar development practices and tooling for consistency

This appears to be a modern, well-structured enterprise application with proper separation of concerns between frontend and backend, along with comprehensive development and deployment tooling.
