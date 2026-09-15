# E-Commerce API Documentation

## Base URL
```
http://localhost:5000
```

## Products Endpoints

### Get All Products
```
GET /api/products
```
**Query Parameters:**
- `category` (optional) - Filter by category

**Example:**
```bash
curl http://localhost:5000/api/products?category=Electronics
```

**Response:**
```json
{
  "status": "success",
  "count": 3,
  "products": [...]
}
```

### Get Product Details
```
GET /api/products/<id>
```

**Example:**
```bash
curl http://localhost:5000/api/products/1
```

### Search Products
```
GET /api/products/search?q=<query>
```

**Example:**
```bash
curl http://localhost:5000/api/products/search?q=laptop
```

## Shopping Cart Endpoints

### Get Cart
```
GET /api/cart?user_id=<user_id>
```

**Example:**
```bash
curl http://localhost:5000/api/cart?user_id=user123
```

### Add to Cart
```
POST /api/cart/add
```

**Request Body:**
```json
{
  "user_id": "user123",
  "product_id": 1,
  "quantity": 2
}
```

**Example:**
```bash
curl -X POST http://localhost:5000/api/cart/add \
  -H "Content-Type: application/json" \
  -d '{"user_id":"user123","product_id":1,"quantity":2}'
```

### Remove from Cart
```
POST /api/cart/remove
```

**Request Body:**
```json
{
  "user_id": "user123",
  "product_id": 1
}
```

### Clear Cart
```
POST /api/cart/clear
```

**Request Body:**
```json
{
  "user_id": "user123"
}
```

## Checkout Endpoint

### Place Order
```
POST /api/checkout
```

**Request Body:**
```json
{
  "user_id": "user123",
  "address": "123 Main St, City, State 12345",
  "payment_method": "credit_card"
}
```

**Response:**
```json
{
  "status": "success",
  "message": "Order placed successfully",
  "order": {
    "order_id": "ORD-1234567890",
    "user_id": "user123",
    "items": [...],
    "total": 2099.97,
    "status": "pending",
    "created_at": "2026-09-15T15:59:45.123456",
    "shipping_address": "123 Main St, City, State 12345",
    "payment_method": "credit_card"
  }
}
```

## Sample Workflow

1. **Browse Products:**
   ```bash
   curl http://localhost:5000/api/products
   ```

2. **Add Items to Cart:**
   ```bash
   curl -X POST http://localhost:5000/api/cart/add \
     -H "Content-Type: application/json" \
     -d '{"user_id":"customer1","product_id":1,"quantity":1}'
   ```

3. **View Cart:**
   ```bash
   curl http://localhost:5000/api/cart?user_id=customer1
   ```

4. **Checkout:**
   ```bash
   curl -X POST http://localhost:5000/api/checkout \
     -H "Content-Type: application/json" \
     -d '{
       "user_id":"customer1",
       "address":"456 Oak Ave, Town, State 67890",
       "payment_method":"credit_card"
     }'
   ```

## Features

- ✅ Browse products with category filtering
- ✅ Search products by name
- ✅ Add/remove items from shopping cart
- ✅ View cart totals
- ✅ Process checkout with order creation
- ✅ Stock availability checking
- ✅ In-memory data storage (for demo)

## Next Steps

To make this production-ready, consider adding:
- Database integration (PostgreSQL/MongoDB)
- User authentication
- Payment gateway integration
- Order tracking system
- Email notifications
- Admin dashboard
