# JSON Response Examples - Sales Orders Module

This document provides complete JSON response examples for the Oracle Fusion Cloud Order Management (Order Hub) REST API. These examples show the exact structure returned by the mock (and real Oracle API).

> **Note:** Oracle Fusion internally uses XML-based services but exposes them via REST endpoints that return JSON. The structures below represent the JSON responses from REST API calls.

## Table of Contents

1. [Collection Response Format](#collection-response-format)
2. [Sales Orders](#sales-orders)
3. [Sales Order Lines](#sales-order-lines)
4. [Customers](#customers)
5. [Products (Inventory Items)](#products-inventory-items)
6. [Customer Order History](#customer-order-history)
7. [Product Order History](#product-order-history)

---

## Collection Response Format

All collection endpoints return responses wrapped in Oracle's standard format:

```json
{
  "items": [...],
  "count": 6,
  "hasMore": false,
  "limit": 25,
  "offset": 0,
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/salesOrdersForOrderHub",
      "name": "salesOrdersForOrderHub",
      "kind": "collection"
    }
  ]
}
```

| Field | Type | Description |
|-------|------|-------------|
| `items` | array | Array of resource objects |
| `count` | integer | Number of items in current response |
| `hasMore` | boolean | Whether more items exist beyond current page |
| `limit` | integer | Maximum items per page (default 25) |
| `offset` | integer | Starting position in result set |
| `links` | array | HATEOAS navigation links |

---

## Sales Orders

### Endpoint
```
GET /fscmRestApi/resources/11.13.18.05/salesOrdersForOrderHub
GET /fscmRestApi/resources/11.13.18.05/salesOrdersForOrderHub/{HeaderId}
```

### Complete Sales Order Object

```json
{
  "HeaderId": "100100574829001",
  "OrderNumber": "SO-2025-0001",
  "OrderTypeCode": "Standard",
  "StatusCode": "Booked",
  "CustomerId": "CUST-1001",
  "CustomerName": "Acme Corporation",
  "CustomerNumber": "ACME-001",
  "BillToSiteId": "SITE-1001",
  "ShipToSiteId": "SITE-1002",
  "TotalAmount": 15750.00,
  "CurrencyCode": "USD",
  "OrderedDate": "2025-12-01T10:30:00Z",
  "RequestedShipDate": "2025-12-15T00:00:00Z",
  "CreationDate": "2025-12-01T10:30:00Z",
  "LastUpdateDate": "2025-12-10T14:22:00Z",
  "SalespersonId": "SP-1001",
  "SalespersonName": "John Smith",
  "BusinessUnitName": "Vision Operations",
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/salesOrdersForOrderHub/100100574829001",
      "name": "salesOrdersForOrderHub",
      "kind": "item"
    },
    {
      "rel": "child",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/salesOrdersForOrderHub/100100574829001/child/lines",
      "name": "lines",
      "kind": "collection"
    }
  ]
}
```

### Field Reference

| Field | Type | Description |
|-------|------|-------------|
| `HeaderId` | string | Unique order identifier (primary key) |
| `OrderNumber` | string | Human-readable order number |
| `OrderTypeCode` | string | Order type: `Standard`, `Rush`, `Return` |
| `StatusCode` | string | Status: `Entered`, `Booked`, `Awaiting Shipping`, `Closed`, `Pending Approval`, `Cancelled` |
| `CustomerId` | string | Customer identifier |
| `CustomerName` | string | Customer display name |
| `CustomerNumber` | string | Customer number |
| `BillToSiteId` | string | Bill-to site identifier |
| `ShipToSiteId` | string | Ship-to site identifier |
| `TotalAmount` | number | Total order amount |
| `CurrencyCode` | string | Currency code (ISO 4217) |
| `OrderedDate` | datetime | ISO 8601 order date |
| `RequestedShipDate` | datetime | Requested ship date |
| `CreationDate` | datetime | Record creation timestamp |
| `LastUpdateDate` | datetime | Last update timestamp |
| `SalespersonId` | string | Salesperson identifier |
| `SalespersonName` | string | Salesperson name |
| `BusinessUnitName` | string | Business unit name |

### Collection Response Example

```json
{
  "items": [
    {
      "HeaderId": "100100574829001",
      "OrderNumber": "SO-2025-0001",
      "OrderTypeCode": "Standard",
      "StatusCode": "Booked",
      "CustomerId": "CUST-1001",
      "CustomerName": "Acme Corporation",
      "CustomerNumber": "ACME-001",
      "BillToSiteId": "SITE-1001",
      "ShipToSiteId": "SITE-1002",
      "TotalAmount": 15750.00,
      "CurrencyCode": "USD",
      "OrderedDate": "2025-12-01T10:30:00Z",
      "RequestedShipDate": "2025-12-15T00:00:00Z",
      "CreationDate": "2025-12-01T10:30:00Z",
      "LastUpdateDate": "2025-12-10T14:22:00Z",
      "SalespersonId": "SP-1001",
      "SalespersonName": "John Smith",
      "BusinessUnitName": "Vision Operations"
    },
    {
      "HeaderId": "100100574829010",
      "OrderNumber": "SO-2025-0002",
      "OrderTypeCode": "Standard",
      "StatusCode": "Entered",
      "CustomerId": "CUST-1002",
      "CustomerName": "TechStart Inc",
      "CustomerNumber": "TECH-002",
      "BillToSiteId": "SITE-2001",
      "ShipToSiteId": "SITE-2002",
      "TotalAmount": 45000.00,
      "CurrencyCode": "USD",
      "OrderedDate": "2025-12-05T09:15:00Z",
      "RequestedShipDate": "2025-12-20T00:00:00Z",
      "CreationDate": "2025-12-05T09:15:00Z",
      "LastUpdateDate": "2025-12-05T09:15:00Z",
      "SalespersonId": "SP-1002",
      "SalespersonName": "Jane Doe",
      "BusinessUnitName": "Vision Operations"
    },
    {
      "HeaderId": "100100574829020",
      "OrderNumber": "SO-2025-0003",
      "OrderTypeCode": "Rush",
      "StatusCode": "Booked",
      "CustomerId": "CUST-1001",
      "CustomerName": "Acme Corporation",
      "CustomerNumber": "ACME-001",
      "BillToSiteId": "SITE-1001",
      "ShipToSiteId": "SITE-1003",
      "TotalAmount": 8500.00,
      "CurrencyCode": "USD",
      "OrderedDate": "2025-12-10T11:00:00Z",
      "RequestedShipDate": "2025-12-12T00:00:00Z",
      "CreationDate": "2025-12-10T11:00:00Z",
      "LastUpdateDate": "2025-12-10T15:30:00Z",
      "SalespersonId": "SP-1001",
      "SalespersonName": "John Smith",
      "BusinessUnitName": "Vision Operations"
    },
    {
      "HeaderId": "100100574829030",
      "OrderNumber": "SO-2025-0004",
      "OrderTypeCode": "Standard",
      "StatusCode": "Closed",
      "CustomerId": "CUST-1003",
      "CustomerName": "Global Manufacturing Co",
      "CustomerNumber": "GLOB-003",
      "BillToSiteId": "SITE-3001",
      "ShipToSiteId": "SITE-3001",
      "TotalAmount": 3200.00,
      "CurrencyCode": "USD",
      "OrderedDate": "2025-11-01T08:00:00Z",
      "RequestedShipDate": "2025-11-15T00:00:00Z",
      "CreationDate": "2025-11-01T08:00:00Z",
      "LastUpdateDate": "2025-11-20T16:00:00Z",
      "SalespersonId": "SP-1002",
      "SalespersonName": "Jane Doe",
      "BusinessUnitName": "Vision Operations"
    },
    {
      "HeaderId": "100100574829040",
      "OrderNumber": "SO-2025-0005",
      "OrderTypeCode": "Standard",
      "StatusCode": "Booked",
      "CustomerId": "CUST-1002",
      "CustomerName": "TechStart Inc",
      "CustomerNumber": "TECH-002",
      "BillToSiteId": "SITE-2001",
      "ShipToSiteId": "SITE-2001",
      "TotalAmount": 125000.00,
      "CurrencyCode": "USD",
      "OrderedDate": "2025-12-12T14:00:00Z",
      "RequestedShipDate": "2025-12-30T00:00:00Z",
      "CreationDate": "2025-12-12T14:00:00Z",
      "LastUpdateDate": "2025-12-12T14:00:00Z",
      "SalespersonId": "SP-1002",
      "SalespersonName": "Jane Doe",
      "BusinessUnitName": "Vision Operations"
    },
    {
      "HeaderId": "100100574829050",
      "OrderNumber": "SO-2026-0006",
      "OrderTypeCode": "Standard",
      "StatusCode": "Pending Approval",
      "CustomerId": "CUST-1004",
      "CustomerName": "Small Business LLC",
      "CustomerNumber": "SMALL-004",
      "BillToSiteId": "SITE-4001",
      "ShipToSiteId": "SITE-4001",
      "TotalAmount": 750.00,
      "CurrencyCode": "USD",
      "OrderedDate": "2026-01-10T10:00:00Z",
      "RequestedShipDate": "2026-01-20T00:00:00Z",
      "CreationDate": "2026-01-10T10:00:00Z",
      "LastUpdateDate": "2026-01-10T10:00:00Z",
      "SalespersonId": "SP-1003",
      "SalespersonName": "Mike Wilson",
      "BusinessUnitName": "Vision Operations"
    }
  ],
  "count": 6,
  "hasMore": false,
  "limit": 25,
  "offset": 0,
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/salesOrdersForOrderHub",
      "name": "salesOrdersForOrderHub",
      "kind": "collection"
    }
  ]
}
```

### Status Codes

| StatusCode | Description |
|------------|-------------|
| `Entered` | Order created but not yet submitted |
| `Pending Approval` | Awaiting approval |
| `Booked` | Order confirmed and processing |
| `Awaiting Shipping` | Ready to ship |
| `Shipped` | Order shipped |
| `Closed` | Order completed |
| `Cancelled` | Order cancelled |

---

## Sales Order Lines

### Endpoint
```
GET /fscmRestApi/resources/11.13.18.05/salesOrdersForOrderHub/{HeaderId}/child/lines
```

### Complete Line Object

```json
{
  "OrderLineId": "100100574829002",
  "LineNumber": 1,
  "InventoryItemId": "ITEM-5001",
  "ProductNumber": "WIDGET-A100",
  "ProductDescription": "Premium Widget A100",
  "OrderedQuantity": 500,
  "OrderedUOMCode": "EA",
  "UnitSellingPrice": 25.00,
  "ExtendedAmount": 12500.00,
  "StatusCode": "Awaiting Shipping",
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/salesOrdersForOrderHub/100100574829001/child/lines/100100574829002",
      "name": "lines",
      "kind": "item"
    }
  ]
}
```

### Field Reference

| Field | Type | Description |
|-------|------|-------------|
| `OrderLineId` | string | Unique line identifier |
| `LineNumber` | integer | Line sequence number |
| `InventoryItemId` | string | Inventory item identifier |
| `ProductNumber` | string | Product SKU/number |
| `ProductDescription` | string | Product description |
| `OrderedQuantity` | number | Quantity ordered |
| `OrderedUOMCode` | string | Unit of measure code |
| `UnitSellingPrice` | number | Price per unit |
| `ExtendedAmount` | number | Line total (Quantity x Price) |
| `StatusCode` | string | Line status |

### Lines Collection Response

```json
{
  "items": [
    {
      "OrderLineId": "100100574829002",
      "LineNumber": 1,
      "InventoryItemId": "ITEM-5001",
      "ProductNumber": "WIDGET-A100",
      "ProductDescription": "Premium Widget A100",
      "OrderedQuantity": 500,
      "OrderedUOMCode": "EA",
      "UnitSellingPrice": 25.00,
      "ExtendedAmount": 12500.00,
      "StatusCode": "Awaiting Shipping"
    },
    {
      "OrderLineId": "100100574829003",
      "LineNumber": 2,
      "InventoryItemId": "ITEM-5002",
      "ProductNumber": "GADGET-B200",
      "ProductDescription": "Standard Gadget B200",
      "OrderedQuantity": 100,
      "OrderedUOMCode": "EA",
      "UnitSellingPrice": 32.50,
      "ExtendedAmount": 3250.00,
      "StatusCode": "Awaiting Shipping"
    }
  ],
  "count": 2,
  "hasMore": false,
  "limit": 25,
  "offset": 0,
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/salesOrdersForOrderHub/100100574829001/child/lines",
      "name": "lines",
      "kind": "collection"
    }
  ]
}
```

### Order with Embedded Lines

When using `?expand=lines`, the order includes embedded lines:

```json
{
  "HeaderId": "100100574829001",
  "OrderNumber": "SO-2025-0001",
  "OrderTypeCode": "Standard",
  "StatusCode": "Booked",
  "CustomerId": "CUST-1001",
  "CustomerName": "Acme Corporation",
  "CustomerNumber": "ACME-001",
  "BillToSiteId": "SITE-1001",
  "ShipToSiteId": "SITE-1002",
  "TotalAmount": 15750.00,
  "CurrencyCode": "USD",
  "OrderedDate": "2025-12-01T10:30:00Z",
  "RequestedShipDate": "2025-12-15T00:00:00Z",
  "CreationDate": "2025-12-01T10:30:00Z",
  "LastUpdateDate": "2025-12-10T14:22:00Z",
  "SalespersonId": "SP-1001",
  "SalespersonName": "John Smith",
  "BusinessUnitName": "Vision Operations",
  "lines": {
    "items": [
      {
        "OrderLineId": "100100574829002",
        "LineNumber": 1,
        "InventoryItemId": "ITEM-5001",
        "ProductNumber": "WIDGET-A100",
        "ProductDescription": "Premium Widget A100",
        "OrderedQuantity": 500,
        "OrderedUOMCode": "EA",
        "UnitSellingPrice": 25.00,
        "ExtendedAmount": 12500.00,
        "StatusCode": "Awaiting Shipping"
      },
      {
        "OrderLineId": "100100574829003",
        "LineNumber": 2,
        "InventoryItemId": "ITEM-5002",
        "ProductNumber": "GADGET-B200",
        "ProductDescription": "Standard Gadget B200",
        "OrderedQuantity": 100,
        "OrderedUOMCode": "EA",
        "UnitSellingPrice": 32.50,
        "ExtendedAmount": 3250.00,
        "StatusCode": "Awaiting Shipping"
      }
    ],
    "count": 2,
    "hasMore": false,
    "limit": 25,
    "offset": 0
  }
}
```

---

## Customers

### Endpoint
```
GET /fscmRestApi/resources/11.13.18.05/accounts
GET /fscmRestApi/resources/11.13.18.05/accounts/{CustomerId}
```

### Complete Customer Object

```json
{
  "CustomerId": "CUST-1001",
  "CustomerNumber": "ACME-001",
  "CustomerName": "Acme Corporation",
  "AccountNumber": "ACC-10001",
  "BillToSiteId": "SITE-1001",
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/accounts/CUST-1001",
      "name": "accounts",
      "kind": "item"
    }
  ]
}
```

### Field Reference

| Field | Type | Description |
|-------|------|-------------|
| `CustomerId` | string | Unique customer identifier |
| `CustomerNumber` | string | Customer number |
| `CustomerName` | string | Customer display name |
| `AccountNumber` | string | Account number |
| `BillToSiteId` | string | Default bill-to site |

### Collection Response Example

```json
{
  "items": [
    {
      "CustomerId": "CUST-1001",
      "CustomerNumber": "ACME-001",
      "CustomerName": "Acme Corporation",
      "AccountNumber": "ACC-10001",
      "BillToSiteId": "SITE-1001"
    },
    {
      "CustomerId": "CUST-1002",
      "CustomerNumber": "TECH-002",
      "CustomerName": "TechStart Inc",
      "AccountNumber": "ACC-10002",
      "BillToSiteId": "SITE-2001"
    },
    {
      "CustomerId": "CUST-1003",
      "CustomerNumber": "GLOB-003",
      "CustomerName": "Global Manufacturing Co",
      "AccountNumber": "ACC-10003",
      "BillToSiteId": "SITE-3001"
    },
    {
      "CustomerId": "CUST-1004",
      "CustomerNumber": "SMALL-004",
      "CustomerName": "Small Business LLC",
      "AccountNumber": "ACC-10004",
      "BillToSiteId": "SITE-4001"
    }
  ],
  "count": 4,
  "hasMore": false,
  "limit": 25,
  "offset": 0,
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/accounts",
      "name": "accounts",
      "kind": "collection"
    }
  ]
}
```

---

## Products (Inventory Items)

### Endpoint
```
GET /fscmRestApi/resources/11.13.18.05/inventoryItems
GET /fscmRestApi/resources/11.13.18.05/inventoryItems/{InventoryItemId}
```

### Complete Product Object

```json
{
  "InventoryItemId": "ITEM-5001",
  "ProductNumber": "WIDGET-A100",
  "ProductDescription": "Premium Widget A100",
  "UOMCode": "EA",
  "UnitSellingPrice": 25.00,
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/inventoryItems/ITEM-5001",
      "name": "inventoryItems",
      "kind": "item"
    }
  ]
}
```

### Field Reference

| Field | Type | Description |
|-------|------|-------------|
| `InventoryItemId` | string | Unique item identifier |
| `ProductNumber` | string | Product SKU/number |
| `ProductDescription` | string | Product description |
| `UOMCode` | string | Primary unit of measure |
| `UnitSellingPrice` | number | Standard selling price |

### Collection Response Example

```json
{
  "items": [
    {
      "InventoryItemId": "ITEM-5001",
      "ProductNumber": "WIDGET-A100",
      "ProductDescription": "Premium Widget A100",
      "UOMCode": "EA",
      "UnitSellingPrice": 25.00
    },
    {
      "InventoryItemId": "ITEM-5002",
      "ProductNumber": "GADGET-B200",
      "ProductDescription": "Standard Gadget B200",
      "UOMCode": "EA",
      "UnitSellingPrice": 32.50
    },
    {
      "InventoryItemId": "ITEM-5003",
      "ProductNumber": "MOTOR-M500",
      "ProductDescription": "Industrial Motor M500",
      "UOMCode": "EA",
      "UnitSellingPrice": 1200.00
    },
    {
      "InventoryItemId": "ITEM-5004",
      "ProductNumber": "BEARING-SET",
      "ProductDescription": "Industrial Bearing Set",
      "UOMCode": "SET",
      "UnitSellingPrice": 50.00
    },
    {
      "InventoryItemId": "ITEM-6001",
      "ProductNumber": "SERVER-X500",
      "ProductDescription": "Enterprise Server X500",
      "UOMCode": "EA",
      "UnitSellingPrice": 3500.00
    },
    {
      "InventoryItemId": "ITEM-6002",
      "ProductNumber": "RACK-R100",
      "ProductDescription": "Server Rack R100",
      "UOMCode": "EA",
      "UnitSellingPrice": 2000.00
    },
    {
      "InventoryItemId": "ITEM-6003",
      "ProductNumber": "SWITCH-S200",
      "ProductDescription": "Network Switch S200",
      "UOMCode": "EA",
      "UnitSellingPrice": 750.00
    }
  ],
  "count": 7,
  "hasMore": false,
  "limit": 25,
  "offset": 0,
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/inventoryItems",
      "name": "inventoryItems",
      "kind": "collection"
    }
  ]
}
```

---

## Customer Order History

This is a computed object returned by `SalesOrderMockOperations.get_customer_order_history()`. It aggregates historical order data for anomaly detection.

### Complete CustomerOrderHistory Object

```json
{
  "customer_id": "CUST-1001",
  "customer_name": "Acme Corporation",
  "total_orders": 2,
  "total_amount": 24250.00,
  "average_order_amount": 12125.00,
  "max_order_amount": 15750.00,
  "min_order_amount": 8500.00,
  "std_dev_amount": 5125.00,
  "average_quantity": 377.5,
  "last_order_date": "2025-12-10T11:00:00Z",
  "first_order_date": "2025-12-01T10:30:00Z",
  "orders": [
    {
      "HeaderId": "100100574829001",
      "OrderNumber": "SO-2025-0001",
      "OrderTypeCode": "Standard",
      "StatusCode": "Booked",
      "CustomerId": "CUST-1001",
      "CustomerName": "Acme Corporation",
      "CustomerNumber": "ACME-001",
      "BillToSiteId": "SITE-1001",
      "ShipToSiteId": "SITE-1002",
      "TotalAmount": 15750.00,
      "CurrencyCode": "USD",
      "OrderedDate": "2025-12-01T10:30:00Z",
      "RequestedShipDate": "2025-12-15T00:00:00Z",
      "CreationDate": "2025-12-01T10:30:00Z",
      "LastUpdateDate": "2025-12-10T14:22:00Z",
      "SalespersonId": "SP-1001",
      "SalespersonName": "John Smith",
      "BusinessUnitName": "Vision Operations",
      "lines": [
        {
          "OrderLineId": "100100574829002",
          "LineNumber": 1,
          "InventoryItemId": "ITEM-5001",
          "ProductNumber": "WIDGET-A100",
          "ProductDescription": "Premium Widget A100",
          "OrderedQuantity": 500,
          "OrderedUOMCode": "EA",
          "UnitSellingPrice": 25.00,
          "ExtendedAmount": 12500.00,
          "StatusCode": "Awaiting Shipping"
        },
        {
          "OrderLineId": "100100574829003",
          "LineNumber": 2,
          "InventoryItemId": "ITEM-5002",
          "ProductNumber": "GADGET-B200",
          "ProductDescription": "Standard Gadget B200",
          "OrderedQuantity": 100,
          "OrderedUOMCode": "EA",
          "UnitSellingPrice": 32.50,
          "ExtendedAmount": 3250.00,
          "StatusCode": "Awaiting Shipping"
        }
      ]
    },
    {
      "HeaderId": "100100574829020",
      "OrderNumber": "SO-2025-0003",
      "OrderTypeCode": "Rush",
      "StatusCode": "Booked",
      "CustomerId": "CUST-1001",
      "CustomerName": "Acme Corporation",
      "CustomerNumber": "ACME-001",
      "BillToSiteId": "SITE-1001",
      "ShipToSiteId": "SITE-1003",
      "TotalAmount": 8500.00,
      "CurrencyCode": "USD",
      "OrderedDate": "2025-12-10T11:00:00Z",
      "RequestedShipDate": "2025-12-12T00:00:00Z",
      "CreationDate": "2025-12-10T11:00:00Z",
      "LastUpdateDate": "2025-12-10T15:30:00Z",
      "SalespersonId": "SP-1001",
      "SalespersonName": "John Smith",
      "BusinessUnitName": "Vision Operations",
      "lines": [
        {
          "OrderLineId": "100100574829021",
          "LineNumber": 1,
          "InventoryItemId": "ITEM-5003",
          "ProductNumber": "MOTOR-M500",
          "ProductDescription": "Industrial Motor M500",
          "OrderedQuantity": 5,
          "OrderedUOMCode": "EA",
          "UnitSellingPrice": 1200.00,
          "ExtendedAmount": 6000.00,
          "StatusCode": "Awaiting Shipping"
        },
        {
          "OrderLineId": "100100574829022",
          "LineNumber": 2,
          "InventoryItemId": "ITEM-5004",
          "ProductNumber": "BEARING-SET",
          "ProductDescription": "Industrial Bearing Set",
          "OrderedQuantity": 50,
          "OrderedUOMCode": "SET",
          "UnitSellingPrice": 50.00,
          "ExtendedAmount": 2500.00,
          "StatusCode": "Awaiting Shipping"
        }
      ]
    }
  ]
}
```

### Field Reference

| Field | Type | Description |
|-------|------|-------------|
| `customer_id` | string | Customer identifier |
| `customer_name` | string | Customer name |
| `total_orders` | integer | Number of orders in period |
| `total_amount` | Decimal | Sum of all order amounts |
| `average_order_amount` | Decimal | Mean order amount |
| `max_order_amount` | Decimal | Maximum single order amount |
| `min_order_amount` | Decimal | Minimum single order amount |
| `std_dev_amount` | Decimal | Standard deviation of amounts |
| `average_quantity` | Decimal | Average total quantity per order |
| `last_order_date` | datetime | Most recent order date |
| `first_order_date` | datetime | Oldest order date in period |
| `orders` | array | List of Order objects |

### Usage for Anomaly Detection

```python
# Z-score calculation for anomaly detection
z_score = abs(
    float(new_order.total_amount - history.average_order_amount)
    / float(history.std_dev_amount)
)

is_anomaly = z_score > 2  # Flag if >2 standard deviations
```

---

## Product Order History

This is a computed object returned by `SalesOrderMockOperations.get_product_order_history()`. It aggregates historical sales data for a specific product.

### Complete ProductOrderHistory Object

```json
{
  "product_number": "WIDGET-A100",
  "product_description": "Premium Widget A100",
  "total_orders": 3,
  "total_quantity": 1128,
  "average_quantity": 376.0,
  "max_quantity": 500,
  "min_quantity": 30,
  "std_dev_quantity": 243.85,
  "average_price": 25.00,
  "order_lines": [
    {
      "OrderLineId": "100100574829002",
      "LineNumber": 1,
      "InventoryItemId": "ITEM-5001",
      "ProductNumber": "WIDGET-A100",
      "ProductDescription": "Premium Widget A100",
      "OrderedQuantity": 500,
      "OrderedUOMCode": "EA",
      "UnitSellingPrice": 25.00,
      "ExtendedAmount": 12500.00,
      "StatusCode": "Awaiting Shipping",
      "_order_number": "SO-2025-0001",
      "_order_date": "2025-12-01T10:30:00Z",
      "_customer_name": "Acme Corporation"
    },
    {
      "OrderLineId": "100100574829031",
      "LineNumber": 1,
      "InventoryItemId": "ITEM-5001",
      "ProductNumber": "WIDGET-A100",
      "ProductDescription": "Premium Widget A100",
      "OrderedQuantity": 128,
      "OrderedUOMCode": "EA",
      "UnitSellingPrice": 25.00,
      "ExtendedAmount": 3200.00,
      "StatusCode": "Closed",
      "_order_number": "SO-2025-0004",
      "_order_date": "2025-11-01T08:00:00Z",
      "_customer_name": "Global Manufacturing Co"
    },
    {
      "OrderLineId": "100100574829051",
      "LineNumber": 1,
      "InventoryItemId": "ITEM-5001",
      "ProductNumber": "WIDGET-A100",
      "ProductDescription": "Premium Widget A100",
      "OrderedQuantity": 30,
      "OrderedUOMCode": "EA",
      "UnitSellingPrice": 25.00,
      "ExtendedAmount": 750.00,
      "StatusCode": "Pending Approval",
      "_order_number": "SO-2026-0006",
      "_order_date": "2026-01-10T10:00:00Z",
      "_customer_name": "Small Business LLC"
    }
  ]
}
```

### Field Reference

| Field | Type | Description |
|-------|------|-------------|
| `product_number` | string | Product SKU/number |
| `product_description` | string | Product description |
| `total_orders` | integer | Number of orders containing this product |
| `total_quantity` | integer | Sum of all quantities ordered |
| `average_quantity` | Decimal | Mean quantity per order |
| `max_quantity` | integer | Maximum single order quantity |
| `min_quantity` | integer | Minimum single order quantity |
| `std_dev_quantity` | Decimal | Standard deviation of quantities |
| `average_price` | Decimal | Average selling price |
| `order_lines` | array | List of OrderLine objects with metadata |

### Extended OrderLine Fields

Order lines in `ProductOrderHistory` include additional metadata:

| Field | Type | Description |
|-------|------|-------------|
| `_order_number` | string | Parent order number |
| `_order_date` | datetime | Parent order date |
| `_customer_name` | string | Customer who placed the order |

---

## Query Parameters

All collection endpoints support these query parameters:

| Parameter | Example | Description |
|-----------|---------|-------------|
| `limit` | `?limit=10` | Items per page (max 500) |
| `offset` | `?offset=25` | Starting position |
| `q` | `?q=StatusCode='Booked'` | Filter expression |
| `orderBy` | `?orderBy=OrderedDate:desc` | Sort order |
| `fields` | `?fields=OrderNumber,StatusCode` | Select specific fields |
| `expand` | `?expand=lines` | Include child resources |

### Filter Examples

```
# Booked orders
?q=StatusCode='Booked'

# Orders for specific customer
?q=CustomerId='CUST-1001'

# Orders after date
?q=OrderedDate>='2025-12-01'

# Combined filters
?q=StatusCode='Booked' AND CustomerId='CUST-1001'

# Orders by amount range
?q=TotalAmount>=1000 AND TotalAmount<=50000
```

---

## Error Responses

### Not Found (404)

```json
{
  "type": "https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.4.5",
  "title": "Not Found",
  "status": 404,
  "detail": "Resource with identifier '999999' not found",
  "o:errorCode": "RESOURCE_NOT_FOUND"
}
```

### Validation Error (400)

```json
{
  "type": "https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.4.1",
  "title": "Bad Request",
  "status": 400,
  "detail": "Invalid filter expression",
  "o:errorCode": "INVALID_QUERY_PARAMETER",
  "o:errorDetails": [
    {
      "field": "q",
      "message": "Syntax error in filter expression"
    }
  ]
}
```

### Authentication Error (401)

```json
{
  "type": "https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.4.2",
  "title": "Unauthorized",
  "status": 401,
  "detail": "Authentication credentials are missing or invalid",
  "o:errorCode": "AUTHENTICATION_REQUIRED"
}
```
