# Task Management API

A RESTful API for managing tasks and projects, built with Node.js, Express, and PostgreSQL.

## Overview

This API provides task management functionality including:
- User authentication and authorization
- Project creation and management
- Task CRUD operations with assignments
- Task status tracking and filtering
- Team collaboration features

## Tech Stack

- **Runtime**: Node.js 18+
- **Framework**: Express.js 4.x
- **Language**: TypeScript 5.x (strict mode)
- **Database**: PostgreSQL 14+
- **ORM**: Prisma 5.x
- **Authentication**: JWT (jsonwebtoken)
- **Testing**: Jest with supertest
- **Validation**: Joi
- **Documentation**: OpenAPI/Swagger

## Architecture

This project follows a layered architecture pattern:

```
┌─────────────────────┐
│   API Endpoints     │  HTTP layer: request/response handling
├─────────────────────┤
│   Services          │  Business logic layer
├─────────────────────┤
│   Models/Prisma     │  Data access layer
├─────────────────────┤
│   PostgreSQL        │  Data storage
└─────────────────────┘
```

### Folder Structure

```
/
├── src/
│   ├── api/
│   │   ├── endpoints/      # API endpoint handlers
│   │   ├── middleware/     # Express middleware
│   │   └── routes.ts       # Route registration
│   ├── services/           # Business logic
│   ├── models/             # Data models and types
│   ├── utils/              # Utility functions
│   ├── config/             # Configuration
│   └── index.ts            # Application entry point
├── tests/
│   ├── api/                # API integration tests
│   ├── services/           # Service unit tests
│   └── fixtures/           # Test data
├── docs/
│   ├── API.md              # API documentation
│   ├── ARCHITECTURE.md     # Architecture decisions
│   └── DEPLOYMENT.md       # Deployment guide
├── prisma/
│   ├── schema.prisma       # Database schema
│   └── migrations/         # Database migrations
├── .claude/
│   ├── rules.md            # Claude coding rules
│   └── skills/             # Custom skills
└── scripts/                # Utility scripts
```

## Quick Start

### Prerequisites

- Node.js 18+ installed
- PostgreSQL 14+ running
- npm or yarn package manager

### Installation

```bash
# Clone the repository
git clone <repository-url>
cd task-management-api

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Edit .env with your configuration

# Set up database
npm run db:migrate

# Seed database with sample data (optional)
npm run db:seed
```

### Running the Application

```bash
# Development mode (with hot reload)
npm run dev

# Production mode
npm run build
npm start

# Run tests
npm test

# Run tests with coverage
npm run test:coverage

# Lint code
npm run lint

# Format code
npm run format
```

### API Endpoints

Once running, the API is available at `http://localhost:3000`

**Core endpoints:**
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/projects` - List projects
- `POST /api/projects` - Create project
- `GET /api/tasks` - List tasks
- `POST /api/tasks` - Create task
- `PUT /api/tasks/:id` - Update task
- `DELETE /api/tasks/:id` - Delete task

See [API Documentation](docs/API.md) for complete endpoint reference.

## Development Guidelines

### Code Style

We follow strict TypeScript and ESLint rules:
- TypeScript strict mode enabled
- ESLint with Airbnb configuration
- Prettier for code formatting
- 2 spaces indentation, single quotes, semicolons required

### Testing

- All services must have unit tests
- All endpoints must have integration tests
- Minimum test coverage: 80%
- Use Jest with describe/it structure
- Follow Arrange-Act-Assert pattern

### Documentation

- All exported functions require JSDoc comments
- All public APIs documented in docs/API.md
- Complex logic includes inline comments
- Architectural decisions recorded in docs/ARCHITECTURE.md

### Git Workflow

- Feature branches: `feature/feature-name`
- Bug fixes: `fix/bug-description`
- Commit messages follow conventional commits format
- All commits must pass tests and linting

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

## Project Structure Explained

### `/src/api/endpoints`
Contains HTTP endpoint handlers. Each file exports handler functions that:
- Extract and validate request data
- Call appropriate service methods
- Format and return responses
- Handle errors with appropriate status codes

### `/src/services`
Contains business logic. Services are stateless classes with static methods that:
- Implement business rules
- Perform data validation
- Orchestrate database operations
- Throw domain-specific errors

### `/src/models`
Contains TypeScript interfaces and types for:
- Database entities
- API request/response shapes
- Domain objects
- Validation schemas

### `/src/utils`
Shared utility functions for:
- Validation helpers
- Date/time utilities
- Error handling
- Common transformations

## Environment Variables

Required environment variables:

```bash
# Server
PORT=3000
NODE_ENV=development

# Database
DATABASE_URL=postgresql://user:password@localhost:5432/taskdb

# Authentication
JWT_SECRET=your-secret-key
JWT_EXPIRATION=24h

# CORS
CORS_ORIGIN=http://localhost:3000
```

See `.env.example` for complete list.

## Database Schema

Key entities:
- **Users**: User accounts and authentication
- **Projects**: Project containers for tasks
- **Tasks**: Individual tasks with status and assignments
- **Teams**: User groups for collaboration

See `prisma/schema.prisma` for complete schema.

## API Documentation

Comprehensive API documentation available at:
- Local: `http://localhost:3000/api-docs` (when running)
- Markdown: [docs/API.md](docs/API.md)

## Testing

```bash
# Run all tests
npm test

# Run specific test file
npm test -- tasks.test.ts

# Run tests in watch mode
npm test -- --watch

# Generate coverage report
npm run test:coverage
```

## Deployment

See [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md) for deployment instructions covering:
- Production environment setup
- Database migration strategies
- CI/CD pipeline configuration
- Monitoring and logging

## Troubleshooting

### Common Issues

**Database connection fails:**
- Verify PostgreSQL is running
- Check DATABASE_URL in .env
- Ensure database exists

**Tests failing:**
- Run `npm run db:reset` to reset test database
- Check test environment variables
- Verify test fixtures are valid

**Build errors:**
- Clear `node_modules` and reinstall: `rm -rf node_modules && npm install`
- Clear TypeScript cache: `rm -rf dist`

## Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for:
- Code of conduct
- Development setup
- Coding standards
- Pull request process
- Testing requirements

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Support

- Documentation: [docs/](docs/)
- Issues: [GitHub Issues](https://github.com/yourorg/task-api/issues)
- Discussions: [GitHub Discussions](https://github.com/yourorg/task-api/discussions)

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for version history and release notes.

---

Built with ❤️ using Claude Code for AI-assisted development.
