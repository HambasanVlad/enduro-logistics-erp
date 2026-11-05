# Enduro ERP - Logistics & Fleet Manager

> A Native Enterprise Resource Planning (ERP) application tailored for hard enduro tour operations and race support logistics.

## 1. Project Description

The objective of this project is to develop a Native mobile application designed to efficiently manage the operations of hard enduro tour and race support companies. Managing dozens of clients, a large fleet of motorcycles, and complex logistics at extreme events (e.g., Red Bull Romaniacs, Sea to Sky) presents significant challenges in the field. 

This application allows tour managers to track scheduled events, monitor the maintenance schedule for every motorcycle (engine hours, spare parts), manage task checklists, and calculate the balance of costs and profit per event. With this tool, daily business and race management become organized, secure, and data-driven, directly from the racing paddock.

## 2. Domain Details (Data Models)

The main entities tracked within the system are the **Tour Profile** and the **Bike Profile**. For each entity, the application records the following details:

### For Tours/Races
- **Name and Type:** The specific event or package (e.g., "Romaniacs Support Package" or "Weekend Enduro Tour").
- **Dates and Calendar:** The start and end dates integrated into the general company schedule.
- **Rider List & Assignments:** The list of participating clients and the specific motorcycles assigned to them.
- **Financials (Costs and Profit):** The collected revenue versus operational expenses (fuel, mechanic daily rates, accommodation, spare parts consumed from inventory).
- **To-Do List:** Operational and logistical checklists (e.g., "Prep 5 bikes," "Restock 2-stroke oil").

### For Motorcycles (Fleet)
- **Identification (VIN) / Model:** The specific make and model of the motorcycle (e.g., KTM 300 EXC).
- **Engine Hours:** The total running hours of the engine, which is the primary metric for scheduling maintenance.
- **Maintenance Status:** Alerts and logs for scheduled interventions like oil changes, piston replacements, or tire swaps.
- **Availability:** The current status of the motorcycle (available, in the shop for repairs, or allocated to an active tour).

## 3. App Operations (Managing the Logistics)

The system supports the following core interactions for managing logistics:

- **Adding an Entity (Create):** When planning a new tour or acquiring a new motorcycle, the user opens an "Add Tour/Bike" form, inputs the basic details (dates, model, estimated budget), and saves it to the central database.
- **Viewing Details (Read):** Users access a main list view and a calendar showing all upcoming tours. Tapping on a specific tour reveals a detailed dashboard displaying logistical checklists, assigned mechanics, allocated motorcycles, and real-time profit calculations.
- **Updating Information (Update):** After a riding session or post-race, mechanics and managers open bike profiles to log new engine hours, check off completed items from the tour's to-do list, and record unexpected field expenses.
- **Removing an Entity (Delete):** If a tour is canceled or a motorcycle is sold, the user can permanently remove or archive the profile from active lists, ensuring calendar and financial data remain accurate.

## 4. Data Storage and Cloud Backup (Persistence)

To ensure business and fleet data is secure and consistently accessible, the application utilizes a dual-storage architecture. Data is saved both locally on the mobile device (e.g., SQLite/Realm) and centrally on a backend server. Specifically, the following operations must be persisted across **both** layers:

1. **Creating** a new tour or registering a new motorcycle.
2. **Updating** a motorcycle's engine hours, a tour's checklist, or financial records.
3. **Deleting or archiving** an entity from the system.

This dual approach guarantees fast UI performance through local reads, while background server synchronization prevents data loss in case a device is damaged or lost during a tour.

## 5. Field Operations (Offline Protocol)

Because mountainous terrains or remote racing paddocks often lack cellular service, the native application is built with an offline-first architecture. The system handles connectivity drops as follows:

- **Offline Adding (Create):** If a user adds a new expense or task without an internet connection, the app immediately writes the data to the local mobile database. Upon reconnecting to Wi-Fi or cellular data, the app automatically uploads the new records to the central server via a background synchronization queue.
- **Offline Viewing (Read):** Users can view the entire calendar, tour schedules, and required spare parts lists regardless of signal strength. All read operations query the local database directly.
- **Offline Editing (Update):** Engine hours or task updates recorded offline are saved locally and flagged for synchronization. The system resolves these queued changes with the backend once connectivity is restored.
- **Offline Removing (Delete):** Canceled tasks or tours are immediately hidden from the user interface. The deletion command is cached locally and executed on the main server during the next synchronization cycle.

---

## Tech Stack (Proposed)
- **Frontend / Mobile:** React Native or Flutter (iOS & Android)
- **Local Storage:** SQLite / WatermelonDB
- **Backend:** Node.js (Express/NestJS) or Python (FastAPI)
- **Remote Database:** PostgreSQL

## App Mockups

<p align="center">
  <img src="https://github.com/user-attachments/assets/0b1797f7-f7f2-4e8f-967f-a3277892ee5f" width="200" />
  <img src="https://github.com/user-attachments/assets/778d7c7e-fac8-48f6-b73f-a1ad70d66684" width="200" />
  <img src="https://github.com/user-attachments/assets/1afbf4b9-3a67-4ddd-abe3-fb46596f5c37" width="200" />
  <img src="https://github.com/user-attachments/assets/ac9e7ffe-ff54-4d47-8c25-acb888d5764d" width="200" />
</p>
