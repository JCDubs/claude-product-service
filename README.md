# Product Service API

A serverless API for managing products, built with AWS CDK, following clean architecture principles and implementing the Microsoft Common Data Model for products.

## Architecture

This project implements a serverless architecture using AWS services:

- **API Gateway**: RESTful API endpoints
- **Lambda**: Business logic and request handling using NodeJS Lambda construct with esbuild
- **DynamoDB**: Data storage using single-table design
- **Cognito**: Authentication and authorization
- **CloudWatch**: Monitoring and alerting

The codebase follows clean architecture principles with a clear separation of concerns:

```
/lib
  /core              # Domain models, interfaces, business logic
  /adapters          # External adapters (DynamoDB, etc.)
  /handlers          # Lambda handlers
  /validation        # Validation schemas
  /constructs        # CDK constructs
```

## Features

- Complete CRUD operations for products
- Microsoft Common Data Model implementation
- OAuth2 authentication with Amazon Cognito
- Strict validation using Joi
- Single-table DynamoDB design
- AWS SDK v3 for improved modularity and reduced bundle size
- Comprehensive monitoring with CloudWatch alarms and dashboard for API Gateway, Lambda, and DynamoDB
- Lambda functions bundled with esbuild for optimal performance
- Unit tests with Jest
- End-to-end tests with Postman/Newman

## Prerequisites

- Node.js 18.x or later
- AWS CLI configured with appropriate credentials
- AWS CDK installed globally (`npm install -g aws-cdk`)

## Installation

1. Clone the repository
2. Install dependencies:

```bash
npm install
```

3. Build the project:

```bash
npm run build
```

## Deployment

1. Bootstrap your AWS environment (if not already done):

```bash
cdk bootstrap
```

2. Deploy the stack:

```bash
npm run deploy
```

## Testing

### Unit Tests

Run the unit tests:

```bash
npm test
```

### End-to-End Tests

1. Update the Postman environment variables in `test/e2e/environment.json` with your deployed API details.
2. Run the Postman collection using Newman:

```bash
npm run postman
```

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | /products | Create a new product |
| GET | /products | List products with optional filtering |
| GET | /products/{id} | Get a product by ID |
| PUT | /products/{id} | Update a product |
| DELETE | /products/{id} | Delete a product |

## Authentication

The API uses Amazon Cognito for authentication. To access the API:

1. Create a user in the Cognito User Pool
2. Obtain an ID token using the Cognito authentication flow
3. Include the ID token in the `Authorization` header as a Bearer token

## Product Model

The product model follows the Microsoft Common Data Model and includes:

- Basic information (name, description)
- Categorization (productType, productCategory)
- Identification (SKU, GTIN)
- Pricing information
- Physical attributes (dimensions, weight)
- Media references
- Related products

## Development

### Project Structure

- `bin/`: CDK app entry point
- `lib/`: Main source code
  - `core/`: Domain models and business logic
  - `adapters/`: External adapters (e.g., DynamoDB)
  - `handlers/`: Lambda function handlers
  - `validation/`: Input validation schemas
  - `constructs/`: CDK infrastructure constructs
- `test/`: Test files
  - `unit/`: Unit tests
  - `e2e/`: End-to-end tests with Postman

### Adding New Features

1. Define domain models in `lib/core/models/`
2. Create repository interfaces in `lib/core/ports/`
3. Implement use cases in `lib/core/use-cases/`
4. Add validation schemas in `lib/validation/`
5. Implement adapters in `lib/adapters/`
6. Create Lambda handlers in `lib/handlers/`
7. Update CDK constructs in `lib/constructs/`
8. Add tests in `test/`

## License

MIT
