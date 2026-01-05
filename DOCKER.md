# Docker Setup for Flores

This project includes Docker and Docker Compose configurations for both development and production environments.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) installed on your machine
- [Docker Compose](https://docs.docker.com/compose/install/) installed on your machine

## Quick Start

### Production Build

To run the application in production mode:

```bash
# Build and start the container
docker-compose up -d

# View logs
docker-compose logs -f

# Stop the container
docker-compose down
```

The application will be available at [http://localhost:3000](http://localhost:3000)

### Development Mode

To run the application in development mode with hot-reload:

```bash
# Build and start the development container
docker-compose -f docker-compose.dev.yml up -d

# View logs
docker-compose -f docker-compose.dev.yml logs -f

# Stop the container
docker-compose -f docker-compose.dev.yml down
```

## Docker Commands

### Build the Docker image

```bash
# Production
docker-compose build

# Development
docker-compose -f docker-compose.dev.yml build
```

### Rebuild without cache

```bash
# Production
docker-compose build --no-cache

# Development
docker-compose -f docker-compose.dev.yml build --no-cache
```

### Run in detached mode

```bash
# Production
docker-compose up -d

# Development
docker-compose -f docker-compose.dev.yml up -d
```

### View container logs

```bash
# Production
docker-compose logs -f web

# Development
docker-compose -f docker-compose.dev.yml logs -f web-dev
```

### Stop containers

```bash
# Production
docker-compose down

# Development
docker-compose -f docker-compose.dev.yml down
```

### Remove containers and volumes

```bash
# Production
docker-compose down -v

# Development
docker-compose -f docker-compose.dev.yml down -v
```

## Configuration

### Environment Variables

You can add environment variables in a `.env` file in the root directory:

```env
NODE_ENV=production
PORT=3000
# Add your custom environment variables here
```

### Custom Port

To run the application on a different port, modify the `docker-compose.yml` file:

```yaml
ports:
  - "8080:3000"  # Change 8080 to your desired port
```

## Dockerfile Structure

### Production Dockerfile (`Dockerfile`)

The production Dockerfile uses a multi-stage build process:

1. **Dependencies Stage**: Installs all dependencies
2. **Builder Stage**: Builds the Next.js application
3. **Runner Stage**: Creates a minimal production image with only necessary files

This approach optimizes the final image size and security.

### Development Dockerfile (`Dockerfile.dev`)

The development Dockerfile is simpler and includes:
- Hot-reload support
- Volume mounting for live code updates
- Development dependencies

## Troubleshooting

### Port already in use

If port 3000 is already in use, either:
1. Stop the application using that port
2. Change the port mapping in `docker-compose.yml`

### Build fails

Try rebuilding without cache:

```bash
docker-compose build --no-cache
```

### Permission issues

If you encounter permission issues, ensure Docker has proper permissions on your system.

## Additional Resources

- [Docker Documentation](https://docs.docker.com/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [Next.js Docker Documentation](https://nextjs.org/docs/deployment#docker-image)
