# myCVE

Vulnerability research reports and CVE submissions by **Solitude** (GitHub: Chou-alive).

## Current Target

**Online Food Ordering System in PHP and MySQL** (V1.0, sourcecodester node id=18232)

- Vendor Homepage: https://www.sourcecodester.com/php/18232/food-order-system.html
- Software Link: https://www.sourcecodester.com/sites/default/files/download/katojkalemba/web.zip
- Test Environment: Apache 2.4.39 / PHP 7.3.4 / MySQL 5.7.26 (Windows 11), deployed at `http://localhost/web/`
- Audit Date: 2026-10-16

## Findings Index

| # | Issue | Vulnerability | Auth | CVSS 3.1 |
|---|---|---|---|---|
| 1 | /category-foods.php | SQL Injection (Error + UNION) | Unauthenticated | 9.8 Critical |
| 2 | /order.php | SQL Injection (Boolean + Time + UNION) | Unauthenticated | 9.8 Critical |
| 3 | /admin/delete_category.php | Arbitrary File Deletion (path traversal) | Unauthenticated | 9.1 Critical |
| 4 | /admin/delete.php | Arbitrary File Deletion (path traversal) | Unauthenticated | 9.1 Critical |
| 5 | /admin/delete_admin.php | Unauthenticated Admin Deletion | Unauthenticated | 8.1 High |
| 6 | /admin/add_food.php | SQL Injection (INSERT, boolean) | Admin | 7.5 High |
| 7 | /admin/update_food.php | SQL Injection (UPDATE, time + boolean) | Admin | 7.5 High |
| 8 | /admin/update_category.php | SQL Injection (UPDATE, boolean) | Admin | 7.5 High |
| 9 | /admin/edit_admin.php | SQL Injection (SELECT + UPDATE) | Admin | 7.5 High |
| 10 | /admin/change_pwd.php | SQL Injection (SELECT) | Admin | 7.5 High |
| 11 | /admin/add_category.php | SQL Injection (INSERT, boolean) | Admin | 7.5 High |

## Methodology Notes

- Full-chain reports: black-box enumeration → white-box auth-map (`partials/header.php` → `user_logged.php`) → dynamic verification with complete HTTP request/response packets per step.
- MySQL 5.7 constant-folds subqueries in SET context (SLEEP never executes there) — boolean differential (302 diff / DB-state diff / render diff) used as the unified proof channel for INSERT/UPDATE injection points.
- Each issue carries a "Screenshots (to be added after re-verification)" checklist pending evidence supplementation.
