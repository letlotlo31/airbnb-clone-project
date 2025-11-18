# Database Normalization Process

This document explains the steps taken to ensure the AirBnB Clone database schema adheres to the Third Normal Form (3NF) to reduce redundancy and improve data integrity.

## Step 1: First Normal Form (1NF)
**Objective:** Ensure atomicity and uniqueness.
* **Rule:** Each table cell should contain a single value, and each record needs to be unique.
* **Application:**
    * We ensured that no fields contain lists or arrays of data. For example, instead of storing multiple `reviews` inside a single "Property" row, we created a separate `Review` table.
    * All attributes (e.g., `first_name`, `email`, `price_per_night`) contain atomic, indivisible values.
    * Every table has a primary key (`user_id`, `property_id`, etc.) to uniquely identify rows.

## Step 2: Second Normal Form (2NF)
**Objective:** Remove partial dependencies.
* **Rule:** All non-key attributes must be fully dependent on the entire primary key. This mostly applies to tables with composite primary keys.
* **Application:**
    * Since our schema uses single unique identifiers (UUIDs) as Primary Keys for all tables (e.g., `booking_id` is the PK, not a combination of `user_id` + `property_id`), partial dependency is automatically eliminated.
    * Every non-key attribute (like `status` in the Booking table) depends entirely on the specific `booking_id`, not just part of it.

## Step 3: Third Normal Form (3NF)
**Objective:** Remove transitive dependencies.
* **Rule:** Non-key attributes should depend *only* on the primary key, not on other non-key attributes. (Attributes shouldn't depend on "fields other than the ID").
* **Application:**
    * **Users Table:** `first_name`, `last_name`, and `email` depend solely on `user_id`. We do not store zip codes or city names that might depend on each other within this table.
    * **Properties Table:** We store `host_id` (Foreign Key) rather than the host's name or email. If we stored `host_name` here, it would depend on `host_id`, creating a transitive dependency. By using the Foreign Key, we satisfy 3NF.
    * **Bookings Table:** We link to `property_id` and `user_id`. We do not store property details (like `property_name`) inside the booking record. This ensures that if a property name changes, the booking record does not become outdated.
    * **Constraint:** The `total_price` in Bookings could technically be calculated from `price_per_night` * `days`. However, we store it explicitly to preserve historical accuracy (snapshotting) in case the property price changes later. This is a deliberate design choice for business logic, even if strictly redundant.

## Conclusion
The database schema is normalized to 3NF. Relationships are handled via Foreign Keys, ensuring that data is stored in only one place and referenced elsewhere.
