# Store API

A RESTful API for managing products built with Node.js, Express, and MongoDB.

## Features

### Search

Search products by name using partial matching (case-insensitive):

```
GET /api/v1/products?name=sofa
```

### Sort

Sort products by one or multiple fields:

```
GET /api/v1/products?sort=name,-price
```

- Use `-` prefix for descending order
- Multiple fields separated by commas

### Filter

**Basic Filters:**

- By featured status: `?featured=true`
- By company: `?company=ikea`

**Numeric Filters:**
Filter by price or rating using comparison operators:

```
GET /api/v1/products?numericFilters=price>100
GET /api/v1/products?numericFilters=rating>=4
```

Supported operators: `>`, `>=`, `=`, `<`, `<=`

### Pagination

Paginate results with `page` and `limit`:

```
GET /api/v1/products?page=2&limit=5
```

- Default: page 1, limit 10

## Project Structure

```
├── app.js              # Express app setup
├── db/
│   └── connect.js      # MongoDB connection
├── models/
│   └── product.js      # Product model
├── controllers/
│   └── products.js     # Product controllers
├── routes/
│   └── products.js     # API routes
├── middleware/
│   ├── error-handler.js
│   └── not-found.js
└── populate.js         # Seed data script
```

## Setup

1. Install dependencies:

   ```bash
   npm install
   ```

2. Create `.env` file:

   ```
   MONGO_URI=your_mongodb_connection_string
   PORT=3000
   ```

3. Run the server:

   ```bash
   node app.js
   ```

4. (Optional) Populate database:
   ```bash
   node populate.js
   ```

## API Endpoints

| Method | Endpoint                  | Description                                              |
| ------ | ------------------------- | -------------------------------------------------------- |
| GET    | `/api/v1/products`        | Get all products (with search, sort, filter, pagination) |
| GET    | `/api/v1/products/static` | Static test route                                        |

## Product Schema

| Field     | Type   | Description                                 |
| --------- | ------ | ------------------------------------------- |
| name      | String | Product name (required)                     |
| price     | Number | Product price (required)                    |
| rating    | Number | Product rating (default: 4.5)               |
| company   | String | Company name (ikea, marcos, caressa, liddy) |
| createdAt | Date   | Creation timestamp                          |
