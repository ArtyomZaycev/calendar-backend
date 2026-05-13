# [Rust Calendar](https://github.com/ArtyomZaycev/rust-calendar) Backend

## Security

User session data is stored in JWT.<br>
Passwords are incrypted with sha512.<br>

## Modules

### [Database](/src/db/)<br>
Lowest-level module. Contains Diesel schema, connection pool and functions for directly accessing the database.

### [Requests](/src/requests/)<br>
Higher-level access to the data. Takes into account user permissions.

### [API](/src/api/)<br>
Contains handlers for HTTP requests. Validates received data, validates the user, loads the data and packages it into the expected response.

## Inner workings

Any incoming HTTP request goes through those layers:
* [main.rs](/src/main.rs) - receives the HTTP request, does basic validation and routes it further.
* [api](/src/api/) - validates request parameters and user authentication.
* [requests](/src/requests/) - checks user permissions and filters out data based on them.
* [db](/src/db/) - creates and executes a database query.

## Used technologies

* [Diesel](https://diesel.rs/) - ORM and query builder.
* [actix](https://actix.rs/) - URL routing, receiving HTTPS requests and sending responses.