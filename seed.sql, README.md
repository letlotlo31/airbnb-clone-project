-- AirBnB Clone Database Seeding Script
-- This script populates the database with sample data for testing purposes.
-- UUIDs are pre-generated to ensure foreign key consistency.

-- 1. Insert Users (1 Host, 1 Guest, 1 Admin)
-- Host: John Doe
INSERT INTO User (user_id, first_name, last_name, email, password_hash, phone_number, role)
VALUES 
('uuid-user-1', 'John', 'Doe', 'john.doe@example.com', 'hashed_pass_1', '1234567890', 'host'),
-- Guest: Jane Smith
('uuid-user-2', 'Jane', 'Smith', 'jane.smith@example.com', 'hashed_pass_2', '0987654321', 'guest'),
-- Admin: Alice Admin
('uuid-user-3', 'Alice', 'Admin', 'alice.admin@example.com', 'hashed_pass_3', '1122334455', 'admin');

-- 2. Insert Properties
-- Property owned by John Doe (uuid-user-1)
INSERT INTO Property (property_id, host_id, name, description, location, pricepernight)
VALUES 
('uuid-prop-1', 'uuid-user-1', 'Cozy Cottage', 'A beautiful cottage in the woods.', 'Woodland, CA', 120.00),
('uuid-prop-2', 'uuid-user-1', 'Modern Downtown Apt', 'Walking distance to everything.', 'New York, NY', 250.00);

-- 3. Insert Bookings
-- Jane Smith (uuid-user-2) books the Cozy Cottage (uuid-prop-1)
INSERT INTO Booking (booking_id, property_id, user_id, start_date, end_date, total_price, status)
VALUES 
('uuid-booking-1', 'uuid-prop-1', 'uuid-user-2', '2024-12-01', '2024-12-05', 480.00, 'confirmed'),
('uuid-booking-2', 'uuid-prop-2', 'uuid-user-2', '2025-01-10', '2025-01-15', 1250.00, 'pending');

-- 4. Insert Payments
-- Payment for the confirmed booking (uuid-booking-1)
INSERT INTO Payment (payment_id, booking_id, amount, payment_date, payment_method)
VALUES 
('uuid-payment-1', 'uuid-booking-1', 480.00, '2024-11-25 10:00:00', 'credit_card');

-- 5. Insert Reviews
-- Jane Smith (uuid-user-2) reviews the Cozy Cottage (uuid-prop-1)
INSERT INTO Review (review_id, property_id, user_id, rating, comment)
VALUES 
('uuid-review-1', 'uuid-prop-1', 'uuid-user-2', 5, 'Absolutely loved the stay! Very cozy indeed.');

-- 6. Insert Messages
-- Communication between Jane (Guest) and John (Host)
INSERT INTO Message (message_id, sender_id, recipient_id, message_body, sent_at)
VALUES 
('uuid-msg-1', 'uuid-user-2', 'uuid-user-1', 'Hi John, is the cottage pet-friendly?', '2024-11-20 14:00:00'),
('uuid-msg-2', 'uuid-user-1', 'uuid-user-2', 'Hi Jane, yes it is! We love dogs.', '2024-11-20 14:30:00');


Database Script 0x02

This directory contains the SQL Data Manipulation Language (DML) script to populate the AirBnB clone database with sample data.

Files

seed.sql: Contains INSERT statements to add users, properties, bookings, payments, reviews, and messages.

Usage

To execute this script against your MySQL database (after running the schema script from 0x01), run:

cat seed.sql | mysql -u <username> -p <database_name>


Data Overview

The script creates a realistic scenario:

Users: Creates a Host (John), a Guest (Jane), and an Admin (Alice).

Properties: John lists two properties ("Cozy Cottage" and "Downtown Apt").

Flow: Jane books the cottage, pays for it, and leaves a 5-star review.

Communication: Includes a message thread between Jane and John regarding pet policies.
