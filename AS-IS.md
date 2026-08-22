# As-Is Process: Uber Ride Booking Flow

## Overview

Today, a rider's journey from requesting a ride to completing a paid trip passes through several stages — request, driver matching, pickup, trip execution, payment, and rating — each tracked separately with its own status codes and timestamps. There is no single, unified view of where a given booking stands at any point in time; visibility is fragmented across the request system, driver-matching engine, and payment processing. This document describes how the process currently works, based on the structure of the Uber Ride Analytics dataset (bookings, cancellations, payment methods, vehicle types, and ratings).

## Current Process Narrative

A customer opens the app and requests a ride, specifying pickup and drop locations and a vehicle type. The system attempts to **match** the request with an available driver. During this matching window, either the **customer can cancel** (e.g. changed plans, long wait time) or the **driver can cancel** (e.g. too far from pickup, other constraints) — both are tracked as distinct cancellation categories with separate reasons.

If a driver is successfully matched and accepts, the booking moves to **trip in progress**: the driver travels to the pickup point (tracked via VTAT — average vehicle turnaround time), picks up the customer, and completes the trip to the drop location (tracked via CTAT — average customer turnaround time). Some bookings end as **incomplete rides** — trips that started but did not finish as expected, for reasons distinct from pre-trip cancellations.

Once the trip is completed, payment is settled through one of several methods — Credit Card, Debit Card, UPI, or Cash — and the booking value is recorded. After payment, both the **customer rates the driver** and the **driver rates the customer**, closing the loop on the transaction.

Each of these stages — request, match, cancel/accept, trip execution, payment, rating — is currently tracked as booking-level status data, but there is no real-time operational view that ties a single ride's full lifecycle together as it happens. Today, understanding what went wrong (or right) with ride completion happens retroactively, through analysis of historical booking status and cancellation-reason data, rather than through live process monitoring.

## Stakeholders Involved

- **Riders (customers)** — request rides, select vehicle type, may cancel before pickup, pay for and rate completed trips.
- **Drivers** — accept or decline/cancel ride requests, execute trips, rate customers.
- **Payment providers** — process card and UPI payments; cash is settled directly between driver and rider.
- **Platform operations/analytics teams** — monitor booking volume, cancellation rates, and completion performance after the fact.

## Pain Points in the Current State

1. **Cancellation reasons are captured but not acted on in real time.** Both customer-initiated and driver-initiated cancellations are logged with reasons, but there is no current process step that intervenes during the matching window to reduce cancellation likelihood (e.g. rematching proactively, surfacing wait-time expectations).
2. **Driver cancellations and customer cancellations are tracked separately with no unified "booking failure" view**, making it harder to see the full picture of why a given ride never happened without joining across cancellation categories.
3. **Incomplete rides are a distinct, under-addressed failure mode.** A trip that starts but doesn't finish is operationally different from a pre-trip cancellation, yet the current process has no clear escalation or resolution path once a ride is marked incomplete.
4. **Payment method creates uneven risk exposure.** Cash payments settle outside the platform's payment infrastructure entirely, meaning there's no system-level confirmation that payment was actually collected — unlike Card or UPI, which are processed and confirmed digitally.
5. **Pickup delay (VTAT) is only visible in aggregate, after the fact**, rather than being surfaced to the rider or flagged operationally in the moment a match results in an unusually long driver ETA.
6. **Repeat vs. first-time rider behavior is not treated differently operationally**, even though cancellation tendencies, price sensitivity, and trust in the platform likely differ meaningfully between the two groups.
7. **No unified booking-status view.** Reconstructing a single ride's full lifecycle — request, match attempt, cancellation or completion, payment, rating — currently requires joining across multiple status fields and categories rather than consulting one source of truth.

## Why This Matters

These gaps directly limit the platform's ability to reduce cancellations, respond to incomplete rides, and understand payment-method risk — the objectives at the center of this project. This as-is documentation will serve as the baseline for Strategy Analysis: identifying which of these pain points represent the highest-value opportunities for change, and what a "to-be" state should look like in Phase 2.
