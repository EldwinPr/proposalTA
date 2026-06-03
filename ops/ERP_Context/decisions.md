# Architectural Decisions Log

## DECISION-01: Separation of Value Chain (Flow) and Capacity Management (Schedule)

**Date**: 2026-03-30
**Status**: Accepted

### Context
There was a question of whether `UC-20-22` (Schedule Management) should be part of the main "Operational Flow" (Value Chain). 

### Decision
We have decided to decouple **Schedule Management** from the **Sales Order Chain**. 

1. **The Operational Flow** (UC-01 to UC-25) represents the lifecycle of a specific Sample/SO.
2. **The Schedule Management** (UC-20-22) represents the availability of the Lab's resources (Machines and Staff).

### Consequence
- **Proactive Planning**: Scheduling can (and should) happen independently of specific Sales Orders. You can schedule staff for the next 3 months without knowing which samples will arrive.
- **Dynamic Matching**: The matching of a Sample to a Schedule happens at the last possible moment (In the "Antrian" or Queue), allowing for maximum flexibility if a machine breaks down or a staff member is sick.
- **Simplified Schema**: We do not link `jadwal_pengujian` directly to `sales_orders`. Instead, they meet at the `Alat` (Machine) level.

---

## DECISION-03: Coordinate-Based Labeling Architecture (X.Y.Z/AB/N)

**Date**: 2026-03-31
**Status**: Accepted

### Context
The previous `kode_sampling` was unconventional and lacked structural meaning for lab technicians. We need a system that maps a physical sample to its exact "coordinate" within a Sales Order.

### Decision
We will implement a **Coordinate-Based Identity** for every sample: `{X}.{Y}.{Z}/{AB}/{N}`.

1.  **X (SOD Rank)**: Sequential index of the `SalesOrderDetail` within the SO.
2.  **Y (Titik)**: Sampling point number. `0` if `is_composite_titik = true`.
3.  **Z (Freq)**: Frequency number. `0` if `is_composite_frekuensi = true`.
4.  **AB (Matrix Code)**: A single-letter abbreviation from the `produk_ujis` table (e.g., `A`, `B`).
5.  **N (Sample Rank)**: Sequential index of the physical bottle/sample within that specific Spot/Freq.

### Consequence
- **Database Renaming**: `sales_order_details.kode_sampling` will be renamed to `kode_titik`.
- **New Columns**: 
    - `sales_order_details` gets `nomor_urut` (X).
    - `samples` gets `nomor_urut` (N) and `label_alias` (the full pre-calculated string).
    - `produk_ujis` gets `singkatan` (AB).
- **QR Integrity**: The QR code on the sticker will contain the **Sample ULID** for 100% database integrity, while the human-readable label displays the coordinate string.
- **Searchability**: The system must allow searching by both the ULID (Scan) and the `label_alias` (Manual).
