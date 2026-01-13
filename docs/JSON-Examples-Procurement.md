# JSON Response Examples - Procurement Module

This document provides complete JSON response examples for the Oracle Fusion Cloud Procurement REST API. These examples show the exact structure returned by the mock (and real Oracle API).

> **Note:** Oracle Fusion internally uses XML-based services but exposes them via REST endpoints that return JSON. The structures below represent the JSON responses from REST API calls.

## Table of Contents

1. [Collection Response Format](#collection-response-format)
2. [Purchase Orders](#purchase-orders)
3. [Purchase Order Lines](#purchase-order-lines)
4. [Purchase Order Schedules](#purchase-order-schedules)
5. [Draft Purchase Orders](#draft-purchase-orders)
6. [Purchase Requisitions](#purchase-requisitions)
7. [Suppliers](#suppliers)
8. [Supplier Sites](#supplier-sites)
9. [Supplier Contacts](#supplier-contacts)
10. [Purchase Agreements](#purchase-agreements)
11. [PO Acknowledgments](#po-acknowledgments)

---

## Collection Response Format

All collection endpoints return responses wrapped in Oracle's standard format:

```json
{
  "items": [...],
  "count": 4,
  "hasMore": false,
  "limit": 25,
  "offset": 0,
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/purchaseOrders",
      "name": "purchaseOrders",
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

## Purchase Orders

### Endpoint
```
GET /fscmRestApi/resources/11.13.18.05/purchaseOrders
GET /fscmRestApi/resources/11.13.18.05/purchaseOrders/{POHeaderId}
```

### Complete Purchase Order Object

```json
{
  "POHeaderId": 300100574829561,
  "OrderNumber": "PO-2024-0001",
  "Status": "Open",
  "StatusCode": "OPEN",
  "Supplier": "ABC Office Supplies Inc",
  "SupplierId": 1001,
  "SupplierSite": "MAIN",
  "SupplierSiteId": 2001,
  "ProcurementBU": "Vision Operations",
  "ProcurementBUId": 204,
  "RequisitioningBU": "Vision Operations",
  "RequisitioningBUId": 204,
  "SoldToLegalEntity": "Vision Corporation",
  "SoldToLegalEntityId": 300100002870255,
  "BillToLocation": "Vision HQ",
  "BillToLocationId": 300100002870260,
  "Buyer": "John Smith",
  "BuyerId": 100010025889012,
  "Currency": "USD",
  "TotalAmount": 15750,
  "CreationDate": "2024-12-01T10:30:00Z",
  "LastUpdateDate": "2024-12-10T14:22:00Z",
  "OrderDate": "2024-12-01",
  "Description": "Office supplies Q4 2024",
  "PaymentTerms": "Net 30",
  "PaymentTermsId": 10001,
  "FOBPoint": "Destination",
  "FreightTerms": "Due",
  "ShippingMethod": "Ground",
  "AcknowledgmentStatus": "Accepted",
  "RequiredAcknowledgment": "Document",
  "RequiredAcknowledgmentCode": "D",
  "AcknowledgmentDueDate": "2024-12-08",
  "CommunicatedDate": "2024-12-02T09:00:00Z",
  "CommunicatedVersion": 1,
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/purchaseOrders/300100574829561",
      "name": "purchaseOrders",
      "kind": "item"
    },
    {
      "rel": "child",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/purchaseOrders/300100574829561/child/lines",
      "name": "lines",
      "kind": "collection"
    }
  ]
}
```

### Field Reference

| Field | Type | Description |
|-------|------|-------------|
| `POHeaderId` | integer | Unique identifier (primary key) |
| `OrderNumber` | string | Human-readable PO number |
| `Status` | string | Display status name |
| `StatusCode` | string | Status code: `OPEN`, `CLOSED`, `PENDING_APPROVAL`, `PENDING_SUPPLIER_ACK`, `CANCELLED` |
| `Supplier` | string | Supplier name |
| `SupplierId` | integer | Supplier identifier |
| `SupplierSite` | string | Supplier site name |
| `SupplierSiteId` | integer | Supplier site identifier |
| `ProcurementBU` | string | Procurement business unit name |
| `ProcurementBUId` | integer | Procurement business unit ID |
| `RequisitioningBU` | string | Requisitioning business unit name |
| `RequisitioningBUId` | integer | Requisitioning business unit ID |
| `SoldToLegalEntity` | string | Legal entity name |
| `SoldToLegalEntityId` | integer | Legal entity ID |
| `BillToLocation` | string | Bill-to location name |
| `BillToLocationId` | integer | Bill-to location ID |
| `Buyer` | string | Buyer name |
| `BuyerId` | integer | Buyer employee ID |
| `Currency` | string | Currency code (ISO 4217) |
| `TotalAmount` | number | Total PO amount |
| `CreationDate` | datetime | ISO 8601 creation timestamp |
| `LastUpdateDate` | datetime | ISO 8601 last update timestamp |
| `OrderDate` | date | Order date (YYYY-MM-DD) |
| `Description` | string | PO description |
| `PaymentTerms` | string | Payment terms name |
| `PaymentTermsId` | integer | Payment terms ID |
| `FOBPoint` | string | FOB point |
| `FreightTerms` | string | Freight terms |
| `ShippingMethod` | string | Shipping method |
| `AcknowledgmentStatus` | string | Current acknowledgment status |
| `RequiredAcknowledgment` | string | Required acknowledgment type display |
| `RequiredAcknowledgmentCode` | string | `N` (None), `D` (Document), `Y` (Document and Schedule) |
| `AcknowledgmentDueDate` | date | Acknowledgment due date |
| `CommunicatedDate` | datetime | When PO was communicated to supplier |
| `CommunicatedVersion` | integer | Version number communicated |
| `ClosedDate` | date | Date PO was closed (if applicable) |

### Collection Response Example

```json
{
  "items": [
    {
      "POHeaderId": 300100574829561,
      "OrderNumber": "PO-2024-0001",
      "Status": "Open",
      "StatusCode": "OPEN",
      "Supplier": "ABC Office Supplies Inc",
      "SupplierId": 1001,
      "SupplierSite": "MAIN",
      "SupplierSiteId": 2001,
      "ProcurementBU": "Vision Operations",
      "ProcurementBUId": 204,
      "RequisitioningBU": "Vision Operations",
      "RequisitioningBUId": 204,
      "SoldToLegalEntity": "Vision Corporation",
      "SoldToLegalEntityId": 300100002870255,
      "BillToLocation": "Vision HQ",
      "BillToLocationId": 300100002870260,
      "Buyer": "John Smith",
      "BuyerId": 100010025889012,
      "Currency": "USD",
      "TotalAmount": 15750,
      "CreationDate": "2024-12-01T10:30:00Z",
      "LastUpdateDate": "2024-12-10T14:22:00Z",
      "OrderDate": "2024-12-01",
      "Description": "Office supplies Q4 2024",
      "PaymentTerms": "Net 30",
      "PaymentTermsId": 10001,
      "FOBPoint": "Destination",
      "FreightTerms": "Due",
      "ShippingMethod": "Ground",
      "AcknowledgmentStatus": "Accepted",
      "RequiredAcknowledgment": "Document",
      "RequiredAcknowledgmentCode": "D",
      "AcknowledgmentDueDate": "2024-12-08",
      "CommunicatedDate": "2024-12-02T09:00:00Z",
      "CommunicatedVersion": 1
    },
    {
      "POHeaderId": 300100574829570,
      "OrderNumber": "PO-2024-0002",
      "Status": "Pending Approval",
      "StatusCode": "PENDING_APPROVAL",
      "Supplier": "Tech Hardware Solutions",
      "SupplierId": 1002,
      "SupplierSite": "WAREHOUSE-1",
      "SupplierSiteId": 2002,
      "ProcurementBU": "Vision Operations",
      "ProcurementBUId": 204,
      "SoldToLegalEntity": "Vision Corporation",
      "SoldToLegalEntityId": 300100002870255,
      "Buyer": "Jane Doe",
      "BuyerId": 100010025889013,
      "Currency": "USD",
      "TotalAmount": 45000,
      "CreationDate": "2024-12-05T09:15:00Z",
      "LastUpdateDate": "2024-12-05T09:15:00Z",
      "OrderDate": "2024-12-05",
      "Description": "IT Equipment renewal",
      "PaymentTerms": "Net 45",
      "RequiredAcknowledgment": "None",
      "RequiredAcknowledgmentCode": "N"
    },
    {
      "POHeaderId": 300100574829580,
      "OrderNumber": "PO-2024-0003",
      "Status": "Pending Supplier Acknowledgment",
      "StatusCode": "PENDING_SUPPLIER_ACK",
      "Supplier": "Global Parts Co",
      "SupplierId": 1003,
      "SupplierSite": "US-EAST",
      "SupplierSiteId": 2003,
      "ProcurementBU": "Vision Operations",
      "ProcurementBUId": 204,
      "SoldToLegalEntity": "Vision Corporation",
      "SoldToLegalEntityId": 300100002870255,
      "Buyer": "John Smith",
      "BuyerId": 100010025889012,
      "Currency": "USD",
      "TotalAmount": 8500,
      "CreationDate": "2024-12-10T11:00:00Z",
      "LastUpdateDate": "2024-12-10T11:00:00Z",
      "OrderDate": "2024-12-10",
      "Description": "Replacement parts order",
      "PaymentTerms": "Net 30",
      "RequiredAcknowledgment": "Document and Schedule",
      "RequiredAcknowledgmentCode": "Y",
      "AcknowledgmentDueDate": "2024-12-17",
      "AcknowledgmentWithinDays": 7,
      "CommunicatedDate": "2024-12-10T12:00:00Z",
      "CommunicatedVersion": 1
    },
    {
      "POHeaderId": 300100574829590,
      "OrderNumber": "PO-2024-0004",
      "Status": "Closed",
      "StatusCode": "CLOSED",
      "Supplier": "ABC Office Supplies Inc",
      "SupplierId": 1001,
      "SupplierSite": "MAIN",
      "ProcurementBU": "Vision Operations",
      "ProcurementBUId": 204,
      "SoldToLegalEntity": "Vision Corporation",
      "Buyer": "Jane Doe",
      "BuyerId": 100010025889013,
      "Currency": "USD",
      "TotalAmount": 3200,
      "CreationDate": "2024-11-01T08:00:00Z",
      "LastUpdateDate": "2024-11-30T16:00:00Z",
      "OrderDate": "2024-11-01",
      "Description": "November office supplies",
      "PaymentTerms": "Net 30",
      "RequiredAcknowledgment": "None",
      "RequiredAcknowledgmentCode": "N",
      "ClosedDate": "2024-11-30"
    }
  ],
  "count": 4,
  "hasMore": false,
  "limit": 25,
  "offset": 0,
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/purchaseOrders",
      "name": "purchaseOrders",
      "kind": "collection"
    }
  ]
}
```

---

## Purchase Order Lines

### Endpoint
```
GET /fscmRestApi/resources/11.13.18.05/purchaseOrders/{POHeaderId}/child/lines
```

### Complete Line Object

```json
{
  "POLineId": 300100574829562,
  "LineNumber": 1,
  "LineStatus": "Open",
  "LineStatusCode": "OPEN",
  "ItemDescription": "Premium Copy Paper A4",
  "ItemNumber": "PAPER-A4-500",
  "ItemId": 500001,
  "CategoryName": "Office Supplies",
  "CategoryId": 100,
  "Quantity": 500,
  "UOM": "Box",
  "UOMCode": "BOX",
  "UnitPrice": 25,
  "Amount": 12500,
  "CurrencyAmount": 12500,
  "NeedByDate": "2024-12-20",
  "PromisedDate": null,
  "SourceAgreement": "BPA-2024-001",
  "SourceAgreementId": 300100574820001,
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/purchaseOrders/300100574829561/child/lines/300100574829562",
      "name": "lines",
      "kind": "item"
    },
    {
      "rel": "child",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/purchaseOrders/300100574829561/child/lines/300100574829562/child/schedules",
      "name": "schedules",
      "kind": "collection"
    }
  ]
}
```

### Field Reference

| Field | Type | Description |
|-------|------|-------------|
| `POLineId` | integer | Unique line identifier |
| `LineNumber` | integer | Line sequence number |
| `LineStatus` | string | Line status display |
| `LineStatusCode` | string | `OPEN`, `CLOSED`, `CANCELLED` |
| `ItemDescription` | string | Item description |
| `ItemNumber` | string | Item number/SKU |
| `ItemId` | integer | Item identifier |
| `CategoryName` | string | Category display name |
| `CategoryId` | integer | Category identifier |
| `Quantity` | number | Ordered quantity |
| `UOM` | string | Unit of measure display |
| `UOMCode` | string | UOM code |
| `UnitPrice` | number | Unit price |
| `Amount` | number | Line amount (Quantity x UnitPrice) |
| `CurrencyAmount` | number | Amount in PO currency |
| `NeedByDate` | date | Required delivery date |
| `PromisedDate` | date | Supplier promised date |
| `SourceAgreement` | string | Source agreement number (if applicable) |
| `SourceAgreementId` | integer | Source agreement ID |

### Lines Collection Response

```json
{
  "items": [
    {
      "POLineId": 300100574829562,
      "LineNumber": 1,
      "LineStatus": "Open",
      "LineStatusCode": "OPEN",
      "ItemDescription": "Premium Copy Paper A4",
      "ItemNumber": "PAPER-A4-500",
      "ItemId": 500001,
      "CategoryName": "Office Supplies",
      "CategoryId": 100,
      "Quantity": 500,
      "UOM": "Box",
      "UOMCode": "BOX",
      "UnitPrice": 25,
      "Amount": 12500,
      "CurrencyAmount": 12500,
      "NeedByDate": "2024-12-20",
      "PromisedDate": null,
      "SourceAgreement": "BPA-2024-001",
      "SourceAgreementId": 300100574820001
    },
    {
      "POLineId": 300100574829563,
      "LineNumber": 2,
      "LineStatus": "Open",
      "LineStatusCode": "OPEN",
      "ItemDescription": "Ballpoint Pens Blue",
      "ItemNumber": "PEN-BP-BLUE",
      "ItemId": 500002,
      "CategoryName": "Office Supplies",
      "CategoryId": 100,
      "Quantity": 100,
      "UOM": "Pack",
      "UOMCode": "PK",
      "UnitPrice": 32.5,
      "Amount": 3250,
      "CurrencyAmount": 3250,
      "NeedByDate": "2024-12-20",
      "PromisedDate": null
    }
  ],
  "count": 2,
  "hasMore": false,
  "limit": 25,
  "offset": 0,
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/purchaseOrders/300100574829561/child/lines",
      "name": "lines",
      "kind": "collection"
    }
  ]
}
```

---

## Purchase Order Schedules

### Endpoint
```
GET /fscmRestApi/resources/11.13.18.05/purchaseOrders/{POHeaderId}/child/lines/{POLineId}/child/schedules
```

### Complete Schedule Object

```json
{
  "LineLocationId": 300100574829564,
  "ScheduleNumber": 1,
  "Quantity": 500,
  "QuantityReceived": 0,
  "QuantityBilled": 0,
  "ShipToOrganization": "Vision Warehouse",
  "ShipToOrganizationId": 300100002870270,
  "ShipToLocation": "Main Warehouse",
  "ShipToLocationId": 300100002870271,
  "NeedByDate": "2024-12-20",
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/purchaseOrders/300100574829561/child/lines/300100574829562/child/schedules/300100574829564",
      "name": "schedules",
      "kind": "item"
    }
  ]
}
```

### Field Reference

| Field | Type | Description |
|-------|------|-------------|
| `LineLocationId` | integer | Unique schedule identifier |
| `ScheduleNumber` | integer | Schedule sequence number |
| `Quantity` | number | Scheduled quantity |
| `QuantityReceived` | number | Quantity received to date |
| `QuantityBilled` | number | Quantity billed to date |
| `ShipToOrganization` | string | Ship-to organization name |
| `ShipToOrganizationId` | integer | Ship-to organization ID |
| `ShipToLocation` | string | Ship-to location name |
| `ShipToLocationId` | integer | Ship-to location ID |
| `NeedByDate` | date | Need-by date for this schedule |

---

## Draft Purchase Orders

### Endpoint
```
GET /fscmRestApi/resources/11.13.18.05/draftPurchaseOrders
GET /fscmRestApi/resources/11.13.18.05/draftPurchaseOrders/{POHeaderId}
```

### Complete Draft PO Object

```json
{
  "POHeaderId": 300100574830001,
  "OrderNumber": "PO-DRAFT-0001",
  "Status": "Incomplete",
  "StatusCode": "INCOMPLETE",
  "Supplier": "ABC Office Supplies Inc",
  "SupplierId": 1001,
  "SupplierSite": "MAIN",
  "ProcurementBU": "Vision Operations",
  "ProcurementBUId": 204,
  "SoldToLegalEntity": "Vision Corporation",
  "SoldToLegalEntityId": 300100002870255,
  "Buyer": "John Smith",
  "BuyerId": 100010025889012,
  "Currency": "USD",
  "TotalAmount": 5000,
  "CreationDate": "2024-12-12T08:00:00Z",
  "LastUpdateDate": "2024-12-12T08:00:00Z",
  "Description": "Q1 2025 office supplies planning",
  "lines": [
    {
      "POLineId": 300100574830002,
      "LineNumber": 1,
      "ItemDescription": "Desk Organizers - Premium",
      "ItemNumber": "DESK-ORG-PREM",
      "CategoryName": "Office Supplies",
      "Quantity": 50,
      "UOM": "Each",
      "UnitPrice": 100,
      "Amount": 5000,
      "NeedByDate": "2025-01-15"
    }
  ],
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/draftPurchaseOrders/300100574830001",
      "name": "draftPurchaseOrders",
      "kind": "item"
    }
  ]
}
```

### Status Codes

| StatusCode | Description |
|------------|-------------|
| `INCOMPLETE` | Draft is incomplete and cannot be submitted |
| `PENDING_VALIDATION` | Awaiting validation |
| `READY_TO_SUBMIT` | Ready for submission |

---

## Purchase Requisitions

### Endpoint
```
GET /fscmRestApi/resources/11.13.18.05/purchaseRequisitions
GET /fscmRestApi/resources/11.13.18.05/purchaseRequisitions/{RequisitionHeaderId}
```

### Complete Requisition Object

```json
{
  "RequisitionHeaderId": 300100574825001,
  "Requisition": "REQ-2024-0001",
  "Description": "Marketing materials request",
  "Status": "Approved",
  "StatusCode": "APPROVED",
  "PreparerName": "Mike Johnson",
  "PreparerId": 100010025889014,
  "RequisitioningBU": "Vision Operations",
  "RequisitioningBUId": 204,
  "Currency": "USD",
  "TotalAmount": 2500,
  "CreationDate": "2024-11-28T14:00:00Z",
  "SubmittedDate": "2024-11-28T14:30:00Z",
  "ApprovalDate": "2024-11-30T10:00:00Z",
  "lines": [
    {
      "RequisitionLineId": 300100574825002,
      "LineNumber": 1,
      "LineStatus": "Approved",
      "ItemDescription": "Marketing Brochures - Full Color",
      "ItemNumber": "MKT-BROCH-FC",
      "CategoryName": "Marketing Materials",
      "Quantity": 1000,
      "UOM": "Each",
      "UnitPrice": 2.5,
      "Amount": 2500,
      "NeedByDate": "2024-12-15",
      "SuggestedSupplier": "PrintCo Services",
      "SuggestedSupplierId": 1004,
      "DeliverToLocation": "Marketing Dept",
      "DeliverToLocationId": 300100002870275
    }
  ],
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/purchaseRequisitions/300100574825001",
      "name": "purchaseRequisitions",
      "kind": "item"
    }
  ]
}
```

### Requisition Line Fields

| Field | Type | Description |
|-------|------|-------------|
| `RequisitionLineId` | integer | Unique line identifier |
| `LineNumber` | integer | Line sequence |
| `LineStatus` | string | Line status |
| `ItemDescription` | string | Item description |
| `ItemNumber` | string | Item number |
| `CategoryName` | string | Category name |
| `Quantity` | number | Requested quantity |
| `UOM` | string | Unit of measure |
| `UnitPrice` | number | Estimated unit price |
| `Amount` | number | Line amount |
| `NeedByDate` | date | Required date |
| `SuggestedSupplier` | string | Suggested supplier name |
| `SuggestedSupplierId` | integer | Suggested supplier ID |
| `DeliverToLocation` | string | Delivery location |
| `DeliverToLocationId` | integer | Delivery location ID |
| `UrgentFlag` | boolean | Urgent request indicator |

### Status Codes

| StatusCode | Description |
|------------|-------------|
| `INCOMPLETE` | Draft, not submitted |
| `PENDING_APPROVAL` | Awaiting approval |
| `APPROVED` | Approved, ready for sourcing |
| `REJECTED` | Rejected by approver |

---

## Suppliers

### Endpoint
```
GET /fscmRestApi/resources/11.13.18.05/suppliers
GET /fscmRestApi/resources/11.13.18.05/suppliers/{SupplierId}
```

### Complete Supplier Object

```json
{
  "SupplierId": 1001,
  "Supplier": "ABC Office Supplies Inc",
  "SupplierNumber": "SUP-001",
  "Status": "Active",
  "StatusCode": "ACTIVE",
  "TaxRegistrationNumber": "12-3456789",
  "TaxRegistrationCountry": "US",
  "DUNSNumber": "123456789",
  "SupplierType": "Goods",
  "SupplierTypeCode": "GOODS",
  "BusinessRelationship": "Spend Authorized",
  "BusinessRelationshipCode": "SPEND_AUTHORIZED",
  "OneTimeSupplierFlag": false,
  "CreationDate": "2020-01-15T00:00:00Z",
  "LastUpdateDate": "2024-06-01T10:00:00Z",
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/suppliers/1001",
      "name": "suppliers",
      "kind": "item"
    },
    {
      "rel": "child",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/suppliers/1001/child/sites",
      "name": "sites",
      "kind": "collection"
    },
    {
      "rel": "child",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/suppliers/1001/child/contacts",
      "name": "contacts",
      "kind": "collection"
    }
  ]
}
```

### Field Reference

| Field | Type | Description |
|-------|------|-------------|
| `SupplierId` | integer | Unique supplier identifier |
| `Supplier` | string | Supplier name |
| `SupplierNumber` | string | Supplier number |
| `Status` | string | Status display |
| `StatusCode` | string | `ACTIVE`, `INACTIVE` |
| `TaxRegistrationNumber` | string | Tax ID / EIN |
| `TaxRegistrationCountry` | string | Tax registration country |
| `DUNSNumber` | string | D-U-N-S number |
| `SupplierType` | string | Type display: Goods, Services |
| `SupplierTypeCode` | string | `GOODS`, `SERVICES` |
| `BusinessRelationship` | string | Relationship display |
| `BusinessRelationshipCode` | string | `SPEND_AUTHORIZED`, `PROSPECTIVE` |
| `OneTimeSupplierFlag` | boolean | One-time supplier indicator |
| `CreationDate` | datetime | Record creation date |
| `LastUpdateDate` | datetime | Last update date |

---

## Supplier Sites

### Endpoint
```
GET /fscmRestApi/resources/11.13.18.05/suppliers/{SupplierId}/child/sites
```

### Complete Site Object

```json
{
  "SupplierSiteId": 2001,
  "SupplierSite": "MAIN",
  "Address": "123 Business Ave",
  "City": "New York",
  "State": "NY",
  "PostalCode": "10001",
  "Country": "US",
  "CountryCode": "US",
  "Status": "Active",
  "StatusCode": "ACTIVE",
  "PaymentTerms": "Net 30",
  "PaymentTermsId": 10001,
  "PaySiteFlag": true,
  "PurchasingSiteFlag": true,
  "RFQSiteFlag": true,
  "Email": "orders@abcsupplies.com",
  "Phone": "+1-555-123-4567",
  "Fax": "+1-555-123-4568",
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/suppliers/1001/child/sites/2001",
      "name": "sites",
      "kind": "item"
    }
  ]
}
```

### Sites Collection Response

```json
{
  "items": [
    {
      "SupplierSiteId": 2001,
      "SupplierSite": "MAIN",
      "Address": "123 Business Ave",
      "City": "New York",
      "State": "NY",
      "PostalCode": "10001",
      "Country": "US",
      "CountryCode": "US",
      "Status": "Active",
      "StatusCode": "ACTIVE",
      "PaymentTerms": "Net 30",
      "PaymentTermsId": 10001,
      "PaySiteFlag": true,
      "PurchasingSiteFlag": true,
      "RFQSiteFlag": true,
      "Email": "orders@abcsupplies.com",
      "Phone": "+1-555-123-4567",
      "Fax": "+1-555-123-4568"
    },
    {
      "SupplierSiteId": 2010,
      "SupplierSite": "WEST-COAST",
      "Address": "789 Pacific Blvd",
      "City": "Los Angeles",
      "State": "CA",
      "PostalCode": "90001",
      "Country": "US",
      "CountryCode": "US",
      "Status": "Active",
      "PaymentTerms": "Net 30",
      "PaySiteFlag": false,
      "PurchasingSiteFlag": true
    }
  ],
  "count": 2,
  "hasMore": false,
  "limit": 25,
  "offset": 0
}
```

---

## Supplier Contacts

### Endpoint
```
GET /fscmRestApi/resources/11.13.18.05/suppliers/{SupplierId}/child/contacts
```

### Complete Contact Object

```json
{
  "ContactId": 3001,
  "ContactName": "Robert Brown",
  "FirstName": "Robert",
  "LastName": "Brown",
  "Email": "rbrown@abcsupplies.com",
  "Phone": "+1-555-123-4567",
  "Mobile": "+1-555-987-6543",
  "Role": "Sales Representative",
  "PrimaryContactFlag": true,
  "Status": "Active",
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/suppliers/1001/child/contacts/3001",
      "name": "contacts",
      "kind": "item"
    }
  ]
}
```

### Contacts Collection Response

```json
{
  "items": [
    {
      "ContactId": 3001,
      "ContactName": "Robert Brown",
      "FirstName": "Robert",
      "LastName": "Brown",
      "Email": "rbrown@abcsupplies.com",
      "Phone": "+1-555-123-4567",
      "Mobile": "+1-555-987-6543",
      "Role": "Sales Representative",
      "PrimaryContactFlag": true,
      "Status": "Active"
    },
    {
      "ContactId": 3002,
      "ContactName": "Lisa Chen",
      "FirstName": "Lisa",
      "LastName": "Chen",
      "Email": "lchen@abcsupplies.com",
      "Phone": "+1-555-123-4569",
      "Role": "Account Manager",
      "PrimaryContactFlag": false,
      "Status": "Active"
    }
  ],
  "count": 2,
  "hasMore": false,
  "limit": 25,
  "offset": 0
}
```

---

## Purchase Agreements

### Endpoint
```
GET /fscmRestApi/resources/11.13.18.05/purchaseAgreements
GET /fscmRestApi/resources/11.13.18.05/purchaseAgreements/{AgreementHeaderId}
```

### Complete Agreement Object

```json
{
  "AgreementHeaderId": 300100574820001,
  "Agreement": "BPA-2024-001",
  "Description": "Annual Office Supplies Agreement",
  "Type": "Blanket Purchase Agreement",
  "TypeCode": "BLANKET",
  "Status": "Active",
  "StatusCode": "ACTIVE",
  "Supplier": "ABC Office Supplies Inc",
  "SupplierId": 1001,
  "SupplierSite": "MAIN",
  "SupplierSiteId": 2001,
  "ProcurementBU": "Vision Operations",
  "ProcurementBUId": 204,
  "Currency": "USD",
  "AgreedAmount": 100000,
  "AmountReleased": 18950,
  "AmountRemaining": 81050,
  "EffectiveDate": "2024-01-01",
  "ExpirationDate": "2024-12-31",
  "Buyer": "John Smith",
  "BuyerId": 100010025889012,
  "PaymentTerms": "Net 30",
  "AutomaticallyGenerateOrdersFlag": false,
  "CreationDate": "2023-12-15T00:00:00Z",
  "LastUpdateDate": "2024-12-10T14:22:00Z",
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/purchaseAgreements/300100574820001",
      "name": "purchaseAgreements",
      "kind": "item"
    }
  ]
}
```

### Field Reference

| Field | Type | Description |
|-------|------|-------------|
| `AgreementHeaderId` | integer | Unique agreement identifier |
| `Agreement` | string | Agreement number |
| `Description` | string | Agreement description |
| `Type` | string | Agreement type display |
| `TypeCode` | string | `BLANKET`, `CONTRACT` |
| `Status` | string | Status display |
| `StatusCode` | string | `ACTIVE`, `EXPIRED`, `CLOSED` |
| `AgreedAmount` | number | Total agreed amount |
| `AmountReleased` | number | Amount released to POs |
| `AmountRemaining` | number | Remaining available amount |
| `EffectiveDate` | date | Agreement start date |
| `ExpirationDate` | date | Agreement end date |
| `AutomaticallyGenerateOrdersFlag` | boolean | Auto-generate release orders |

---

## PO Acknowledgments

### Endpoint
```
GET /fscmRestApi/resources/11.13.18.05/purchaseOrderAcknowledgments
GET /fscmRestApi/resources/11.13.18.05/purchaseOrderAcknowledgments/{POHeaderId}
```

### Complete Acknowledgment Object

```json
{
  "POHeaderId": 300100574829580,
  "OrderNumber": "PO-2024-0003",
  "SoldToLegalEntity": "Vision Corporation",
  "SoldToLegalEntityId": 300100002870255,
  "RequiredAcknowledgment": "Document and Schedule",
  "RequiredAcknowledgmentCode": "Y",
  "AcknowledgmentDueDate": "2024-12-17",
  "AcknowledgmentWithinDays": 7,
  "AcknowledgmentResponse": null,
  "AcknowledgmentNote": null,
  "SupplierOrder": null,
  "ChangeOrderNumber": null,
  "schedules": [
    {
      "LineLocationId": 300100574829582,
      "POHeaderId": 300100574829580,
      "POLineId": 300100574829581,
      "LineNumber": 1,
      "ScheduleNumber": 1,
      "Response": null,
      "RejectionReason": null,
      "SupplierOrderLineNumber": null
    },
    {
      "LineLocationId": 300100574829584,
      "POHeaderId": 300100574829580,
      "POLineId": 300100574829583,
      "LineNumber": 2,
      "ScheduleNumber": 1,
      "Response": null,
      "RejectionReason": null,
      "SupplierOrderLineNumber": null
    }
  ],
  "links": [
    {
      "rel": "self",
      "href": "https://server/fscmRestApi/resources/11.13.18.05/purchaseOrderAcknowledgments/300100574829580",
      "name": "purchaseOrderAcknowledgments",
      "kind": "item"
    }
  ]
}
```

### Acknowledged PO Example

```json
{
  "POHeaderId": 300100574829561,
  "OrderNumber": "PO-2024-0001",
  "SoldToLegalEntity": "Vision Corporation",
  "SoldToLegalEntityId": 300100002870255,
  "RequiredAcknowledgment": "Document",
  "RequiredAcknowledgmentCode": "D",
  "AcknowledgmentDueDate": "2024-12-08",
  "AcknowledgmentWithinDays": 7,
  "AcknowledgmentResponse": "ACCEPT",
  "AcknowledgmentNote": "Order confirmed. Shipping by Dec 18.",
  "SupplierOrder": "ABC-SO-2024-1234",
  "ChangeOrderNumber": null,
  "schedules": []
}
```

### Field Reference

| Field | Type | Description |
|-------|------|-------------|
| `POHeaderId` | integer | Purchase order ID |
| `OrderNumber` | string | PO number |
| `RequiredAcknowledgment` | string | Required acknowledgment type |
| `RequiredAcknowledgmentCode` | string | `N`, `D`, `Y` |
| `AcknowledgmentDueDate` | date | Due date for acknowledgment |
| `AcknowledgmentWithinDays` | integer | Days allowed for acknowledgment |
| `AcknowledgmentResponse` | string | `ACCEPT`, `REJECT`, `PENDING` |
| `AcknowledgmentNote` | string | Supplier's note |
| `SupplierOrder` | string | Supplier's order number |
| `ChangeOrderNumber` | string | Change order number (if applicable) |

### Schedule Acknowledgment Fields

| Field | Type | Description |
|-------|------|-------------|
| `LineLocationId` | integer | Schedule identifier |
| `POLineId` | integer | Line identifier |
| `LineNumber` | integer | Line number |
| `ScheduleNumber` | integer | Schedule number |
| `Response` | string | `ACCEPT`, `REJECT`, null |
| `RejectionReason` | string | Reason if rejected |
| `SupplierOrderLineNumber` | string | Supplier's line reference |

---

## Action Responses

Actions return a standard response format:

### Successful Action Response

```json
{
  "result": "SUCCESS",
  "message": "Action completed successfully",
  "POHeaderId": 300100574829561,
  "OrderNumber": "PO-2024-0001"
}
```

### Failed Action Response

```json
{
  "result": "ERROR",
  "message": "Cannot cancel: PO has received quantities",
  "errorCode": "PO_CANNOT_CANCEL_RECEIVED",
  "POHeaderId": 300100574829561
}
```

---

## Query Parameters

All collection endpoints support these query parameters:

| Parameter | Example | Description |
|-----------|---------|-------------|
| `limit` | `?limit=10` | Items per page (max 500) |
| `offset` | `?offset=25` | Starting position |
| `q` | `?q=StatusCode='OPEN'` | Filter expression |
| `orderBy` | `?orderBy=CreationDate:desc` | Sort order |
| `fields` | `?fields=OrderNumber,Status` | Select specific fields |
| `expand` | `?expand=lines` | Include child resources |

### Filter Examples

```
# Open purchase orders
?q=StatusCode='OPEN'

# POs for specific supplier
?q=SupplierId=1001

# POs created after date
?q=CreationDate>='2024-12-01'

# Combined filters
?q=StatusCode='OPEN' AND SupplierId=1001
```
