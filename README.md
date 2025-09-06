EcoFinds API Documentation
Overview
The EcoFinds backend is a comprehensive RESTful API built with Flask that powers the sustainable marketplace. It provides all the necessary endpoints for user management, item listings, categories, and search functionality.

API Base URL
http://localhost:8000/api
Authentication
The API uses JWT (JSON Web Tokens) for authentication. Include the token in the Authorization header:

Authorization: Bearer <your_jwt_token>
Endpoints
Health Check
GET /health
Returns API status
Response: {"status": "healthy", "message": "EcoFinds API is running"}
Authentication
Register User
POST /auth/register
Body:
{
  "email": "user@example.com",
  "password": "securepassword",
  "first_name": "John",
  "last_name": "Doe",
  "phone": "+1234567890",
  "location": "City, Country"
}
Login User
POST /auth/login
Body:
{
  "email": "user@example.com",
  "password": "securepassword"
}
Get Profile
GET /auth/profile
Auth Required: Yes
Categories
Get All Categories
GET /categories
Response: List of all active categories
Create Category
POST /categories
Auth Required: Yes
Body:
{
  "name": "New Category",
  "description": "Category description",
  "icon": "🏷️"
}
Items
Get All Items
GET /items
Query Parameters:
page (int): Page number
per_page (int): Items per page
category_id (int): Filter by category
search (string): Search in title/description
condition (string): Filter by condition
min_price (float): Minimum price
max_price (float): Maximum price
Get Single Item
GET /items/{id}
Create Item
POST /items
Auth Required: Yes
Body:
{
  "title": "Item Title",
  "description": "Detailed description",
  "price": 29.99,
  "category_id": 1,
  "condition": "like_new",
  "location": "City, Country",
  "images": ["url1", "url2"],
  "tags": ["sustainable", "organic"]
}
Update Item
PUT /items/{id}
Auth Required: Yes (Owner only)
Delete Item
DELETE /items/{id}
Auth Required: Yes (Owner only)
Get User's Items
GET /users/{user_id}/items
Search
Search Items
GET /search
Query Parameters:
q (string): Search query (required)
category (string): Filter by category name
condition (string): Filter by condition
min_price (float): Minimum price
max_price (float): Maximum price
page (int): Page number
per_page (int): Items per page
Item Conditions
Valid condition values:

new
like_new
good
fair
poor
Database Models
User
id, email, password_hash, first_name, last_name
phone, bio, location, profile_image
is_active, email_verified, created_at, updated_at
Category
id, name, description, icon
is_active, created_at
Item
id, title, description, price, condition
location, images, tags, is_available, is_featured
views_count, seller_id, category_id
created_at, updated_at
Response Format
All responses follow this format:

Success Response:

{
  "message": "Success message",
  "data": {...}
}
Error Response:

{
  "error": "Error message"
}
Default Categories
The API creates these categories by default:

👕 Clothing - Pre-loved fashion that saves the planet
💻 Electronics - Gadgets with a second life
🛋️ Furniture - Style meets sustainability
📚 Books - Knowledge that never goes out of style
⚽ Sports & Outdoors - Gear for active sustainable living
🏠 Home & Garden - Beautiful items for sustainable homes
