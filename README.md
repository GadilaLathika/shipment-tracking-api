# MuleSoft Shipment Tracking API

A shipment tracking integration project built with MuleSoft Mule 4 to receive, normalize, process, and store shipment tracking events from multiple logistics providers, including Blue Dart and Delhivery.

## Overview

The project provides a unified API for handling carrier tracking updates. It validates incoming requests, converts carrier-specific statuses into a common format, processes events asynchronously through a Mule VM queue, and stores tracking information in MySQL.

## Architecture

The solution is organized around three API-led connectivity layers:
<img width="1168" height="739" alt="mInr7" src="https://github.com/user-attachments/assets/812061c0-2a63-4874-a9d1-e3ce97abbb6d" />

1. **Experience API:** Exposes HTTP endpoints using RAML and APIKit, accepts shipment events, and validates API-key authentication.
2. **Process Layer:** Validates event fields, normalizes carrier names and status values using DataWeave, and dispatches events for asynchronous processing.
3. **System / Integration Layer:** Integrates with MySQL to persist shipment events and retrieve the latest shipment status and tracking history.

### Processing flow

Blue Dart / Delhivery → Experience API → Process and normalization → VM Queue → Asynchronous processing → MySQL

## Technology Stack

- MuleSoft Anypoint Studio
- Mule Runtime 4
- RAML 1.0 and APIKit
- DataWeave 2.0
- HTTP Listener
- Mule VM messaging
- MySQL 8
- MUnit
- Git and GitHub

## API Endpoints

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/api/shipment-events` | Accept a shipment tracking event |
| GET | `/api/shipments/{trackingNumber}` | Retrieve the latest shipment status |
| GET | `/api/shipments/{trackingNumber}/events` | Retrieve shipment event history |

## Current Features

- Carrier event ingestion for Blue Dart and Delhivery.
- API-key validation for incoming events.
- Carrier-name and status normalization using DataWeave.
- Asynchronous event dispatch using a Mule VM queue.
- MySQL persistence with duplicate-event protection.
- Shipment status and tracking-history retrieval.
- RAML-based API definition and APIKit routing.
- MUnit tests for valid requests, missing fields, and tracking queries.

<img width="1168" height="739" alt="5kEDE" src="https://github.com/user-attachments/assets/4c92b8b4-1823-4ecf-96c5-7dfd69ccf310" />


## Planned Enhancements

- Anypoint MQ integration and dead-letter queue handling.
- Complete milestone mapping and forward-only status progression.
- Unknown-shipment event parking and resolution.
- Estimated delivery date recalculation and delay detection.
- Customer-facing notifications for selected milestones.
- Expanded MUnit coverage for error handling and business rules.
- Improved logging, correlation IDs, and monitoring.

## Local Setup

1. Install Anypoint Studio and a compatible Mule runtime.
2. Install MySQL and create the required shipment tracking database and tables.
3. Configure local database credentials and the webhook API key in your local `config.properties` file.
4. Import the project into Anypoint Studio.
5. Resolve Maven dependencies and run the Mule application.
6. Test the endpoints using Postman.

**Security:** Never commit passwords, API keys, or other secrets to GitHub. Use local configuration or secure properties for credentials.

## Project Status

The project is being developed incrementally as a shipment tracking integration prototype. Features listed under Planned Enhancements are not yet represented as completed functionality.
