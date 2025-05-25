# PL/SQL Market Access System - Capstone Project

## Introduction
- **Student**: Ishimwe Honore (26578)
- **Course**: Database Development with PL/SQL (INSY 8311)
- **Lecturer**: Eric Maniraguha

## Problem Statement
Rwandan smallholder farmers face challenges accessing fair markets due to digital barriers, weak logistics, and middlemen dominance, leading to low income and post-harvest wastage. This project develops a PL/SQL-based Oracle database to automate transactions, improve trade fairness, and reduce losses.

## Methodology
- **Phase I**: Defined problem and presented objectives.
- **Phase II**: Modeled order processing using UML.
- **Phase III**: Designed logical data model with ER diagram.
- **Phase IV**: Created pluggable database (Tues_26578_Honore_MarketAccess_DB).
- **Phase V**: Implemented tables and inserted realistic data.
- **Phase VI**: Developed procedures for order processing and data retrieval.
- **Phase VII**: Implemented triggers and auditing for security.
- **Phase VIII**: Compiled documentation and presentation.

## Screenshots
- **ER Diagram**: ![ER-Diagram](https://github.com/user-attachments/assets/6c84210a-e07a-4e47-8e90-2d483fb1609c)

**Entities:**

The diagram includes the following key entities, represented by blue rectangles:

* **FARMER:** Represents individual farmers who offer produce. Attributes include `FarmerID` (primary key), `FirstName`, `LastName`, `Phone`, and `Location`.
* **PRODUCE:** Represents the agricultural products offered by farmers. Attributes include `ProduceID` (primary key) and `Name`.
* **BUYER:** Represents individuals or entities that purchase produce. Attributes include `BuyerID` (primary key), `FirstName`, `LastName`, `Email`, and `Address`.
* **ORDER:** Represents a purchase order placed by a buyer. Attributes include `OrderID` (primary key), `OrderDate`, and `Quantity`.
* **PAYMENT:** Represents the payment made for an order. Attributes include `PaymentID` (primary key), `PaymentDate`, `Amount`, and `Status`.
* **LOGISTICS:** Represents the shipping and delivery details for an order. Attributes include `LogisticsID` (primary key), `ProviderName`, `DeliveryDate`, and `Status`.

**Attributes:**

Each entity has associated attributes, shown in yellow ovals. As mentioned above, the underlined attributes represent the primary keys for their respective entities.

**Relationships:**

The relationships between the entities are depicted by diamond shapes with lines connecting them to the entities. The cardinality of each relationship is also indicated (`1` for "one" and `M` for "many").

* **OWNS:** A `FARMER` can own (offer) many `PRODUCE` items (1:M relationship).
* **CONTAINS:** An `ORDER` can contain one specific `PRODUCE` item. The relationship also includes the attribute `PricePerUnit` which describes the price of that specific produce item within that order (M:1 relationship from `ORDER` to `PRODUCE`).
* **PLACES:** A `BUYER` can place many `ORDERS` (1:M relationship).
* **REQUIRES:** An `ORDER` requires one `PAYMENT` (1:1 relationship).
* **SHIPPED VIA:** An `ORDER` is shipped via one `LOGISTICS` arrangement (1:1 relationship).

- **UML Diagram**:![DBMS ER diagram (UML notation) - Page 1](https://github.com/user-attachments/assets/c24fff2c-2225-4a8b-885d-2351866202c0)

This diagram illustrates the business process flow for the Market Access System, outlining the steps involved from a farmer listing their products to the buyer receiving them and the farmer getting paid.

**Process Steps:**

1.  **Start:** The process begins.
2.  **Farmer lists agricultural products with published listings to detailed marketplace:** Farmers input information about their produce, creating listings on the platform.
3.  **Market Access System validates and publishes listings to marketplace:** The system checks the submitted listings and makes them available to potential buyers.
4.  **Is listing validation successful?** (Decision): The system checks if the listing meets the required criteria.
    * **Yes:** The process continues to notifying potential buyers.
    * **No:** The process goes back to "Revise listing creation", where the farmer needs to adjust their listing.
5.  **Notify potential buyers:** Buyers are informed about new or relevant listings.
6.  **Buyer discovers and places order:** A buyer finds a suitable listing and submits an order.
7.  **System creates order record:** The system records the details of the buyer's order.
8.  **Does farmer confirm availability?** (Decision): The system or the farmer confirms if the ordered produce is available.
    * **Yes:** The process proceeds to logistics.
    * **No:** The process leads to "Order cancellation or dispute resolution".
9.  **Logistics provider picks up and delivers produce:** A logistics service handles the transportation of the produce to the buyer.
10. **Buyer verifies quality:** The buyer inspects the received produce to ensure it meets the expected quality.
11. **Buyer verifies quality - Yes:** (Implied transition) If the quality is satisfactory, the process moves to payment initiation.
12. **Buyer verifies quality - No:** (Dashed red line) If the quality is not satisfactory, it leads back to "Order cancellation or dispute resolution".
13. **Initiate payment processing:** The payment process is started.
14. **Payment system processes transaction:** The system handles the financial transaction.
15. **Is payment validation successful?** (Decision): The system verifies if the payment was successful.
    * **Yes:** "Funds released to farmer".
    * **No:** "Handle payment failure".
16. **Funds released to farmer:** The payment is transferred to the farmer.
17. **End:** The process concludes.


- **OEM Dashboard**:![pdb1](https://github.com/user-attachments/assets/842d9bc7-2920-4555-ac3e-2c4d25ca3016)
![pdb2](https://github.com/user-attachments/assets/660fb6e8-896f-4dc0-863c-b0beacc44a03)
![grant1](https://github.com/user-attachments/assets/6a3f9a2c-61e0-4ead-b456-d2d6724d5105)
![grant2](https://github.com/user-attachments/assets/afb8fb42-65c2-47a8-b083-ef43e8cedbc1)

These screenshots demonstrate the process of setting up the Oracle database for the Market Access System.

**Image 1 & 2: Granting Privileges to User `honore12`**

These images show the SQL commands used to grant various privileges to the database user `honore12`. This involves giving the user the necessary permissions to perform actions within the database, such as creating tables, connecting, and managing database objects.

* We can see successful `GRANT` commands for system privileges like `DBA`, `CONNECT`, `RESOURCE`, etc.
* There are instances where errors like `ORA-00990: missing or invalid privilege` occurred, likely due to syntax variations when granting multiple object privileges or specific system privileges. These were subsequently corrected.

**Image 3: Creating and Managing a Pluggable Database**

This screenshot illustrates the creation and management of a Pluggable Database (PDB) named `TUE_26578_HONORE_SMALLHOLDER_MARKET_ACCESS_SYSTEM_DB`. Oracle's PDB architecture allows for more efficient management of multiple databases.

1.  **`CREATE PLUGGABLE DATABASE ...`**: This command creates the new PDB, including specifying an administrative user (`honore`) and the location for the database files.
2.  **`SHOW PDBS`**: This command lists the existing PDBs, showing the newly created one in a `MOUNTED` state.
3.  **`ALTER PLUGGABLE DATABASE ... OPEN;`**: This command opens the PDB, making it ready for use.
4.  **`ALTER PLUGGABLE DATABASE ... SAVE STATE;`**: This ensures that the PDB's open/closed status is preserved across database restarts.
5.  **`ALTER SESSION SET CONTAINER = ...;`**: This command switches the current SQL session to operate within the newly created PDB.

**Image 4: Creating a User and Granting Privileges**

This screenshot shows the creation of the `honore12` user and the granting of all system privileges to this user.

1.  An initial attempt to create the user using `create user honore12 by honore;` resulted in an `ORA-00922: missing or invalid option` error, highlighting the correct syntax requires the `IDENTIFIED BY` clause.
2.  The corrected command `create user honore12 identified by honore;` successfully created the user.
3.  Finally, `grant all privileges to honore12;` provided the user with comprehensive permissions within the database instance.

In summary, these steps demonstrate the initial setup of the Oracle database environment, including creating a dedicated pluggable database for the Market Access System and configuring a user (`honore12`) with the necessary privileges to interact with it.

- **Sample Query Output**:![tables-createtion](https://github.com/user-attachments/assets/2746bdae-a720-4fcd-8b31-422c02e9ab09)
![insert data](https://github.com/user-attachments/assets/9431b4cc-0ceb-4ade-91d7-ae22f6aa4c74)
![Create sequences](https://github.com/user-attachments/assets/ff01c227-aa5b-4649-8882-636406376466)
![trigger](https://github.com/user-attachments/assets/ec9af861-7521-45b4-8b1f-c9c0dc8a44c5)
![procedure](https://github.com/user-attachments/assets/e428521e-4615-4009-88fd-c3a3b26cf240)

## SQL Queries
- **Table Creation and Data Insertion**:
```sql
 -- Table Creation
CREATE TABLE Farmer (
    FarmerID NUMBER PRIMARY KEY,
    FirstName VARCHAR2(50) NOT NULL,
    LastName VARCHAR2(50) NOT NULL,
    Phone VARCHAR2(15) UNIQUE,
    Location VARCHAR2(100)
);

CREATE TABLE Buyer (
    BuyerID NUMBER PRIMARY KEY,
    FirstName VARCHAR2(50) NOT NULL,
    LastName VARCHAR2(50) NOT NULL,
    Email VARCHAR2(100) UNIQUE,
    Address VARCHAR2(200)
);

CREATE TABLE Produce (
    ProduceID NUMBER PRIMARY KEY,
    FarmerID NUMBER,
    Name VARCHAR2(50) NOT NULL,
    Quantity NUMBER CHECK (Quantity >= 0),
    PricePerUnit NUMBER CHECK (PricePerUnit > 0),
    FOREIGN KEY (FarmerID) REFERENCES Farmer(FarmerID)
);

CREATE TABLE OrderTable (
    OrderID NUMBER PRIMARY KEY,
    BuyerID NUMBER,
    ProduceID NUMBER,
    OrderDate DATE DEFAULT SYSDATE,
    Quantity NUMBER CHECK (Quantity > 0),
    TotalAmount NUMBER,
    FOREIGN KEY (BuyerID) REFERENCES Buyer(BuyerID),
    FOREIGN KEY (ProduceID) REFERENCES Produce(ProduceID)
);

CREATE TABLE Logistics (
    LogisticsID NUMBER PRIMARY KEY,
    OrderID NUMBER,
    ProviderName VARCHAR2(100),
    DeliveryDate DATE,
    Status VARCHAR2(20) CHECK (Status IN ('Pending', 'In Transit', 'Delivered')),
    FOREIGN KEY (OrderID) REFERENCES OrderTable(OrderID)
);

CREATE TABLE Payment (
    PaymentID NUMBER PRIMARY KEY,
    OrderID NUMBER UNIQUE,
    Amount NUMBER CHECK (Amount > 0),
    PaymentDate DATE DEFAULT SYSDATE,
    Status VARCHAR2(20) CHECK (Status IN ('Pending', 'Completed', 'Failed')),
    FOREIGN KEY (OrderID) REFERENCES OrderTable(OrderID)
);

-- Data Insertion
INSERT INTO Farmer (FarmerID+-- Data Insertion
INSERT INTO Farmer (FarmerID, FirstName, LastName, Phone, Location) VALUES (1, 'John', 'Mugabo', '0781234567', 'Kigali');
INSERT INTO Farmer (FarmerID, FirstName, LastName, Phone, Location) VALUES (2, 'Marie', 'Uwase', '0798765432', 'Musanze');

INSERT INTO Buyer (BuyerID, FirstName, LastName, Email, Address) VALUES (1, 'Paul', 'Kagame', 'paul@example.com', 'Kigali City');
INSERT INTO Buyer (BuyerID, FirstName, LastName, Email, Address) VALUES (2, 'Jane', 'Akili', 'jane@example.com', 'Huye');

INSERT INTO Produce (ProduceID, FarmerID, Name, Quantity, PricePerUnit) VALUES (1, 1, 'Maize', 100, 500);
INSERT INTO Produce (ProduceID, FarmerID, Name, Quantity, PricePerUnit.AbsoluteZero) VALUES (2, 2, 'Beans', 80, 700);

INSERT INTO OrderTable (OrderID, BuyerID, ProduceID, OrderDate, Quantity, TotalAmount) VALUES (1, 1, 1, SYSDATE, 50, 25000);
INSERT INTO OrderTable (OrderID, BuyerID, ProduceID, OrderDate, Quantity, TotalAmount) VALUES (2, 2, 2, SYSDATE, 30, 21000);

INSERT INTO Logistics (LogisticsID, OrderID, ProviderName, DeliveryDate, Status) VALUES (1, 1, 'Rwanda Logistics', TO_DATE('2025-05-20', 'YYYY-MM-DD'), 'Pending');
INSERT INTO Logistics (LogisticsID, OrderID, ProviderName, DeliveryDate, Status) VALUES (2, 2, 'Fast Delivery', TO_DATE('2025-05-21', 'YYYY-MM-DD'), 'In Transit');

INSERT INTO Payment (PaymentID, OrderID, Amount, PaymentDate, Status) VALUES (1, 1, 25000, SYSDATE, 'Completed');
INSERT INTO Payment (PaymentID, OrderID, Amount, PaymentDate, Status) VALUES (2, 2, 21000, SYSDATE, 'Pending');
```
- **Triggers**:
```sql
-- Create Holiday Table
CREATE TABLE PublicHolidays (
    HolidayDate DATE PRIMARY KEY,
    HolidayName VARCHAR2(100)
);

-- Insert Holidays for June 2025
INSERT INTO PublicHolidays (HolidayDate, HolidayName) VALUES (TO_DATE('2025-06-01', 'YYYY-MM-DD'), 'Heroes Day');
INSERT INTO PublicHolidays (HolidayDate, HolidayName) VALUES (TO_DATE('2025-06-04', 'YYYY-MM-DD'), 'Liberation Day');

-- Create Audit Table
CREATE TABLE AuditLog (
    LogID NUMBER PRIMARY KEY,
    UserID VARCHAR2(50),
    ActionDate DATE,
    Operation VARCHAR2(50),
    TableName VARCHAR2(50),
    Status VARCHAR2(20)
);

-- Sequence for AuditLog
CREATE SEQUENCE AuditLog_Seq START WITH 1 INCREMENT BY 1;

-- Compound Trigger to Restrict DML and Log Actions
CREATE OR REPLACE TRIGGER Restrict_DML FOR INSERT OR UPDATE OR DELETE ON Farmer COMPOUND TRIGGER
    -- Variables declaration in declaration section
    v_day VARCHAR2(10);
    v_holiday NUMBER := 0;
    v_operation VARCHAR2(10);
    
    BEFORE STATEMENT IS
    BEGIN
        -- Determine the operation type
        IF INSERTING THEN
            v_operation := 'INSERT';
        ELSIF UPDATING THEN
            v_operation := 'UPDATE';
        ELSIF DELETING THEN
            v_operation := 'DELETE';
        END IF;
        
        -- Get the day of week
        SELECT TO_CHAR(SYSDATE, 'DY') INTO v_day FROM DUAL;
        
        -- Check if it's a weekend
        IF v_day IN ('SAT', 'SUN') THEN
            -- Log the denied operation
            INSERT INTO AuditLog (LogID, UserID, ActionDate, Operation, TableName, Status)
            VALUES (AuditLog_Seq.NEXTVAL, USER, SYSDATE, v_operation, 'Farmer', 'Denied - Weekend');
            
            -- Raise application error
            RAISE_APPLICATION_ERROR(-20001, 'DML operations are not allowed on weekends.');
        END IF;
        
        -- Check if it's a holiday
        BEGIN
            SELECT COUNT(*) INTO v_holiday
            FROM PublicHolidays
            WHERE HolidayDate = TRUNC(SYSDATE);
        EXCEPTION
            WHEN NO_DATA_FOUND THEN
                v_holiday := 0;
        END;
        
        IF v_holiday > 0 THEN
            -- Log the denied operation
            INSERT INTO AuditLog (LogID, UserID, ActionDate, Operation, TableName, Status)
            VALUES (AuditLog_Seq.NEXTVAL, USER, SYSDATE, v_operation, 'Farmer', 'Denied - Holiday');
            
            -- Raise application error
            RAISE_APPLICATION_ERROR(-20002, 'DML operations are not allowed on public holidays.');
        END IF;
    END BEFORE STATEMENT;
    
    AFTER STATEMENT IS
    BEGIN
        -- Log successful operation
        INSERT INTO AuditLog (LogID, UserID, ActionDate, Operation, TableName, Status)
        VALUES (AuditLog_Seq.NEXTVAL, USER, SYSDATE, v_operation, 'Farmer', 'Allowed');
    END AFTER STATEMENT;
END;
/
```
- **Procedures**:
```sql
-- Compound Trigger to Restrict DML and Log Actions
CREATE OR REPLACE TRIGGER Restrict_DML FOR INSERT OR UPDATE OR DELETE ON Farmer COMPOUND TRIGGER
    -- Variables declaration in declaration section
    v_day VARCHAR2(10);
    v_holiday NUMBER := 0;
    v_operation VARCHAR2(10);
    
    BEFORE STATEMENT IS
    BEGIN
        -- Determine the operation type
        IF INSERTING THEN
            v_operation := 'INSERT';
        ELSIF UPDATING THEN
            v_operation := 'UPDATE';
        ELSIF DELETING THEN
            v_operation := 'DELETE';
        END IF;
        
        -- Get the day of week
        SELECT TO_CHAR(SYSDATE, 'DY') INTO v_day FROM DUAL;
        
        -- Check if it's a weekend
        IF v_day IN ('SAT', 'SUN') THEN
            -- Log the denied operation
            INSERT INTO AuditLog (LogID, UserID, ActionDate, Operation, TableName, Status)
            VALUES (AuditLog_Seq.NEXTVAL, USER, SYSDATE, v_operation, 'Farmer', 'Denied - Weekend');
            
            -- Raise application error
            RAISE_APPLICATION_ERROR(-20001, 'DML operations are not allowed on weekends.');
        END IF;
        
        -- Check if it's a holiday
        BEGIN
            SELECT COUNT(*) INTO v_holiday
            FROM PublicHolidays
            WHERE HolidayDate = TRUNC(SYSDATE);
        EXCEPTION
            WHEN NO_DATA_FOUND THEN
                v_holiday := 0;
        END;
        
        IF v_holiday > 0 THEN
            -- Log the denied operation
            INSERT INTO AuditLog (LogID, UserID, ActionDate, Operation, TableName, Status)
            VALUES (AuditLog_Seq.NEXTVAL, USER, SYSDATE, v_operation, 'Farmer', 'Denied - Holiday');
            
            -- Raise application error
            RAISE_APPLICATION_ERROR(-20002, 'DML operations are not allowed on public holidays.');
        END IF;
    END BEFORE STATEMENT;
    
    AFTER STATEMENT IS
    BEGIN
        -- Log successful operation
        INSERT INTO AuditLog (LogID, UserID, ActionDate, Operation, TableName, Status)
        VALUES (AuditLog_Seq.NEXTVAL, USER, SYSDATE, v_operation, 'Farmer', 'Allowed');
    END AFTER STATEMENT;
END;
/
-- Stored Procedure for Order Processing
CREATE OR REPLACE PROCEDURE ProcessOrder (
    p_BuyerID IN NUMBER,
    p_ProduceID IN NUMBER,
    p_Quantity IN NUMBER
) AS
    v_Available NUMBER;
    v_Price NUMBER;
    v_OrderID NUMBER;
BEGIN
    -- Check availability
    SELECT Quantity, PricePerUnit INTO v_Available, v_Price
    FROM Produce
    WHERE ProduceID = p_ProduceID
    FOR UPDATE;
    
    IF v_Available < p_Quantity THEN
        RAISE_APPLICATION_ERROR(-20003, 'Insufficient stock.');
    END IF;
    
    -- Generate OrderID
    SELECT MAX(OrderID) + 1 INTO v_OrderID FROM OrderTable;
    IF v_OrderID IS NULL THEN
        v_OrderID := 1;
    END IF;
    
    -- Insert Order
    INSERT INTO OrderTable (OrderID, BuyerID, ProduceID, Quantity, TotalAmount)
    VALUES (v_OrderID, p_BuyerID, p_ProduceID, p_Quantity, p_Quantity * v_Price);
    
    -- Update Produce Quantity
    UPDATE Produce
    SET Quantity = Quantity - p_Quantity
    WHERE ProduceID = p_ProduceID;
    
    -- Insert Payment
    INSERT INTO Payment (PaymentID, OrderID, Amount, Status)
    VALUES (v_OrderID, v_OrderID, p_Quantity * v_Price, 'Pending');
    
    COMMIT;
EXCEPTION
    WHEN OTHERS THEN
        ROLLBACK;
        RAISE;
END;
/
```

## Results
- Automated order processing with real-time stock updates.
- Secured transactions with auditing and restrictions.
- Reduced wastage through demand-driven sales.
- Enhanced market access for farmers.

## Conclusion
The system addresses key challenges faced by Rwandan farmers, providing a scalable solution for fair trade and efficient supply chains.

## References
- Oracle PL/SQL Documentation
- BPMN 2.0 Specifications
