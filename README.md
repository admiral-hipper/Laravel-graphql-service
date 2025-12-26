# Laravel GraphQL Service

Production-ready Laravel GraphQL backend with Sanctum authentication and external API integration architecture.

---

## Overview

**Laravel GraphQL Service** is a clean, extensible backend platform for building secure GraphQL APIs on Laravel.  
It provides a structured service layer for integrating third-party APIs, persisting normalized data, and exposing it through a strongly typed GraphQL schema.

Designed as a foundation for:

- SaaS backends  
- API gateways  
- Catalog services  
- CRM / ERP integrations  
- Billing platforms  
- External API aggregation services  

---

## Tech Stack

- Laravel 9  
- PHP 8+  
- GraphQL (nuwave/lighthouse)  
- Laravel Sanctum (Bearer authentication)  
- Guzzle HTTP Client  
- MySQL / PostgreSQL / SQLite  
- PHPUnit  

---

## Architecture
<pre>
        GraphQL API
            ↓
Service Integrations Layer
            ↓
Normalizers / Formatters
            ↓
    Database Persistence
            ↓
Paginated GraphQL Queries
</pre>


Each layer is isolated and easily replaceable.

---

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/your-org/laravel-graphql-service.git
cd laravel-graphql-service
```

## Install dependencies
```bash
composer install
```
## Environment configuration
```bash
cp .env.example .env
php artisan key:generate
```
## Run migrations
```bash
php artisan migrate
```
## Generate API token
```bash
php artisan generate:apikey
```

### Use the generated token in every request:

Authorization: Bearer YOUR_TOKEN

## GraphQL Endpoint
POST /graphql


All requests require Sanctum authentication.

## GraphQL Usage
### Query paginated entities
```graphql
query {
  movies {
    data {
      imdbID
      title
      year
      type
      poster
    }
  }
}
```

### Query single entity
```graphql
query {
  movie(imdbID: "tt0133093") {
    title
    year
    ratings {
      source
      value
    }
  }
}
```
### Import data from external API
```graphql
mutation {
  searchMovies(search: "Matrix", type: MOVIE, page: 1) {
    imdbID
    title
    year
    poster
  }
}
```

This mutation connects to an external provider, normalizes the response, persists the data, and returns stored entities.

### Update stored entity
```graphql
mutation {
  updateMovie(movieInput: {
    imdbID: "tt0133093"
    title: "The Matrix"
    year: "1999"
    poster: "https://..."
    ratings: [
      { source: "Internet Movie Database", value: "8.7/10" }
    ]
  }) {
    imdbID
    title
  }
}
```
Testing

Run the test suite:
```bash
php artisan test
```

### Ideal Use Cases
- SaaS backend services

- API gateways

- Product catalogs

- CRM / ERP connectors

- Billing and payment services

- External API synchronization platforms

## Why this repository exists

- This is not a demo project.

- It is a production-structured service template demonstrating:

- GraphQL-first architecture

- Secure authentication design

- Integration service layers

- Database normalization

- Pagination-ready queries

- Automated testing foundations

This repository is designed to be extended and shipped.


