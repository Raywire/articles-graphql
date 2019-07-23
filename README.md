## Title
Articles GraphQL

## Description
A GraphQL app to create articles, view articles with user auth

## Running the API
It's very simple to get the API up and running. First, create the database (and database user if necessary) and add them to the .env file.

```env
DB_DATABASE=your_db_name
DB_USERNAME=your_db_user
DB_PASSWORD=your_password
```

Then install, migrate, seed, and run the server:

```php
composer install
php artisan migrate
php artisan serve
```

## Testing Environment
Use this url: http://localhost:8000/graphql to test the API on Postman or Insomnia

## Seeding the database
Run the following command on your terminal
```php
composer seed
```
## Queries and Mutations

## Fetch all users
```
{
  user(id: 1) {
    id
    name
    email
  }
}
```

## Fetch all users with pagination
```
{
  users(count:11) {
    paginatorInfo {
      total
      hasMorePages
    }
    data {
      id
      name
      email
    }
  }
}
```

## Fetch all articles of a user
```
{
  user(id:1) {
    articles {
      id
      title
    }
  }
}
```

### Fetch all articles
```
{
  articles(count:4) {
    paginatorInfo {
      total
      hasMorePages
    }
    data {
      id
      title
      author {
        name
        email
      }
    }
  }
}
```

### Create a user
```
mutation {
  createUser(
    name:"John Doe"
    email:"john.doe@example.com"
    password: "secret"
  ) {
    id
    name
    email
  }
}
```

### Login a user
```
mutation {
  login(email:"graphql@test.com", password:"secret")
}
```

### Fetch current user's articles
Add the token from login as a Bearer Token
```
{
  me {
    email
    articles {
      id
      title
    }
  }
}
```

### Create an article with authentication
Add the token from login as a Bearer Token
```
mutation {
  createArticle(
    title:"Building a GraphQL Server with Laravel"
    content:"In case you're not currently familiar with it, GraphQL is a query language used to interact with your API..."
  ) {
    id
    author {
      id
      email
    }
  }
}
```
