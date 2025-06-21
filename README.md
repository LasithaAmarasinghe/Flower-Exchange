# Flower-Exchange

## Project Overview
The Flower Exchange project is a simple trading system that enables traders to submit buy or sell orders for flowers through a Trader Application. The Exchange Application processes these orders against existing orders in the order book and executes them, providing an execution report. The system supports validation, rejection of invalid orders, and full/partial execution of valid orders.

## Key Features
- **Trader Application**: Allows traders to submit buy or sell orders.
- **Exchange Application**: Processes the orders and provides execution reports.
- **Order Book**: Stores buy and sell orders for each flower type (e.g., Rose, Lavender, Lotus).
- **Execution Report**: Contains status and details of the execution (e.g., fill, reject, partially filled).
- **Order Validation**: Ensures that orders are valid, rejecting orders with invalid data.

## C++ Concepts Used
- **Classes and Objects**: Used for representing different entities like orders, traders, and the exchange system.
- **Encapsulation**: Ensures that the internal details of each component (such as order processing and execution reports) are hidden from the outside.
- **Inheritance**: Can be used to extend base functionality for different types of orders or flowers.
- **Polymorphism**: Allows for flexible order matching and report generation, depending on the type of order (buy/sell).
- **File Handling**: Reading from and writing to CSV files for order input and execution reports.

## High-Level Architecture
![High-Level Architecture](https://github.com/user-attachments/assets/4a0d7264-c9f5-4a97-b0ce-db07971f113a)

The system consists of two main components:
- **Trader Application**: Submits orders.
- **Exchange Application**: Processes orders against the order book and generates execution reports.

## Input Order Format
Orders are submitted in CSV format with the following fields:
- **Client Order ID**: Unique identifier (max 7 chars).
- **Instrument**: Flower type (e.g., Rose, Lavender, etc.).
- **Side**: 1 for Buy, 2 for Sell.
- **Price**: Price per unit (greater than 0).
- **Quantity**: Order size (must be a multiple of 10, min 10, max 1000).

### Example Input (`orders.csv`)
```csv
Client Order ID, Instrument, Side, Price, Quantity
ORD12345, Rose, 1, 50.00, 100
ORD12346, Lavender, 2, 45.00, 200
```

## Execution Report Format
The execution report contains the following fields:

- **Client Order ID**: The original order's ID.
- **Order ID**: System-generated unique ID.
- **Instrument**: Flower type.
- **Side**: Buy (1) or Sell (2).
- **Price**: Price per unit.
- **Quantity**: Quantity of the order.
- **Status**: 
  - 0 (New)
  - 1 (Rejected)
  - 2 (Fill)
  - 3 (Partial Fill)
- **Reason**: Reason for rejection (if applicable).
- **Transaction Time**: Timestamp of the transaction.

### Example Execution Report (`execution_rep.csv`)
```csv
Client Order ID, Order ID, Instrument, Side, Price, Quantity, Status, Reason, Transaction Time
ORD12345, 001, Rose, 1, 50.00, 100, 2, , 20240704-101500.123
ORD12346, 002, Lavender, 2, 45.00, 200, 1, Invalid Quantity, 20240704-101502.456
```

## Order Book Management
- **Buy Side**: Sorted in ascending order of price (higher price = more attractive).
- **Sell Side**: Sorted in descending order of price (lower price = more attractive).
- Orders with the same price are prioritized by time.

### Example Order Book
- **Initial State**: Empty order book.
- **After Order Entry**: Orders are placed on the appropriate side (Buy/Sell).
- **Execution**: Orders are matched, and an execution report is generated.

## Order Execution Scenarios
- **Full Fill (FILL)**: An incoming order completely matches an existing order.
- **Partial Fill (PFILL)**: Part of an incoming order matches an existing order.

## Input Validations
Orders will be rejected if:
- Missing required fields.
- Invalid instrument or side.
- Price is less than or equal to 0.
- Quantity is not a multiple of 10 or outside the valid range (10 to 1000).

## Contributors
* Lasitha Amarasinghe
* Sahan Abeyrathna
