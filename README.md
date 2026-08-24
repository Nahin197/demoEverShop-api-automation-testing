# 🛒 E-Commerce API Automation — EverShop Demo

> **Postman Collection · API Test Automation · Module 10**

![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)
![Newman](https://img.shields.io/badge/Newman-CLI-green?style=for-the-badge)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6-yellow?style=for-the-badge&logo=javascript)
![Tests](https://img.shields.io/badge/Tests-Passing-brightgreen?style=for-the-badge)

---

## 📋 Project Overview

Automated **end-to-end API test suite** for the [EverShop](https://demo.evershop.io) open-source e-commerce platform.  
Covers the full shopping workflow — **Search → View Cart → Add to Cart → Verify Cart → Delete Item → Bulk Cleanup** — using Postman collection scripts and Newman for CLI/CI execution with HTML reports.

---

## 🎯 Test Scenarios

| # | Request | Method | Description |
|---|---------|--------|-------------|
| 1 | search | GET | Randomly selects a keyword (Thermos/Vase), searches products, validates results |
| 2 | pre_viewCart | GET | Captures cart quantity **before** add (baseline snapshot) |
| 3 | ddtoCarT | POST | Adds searched product with random qty (1–4) to cart |
| 4 | Post_viewCarT | GET | Verifies cart quantity updated correctly **after** add |
| 5 | delete_from_cart | DELETE | Removes single item using dynamic emoveApi URL |
| 6 | delete_all_iteams | DELETE | Bulk-clears entire cart via pm.sendRequest loop |

---

## 🔧 Key Automation Techniques

- **Dynamic Data Generation** — Math.random() in pre-request scripts for keyword & quantity
- **Chained Requests** — pm.collectionVariables pass product_sku, pre_total_qty, emove_api between requests
- **Response Assertions** — Status codes, JSON fields, search-text containment, quantity arithmetic
- **Error Handling** — 	ry/catch in pre_viewCart handles empty-cart edge case gracefully
- **Bulk Operations** — pm.sendRequest loop dynamically deletes all cart items
- **Newman HTML Report** — Full execution report generated via Newman CLI

---

## 📂 Project Structure

`
Module-10/
├── api_automation.postman_collection.json   # Postman collection (6 requests, 13 assertions)
├── newman/
│   └── api automation-2026-08-24-*.html    # Newman HTML execution report
└── README.md
`

---

## ⚙️ Collection Variables

| Variable | Description |
|----------|-------------|
| search_text | Randomly selected keyword ("Thermos" or "Vase") |
| product_sku | SKU extracted from first search result |
| product_Qty | Random quantity 1–4 to add to cart |
| pre_total_qty | Cart total **before** add operation |
| post_total_qty | Cart total **after** add operation |
| emove_api | Dynamic DELETE endpoint for cart item removal |

---

## 🚀 How to Run

### Option 1 — Postman GUI

1. Open **Postman** → **Import** → select pi_automation.postman_collection.json
2. Click **Run collection** in Collection Runner

### Option 2 — Newman CLI

`ash
# Install
npm install -g newman
npm install -g newman-reporter-htmlextra

# Run with HTML report
newman run api_automation.postman_collection.json \
  -r htmlextra \
  --reporter-htmlextra-export newman/report.html

# Run multiple iterations
newman run api_automation.postman_collection.json -n 3 \
  -r htmlextra \
  --reporter-htmlextra-export newman/report.html
`

---

## 📌 Assertions Implemented (13 total)

| Assertion | Request |
|-----------|---------|
| ✅ Status 200 | search |
| ✅ Search keyword present in currentFilters | search |
| ✅ success flag is 	rue | search |
| ✅ All product names contain search keyword | search |
| ✅ Status 200 | pre_viewCart |
| ✅ Status 200 | addtoCarT |
| ✅ Product SKU matches search result | addtoCarT |
| ✅ Cart qty = pre_qty + added_qty | addtoCarT |
| ✅ Total cart quantity correct after add | Post_viewCarT |
| ✅ Status 500 handled for delete | delete_from_cart |

---

## 🌐 Target Application

| Field | Value |
|-------|-------|
| App | [EverShop Demo](https://demo.evershop.io) |
| Type | Open-source Node.js e-commerce |
| API | REST with embedded GraphQL response context |
| Base URL | https://demo.evershop.io |

---

## 🛠️ Tech Stack

| Tool | Role |
|------|------|
| **Postman** | Collection authoring & manual execution |
| **Newman** | CLI / CI pipeline runner |
| **Newman HTMLExtra** | HTML report generation |
| **JavaScript ES6** | Pre-request scripts & test assertions |

---

## 👨‍💻 Author

**[Your Name]**  
SQA Engineer · Ostad SQA Bootcamp — Module 10 (API Automation)

---

*This project is part of the **Ostad SQA Course** curriculum for educational purposes.*
