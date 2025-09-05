# E-Commerce Database Management System

A comprehensive relational database schema designed for a full-featured e-commerce platform using MySQL. This project demonstrates advanced database design principles including proper normalization, referential integrity, and complex relationship modeling.

## 🎯 Project Overview

This database management system provides a complete foundation for an e-commerce application, supporting:

- **User Management** - Customer accounts, profiles, and authentication
- **Product Catalog** - Hierarchical categories and detailed product information
- **Order Processing** - Complete order lifecycle from cart to fulfillment
- **Payment Systems** - Multiple payment methods and transaction tracking
- **Review System** - Customer feedback and product ratings
- **Inventory Management** - Stock tracking and availability
- **Promotional Tools** - Coupon and discount management

## 🗄️ Database Schema

### Core Entities

| Table | Purpose | Key Relationships |
|-------|---------|-------------------|
| `users` | Customer and admin accounts | → profiles, addresses, orders |
| `products` | Product catalog | ← categories, → order_items, reviews |
| `orders` | Purchase transactions | ← users, → order_items, payments |
| `categories` | Product organization | → products (hierarchical) |

### Relationship Types Implemented

#### One-to-One Relationships
- **Users ↔ User Profiles**: Each user has exactly one detailed profile
  \`\`\`sql
  users.id → user_profiles.user_id (UNIQUE)
  \`\`\`

#### One-to-Many Relationships
- **Users → Addresses**: Customers can have multiple shipping/billing addresses
- **Users → Orders**: Customers can place multiple orders
- **Categories → Products**: Each category contains multiple products
- **Orders → Order Items**: Each order contains multiple line items

#### Many-to-Many Relationships
- **Users ↔ Products** (via Shopping Cart): Users can have multiple products in cart
- **Users ↔ Products** (via Reviews): Users can review multiple products
- **Orders ↔ Products** (via Order Items): Orders can contain multiple products

## 🚀 Setup Instructions

### Prerequisites
- MySQL 8.0 or higher
- MySQL client or workbench

### Installation

1. **Clone or download the project**
   \`\`\`bash
   git clone <repository-url>
   cd ecommerce-database
   \`\`\`

2. **Execute the database schema**
   \`\`\`bash
   mysql -u your_username -p < scripts/ecommerce_database_schema.sql
   \`\`\`

3. **Verify installation**
   \`\`\`sql
   USE ecommerce_db;
   SHOW TABLES;
   \`\`\`

## 📊 Database Features

### Data Integrity
- ✅ **Primary Keys**: Every table has a proper primary key
- ✅ **Foreign Keys**: Referential integrity with CASCADE/RESTRICT options
- ✅ **Constraints**: NOT NULL, UNIQUE, CHECK constraints for data validation
- ✅ **Indexes**: Strategic indexing for performance optimization

### Advanced Features
- **Hierarchical Categories**: Self-referencing category structure
- **Audit Trails**: Created/updated timestamps on all entities
- **Soft Deletes**: Logical deletion for order history preservation
- **Data Validation**: Email format, price ranges, rating constraints
- **Performance Optimization**: Composite indexes on frequently queried columns

### Security Considerations
- Password fields designed for hashed storage
- Email validation constraints
- Proper foreign key relationships prevent orphaned records
- Enumerated values for status fields

## 💡 Usage Examples

### Sample Queries

**Get all products in a category with stock:**
\`\`\`sql
SELECT p.name, p.price, p.stock_quantity 
FROM products p 
JOIN categories c ON p.category_id = c.id 
WHERE c.name = 'Electronics' AND p.stock_quantity > 0;
\`\`\`

**Calculate order total:**
\`\`\`sql
SELECT o.id, SUM(oi.quantity * oi.price) as total
FROM orders o
JOIN order_items oi ON o.id = oi.order_id
WHERE o.id = 1
GROUP BY o.id;
\`\`\`

**Get user's order history:**
\`\`\`sql
SELECT o.id, o.order_date, o.status, o.total_amount
FROM orders o
JOIN users u ON o.user_id = u.id
WHERE u.email = 'customer@example.com'
ORDER BY o.order_date DESC;
\`\`\`

## 🏗️ Technical Specifications

### Database Engine
- **MySQL 8.0+** with InnoDB storage engine
- **UTF8MB4** character set for full Unicode support
- **Collation**: utf8mb4_unicode_ci for proper sorting

### Performance Features
- **Composite Indexes**: On frequently queried column combinations
- **Foreign Key Indexes**: Automatic indexing on foreign key columns
- **Optimized Data Types**: Appropriate field sizes and types

### Scalability Considerations
- **Normalized Design**: Reduces data redundancy
- **Efficient Relationships**: Proper junction tables for many-to-many
- **Index Strategy**: Balanced between query performance and write overhead

## 📋 Table Summary

| Tables | Count | Purpose |
|--------|-------|---------|
| **Core Entities** | 4 | users, products, orders, categories |
| **Relationship Tables** | 6 | order_items, shopping_cart, reviews, etc. |
| **Supporting Tables** | 5 | addresses, payments, coupons, etc. |
| **Total Tables** | 15 | Complete e-commerce functionality |

## 🔧 Maintenance

### Regular Tasks
- Monitor index usage and performance
- Archive old order data periodically
- Update product stock quantities
- Clean up expired shopping cart items

### Backup Strategy
- Daily full database backups
- Transaction log backups every 15 minutes
- Test restore procedures monthly

## 📝 License

This project is designed for educational and commercial use. Feel free to adapt and modify according to your needs.

---

**Created with ❤️ for database learning and e-commerce development**
