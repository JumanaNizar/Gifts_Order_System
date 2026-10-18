# Personalized Gift Shop

A small local web app for ordering customized gifts (mugs, frames, teddy bears, and similar items).

One C++ program is the website **and** the backend. The browser only displays pages. C++ handles login, products, order validation, prices, saving orders, and the admin dashboard.

Open **http://localhost:8080** after you start the program. Nothing is deployed to the internet; it only listens on your own computer.

## What you can do

**Customer**

1. Register or log in
2. Browse gifts
3. Personalize an item: printed message (max 30 characters), design style, optional photo, quantity
4. Place an order with name, phone, and address
5. View your own orders on **My Orders**

**Admin** (`admin@giftshop.lk` / `admin123`)

- Dashboard: order count, customers, sales
- Add, edit, or hide products
- View all orders and update status: Pending → Processing → Shipped → Delivered (or Cancelled)
- Sales report for today, this week, or this month

Prices are in Sri Lankan rupees (Rs.). The server always calculates `unit price × quantity` from the database. The total shown in the browser is not trusted.

## How it is built

```
Browser (HTML / CSS / JavaScript in public/)
    → HTTP + JSON APIs
        → C++ server (src/main.cpp)
            → SQLite file (data/giftshop.db)
```
| Part | Technology |
|---|---|
| Server and business rules | C++17 + cpp-httplib |
| Database | SQLite (`data/giftshop.db`, created on first run) |
| JSON | nlohmann/json |
| Passwords | salted SHA-256 |
| Pages | `public/` (HTML, CSS, JavaScript) |

All libraries are already in `third_party/`. You do not need npm, PHP, or a separate database server.

On first run the program creates:

- the admin account
- six sample products
- the `data/` folder (database + uploaded photos)

Login uses an `sid` cookie stored in memory. If you stop the program, everyone is logged out.
