# Adjustment Audit System - Product Requirements Document

## 1. Overview

The Adjustment Audit System consists of three core modules for managing financial adjustments in the Vantage platform:

- **Funding Adjustment Audit** (`index.html`) - Funding account adjustments (Funding / Prep / VTS)
- **Cash Adjustment Audit New** (`mt-adjustment.html`) - MT Trading Account cash adjustments
- **Credit Adjustment Audit New** (`credit-adjustment.html`) - Credit adjustments for trading accounts

All pages are deployed at: `https://delia88888.github.io/0818Adjustment/`

---

## 2. Funding Adjustment Audit (index.html)

### 2.1 Page Structure

- **Navigation**: English menu (Users, Client, Account, Reports, Task, Funding, Security, System Setting, Partner)
- **Breadcrumb**: Home / Funding / Adjustment Audit
- **User**: lemon

### 2.2 Search Fields

| Field | Type |
|-------|------|
| Adjustment Application ID | Text Input |
| Account Adjustment OrderID | Text Input |
| Internal Account OrderID | Text Input |
| UID | Text Input |
| Funding Account ID | Text Input |

### 2.3 Tab Filters

- All
- **Unapproved** (default active, red highlight)
- Approved
- Related to Me

### 2.4 Action Buttons

| Button | Function |
|--------|----------|
| Approve | Batch approve selected records |
| Reject | Batch reject selected records |
| + Add | Open Add Adjustment modal |
| Download | Export data |
| Settings | Column settings |

### 2.5 Data Table Columns

Adjustment Application ID, Account Adjustment OrderID, Internal Account OrderID, UID, Account Type, Account ID, Adjustment Type, Coin, Amount, Internal Account ID, Campaign ID, Comment, Note, Reject Reason, Applicant, Reviewer, Application Status, UpdateTime (UTC+3), Action

### 2.6 Add Adjustment Modal

#### Single Mode

| Field | Required | Type | Options |
|-------|----------|------|---------|
| UID | Yes | Text Input | - |
| Account Type | Yes | Dropdown | Funding / Prep / VTS |
| Account | Yes (VTS only) | Dropdown | Dynamic based on UID |
| Adjustment Type | Yes | Dropdown | Adjustment Deposit / Adjustment Withdraw / Adjustment Reward |
| Coin | Yes | Dropdown | USD / USDT / ETH / BTC (auto-filled for Prep/VTS) |
| Amount | Yes | Text Input | - |
| Internal Account | Yes | Dropdown | Multiple internal accounts |
| Campaign ID | No | Dropdown | Optional IDs |
| Comment | Yes | Dropdown | System Generated |
| Note | No | Textarea | Max 100 characters |

**Conditional Logic**:
- Account Type = Prep: Coin auto-set to USD (disabled), Account field hidden
- Account Type = VTS: Show Account dropdown, Coin auto-set to USD after account selection
- Account Type = Funding: Coin dropdown enabled, Account field hidden

#### Batch Mode

- Click "Select File" button to open the **Batch Confirm** secondary confirmation page
- Confirm page displays a wide table with all parsed CSV data
- Columns: UID, Account Type, Account ID, Adjustment Type, Coin, Amount, Internal Account, Campaign ID, Comment, Note, Validation Status, Validation Fail Reason
- Footer: Back / Submit buttons

---

## 3. Cash Adjustment Audit New (mt-adjustment.html)

### 3.1 Page Structure

- **Navigation**: Chinese menu with dropdown (user management, customer management, account management, statistics, **task management** with full submenu, wallet management, system settings)
- **Breadcrumb**: Home / Task Management / Cash Adjustment Audit New
- **User**: Delia Zhao

### 3.2 Search Fields

| Field | Type |
|-------|------|
| License | Text Input |
| User ID | Text Input |
| Adjustment OrderID | Text Input |
| Account | Text Input |
| Account Type | Dropdown (Trading Account / Rebate Account) |

### 3.3 Action Buttons

| Button | Function |
|--------|----------|
| + New Adjustment | Open single adjustment modal |
| Batch CSV | Open batch CSV import modal |
| Approve | Batch approve |
| Reject | Batch reject |
| Download | Export data |
| Settings | Column settings |

### 3.4 Data Table Columns

Adjustment OrderID, License, User ID, Account, Account Type, Type, Amount, Currency, Status (Completed / Rejected / Pending), Comment, Application Note, Applicant, Creation Time, Update Time, Reviewer, Reject Reason, System Type

### 3.5 New Adjustment Modal

| Field | Required | Type | Options |
|-------|----------|------|---------|
| UID | Yes | Text Input | - |
| Account Type | Yes | Dropdown | MT Trading Account / VTS Account |
| Account | Yes | Dropdown | Dynamic |
| Adjustment Type | Yes | Dropdown | Deposit / Withdraw |
| Currency | No | Auto-filled | Based on account validation |
| Amount | Yes | Text Input | - |
| Comment | Yes | Dropdown | Cash Adjustment / Cash Adjustment - Deposit / Cash Adjustment - Withdraw / Cash Adj-AU VPS Reimbursement / Cash Adj-Cost-Rebate UK / Cash Adj-Cost-Rebate_192858 / Cash Adj-Cost-Rebate_58547 / Cash Adj-Cost-Rebate_74381 |
| Application Note | No | Textarea | Max 300 characters |

### 3.6 Batch CSV Import

The Batch CSV modal contains two tabs:

#### Funding Account Tab
- Download template: `funding_adjustment_template.csv`
- Upload CSV file
- Click Upload to open **Import Preview** modal

#### Non-Funding Account Tab
- Download template: `non_funding_adjustment_template.csv`
- Upload CSV file
- Click Upload to open **Import Preview** modal

### 3.7 Import Preview Modal (Batch Upload Confirmation)

Width: 90vw (max 1400px) to display all columns.

#### Funding Account Preview

| Column | Description |
|--------|-------------|
| UID | User ID |
| Type | Adjustment type |
| Coin | Currency type |
| Amount | Adjustment amount |
| Comment | Comment text |
| Application Note | Note text |
| Fail Reason | "-" if valid; error message (red) if failed, e.g. "Insufficient cash for Cash Out operation" |
| Action | Empty if valid; red "Remove" button if failed |

#### Non-Funding Account Preview

| Column | Description |
|--------|-------------|
| Account | Account number |
| Type | Deposit / Withdraw |
| Amount | Adjustment amount |
| Comment | Comment text |
| Ticket ID | Related ticket |
| Fail Reason | "-" if valid; error message (red) if failed |
| Action | Empty if valid; red "Remove" button if failed |

**Footer**: Cancel / Confirm import

---

## 4. Credit Adjustment Audit New (credit-adjustment.html)

### 4.1 Page Structure

- **Navigation**: Chinese menu with dropdown (same as Cash Adjustment, including full task management submenu with links to `mt-adjustment.html` and `credit-adjustment.html`)
- **Breadcrumb**: Home / Task Management / Credit Adjustment Audit New
- **User**: lemon
- **Section Title**: "Search Table" displayed above action buttons

### 4.2 Search Fields

| Field | Type |
|-------|------|
| User ID | Text Input |
| Account | Text Input |
| Adjustment OrderID | Text Input |
| Account Group | Text Input |
| Account Type | Dropdown (MT Trading Account / VTS Trading Account) |
| Type | Dropdown (Credit In / Credit Out) |

### 4.3 Action Buttons

| Button | Style | Function |
|--------|-------|----------|
| Single Item Upload | Blue | Open single item upload modal |
| Batch Import | Black/Dark | Open batch CSV import modal |
| Approve | Default | Batch approve |
| Reject | Default | Batch reject |
| Download | Icon | Export data |
| Settings | Icon | Column settings |

### 4.4 Data Table Columns

| Column | Sortable | Notes |
|--------|----------|-------|
| Adjustment OrderID | Yes | First column after checkbox |
| License | No | e.g. SVG |
| User ID | Yes | - |
| Account | Yes | - |
| Account Group | No | e.g. TEST_MY_USD, TEST\TEST_RISK_USD |
| Account Type | No | MT Trading Account / VTS Trading Account |
| Type | Yes | Credit In / Credit Out |
| Credits | Yes | Numeric value |
| Currency | Yes | e.g. USD |
| Status | No | COMPLETED (green dot) / SUBMITTED (orange dot) |
| Comment | No | e.g. Remark, Credit out-User Request, Credit Out-Debt W/O |
| Application Note | No | - |
| Creation Time | Yes | DateTime format |
| Update Time | Yes | DateTime format |
| Applicant | No | - |
| Reviewer | No | - |
| Reject Reason | No | - |
| System Type | No | New System / Old System |
| Blacklist | No | Icon link |

### 4.5 Single Item Upload Modal

Two-column form layout:

| Row | Left Field | Right Field |
|-----|-----------|-------------|
| 1 | *Account (Text Input, placeholder: "Please enter account") | *Type (Dropdown: Credit In / Credit Out) |
| 2 | *Currency (Dropdown: USD / EUR / GBP) | *Credit (Text Input, placeholder: "Please enter credit") |
| 3 | *Comment (Dropdown, full width: Remark / Credit out-User Request / Credit Out-Debt W/O) | - |
| 4 | Application Note (Textarea, full width, placeholder: "Please enter") | - |

Below the form: **Operation History Table**

| Column |
|--------|
| Operation ID |
| Operation Time |
| Operation Content |
| Credits |
| Operation |
| Comment |
| Application Note |

Default state: "No data" empty placeholder.

**Footer**: Cancel / Confirm

### 4.6 Batch Import Modal

- Template file: `credit_adjustment_template.csv`
- Download link: `https://pj4w2l1pwuq.sg.larksuite.com/sheets/KziIs5djJhxOgVtxSjplTHotgid?sheet=2LMNn4`
- Upload CSV file area
- **Footer**: Cancel / Upload

### 4.7 Pagination

- Total 601 items
- Page sizes: 10 / 20 / 50 / 100 per page
- Page navigation with ellipsis

---

## 5. Cross-Module Navigation

All three pages share a consistent top navigation bar with the task management dropdown containing links to:

- Cash Adjustment Audit New (`mt-adjustment.html`)
- Credit Adjustment Audit New (`credit-adjustment.html`)

Other menu items link to placeholder (`#`) pages.

---

## 6. Deployment

| Environment | URL |
|-------------|-----|
| GitHub Pages | `https://delia88888.github.io/0818Adjustment/` |
| index.html | `https://delia88888.github.io/0818Adjustment/index.html` |
| mt-adjustment.html | `https://delia88888.github.io/0818Adjustment/mt-adjustment.html` |
| credit-adjustment.html | `https://delia88888.github.io/0818Adjustment/credit-adjustment.html` |
