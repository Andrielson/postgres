# PostgreSQL Docker Image

A production-ready PostgreSQL Docker image based on Ubuntu Noble (24.04) with PostgreSQL 16.9.

## Features

- Based on Ubuntu Noble (24.04)
- PostgreSQL 16.9
- UTF-8 enabled by default
- Secure initialization process
- Configurable through environment variables
- Support for initialization scripts
- Proper signal handling for graceful shutdowns

## Quick Start

```bash
# Basic usage
docker run -d \
  --name postgres \
  -e POSTGRES_PASSWORD=yourpassword \
  -p 5432:5432 \
  ghcr.io/andrielson/postgres:16-noble

# With persistent storage
docker run -d \
  --name postgres \
  -e POSTGRES_PASSWORD=yourpassword \
  -v /path/to/data:/var/lib/postgresql/data \
  -p 5432:5432 \
  ghcr.io/andrielson/postgres:16-noble
```

## Environment Variables

The following environment variables can be used to configure the PostgreSQL instance:

- `POSTGRES_PASSWORD`: (Required) Sets the superuser password
- `POSTGRES_USER`: (Optional) Sets the superuser username (defaults to 'postgres')
- `POSTGRES_DB`: (Optional) Creates a database with this name
- `POSTGRES_HOST_AUTH_METHOD`: (Optional) Sets the authentication method
- `POSTGRES_INITDB_ARGS`: (Optional) Additional arguments for initdb
- `POSTGRES_INITDB_WALDIR`: (Optional) Custom WAL directory location

## Initialization Scripts

You can add initialization scripts in two ways:

1. Mount a directory containing `.sql` or `.sh` files to `/docker-entrypoint-initdb.d/`
2. Add files to the `docker-entrypoint-initdb.d` directory in the image

Scripts are executed in alphabetical order.

## Security Considerations

- The image runs PostgreSQL as a non-root user
- Default configuration is secure but can be customized
- Password is required by default (can be changed to trust mode, but not recommended)
- Proper file permissions are enforced

## Building the Image

```bash
docker build -t postgres:16-noble .
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the PostgreSQL License.

## Acknowledgments

This image is based on the official PostgreSQL Docker image and includes various security and usability improvements. 