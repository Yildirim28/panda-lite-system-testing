# Panda-Lite System Testing

This repository contains the complete system testing deliverables for the **Panda-Lite** food-delivery REST API, performed as part of the **Software Testing and Quality Assurance (STQA)** course.

## About the Project

**Panda-Lite** is a lightweight food-delivery backend built with **Node.js (Express 5)** and **PostgreSQL**, sitting behind the STQA Gateway. It models the core workflow of a delivery platform — customers order from restaurants, restaurants prepare the orders, and riders deliver them — with orders moving through a defined lifecycle:

```
placed → accepted → preparing → ready_for_pickup → picked_up → delivered
```

The API exposes endpoints for authentication (JWT), restaurants, menu management, orders, order lifecycle transitions, cancellations, and ratings, with role-based access control (`customer`, `restaurant`, `rider`).

## What We Did

We designed and executed a comprehensive system test suite using **Postman**, covering:

- **Authentication** — registration and login across all roles, validation rules, duplicate emails, password policies
- **Restaurant & Menu Management** — creation, updates, owner-only access control, input validation
- **Order Lifecycle** — placement, status transitions, claiming, cancellation rules and penalties
- **Ratings** — scoring rules, duplicate prevention, delivered-only rating
- **Sorting & Filtering** — list query parameters (`sort_by`, `filter_field`, `filter_value`) across endpoints
- **Security & Negative Testing** — missing/invalid tokens, role-based access (403), IDOR, invalid inputs, boundary conditions

The testing surfaced several significant defects, including an **IDOR vulnerability** allowing customers to view other customers' orders, **exposed `passwordHash`** in order responses, **500 errors** instead of proper 4xx responses on invalid input, and **duplicate rating** acceptance.

## Team

| Name | ID | Section | Area Covered |
|---|---|---|---|
| Md. Fahim Montasir Seyam | 0112230232 | C | Auth, Restaurants, Menu |
| MD. Shamim Osman Chowdhury | 0112230663 | B | Orders, Lifecycle, Cancellations, Ratings |

## Repository Contents

| File | Description |
|---|---|
| `0112230663_SystemTesting.postman_collection(2).json` | Postman collection — Orders, Lifecycle, Cancellations & Ratings |
| `0112230232_SystemTesting.postman_collection (1).json` | Postman collection — Auth, Restaurants & Menu |
| `0112230663_0112230232_SystemTesting.postman_environment.json` | Postman environment for running the collections |
| `0112230663_0112230232_SystemTestingReport.md` | Full system testing report — test plans, test cases, and defect reports |
| `documentation.md` | Full API documentation of the Panda-Lite system under test |

## How to Run the Tests

1. Import both Postman collections and the environment file into Postman.
2. Set the `BASE_URL` variable (and obtain your `X-STQA-Key`).
3. Run the collections using **Collection Runner** or **Newman**:

```bash
newman run "0112230663_SystemTesting.postman_collection(2).json" -e "0112230663_0112230232_SystemTesting.postman_environment.json"
```

Detailed test plans, executed test cases (with expected vs. actual status codes), and defect reports can be found in the [System Testing Report](0112230663_0112230232_SystemTestingReport.md).
