# Data Quality Rules

## 1. Customer Data

| Rule | Description | Action |
|---|---|---|
| Customer ID must exist | Every customer must have a unique ID | Reject/flag invalid record |
| Customer ID must be unique | Duplicate customer IDs must be identified | Deduplicate using latest update |
| Customer name must exist | Customer name is mandatory | Flag invalid record |
| Email format | Email should follow a valid email pattern | Flag invalid email |
| Created date | Must be a valid date | Reject/flag invalid record |
| Updated date | Must be a valid date | Reject/flag invalid record |

## 2. Product Data

| Rule | Description | Action |
|---|---|---|
| Product ID must exist | Product must have a unique ID | Reject/flag invalid record |
| Product ID must be unique | Duplicate products must be identified | Deduplicate |
| Product name must exist | Product name is mandatory | Flag invalid record |
| Unit price | Must be greater than zero | Reject/flag invalid record |
| Stock quantity | Must not be negative | Reject/flag invalid record |

## 3. Order Data

| Rule | Description | Action |
|---|---|---|
| Order ID must exist | Every order must have an ID | Reject/flag invalid record |
| Order ID must be unique | Duplicate orders must be identified | Deduplicate |
| Customer ID | Must exist in customer master | Referential integrity check |
| Order date | Must be a valid date | Reject/flag invalid record |
| Order amount | Must be greater than zero | Reject/flag invalid record |
| Order status | Must belong to approved status values | Flag invalid record |

### Valid Order Status

- CREATED
- CONFIRMED
- SHIPPED
- OUT_FOR_DELIVERY
- DELIVERED
- CANCELLED

## 4. Order Item Data

| Rule | Description | Action |
|---|---|---|
| Order ID | Must exist in orders | Referential integrity check |
| Product ID | Must exist in products | Referential integrity check |
| Quantity | Must be greater than zero | Reject/flag invalid record |
| Line amount | Must be greater than zero | Reject/flag invalid record |

## 5. Data Quality Categories

The pipeline will classify quality issues into:

### Critical

Records that cannot safely enter the Silver layer.

Examples:

- Missing primary key
- Invalid foreign key
- Invalid date
- Negative quantity

### Warning

Records that can be processed but should be flagged.

Examples:

- Missing email
- Invalid email format
- Optional descriptive fields missing

### Duplicate

Records that represent repeated source data.

Examples:

- Duplicate customer records
- Duplicate orders

## 6. Silver Layer Strategy

The Silver layer will:

1. Standardize data types
2. Remove exact duplicate records
3. Deduplicate business keys
4. Validate mandatory fields
5. Validate referential integrity
6. Apply business rules
7. Add data-quality indicators
8. Preserve valid records for downstream processing

Invalid records may be redirected to a quarantine/error dataset for further investigation.