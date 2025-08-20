# Blog API

A RESTful API for blog management built with Laravel 9, Eloquent ORM, and Laravel Sanctum authentication. This API provides comprehensive blog functionality including article management, user authentication, and content publishing.

## Features

- 📝 **Article Management** - Full CRUD operations for blog articles
- 👤 **User Authentication** - Secure registration and login with Laravel Sanctum
- 📚 **Content Publishing** - Publish/unpublish articles with status management
- 🏷️ **Categorization** - Organize articles by categories
- 🔍 **Search & Filter** - Advanced filtering and search capabilities
- 📊 **Database** - SQLite/MySQL with Eloquent ORM
- ✅ **Validation** - Comprehensive input validation
- 🏗️ **Clean Architecture** - Laravel best practices and conventions

## Tech Stack

- **Framework**: Laravel 9
- **Database**: SQLite (default) / MySQL
- **ORM**: Eloquent
- **Authentication**: Laravel Sanctum
- **Validation**: Laravel Form Requests
- **Language**: PHP 8.1+

## Project Structure

```
app/
├── Http/
│   ├── Controllers/
│   │   ├── ArticleController.php
│   │   └── AuthController.php
│   ├── Requests/
│   │   ├── StoreArticleRequest.php
│   │   └── UpdateArticleRequest.php
│   └── Resources/
│       └── ArticleResource.php
├── Models/
│   ├── Article.php
│   └── User.php
└── Providers/

database/
├── migrations/
│   ├── create_users_table.php
│   ├── create_articles_table.php
│   └── create_personal_access_tokens_table.php
├── factories/
│   └── ArticleFactory.php
└── seeders/
    └── DatabaseSeeder.php

routes/
├── api.php              # API routes
└── web.php              # Web routes
```

## Getting Started

### Prerequisites

- PHP 8.1 or higher
- Composer
- MySQL

### Installation

1. **Clone the repository**:
```bash
git clone https://github.com/Mhammad2022Ibrahim/blogApiLaravel
cd blogApiLaravel
```

2. **Install dependencies**:
```bash
composer install
```

3. **Set up environment**:
```bash
cp .env.example .env
php artisan key:generate
```


4. **Run migrations**:
```bash
php artisan migrate
```

5. **Seed database** (optional):
```bash
php artisan db:seed
```

6. **Start the server**:
```bash
php artisan serve
```

The API will be available at `http://localhost:8000`

## API Endpoints

### Authentication

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/register` | Register a new user |
| POST | `/api/login` | Login user |
| POST | `/api/logout` | Logout user (authenticated) |
| GET | `/api/user` | Get current user (authenticated) |

### Articles

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/articles` | Get all articles |
| GET | `/api/articles/{id}` | Get specific article |
| POST | `/api/articles` | Create new article (authenticated) |
| PUT | `/api/articles/{id}` | Update article (authenticated) |
| DELETE | `/api/articles/{id}` | Delete article (authenticated) |
| PATCH | `/api/articles/{id}/publish` | Publish/unpublish article |

## API Usage Examples

### Register User
```bash
curl -X POST http://localhost:8000/api/register \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Mhammad",
    "email": "mhammad@example.com",
    "password": "password123",
    "password_confirmation": "password123"
  }'
```

### Login
```bash
curl -X POST http://localhost:8000/api/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "mhammad@example.com",
    "password": "password123"
  }'
```

### Create Article
```bash
curl -X POST http://localhost:8000/api/articles \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <your-token>" \
  -d '{
    "title": "My First Blog Post",
    "content": "This is the content of my blog post...",
    "author": "mhammad",
    "category": "Technology",
    "is_published": true
  }'
```

### Get All Articles
```bash
curl -X GET http://localhost:8000/api/articles \
  -H "Accept: application/json"
```

## Database Schema

### Articles Table
```php
Schema::create('articles', function (Blueprint $table) {
    $table->id();
    $table->string('title');
    $table->text('content');
    $table->string('author');
    $table->boolean('is_published')->default(false);
    $table->string('category')->nullable();
    $table->timestamps();
});
```

### Users Table
```php
Schema::create('users', function (Blueprint $table) {
    $table->id();
    $table->string('name');
    $table->string('email')->unique();
    $table->timestamp('email_verified_at')->nullable();
    $table->string('password');
    $table->rememberToken();
    $table->timestamps();
});
```

## Development

### Running Tests
```bash
# Run all tests
php artisan test

# Run specific test
php artisan test --filter ArticleTest

# Run with coverage
php artisan test --coverage
```

### Code Quality
```bash
# Format code
./vendor/bin/php-cs-fixer fix

# Static analysis
./vendor/bin/phpstan analyse
```

### Database Operations
```bash
# Create migration
php artisan make:migration create_articles_table

# Run migrations
php artisan migrate

# Rollback migrations
php artisan migrate:rollback

# Seed database
php artisan db:seed

# Fresh migration with seeding
php artisan migrate:fresh --seed
```

### Artisan Commands
```bash
# Create controller
php artisan make:controller ArticleController --api

# Create model with migration
php artisan make:model Article -m

# Create request
php artisan make:request StoreArticleRequest

# Create resource
php artisan make:resource ArticleResource

# Create factory
php artisan make:factory ArticleFactory

# Create seeder
php artisan make:seeder ArticleSeeder
```

## Environment Configuration

### MySQL
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=blog_api
DB_USERNAME=root
DB_PASSWORD=your_password
```

## Features Overview

- **RESTful API Design** - Following REST conventions
- **Authentication** - Token-based authentication with Sanctum
- **Validation** - Comprehensive input validation
- **Error Handling** - Consistent error responses
- **Resource Transformation** - API resources for consistent output
- **Database Relationships** - Eloquent relationships
- **Middleware** - Authentication and CORS middleware
- **Testing** - Feature and unit tests
- **Documentation** - Comprehensive API documentation

