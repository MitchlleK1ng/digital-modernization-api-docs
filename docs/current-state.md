# Current-State System

## Purpose

This document describes the current state of the customer management environment before modernization.

The purpose is to establish a baseline for the modernization initiative by documenting the existing system, major components, data flow, integrations, and operational challenges.

## System Overview

The organization currently uses a legacy customer management application to manage customer records and support business processes.

The application was developed around a centralized architecture in which the primary application, database, and business logic are closely coupled.

External applications have limited direct access to customer information and generally rely on manual processes or custom integrations.

## Current Architecture

The current environment consists of the following major components:

* Legacy customer management application
* Relational customer database
* Internal business applications
* File-based data exchange processes
* Manual administrative workflows
* Limited external integrations

The legacy application contains much of the business logic required to create, retrieve, update, and manage customer records.

### Logical Architecture

```text
+------------------------+
| Internal Users         |
+-----------+------------+
            |
            v
+------------------------+
| Legacy Customer        |
| Management Application |
+-----------+------------+
            |
            v
+------------------------+
| Customer Database      |
+------------------------+

+------------------------+
| Other Business         |
| Applications           |
+-----------+------------+
            |
            | Limited / Custom Integration
            v
+------------------------+
| Legacy Customer        |
| Management Application |
+------------------------+
```

## Customer Data

The legacy system maintains customer information such as:

* Customer identifier
* Name
* Contact information
* Account status
* Address information
* Account creation date
* Last updated date

Customer information is primarily stored in the centralized relational database.

## Data Access

Applications and users currently access customer information through the legacy application.

The system does not provide a standardized REST API for external application access.

As a result, integrations may require custom development, manual data exchange, or direct coordination with the legacy application.

## Integration Environment

The current environment has limited integration capabilities.

Some business processes use file-based exchanges to transfer information between systems.

These processes can introduce additional operational work and may make it more difficult to provide timely access to customer information.

The absence of a standardized API also limits the ability of newer applications to consume customer information through consistent interfaces.

## Operational Processes

Several operational activities depend on manual processes.

Examples include:

* Data preparation
* File-based information exchange
* Manual validation
* Reconciliation of information between systems
* Coordination between teams when changes are required

These processes can increase operational effort and create additional opportunities for inconsistent information.

## Documentation Challenges

The existing environment has limited centralized technical documentation.

Documentation gaps may include:

* Inconsistent descriptions of system behavior
* Limited integration documentation
* Incomplete data-flow information
* Inconsistent terminology
* Limited documentation of operational procedures

These gaps can increase the time required for developers, administrators, and support personnel to understand the system.

## Current-State Limitations

The current environment presents several limitations relevant to modernization:

### Integration

The lack of a standardized API makes integration with modern applications more difficult.

### Maintainability

The tightly coupled architecture can make changes more difficult to implement and test.

### Automation

Manual processes limit opportunities for automation.

### Accessibility

Customer information is not consistently accessible to other applications through standardized interfaces.

### Documentation

Incomplete documentation can increase dependency on individual subject-matter experts and institutional knowledge.

## Current-State Summary

The current customer management environment provides the organization's core customer-management capabilities but presents limitations in integration, maintainability, automation, and documentation.

The modernization initiative will use this current-state baseline to define a future-state architecture and establish a standardized API-driven approach to customer data access.

## Assumptions

The following assumptions apply to this scenario:

* The legacy application remains operational during the initial modernization phases.
* Existing customer data will need to be preserved during migration.
* Business users will continue using customer management capabilities during the transition.
* The organization requires controlled and authenticated access to customer information.
* The modernized platform will provide standardized interfaces for application integration.
