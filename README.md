# ba-portfolio
# Business Analyst Portfolio — 75-Day Capstone Program

This repo tracks my capstone project — modeled entirely on one business domain and extended progressively through each phase.

## 🚗 Project 1: Uber Ride Booking Analytics

An end-to-end business analysis and data project modeling the Uber ride-booking flow — from ride request to driver match, trip completion, and payment — to deliver actionable insights across bookings, cancellations, payments, and driver/customer experience.

This project focuses on process modeling, SQL-based analysis, and requirements-driven data design, extended through Phase 4.

### 📎 Scope Statement

"I will model the Uber ride-booking flow — from ride request to trip completion and payment — analyzing booking volume, cancellation patterns (by customer and by driver), and payment method performance, using a public Uber ride analytics dataset."

### 📌 Project Overview

Ride-hailing platforms process thousands of ride requests daily. Managing this reliably requires understanding how a ride request becomes a matched, completed, and paid trip — and where that process breaks down, whether through customer cancellations, driver cancellations, or incomplete rides.

This project addresses key business questions related to booking performance, cancellation drivers, payment success, and customer/driver satisfaction using SQL and process/data modeling (draw.io).

### 🎯 Business Objectives

- Monitor overall booking volume and ride completion performance
- Identify where and why rides fail to complete (customer cancellations, driver cancellations, incomplete rides)
- Analyze booking value and revenue by vehicle type and payment method
- Understand customer behavior across repeat vs. first-time riders
- Identify driver-matching and pickup delay patterns (VTAT/CTAT)
- Enable data-driven decisions to reduce ride cancellations and improve completion rate

### 📂 Dataset

Source: Uber Ride Analytics Dataset (public, Kaggle)

Booking-level transactional data including:

- Booking details (Booking ID, Booking Status, Booking Value, Timestamps)
- Payment details (Payment method — Credit Card, Debit Card, UPI, Cash)
- Customer information (Customer ID, ride history)
- Vehicle type and driver information
- Trip timelines (Avg VTAT — vehicle turnaround time, Avg CTAT — customer turnaround time)
- Cancellation details (cancelled by customer, cancelled by driver, incomplete rides, cancellation reason)
- Ratings (Driver rating, Customer rating)

### 🧱 Project Structure

Structured into analytical areas, each mapped to a business requirement (extended through later phases):

- Booking & Trip Overview
- Cancellation Analysis (customer vs. driver)
- Payment Performance
- Customer & Driver Behavior
- Revenue by Vehicle Type

### 🛠 Tools & Technologies

- SQL — DataLemur (learning) → Mode (project queries)
- draw.io — process flow & ER diagrams
- Requirements gathering & business process modeling
- GitHub — version-controlled portfolio

### 📈 Status

| Phase | Task | Status |
|---|---|---|
| Kickoff | Pick domain + set up toolkit | ✅ Done |
| Phase 1 | Document current state ('as-is') | ✅ Done |
| Phase 1 | Process flow diagram (draw.io) | ⬜ Not Started |
| Phase 1 | ER diagram of dataset tables | ⬜ Not Started |
| Phase 1 | First SQL queries on dataset | ⬜ Not Started |

### 👤 Author

Aspiring Business Analyst | SQL | Data Analytics
