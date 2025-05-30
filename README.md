



## Architecture

The system consists of two main components:

1. **Express API Server**: Receives code submissions from users and queues them in Redis
2. **Worker Service**: Processes submissions from the queue and evaluates the code

## Components

### Express API Server

The API server provides endpoints for submitting code:

- **POST /submit**: Accepts code submissions with problemId, code, and language
- Submissions are pushed to a Redis queue for asynchronous processing

### Worker Service

The worker:
- Continuously polls the Redis queue for new submissions
- Processes each submission by executing the code (using Docker for isolation)
- Handles results and provides feedback

## Technology Stack

- **Backend**: Node.js with TypeScript
- **API**: Express.js
- **Message Queue**: Redis
- **Code Execution**: Docker (planned)

## Setup

### Prerequisites

- Node.js (latest LTS version)
- Redis server
- Docker (for code execution)

### Installation

1. Clone the repository
```bash
git clone <repository-url>
```

2. Install dependencies for Express server
```bash
cd express
npm install
npm run build
```

3. Install dependencies for Worker
```bash
cd ../worker
npm install
npm run build
```

### Running the Application

1. Start Redis server
```bash
redis-server
or

docker run --name my-redis-3 -d -p 6379:6379 redis
```

2. Start the Express API server
```bash
cd express
npm start
```

3. Start the Worker service
```bash
cd worker
npm start
```

## API Usage

Submit code for evaluation:
```bash
curl -X POST http://localhost:3000/submit -H "Content-Type: application/json" -d '{
  "problemId": "problem-123",
  "code": "function solution() { return 42; }",
  "language": "javascript"
}'
```

## Development

For development with hot reload:
```bash
# In express directory
npm run dev

# In worker directory
npm run dev
```

## Note

This is a development system. In production, you would want to add:
- Authentication and authorization
- Rate limiting
- Proper error handling
- Security measures for code execution
- Logging and monitoring