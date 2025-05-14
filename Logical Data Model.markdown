# Logical Data Model for Market Access System

## Entities and Attributes
1. **Farmer**
   - FarmerID (PK, NUMBER)
   - FirstName (VARCHAR2, NOT NULL)
   - LastName (VARCHAR2, NOT NULL)
   - Phone (VARCHAR2, UNIQUE)
   - Location (VARCHAR2)
2. **Buyer**
   - BuyerID (PK, NUMBER)
   - FirstName (VARCHAR2, NOT NULL)
   - LastName (VARCHAR2, NOT NULL)
   - Email (VARCHAR2, UNIQUE)
   - Address (VARCHAR2)
3. **Produce**
   - ProduceID (PK, NUMBER)
   - FarmerID (FK, NUMBER)
   - Name (VARCHAR2, NOT NULL)
   - Quantity (NUMBER, CHECK Quantity >= 0)
   - PricePerUnit (NUMBER, CHECK PricePerUnit > 0)
4. **Order**
   - OrderID (PK, NUMBER)
   - BuyerID (FK, NUMBER)
   - ProduceID (FK, NUMBER)
   - OrderDate (DATE, DEFAULT SYSDATE)
   - Quantity (NUMBER, CHECK Quantity > 0)
   - TotalAmount (NUMBER)
5. **Logistics**
   - LogisticsID (PK, NUMBER)
   - OrderID (FK, NUMBER)
   - ProviderName (VARCHAR2)
   - DeliveryDate (DATE)
   - Status (VARCHAR2, CHECK Status IN ('Pending', 'In Transit', 'Delivered'))
6. **Payment**
   - PaymentID (PK, NUMBER)
   - OrderID (FK, NUMBER, UNIQUE)
   - Amount (NUMBER, CHECK Amount > 0)
   - PaymentDate (DATE, DEFAULT SYSDATE)
   - Status (VARCHAR2, CHECK Status IN ('Pending', 'Completed', 'Failed'))

## Relationships
- **Farmer-Produce**: One-to-Many (One Farmer can list multiple Produce).
- **Buyer-Order**: One-to-Many (One Buyer can place multiple Orders).
- **Produce-Order**: One-to-Many (One Produce can be part of multiple Orders).
- **Order-Logistics**: One-to-Many (One Order can have multiple Logistics updates).
- **Order-Payment**: One-to-One (Each Order has one Payment).

## Constraints
- **Primary Keys**: Unique identifiers for each entity.
- **Foreign Keys**: Ensure referential integrity.
- **NOT NULL**: Enforce mandatory fields (e.g., FirstName, LastName).
- **UNIQUE**: Prevent duplicates (e.g., Phone, Email).
- **CHECK**: Validate data (e.g., Quantity >= 0, Status in specific values).

## Normalization
- **1NF**: All attributes are atomic; no repeating groups.
- **2NF**: No partial dependencies; all non-key attributes depend on the entire primary key.
- **3NF**: No transitive dependencies; non-key attributes depend only on the primary key.
- **Validation**: The model eliminates redundancy (e.g., separating Farmer and Produce prevents duplicate farmer data).

## Data Scenarios
- **Order Placement**: A Buyer orders 50kg of maize from a Farmer. The system checks Produce availability, creates an Order, and initiates a Payment.
- **Delivery Tracking**: Logistics updates the Status to 'Delivered' after confirming delivery.
- **Payment Processing**: Payment is marked 'Completed' after successful transaction.

## Documentation
- ER diagram created using Oracle SQL Developer Data Modeler.
- Submit as PDF with labeled entities, relationships, and constraints.