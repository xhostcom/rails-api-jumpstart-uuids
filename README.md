![build & test & quality](https://github.com/cousins-factory/rails-api-boilerplate/actions/workflows/main.yml/badge.svg?branch=main)
[![Ruby Style Guide](https://img.shields.io/badge/code_style-rubocop-brightgreen.svg)](https://github.com/rubocop/rubocop)
![Ruby Version](https://img.shields.io/badge/ruby_version-3.1.2-blue.svg)
![Rails Version](https://img.shields.io/badge/rails_version-7.0.4-c52f24.svg)
[![Swagger documentation](https://img.shields.io/badge/swagger_documentation-84e92c.svg?&logo=swagger&logoColor=black)](docs/SWAGGER.md)

# Rails API Boilerplate Forked from [https://github.com/shftco/rails-api-boilerplate] with small refactors, ie RSpec/Factory.

![cover](docs/cover.png)

# How to Works?

```mermaid
flowchart TD
  R[Request] --> C[Application Controller]
  C --> O[Application Operation]
  O -- Validate Params --> AC[Application Contract]
  O -- Application Contract returned success?--> S[Application Service]
  AC -- Validation success? --> O[Application Operation]
  AC -- Validation failed? --> E[Contract Errors]
  E --> RE
  S -- Process successful? --> RS[Resource]
  S -- Process failed? --> OE[Resource Errors]
  OE --> RE[Response]
  RS --> RE
  RE -- Returns --> C
```

# Documentations

- [Swagger](docs/SWAGGER.md)
- [Service generator](docs/SERVICE.md)
- [Contract generator](docs/CONTRACT.md)
- [Search & Filter & Sort](docs/RANSACK.md)

# Installation

## Prerequisites

- [Ruby](https://rvm.io/)
- [PostgreSQL](https://www.postgresql.org/)
- [Redis](https://redis.io/)

## Installation

- Install GEM dependencies:

  ```bash
  bundle install
  ```

- Create database, migrate tables and run the seed data:

  ```bash
  rails db:create
  rails db:migrate
  rails db:seed
  ```

- If you are setting up again, when you already have previous databases:

  ```bash
  rails db:reset
  ```

  `reset` is equivalent of `rails db:drop & rails db:setup`.

- Run the server
  ```bash
  ./bin/dev
  ```

###### Doorkeeper

Starting from 5.5.0 RC1 Doorkeeper requires client authentication for Resource Owner Password Grant
as stated in the OAuth RFC.

You have to create a new OAuth client (Doorkeeper::Application) if you didn't
have it before and use client credentials in HTTP Basic auth if you previously used this grant flow without
client authentication.

To opt out of this you could set the "skip_client_authentication_for_password_grant" configuration option
to "true", but note that this is in violation of the OAuth spec and represents a security risk. Is comnented out as default

Read https://github.com/doorkeeper-gem/doorkeeper/issues/561#issuecomment-612857163 for more details.

###### Get Client ID?Secret for client/front end

in Rails console

client = Doorkeeper::Application.first (brings up the default client seeded, unless another is set.)

client.uid (reveal/copy client_id)

client.secret (reveal/copy client_secret)

Put these in env file and use in front end client/app.

###### Generators

rails g scaffold Posts

rails g contract Posts

rails g service Post::Comments

etc.
