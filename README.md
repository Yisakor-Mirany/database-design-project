# Photography Business Database — EER & Sample Data

**Files included**  
- `EER/EER_Diagram_Photography.png`: Enhanced ER diagram with entities, PK/FK labels, and cardinalities.  
- `data/Sample_Data_Photography.xlsx`: 8 sheets with ~40 rows each (synthetic, realistic values).  
- `docs/Normalization_Report.pdf`: Documentation of normalization to 3NF with analysis and scenarios.  
- `docs/README_with_Queries.pdf`: polished PDF version of this README (optional).  
- `sql/example_queries.sql`: example SQL queries demonstrating common lookups.

## Design Summary
This database models a small photography studio’s core operations. The main entities are Clients, Packages, Locations, Staff, Bookings, Invoices, Deliveries, and the junction BookingStaff. Bookings references one client, one package, and one location (all 1:M). Invoices are modeled 1:1 with bookings via a unique foreign key to simplify “one bill per booking.” Deliveries are 1:M from bookings, allowing multiple deliverables (proofs, finals, prints). Staff participate in many bookings and each booking can include many staff, captured by BookingStaff with a composite PK (booking_id, staff_id) and role. Key constraints include non-null FKs on Bookings, invoice totals (amount + tax), and end_datetime > start_datetime.

The database has been normalized through 1NF, 2NF, and 3NF. Each attribute depends only on its PK, partial dependencies were removed, and no transitive dependencies remain. This ensures data integrity and efficient querying. Sample data (~40 rows/table) provides realistic 2024–2025 values to support testing, reporting, and normalization.

---

## Example SQL Queries

### Query 1: Staff members and their roles for wedding sessions
```sql
SELECT 
    b.booking_id,
    s.staff_id,
    s.first_name,
    s.last_name,
    bs.role
FROM Bookings b
JOIN BookingStaff bs ON b.booking_id = bs.booking_id
JOIN Staff s ON bs.staff_id = s.staff_id
JOIN Packages p ON b.package_id = p.package_id
WHERE p.package_type = 'Wedding';
