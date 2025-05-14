# Order Processing UML Activity Diagram

## Scope
This UML Activity Diagram models the order processing workflow for the market access system, enabling Rwandan smallholder farmers to sell produce directly to buyers with automated logistics and payment handling. The process supports MIS by streamlining data flow, enhancing decision-making, and improving operational efficiency.

## Key Entities and Roles
- **Farmer**: Lists available produce and confirms order availability.
- **Buyer**: Browses produce, places orders, and initiates payments.
- **Logistics Provider**: Schedules and tracks deliveries.
- **System Admin**: Monitors system operations and resolves disputes.
- **Database**: Stores and processes transaction data (orders, payments, logistics).

## UML Activity Diagram Overview
- **Swimlanes**: Separate lanes for Farmer, Buyer, Logistics Provider, System Admin, and Database to delineate responsibilities.
- **Flow**:
  1. **Initial Node**: Buyer starts by browsing available produce.
  2. **Activity (Buyer)**: Buyer submits an order request.
  3. **Decision Node**: Database checks produce availability.
     - If available, proceed to Farmer confirmation.
     - If unavailable, notify Buyer and end process.
  4. **Activity (Farmer)**: Farmer confirms order and updates stock.
  5. **Activity (Database)**: Records order details and triggers payment process.
  6. **Activity (Buyer)**: Buyer completes payment.
  7. **Decision Node**: Database validates payment.
     - If successful, proceed to logistics.
     - If failed, notify Buyer and cancel order.
  8. **Activity (Logistics Provider)**: Schedules delivery and updates tracking status.
  9. **Activity (Database)**: Updates order status to 'Delivered'.
  10. **Final Node**: Buyer receives produce, completing the transaction.
- **Data Flows**: Represented by object flows (e.g., order details, payment status) between activities and the Database.
- **Decision Points**: Availability check, payment validation, and delivery confirmation.

## MIS Alignment
- **Decision-Making**: Real-time stock and order data enable fair pricing and demand forecasting.
- **Operational Efficiency**: Automation of order, payment, and logistics processes reduces manual effort.
- **Data Integrity**: Centralized database ensures consistent and accurate transaction records for auditing and reporting.

## Tools
- Diagram created using Lucidchart or draw.io, adhering to UML 2.0 Activity Diagram notations.
- Swimlanes color-coded for clarity, with labeled activities and transitions.
- Exported as PNG for submission.

## Importance
The UML Activity Diagram clarifies the interaction between farmers, buyers, and logistics providers, eliminating middlemen and reducing post-harvest wastage through demand-driven sales. It supports MIS by providing a structured workflow that enhances transparency and efficiency in the market access system.

## Submission
- Include the UML diagram (PNG) and this description (PDF) in the GitHub repository under `Phase_III`.
- File name: `Tues_26578_Honore_MarketAccess_DB_PhaseIII_UMLDiagram`.