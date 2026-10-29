# POS — Hospitality & Retail Management Platform

An offline-first POS platform connecting restaurant operations, hotel management, banquet bookings, inventory, and billing through web and Windows desktop applications.

**Developer / Project Lead:** Jagdish Patidar  
**Company:** Drunall Technologies  
**Project type:** POS & Business Management Software  
**Repository type:** Public product case study  
**Source code:** Private  

[Visit the Web Portal](https://pos.jdpatidar.com/login)

> This repository contains product documentation only. The live portal requires authorized access.

## Overview

POS brings several hospitality and retail workflows into a modular application.

Businesses can use the modules relevant to their operations: restaurant, hotel, banquet, and inventory management.

The platform combines a cloud backend with local data storage and background synchronization. Supported operational workflows can continue during connectivity interruptions, with pending records synchronized when connectivity returns.

A React and TypeScript frontend supports browser access and a Windows desktop application packaged with Electron.

## Business Challenge

Hospitality and retail teams manage connected activities that often span multiple tools:

- Restaurant tables, orders, kitchen tickets, and bills.
- Hotel room allocation, guest records, and settlements.
- Banquet availability, event packages, and food orders.
- Inventory balances, purchases, and supplier payments.
- Receipt printing and customer communication.
- Operations during unreliable internet connectivity.
- Module access and licensing across different businesses.

POS connects these workflows while allowing businesses to use a selected combination of modules.

## My Contribution

As developer and project lead, I worked on the platform's application structure and business workflows, including:

- Modular frontend and backend organization.
- Restaurant, hotel, banquet, and inventory functionality.
- Local data storage and background synchronization.
- Billing, document generation, and printing workflows.
- Windows desktop packaging.
- Tenant administration and licensing.
- Customer messaging integrations.

## Core Business Modules

### 1. Restaurant & Dine-In Management

Tools for managing seating, menus, orders, and billing.

- Configure floor sections and dining tables.
- Track table statuses.
- Organize menu categories, items, and modifiers.
- Manage price lists and pricing history.
- Create Kitchen Order Tickets (KOT).
- Transfer tables and route orders to the kitchen.
- Split bills and apply discounts.
- Display configured tax breakdowns.
- Print thermal receipts.

### 2. Hotel & Property Management

Tools for managing rooms and guest stays.

- Configure room types, bed types, and amenities.
- Manage tariffs and extra-bed charges.
- Register guests and allocate rooms.
- Record advance deposits.
- Extend stays and settle guest folios.
- Complete check-in and check-out workflows.
- Send configured WhatsApp welcome messages.

#### QR-Based Guest ID Upload

The front desk can display a QR code linked to a temporary guest upload session.

Guests scan the code using their phones and upload identification images through a browser, connecting the documents with the relevant hotel record.

### 3. Banquet & Event Management

Tools for coordinating venues, packages, and event operations.

- Review hall and venue availability.
- Schedule banquet bookings.
- Configure per-plate or flat-rate packages.
- Customize event menus.
- Create event-linked food preparation orders.
- Manage milestone billing.

### 4. Inventory & Purchasing

Tools for tracking stock and supplier transactions.

- Maintain ingredient and merchandise records.
- Review stock balances and ledger entries.
- Manage supplier information.
- Record purchases and purchase invoices.
- Track supplier payments and credit.
- Reconcile physical counts against recorded stock.
- Record inventory variances.

### 5. Billing & Settlement

Shared billing functionality supports operational transactions.

- Generate PDF invoices.
- Support thermal and A4 print formats.
- Configure receipt widths and margins.
- Share invoices through the configured WhatsApp integration.
- Review collections by Cash, UPI, Card, and Due.
- Complete day-end cash and shift settlements.

## Offline-First Operation

The documented synchronization design uses Dexie.js and IndexedDB for local records and pending changes.

### Workflow

1. A supported action writes to the local database.
2. The interface reflects the local change.
3. The synchronization process checks connectivity.
4. Pending records are sent to the cloud backend when online.
5. Failed synchronization attempts are logged for review and retry.

### Implementation Elements

- Locally generated UUIDs for record identification.
- Pending-change queues.
- Background synchronization workers.
- Timestamp and version checks for conflict handling.
- Local failure records and diagnostic reporting.

Cloud-dependent services, such as external messaging, still require connectivity. Offline availability depends on the workflow, cached data, and application configuration.

## Multi-Tenant Administration & Licensing

The platform includes business-specific records and central administration.

Administrative capabilities include:

- Business onboarding and activation.
- Subscription plans and module permissions.
- Subscription validity management.
- Desktop license activation and verification.
- Machine binding management.
- Synchronization diagnostics.

## Modular Builds

The frontend supports build configurations for different business combinations:

| Configuration | Modules |
| --- | --- |
| Restaurant | Restaurant and Inventory |
| Hotel | Hotel |
| Banquet | Banquet and Inventory |
| Restaurant + Hotel | Restaurant, Hotel, and Inventory |
| Full Suite | Restaurant, Hotel, Banquet, and Inventory |

Build-time module selection is intended to exclude unused module code from the distributed application.

No bundle-size benchmark is claimed in this case study.

## Customer Communication

Twilio integration supports configured WhatsApp and SMS workflows.

Examples include:

- Hotel check-in welcome messages.
- Restaurant invoice delivery.
- Manual customer communication from operational panels.

Delivery depends on connectivity, provider configuration, and applicable messaging requirements.

## Hardware & Printing

The platform includes workflows for:

- Thermal receipt printers.
- ESC/POS printing.
- Barcode scanners.
- Cash drawers.
- A4 invoice printing.

Hardware compatibility depends on the device, operating environment, drivers, and configured connection method.

## Technology Stack

The following technologies are documented for this project.

| Layer | Technologies |
| --- | --- |
| Frontend | React, TypeScript, Vite |
| Styling | Tailwind CSS |
| Local Storage | Dexie.js, IndexedDB |
| Desktop | Electron, electron-builder |
| Backend | PHP, Laravel Lumen |
| Database | MySQL |
| Authentication | JWT |
| Queue & Cache | Redis-supported configuration |
| PDF Generation | jsPDF, html2canvas |
| Messaging | Twilio WhatsApp and SMS |
| Desktop Updates | electron-updater |

## Architecture Overview

The application separates the client experience from the cloud API.

- **Client layer:** Browser and Electron desktop interfaces.
- **Local data layer:** IndexedDB records, cached data, and pending changes.
- **Synchronization layer:** Background exchange between local records and the API.
- **Backend layer:** Business workflows, authentication, tenancy, and licensing.
- **Cloud services:** MySQL persistence, queue processing, and messaging integrations.

## Example Workflows

### Restaurant Order to Settlement

1. Select a dining table.
2. Add menu items and modifiers.
3. Create the kitchen order ticket.
4. Update the order as required.
5. Generate the bill and record settlement.
6. Print or share the invoice.
7. Synchronize pending records when connected.

### Hotel Guest Check-In

1. Review room availability.
2. Register the guest and select a room.
3. Record the tariff and advance payment.
4. Capture identification through the supported upload workflow.
5. Send the configured welcome message when online.
6. Manage the stay and settle the folio at check-out.

### Banquet Booking

1. Review venue availability.
2. Create the event booking.
3. Select a package and menu.
4. Coordinate food preparation orders.
5. Record payments and complete billing.

### Stock Reconciliation

1. Review recorded stock balances.
2. Enter physical stock counts.
3. Compare quantities.
4. Record variances and applicable adjustments.
5. Review the updated stock ledger.

## Engineering Considerations

### Continuity During Connectivity Interruptions

Local storage and pending-change queues support operational continuity for workflows designed to work offline.

### Synchronization Consistency

Locally generated identifiers, timestamp checks, and failure logging support reconciling changes between clients and the backend.

### Shared Business Components

Authentication, billing, printing, and common interfaces support multiple business modules.

### Platform-Specific Behavior

The browser and desktop clients share application functionality while accommodating desktop packaging and hardware integrations.

### Selective Module Distribution

Build configurations support distributing the modules needed for a particular business setup.

## Functional Outcomes

The platform provides:

- Connected hospitality and retail workflows.
- Restaurant order and billing management.
- Room and guest-stay administration.
- Banquet scheduling and package management.
- Inventory and purchasing records.
- Local operation and synchronization for supported workflows.
- Browser and Windows desktop access.
- Central subscription and licensing administration.

No quantified revenue, productivity, or performance improvement claims are presented in this case study.

## Live Portal

[Open the POS Login Page](https://pos.jdpatidar.com/login)

Access requires an authorized account. Contact us to discuss a guided walkthrough.

## Repository Scope

This public repository contains case study documentation only.

Application source code, customer records, database exports, credentials, and deployment configuration remain private.

No open-source license is granted for the proprietary application through this repository.

## About the Developer

**Jagdish Patidar**  
Founder & CEO — **Drunall Technologies**

I build eCommerce experiences, custom business applications, and workflow automation with a focus on reliability and maintainability.

- [Drunall Technologies](https://www.drunall.com)
- [Portfolio](https://jdpatidar.com)
- [LinkedIn](https://www.linkedin.com/in/jdpatidar/)

> Understand the business first, choose the technology second, and don’t confuse a working demo with a finished product.
