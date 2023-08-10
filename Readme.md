# MovieDB API

The  **MovieDB API** is a Go-based web service that provides various endpoints for managing movie data. It interacts with a PostgreSQL database, implements rate limiting, handles Cross-Origin Resource Sharing (CORS), and includes endpoints for managing movies, users, and authentication tokens. The API also includes features for user account activation via email and permission-based access control.



## Features

- **Authentication and Authorization**: The API supports user registration and authentication. Certain endpoints are protected and require valid authentication tokens. Users can be assigned different permission levels for different operations.

- **Database Connectivity**: The API interacts with a PostgreSQL database to store and retrieve movie records. It uses the `database/sql` package and supports database connection pooling.

- **Rate Limiting**: To prevent abuse and ensure fair usage, the API employs rate limiting. Requests from clients are limited based on a configurable rate and burst.

- **CORS (Cross-Origin Resource Sharing)**: Cross-Origin Resource Sharing is enabled to allow controlled access to the API from different origins. Trusted CORS origins can be configured.

- **Email Notifications**: The API sends email notifications for account activation. Users receive an activation link via email to activate their accounts.

- **Permission Management**: Users have specific permission levels (e.g., `movies:read`, `movies:write`) for different operations. Endpoints are protected based on these permissions.


## Environment Variables

The following environment variables need to be set for the API to function properly:

- `PORT`: The port number on which the API server will listen (default: `4000`).
- `ENV`: The environment in which the API is running (`development`, `staging`, or `production`).
- `DB_DSN`: PostgreSQL Database Connection String.
- `DB_MAX_OPEN_CONNS`: Maximum number of open database connections (default: `25`).
- `DB_MAX_IDLE_CONNS`: Maximum number of idle database connections (default: `25`).
- `DB_MAX_IDLE_TIME`: Maximum duration of a database connection's idle time (default: `15m`).
- `LIMITER_RPS`: Rate limiter maximum requests per second (default: `2`).
- `LIMITER_BURST`: Rate limiter maximum burst (default: `4`).
- `LIMITER_ENABLED`: Enable rate limiter (`true` or `false`, default: `true`).
- `SMTP_HOST`, `SMTP_PORT`, `SMTP_USERNAME`, `SMTP_PASSWORD`, `SMTP_SENDER`: SMTP server details for sending emails.

## API Endpoints

### Health Check

- **Endpoint**: `/v1/healthcheck`
- **Method**: GET
- **Description**: Health check endpoint to verify the API's availability.

### Movies

- **Endpoint**: `/v1/movies`
- **Methods**: GET, POST
- **Description**: Allows listing and creating movie records. Requires appropriate permissions.

- **Endpoint**: `/v1/movies/:id`
- **Methods**: GET, PATCH, DELETE
- **Description**: Allows retrieving, updating, and deleting specific movie records. Requires appropriate permissions.

### Users

- **Endpoint**: `/v1/users`
- **Method**: POST
- **Description**: Allows user registration.

- **Endpoint**: `/v1/users/activated`
- **Method**: PUT
- **Description**: Activates a user account.

### Authentication

- **Endpoint**: `/v1/tokens/authentication`
- **Method**: POST
- **Description**: Creates an authentication token for a user.

### Debug Metrics

- **Endpoint**: `/debug/vars`
- **Method**: GET
- **Description**: Provides access to expvar metrics for monitoring.

## Usage

1. Install required dependencies using `go mod tidy`.
2. Set the required environment variables in a `.envrc` file.
3. Run the API server using `make run/api`.

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request with your changes. Make sure to follow the existing coding style and write comprehensive tests for new features.

## License

This project is licensed under the MIT License. 