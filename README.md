Photography Business Database — EER & Sample Data

**Files included**

EER_Diagram_Photography.png: Enhanced ER diagram with entities, PK/FK labels, and cardinalities.

Sample_Data_Photography.xlsx: 8 sheets with ~40 rows each (synthetic, realistic values).

README.md: detailed design explanation.

**Design Summary**

This database is designed to support the operations of a small photography studio by organizing client information, bookings, payments, staff assignments, and deliverables. The core entities are Clients, Packages, Locations, Staff, Bookings, Invoices, PhotoDeliveries, and a junction table BookingStaff to model many-to-many staff participation. Each entity has a clearly defined primary key and relevant attributes such as contact details, pricing, session details, and delivery formats.

The Bookings table serves as the central hub, connecting to clients, packages, and locations (1:M relationships). Each booking generates exactly one Invoice (1:1) with amount and tax calculations, ensuring accurate billing. PhotoDeliveries link back to bookings in a 1:M relationship, capturing different types of outputs like proofs, edited images, or printed albums. The BookingStaff junction table manages many-to-many scheduling between staff and bookings, with a composite key (booking_id, staff_id) and a role attribute to record responsibilities.

Constraints ensure logical consistency: bookings must reference valid clients, packages, and locations; staff assignments require non-null roles; invoice totals must be non-negative; and booking times enforce end > start. These constraints help maintain data quality and integrity.

Sample data (≈40 rows per table) provides realistic values such as session dates from 2024–2025, multiple payment methods, varied package pricing, and delivery links. This enables meaningful testing, reporting, and validation of normalization. Overall, the design balances flexibility and structure to support real-world studio operations.
