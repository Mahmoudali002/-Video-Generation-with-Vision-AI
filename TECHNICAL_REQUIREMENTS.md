# Technical Requirements for Vision AI Video Generator

## Development Environment

### Required Software
- **Node.js**: Version 18.0.0 or higher
- **npm**: Version 8.0.0 or higher
- **PostgreSQL**: Version 14.0 or higher

### Integrated Development Tools
- **TypeScript**: Version 5.3.2
- **ESLint**: For code quality and consistency
- **Prettier**: For code formatting

## System Architecture

### Frontend Requirements
- **React**: Version 18.2.0 for UI
- **TypeScript**: For type safety
- **TanStack Query**: For data fetching and caching
- **React Hook Form**: For form handling with validation
- **Wouter**: For lightweight routing
- **Tailwind CSS**: For styling
- **Shadcn/UI**: Component library based on Radix UI primitives
- **Vite**: For fast development and optimized builds

### Backend Requirements
- **Node.js**: Runtime environment
- **Express**: Web framework
- **TypeScript**: For type safety
- **PostgreSQL**: Relational database
- **Drizzle ORM**: For database operations and migrations
- **Zod**: For schema validation and type generation
- **Passport**: For authentication (if implementing user login)

### API Integration
- **Google Cloud Vision AI API**: For video generation
  - Requires API key with appropriate permissions
  - Supports models: VideoFusion-8B and other compatible models
  - Rate limits and quotas apply as per Google Cloud terms

## Database Schema

### Users Table
```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  username TEXT NOT NULL UNIQUE,
  password TEXT NOT NULL,
  email TEXT,
  is_active BOOLEAN NOT NULL DEFAULT TRUE,
  created_at TIMESTAMP NOT NULL DEFAULT NOW()
);
```

### Projects Table
```sql
CREATE TABLE projects (
  id SERIAL PRIMARY KEY,
  name TEXT NOT NULL,
  user_id INTEGER NOT NULL,
  api_key TEXT,
  model TEXT DEFAULT 'VideoFusion-8B',
  created_at TIMESTAMP NOT NULL DEFAULT NOW(),
  FOREIGN KEY (user_id) REFERENCES users(id)
);
```

### Videos Table
```sql
CREATE TABLE videos (
  id SERIAL PRIMARY KEY,
  project_id INTEGER NOT NULL,
  name TEXT NOT NULL,
  prompt TEXT NOT NULL,
  negative_prompt TEXT,
  duration INTEGER NOT NULL,
  fps INTEGER NOT NULL,
  resolution TEXT NOT NULL,
  status TEXT NOT NULL,
  url TEXT,
  thumbnail_url TEXT,
  parameters JSONB NOT NULL,
  error TEXT,
  created_at TIMESTAMP NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMP NOT NULL DEFAULT NOW(),
  FOREIGN KEY (project_id) REFERENCES projects(id)
);
```

## API Endpoints Specification

### Projects

#### GET /api/projects
- **Description**: Retrieves all projects
- **Authentication**: Required
- **Response**: `200 OK` with array of project objects
- **Example Response**:
  ```json
  [
    {
      "id": 1,
      "name": "Nature Videos",
      "userId": 1,
      "apiKey": "****",
      "model": "VideoFusion-8B",
      "createdAt": "2023-04-20T12:00:00Z"
    }
  ]
  ```

#### GET /api/projects/:id
- **Description**: Retrieves a specific project
- **Parameters**: `id` - Project ID
- **Authentication**: Required
- **Response**: `200 OK` with project object or `404 Not Found`

#### PATCH /api/projects/:id
- **Description**: Updates a project
- **Parameters**: `id` - Project ID
- **Body**: 
  ```json
  {
    "name": "Updated Project Name",
    "apiKey": "new-api-key",
    "model": "NewModel-V1"
  }
  ```
- **Authentication**: Required
- **Response**: `200 OK` with updated project object or `404 Not Found`

### Videos

#### POST /api/videos/generate
- **Description**: Generates a new video
- **Body**:
  ```json
  {
    "projectId": 1,
    "prompt": "A drone flying over mountains",
    "negativePrompt": "blurry, pixelated",
    "duration": 5,
    "fps": 30,
    "resolution": "720p",
    "apiKey": "your-api-key",
    "model": "VideoFusion-8B"
  }
  ```
- **Authentication**: Required
- **Response**: `201 Created` with generation information
  ```json
  {
    "id": 1,
    "status": "processing",
    "message": "Video generation process started"
  }
  ```

#### GET /api/videos
- **Description**: Lists all videos
- **Authentication**: Required
- **Response**: `200 OK` with array of video objects

#### GET /api/videos/:id
- **Description**: Retrieves a specific video
- **Parameters**: `id` - Video ID
- **Authentication**: Required
- **Response**: `200 OK` with video object or `404 Not Found`

#### GET /api/projects/:id/videos
- **Description**: Lists all videos for a specific project
- **Parameters**: `id` - Project ID
- **Authentication**: Required
- **Response**: `200 OK` with array of video objects

## Performance Requirements

- **Response Time**: API endpoints should respond within 500ms (excluding video generation time)
- **Video Generation**: Handles generation of videos up to 30 seconds in length
- **Concurrency**: Supports multiple simultaneous video generation requests
- **Scalability**: Can handle up to 100 concurrent users

## Security Requirements

- **API Keys**: Secure storage of Vision AI API keys
- **Data Validation**: All input validated using Zod schemas
- **CORS**: Properly configured for production deployment
- **Rate Limiting**: Implementation recommended for production

## Deployment Requirements

- **Node.js Server**: Capable of running on any cloud platform
- **Database**: PostgreSQL instance with proper connection pooling
- **Environment Variables**: Proper configuration for different environments
- **Memory**: Minimum 1GB RAM recommended
- **Storage**: Depends on video retention policy, minimum 10GB recommended

## Monitoring and Logging

- **Error Logging**: All errors captured and logged
- **API Metrics**: Track response times and success rates
- **Database Monitoring**: Monitor connection pool and query performance

## Development Workflow

- **Version Control**: Git with feature branch workflow
- **Code Review**: Required before merging to main branch
- **Testing**: Unit and integration tests recommended
- **Database Migrations**: Use Drizzle Kit for schema changes