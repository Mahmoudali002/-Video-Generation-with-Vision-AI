# Installation and Setup Guide

This document provides detailed steps to install and set up the Vision AI Video Generator application.

## Prerequisites

Before proceeding, ensure you have the following installed:

1. **Node.js** (v18 or higher)
2. **npm** (v8 or higher)
3. **PostgreSQL** (v14 or higher)

## Database Setup

1. Create a PostgreSQL database:

```sql
CREATE DATABASE vidaidb;
CREATE USER vidaiuser WITH ENCRYPTED PASSWORD 'your_password';
GRANT ALL PRIVILEGES ON DATABASE vidaidb TO vidaiuser;
```

2. Note your database connection string, which will be in the format:
```
postgresql://vidaiuser:your_password@localhost:5432/vidaidb
```

## Application Setup

1. Clone the repository:
```bash
git clone https://github.com/yourusername/vision-ai-video-generator.git
cd vision-ai-video-generator
```

2. Install dependencies:
```bash
npm install
```

3. Create a `.env` file in the root directory:
```
DATABASE_URL=postgresql://vidaiuser:your_password@localhost:5432/vidaidb
NODE_ENV=development
PORT=5000
```

4. Push the database schema:
```bash
npm run db:push
```

5. Start the development server:
```bash
npm run dev
```

6. Access the application at [http://localhost:5000](http://localhost:5000)

## Google Cloud Vision AI Setup

To enable video generation functionality, you need to set up Google Cloud Vision AI:

1. Create a Google Cloud account if you don't have one
2. Enable the Vision AI API in your Google Cloud Console
3. Create an API key with access to Vision AI
4. Add the API key to your project in the application

## Production Deployment

For production deployment, follow these additional steps:

1. Build the production assets:
```bash
npm run build
```

2. Set production environment variables:
```
DATABASE_URL=your_production_db_url
NODE_ENV=production
PORT=5000
```

3. Start the production server:
```bash
npm start
```

## Common Issues and Troubleshooting

### Database Connection Issues

If you encounter database connection errors:

1. Verify that PostgreSQL is running
2. Check that your DATABASE_URL is correct
3. Ensure your database user has appropriate permissions

### API Key Issues

If video generation is failing:

1. Verify your Google Cloud Vision AI API key is valid
2. Check that the API is enabled in your Google Cloud Console
3. Verify your account has sufficient quota for video generation requests

## Updating

To update the application:

1. Pull the latest changes:
```bash
git pull origin main
```

2. Install any new dependencies:
```bash
npm install
```

3. Apply any database migrations:
```bash
npm run db:push
```

4. Restart the server