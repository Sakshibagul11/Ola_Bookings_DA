# 🚖 OLA Data Analyst [Power BI & SQL]

The OLA Data Analyst Project analyzes ride-booking data using SQL and Power BI to track ride volumes, customer behavior, and driver performance. It focuses on booking statuses, revenue breakdowns by payment method, and top customers. SQL queries are used to calculate ride statistics, and the final Power BI dashboard visualizes key data, including ride volumes, vehicle performance, and sales. The analysis helps optimize OLA's services by identifying trends and areas for improvement.

# 🚖 OLA DA [SQL]

## 📂 Introduction to the Database
This project involves analyzing ride bookings data for a ride-hailing service, "OLA." The database contains various tables (e.g., `bookings`, `customers`, and `drivers`) that store information about ride bookings, customer ratings, driver ratings, vehicle types, payment methods, and more.

The main objective of this project is to extract meaningful insights and statistics using SQL queries. This document showcases a set of queries to answer specific analytical questions about the business performance and customer behavior.

### 🛠️ How the Database Works

- **📊 Tables**: The database is primarily focused on the `bookings` table, which contains the following key columns:

  - `Booking_ID`: Unique identifier for each ride.
  - `Customer_ID`: ID of the customer who booked the ride.
  - `Vehicle_Type`: Type of vehicle used (e.g., Prime Sedan, Auto, etc.).
  - `Booking_Status`: Status of the ride (e.g., `Success`, `Cancelled by Customer`, etc.).
  - `Ride_Distance`: Distance covered in the ride (in kilometers).
  - `Payment_Method`: Mode of payment used for the ride (e.g., UPI, Card, Cash).
  - `Driver_Ratings`: Ratings provided by customers to the drivers (out of 5).
  - `Customer_Rating`: Ratings provided by drivers to the customers (out of 5).
  - `Booking_Value`: Monetary value of the completed ride.
  - `Incomplete_Rides`: A flag to indicate whether the ride was completed or not.
  - `Incomplete_Rides_Reason`: If the ride was incomplete, this column stores the reason.

- **🔍 Views**: This document includes SQL `CREATE VIEW` statements to predefine specific datasets and make querying simpler for repetitive tasks.

- **📈 Key Insights**: Using SQL, we retrieve data that helps us answer questions such as:
  - The top-performing customers.
  - Average ratings and distances.
  - Trends in cancellations by drivers and customers.
  - The total revenue from successful rides.

---

## 🏗️ Database Setup

```sql
CREATE DATABASE Ola;
USE Ola;
```

## 📜 SQL Queries & Answers

### 1️⃣ Retrieve all successful bookings:

**📝 Query:**

```sql
CREATE VIEW Successful_Bookings AS
SELECT *
FROM bookings
WHERE Booking_Status = 'Success';
```

**📊 Answer:**

```sql
SELECT * FROM Successful_Bookings;
```
![Description of the screenshot](https://github.com/Sakshibagul11/Ola_Bookings_DA/blob/main/success_bookings.png)

---

### 2️⃣ Find the average ride distance for each vehicle type:

**📝 Query:**

```sql
CREATE VIEW ride_distance_for_each_vehicle AS
SELECT Vehicle_Type, AVG(Ride_Distance) AS avg_distance
FROM bookings
GROUP BY Vehicle_Type;
```

**📊 Answer:**

```sql
SELECT * FROM ride_distance_for_each_vehicle;
```

![Description of the screenshot](https://github.com/Sakshibagul11/Ola_Bookings_DA/blob/main/vehicle.png)

---

### 3️⃣ Get the total number of cancelled rides by customers:

**📝 Query:**

```sql
CREATE VIEW cancelled_rides_by_customers AS
SELECT COUNT(*) AS total_cancelled_rides
FROM bookings
WHERE Booking_Status = 'cancelled by Customer';
```

**📊 Answer:**

```sql
SELECT * FROM cancelled_rides_by_customers;
```

![Description of the screenshot](https://github.com/Sakshibagul11/Ola_Bookings_DA/blob/main/Count.png)

---

### 4️⃣ List the top 5 customers who booked the highest number of rides:

**📝 Query:**

```sql
CREATE VIEW Top_5_Customers AS
SELECT Customer_ID, COUNT(Booking_ID) AS total_rides
FROM bookings
GROUP BY Customer_ID
ORDER BY total_rides DESC
LIMIT 5;
```

**📊 Answer:**

```sql
SELECT * FROM Top_5_Customers;
```

![Description of the screenshot](https://github.com/Sakshibagul11/Ola_Bookings_DA/blob/main/Total_Rides.png)

---

### 5️⃣ Get the number of rides cancelled by drivers due to personal and car-related issues:

**📝 Query:**

```sql
CREATE VIEW Rides_cancelled_by_Drivers_P_C_Issues AS
SELECT COUNT(*) AS cancelled_by_drivers
FROM bookings
WHERE cancelled_Rides_by_Driver = 'Personal & Car related issue';
```

**📊 Answer:**

```sql
SELECT * FROM Rides_cancelled_by_Drivers_P_C_Issues;
```

![Description of the screenshot](https://github.com/Sakshibagul11/Ola_Bookings_DA/blob/main/Count_.png)

---

### 6️⃣ Find the maximum and minimum driver ratings for Prime Sedan bookings:

**📝 Query:**

```sql
CREATE VIEW Max_Min_Driver_Rating AS
SELECT MAX(Driver_Ratings) AS max_rating,
       MIN(Driver_Ratings) AS min_rating
FROM bookings
WHERE Vehicle_Type = 'Prime Sedan';
```

**📊 Answer:**

```sql
SELECT * FROM Max_Min_Driver_Rating;
```

![Description of the screenshot](https://github.com/Sakshibagul11/Ola_Bookings_DA/blob/main/Max_Min_Ratings.png)

---

### 7️⃣ Retrieve all rides where payment was made using UPI:

**📝 Query:**

```sql
CREATE VIEW UPI_Payment AS
SELECT *
FROM bookings
WHERE Payment_Method = 'UPI';
```

**📊 Answer:**

```sql
SELECT * FROM UPI_Payment;
```

![Description of the screenshot](https://github.com/Sakshibagul11/Ola_Bookings_DA/blob/main/Successful.png)

---

### 8️⃣ Find the average customer rating per vehicle type:

**📝 Query:**

```sql
CREATE VIEW AVG_Cust_Rating AS
SELECT Vehicle_Type, AVG(Customer_Rating) AS avg_customer_rating
FROM bookings
GROUP BY Vehicle_Type;
```

**📊 Answer:**

```sql
SELECT * FROM AVG_Cust_Rating;
```

![Description of the screenshot]()

---
