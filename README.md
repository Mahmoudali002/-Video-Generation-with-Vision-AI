# Vision AI Video Generator

A modern web application for AI video generation using Google Cloud Vision AI with an intuitive user interface.

![Vision AI Video Generator](https://storage.googleapis.com/gtv-videos-bucket/sample/images/ElephantsDream.jpg)

## Overview

This application provides a user-friendly interface for generating videos using Google Cloud Vision AI. It allows users to create AI-generated videos by providing text prompts, customizing parameters, and managing multiple projects.

## Features

- **Text-to-Video Generation**: Create videos from textual descriptions using Google's Vision AI models
- **Customizable Parameters**: Adjust duration, FPS, resolution, and model settings
- **Project Management**: Organize video generations into projects
- **Real-time Progress Tracking**: Monitor video generation status in real-time
- **Video Preview and Download**: Watch and download generated videos directly from the interface
- **Persistent Storage**: All projects and videos stored in PostgreSQL database

## Tech Stack

### Backend
- **Node.js** with **Express**
- **PostgreSQL** database for persistent storage
- **Drizzle ORM** for database operations
- **Zod** for schema validation
- **Passport** for authentication

### Frontend
- **React** with **TypeScript**
- **TanStack Query** for data fetching
- **React Hook Form** for form management
- **Tailwind CSS** for styling
- **Shadcn UI** components (based on Radix UI)

### Infrastructure
- **Vite** for frontend development and building
- **ESBuild** for fast transpilation
- **Drizzle Kit** for database migrations

## Requirements

### System Requirements
- Node.js 18+ and npm
- PostgreSQL 14+

### API Keys
- Google Cloud Vision AI API key (for production use)

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/vision-ai-video-generator.git
   cd vision-ai-video-generator
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Set up environment variables:
   Create a `.env` file with the following variables:
   ```
   DATABASE_URL=postgresql://username:password@localhost:5432/vidaidb
   ```

4. Set up the database:
   ```bash
   npm run db:push
   ```

5. Start the development server:
   ```bash
   npm run dev
   ```

6. Access the application at [http://localhost:5000](http://localhost:5000)

## Usage

### Creating a Project
1. Navigate to the Projects page
2. Click "New Project"
3. Enter a project name and optionally add your Vision AI API key

### Generating a Video
1. Select a project
2. Enter a text prompt describing the video you want to generate
3. Adjust parameters as needed (duration, fps, resolution)
4. Click "Generate Video"
5. Wait for the generation process to complete
6. Preview and download your video

## Project Structure

```
/
├── client/               # Frontend React application
│   ├── src/
│   │   ├── components/   # UI components
│   │   ├── hooks/        # Custom React hooks
│   │   ├── lib/          # Utility functions and constants
│   │   └── pages/        # Page components
├── server/               # Backend Express application
│   ├── lib/              # Server-side utilities
│   ├── routes.ts         # API route definitions
│   ├── storage.ts        # Database storage interface
│   └── db.ts             # Database connection
├── shared/               # Shared code between client and server
│   └── schema.ts         # Database schema and types
└── migrations/           # Database migrations
```

## API Endpoints

### Projects
- `GET /api/projects` - List all projects
- `GET /api/projects/:id` - Get a specific project
- `PATCH /api/projects/:id` - Update a project
- `GET /api/projects/:id/videos` - Get all videos for a project

### Videos
- `POST /api/videos/generate` - Generate a new video
- `GET /api/videos` - List all videos
- `GET /api/videos/:id` - Get a specific video

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgements

- [Google Cloud Vision AI](https://cloud.google.com/vision)
- [React](https://reactjs.org/)
- [Shadcn UI](https://ui.shadcn.com/)
- [Drizzle ORM](https://orm.drizzle.team/)