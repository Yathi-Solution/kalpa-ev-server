<div align="center">
  <img src="https://iili.io/KQJa4xp.png" alt="Kalpa EV Logo" width="100"/>
</div>


<h2 align="center">
  <strong>Kalpa EV</strong> system- User Hierarchy & Role Management Documentation
</h2>

## Executive Summary

Kalpa EV is an electric vehicle charging platform that operates on three independent pillars: **ECS Providers** (who own charging infrastructure), **B2B Organizations** (bulk demand), and **B2C Users** (individual demand). This document provides a complete breakdown of all user roles, their responsibilities, hierarchies, and how each tier manages access and permissions within the system.


## Table of Contents

1. Platform Architecture Overview
2. The Three Independent Pillars
3. Complete User Role Hierarchy
4. Organizational Structures by Role
5. Role Definitions & Responsibilities
6. Role Permissions Matrix
7. Authentication & Role Context
8. Key Architectural Principles

---

## 1. Platform Architecture Overview

### What is Kalpa EV?

Kalpa EV is a multi-tenant charging infrastructure platform that brings together three distinct business entities:

- **Supply side:** Companies that own and operate physical charging stations
- **Demand side:** Both bulk organizations (B2B) and individual users (B2C)
- **Aggregation layer (optional):** Networks that unify multiple providers into single apps

### Core Architecture

The platform manages role-based access across multiple organizational types, enabling each role to view, modify, and manage only what is within their scope and responsibility.

---

## 2. The Three Independent Pillars

### Critical Clarification: Three Pillars are NOT Nested

These are three independent business domains that connect through Kalpa, not a hierarchical parent-child relationship.

### Pillar 1: Supply Side - ECS Providers

**Definition:** Organizations that own, install, and operate physical charging infrastructure

**What They Manage:**

- Charging stations at specific locations
- Individual connectors/outlets at each station
- Connector status and operations
- Station and network-level data

**Key Characteristics:**

- Own physical assets
- Set base pricing for their entire network
- Manage their own staff (admins, station managers)
- Earn revenue from every session
- Provide service to both B2B and B2C users

**Examples:**

- Green Charging India
- Charge Zone
- Power+
- Regional charging operators

---

### Pillar 2A: Demand Side - B2B Organizations

**Definition:** Companies that operate vehicle fleets and send multiple drivers to charge

**What They Manage:**

- Driver fleet
- Fleet policies
- Driver assignments
- Organization-level access

**Key Characteristics:**

- Send drivers to charge (guaranteed daily commitment)
- Manage drivers as fleet members
- Work with multiple ECS providers
- Have their own staff (org admins, fleet managers)
- Receive organization-level data and reporting

**Examples:**

- Uber India
- Ola
- Taxi fleet companies
- Delivery services

---

### Pillar 2B: Demand Side - B2C Users

**Definition:** Individual EV owners who charge personal vehicles

**What They Manage:**

- Personal vehicle charging
- Personal payment methods
- Personal charging history

**Key Characteristics:**

- No organizational affiliation
- Individual users
- Independent access
- Personal data only

---

### Pillar 3: Aggregation Layer (NOT a User Role)

**Important:** Aggregators are NOT a user role. They are a business/technical layer.

**Definition:** Platforms/apps that unify multiple ECS provider networks

**Examples:**

- Statiq
- Spider Energy
- Chargefox

---

## 3. Complete User Role Hierarchy

### Six Core Roles with Clear Boundaries

The platform has exactly **6 distinct user roles**, cleanly separated by tier, responsibility, and access scope:

```
TIER 0
└─ Super Admin

TIER 1
├─ ECS Provider Admin (Supply)
└─ B2B Organization Admin (Demand)

TIER 2
├─ Station Manager (Supply)
└─ B2B Fleet Manager (Demand)

TIER 3
├─ B2B Driver (Demand)
└─ B2C User (Demand)
```

<div align="center">
  <img src="https://iili.io/KQJa6WN.png" alt="Role Hierarchy Diagram" width="400"/>
</div>

---

## 4. Organizational Structures by Role

### ECS Provider Organization Structure

**Example: Green Charging India**

```
Green Charging India (ECS Provider Org)
│
├─ Provider Admin (1-3 people)
│  └─ Manages entire network
│     ├─ Creates stations
│     ├─ Sets base pricing
│     ├─ Creates station managers
│     └─ Views network data
│
├─ Station Manager - Delhi (reports to Admin)
│  └─ Operates Station Delhi 1 & 2
│
├─ Station Manager - Mumbai (reports to Admin)
│  └─ Operates Station Mumbai 1 & 2
│
└─ Station Manager - Bangalore (reports to Admin)
   └─ Operates Station Bangalore 1
```

**Organization Type:** ecs_provider

**Access Scope:**

- Provider Admin: Entire network
- Station Manager: Assigned stations only
- Hierarchy: Admin → Manager → Operational staff

---

### B2B Organization Structure

**Example: Uber India**

```
Uber India (B2B Customer Org)
│
├─ Organization Admin (2-3 people)
│  └─ Manages driver fleet
│     ├─ Adds/removes drivers
│     ├─ Creates fleet managers
│     ├─ Views fleet data
│     └─ Accesses reports
│
├─ Fleet Manager - Delhi North (reports to Admin)
│  └─ Manages 80 drivers
│
├─ Fleet Manager - Delhi South (reports to Admin)
│  └─ Manages 60 drivers
│
└─ Fleet Manager - Mumbai (reports to Admin)
   └─ Manages 50 drivers
```

**Organization Type:** b2b

**Access Scope:**

- Organization Admin: Entire fleet
- Fleet Manager: Assigned drivers only
- Hierarchy: Admin → Manager → Drivers

---

## 5. Role Definitions & Responsibilities

### Tier 0: System Administration

#### Super Admin

**Organization:** System-wide (no specific organization)

**Count:** 1-2 per system

**Primary Responsibilities:**

- Create and manage ECS provider organizations
- Create and manage B2B customer organizations
- Manage administrator accounts
- Configure system-wide policies
- Handle compliance requirements
- Monitor system health

**What They Can Access:**

- All organizations
- All user data
- All transactions
- System settings

**Role Hierarchy:**

- Highest level
- Outside any specific organization
- Reports to external governance

---

### Tier 1: Organization-Level Administrators

#### ECS Provider Admin

**Organization:** Assigned to one ECS provider (e.g., Green Charging)

**Count:** 1-5 per provider

**Primary Responsibilities:**

- Create and manage charging stations
- Set base pricing for network
- Create and manage station managers
- Negotiate contracts with B2B organizations
- Monitor network operations
- Handle provider-level compliance

**What They Can Access:**

- All stations in their provider
- All connectors in their provider
- Pricing configurations for their network
- Station manager accounts
- Provider-wide analytics
- **Cannot access other providers' data**

**Reporting:**

- Reports to Super Admin (for compliance)
- Company CEO (operationally)

---

#### B2B Organization Admin

**Organization:** Assigned to one B2B company (e.g., Uber)

**Count:** 2-5 per organization

**Primary Responsibilities:**

- Add and manage drivers
- Create fleet manager accounts
- Set organization policies
- Manage driver assignments
- Access billing information
- View organization-level data

**What They Can Access:**

- All drivers in their organization
- All fleet managers
- Organization policies
- Driver session data
- Organization reporting
- **Cannot access other organizations' data**
- **Cannot access ECS provider data**

**Reporting:**

- Reports to company leadership
- Company operations/finance

---

### Tier 2: Operations Managers

#### Station Manager

**Organization:** Inherited from ECS provider

**Reports To:** ECS Provider Admin

**Count:** 1-3 per station

**Primary Responsibilities:**

- Monitor station operations
- Track connector status
- Respond to operational issues
- Document problems and resolutions
- Monitor station usage
- Support end users

**What They Can Access:**

- Assigned station(s) only
- Connector status
- Session history for their station(s)
- Incident and maintenance logs
- **Cannot create new stations**
- **Cannot set pricing**
- **Cannot access other stations**

**Scope Limitation:**

- Single station or small group
- No access to other providers
- No access to organizations

---

#### B2B Fleet Manager

**Organization:** Inherited from B2B organization

**Reports To:** B2B Organization Admin

**Count:** 5-20 per large organization

**Primary Responsibilities:**

- Manage assigned driver group
- Assign drivers to regions or teams
- Track team usage and operations
- Enforce organizational policies
- Handle driver-level issues
- Generate team reports

**What They Can Access:**

- Assigned drivers only (50-100 drivers)
- Team session data
- Team reports
- **Cannot add new drivers (admin does)**
- **Cannot remove drivers (admin does)**
- **Cannot access other teams' data**
- **Cannot access ECS provider data**

**Scope Limitation:**

- Limited to assigned driver group
- No organization-wide access
- No access to other organizations

---

### Tier 3: End Users

#### B2B Driver

**Organization:** Assigned to B2B organization (e.g., Uber)

**Reports To:** Fleet Manager or organization

**Count:** Thousands per organization

**Primary Responsibilities:**

- Find charging stations
- Initiate charging sessions
- Complete charging sessions
- Monitor personal charging activity
- Report technical issues

**What They Can Access:**

- Available stations
- Can start/stop charging sessions
- Personal session history
- Organization-specific pricing rates
- **Cannot make payments (org handles it)**
- **Cannot access other drivers' data**
- **Cannot access organization management**

**Scope Limitation:**

- Personal charging only
- Cannot view organization data
- Cannot view other drivers' sessions
- Cannot modify settings

---

#### B2C User

**Organization:** None (no affiliation)

**Reports To:** No one

**Count:** Millions (consumer base)

**Primary Responsibilities:**

- Find charging stations
- Initiate charging sessions
- Complete charging sessions
- Track personal sessions
- Pay for sessions

**What They Can Access:**

- Available stations (all)
- Can start/stop sessions
- Personal session history
- Pricing information
- Payment methods
- **Cannot access other users' data**
- **Cannot access organization data**
- **Cannot access provider data**

**Scope Limitation:**

- Personal charging only
- Independent user
- No organizational relationships

---

## 6. Role Permissions Matrix

### Complete Permission Access Map

| Permission                       | Super Admin | ECS Admin | Station Mgr | B2B Admin | Fleet Mgr | B2B Driver | B2C User |
| -------------------------------- | ----------- | --------- | ----------- | --------- | --------- | ---------- | -------- |
| **Organization Management**      |
| Create organization              | ✓           | ✗         | ✗           | ✗         | ✗         | ✗          | ✗        |
| Edit organization                | ✓           | ✓\*       | ✗           | ✓\*       | ✗         | ✗          | ✗        |
| View organization                | ✓           | ✓         | ✓           | ✓         | ✓         | ✓          | ✗        |
| Delete organization              | ✓           | ✗         | ✗           | ✗         | ✗         | ✗          | ✗        |
| **Station Management**           |
| Create station                   | ✓           | ✓         | ✗           | ✗         | ✗         | ✗          | ✗        |
| Edit station                     | ✓           | ✓         | ✗           | ✗         | ✗         | ✗          | ✗        |
| View station details             | ✓           | ✓         | ✓           | ✗         | ✗         | ✗          | ✓        |
| View all stations                | ✓           | ✓         | ✗           | ✗         | ✗         | ✗          | ✗        |
| Delete station                   | ✓           | ✓         | ✗           | ✗         | ✗         | ✗          | ✗        |
| **Connector Management**         |
| Create connector                 | ✓           | ✓         | ✗           | ✗         | ✗         | ✗          | ✗        |
| Update connector status          | ✓           | ✓         | ✓           | ✗         | ✗         | ✗          | ✗        |
| View connector status            | ✓           | ✓         | ✓           | ✗         | ✗         | ✗          | ✓        |
| Delete connector                 | ✓           | ✓         | ✗           | ✗         | ✗         | ✗          | ✗        |
| **Pricing Management**           |
| Create pricing rule              | ✓           | ✓         | ✗           | ✓\*\*     | ✗         | ✗          | ✗        |
| Edit pricing rule                | ✓           | ✓         | ✗           | ✓\*\*     | ✗         | ✗          | ✗        |
| View pricing                     | ✓           | ✓         | ✓           | ✓         | ✓         | ✓          | ✓        |
| Delete pricing rule              | ✓           | ✓         | ✗           | ✗         | ✗         | ✗          | ✗        |
| **User Management**              |
| Create users                     | ✓           | ✓         | ✗           | ✓         | ✗         | ✗          | ✗        |
| Edit users                       | ✓           | ✓         | ✗           | ✓         | ✗         | ✗          | ✗        |
| Delete users                     | ✓           | ✓         | ✗           | ✓         | ✗         | ✗          | ✗        |
| View users                       | ✓           | ✓         | ✗           | ✓         | ✓         | ✗          | ✗        |
| **Driver Management**            |
| Add drivers                      | ✓           | ✗         | ✗           | ✓         | ✗         | ✗          | ✗        |
| Remove drivers                   | ✓           | ✗         | ✗           | ✓         | ✗         | ✗          | ✗        |
| View team drivers                | ✓           | ✗         | ✗           | ✓         | ✓         | ✗          | ✗        |
| Edit driver assignments          | ✓           | ✗         | ✗           | ✓         | ✓         | ✗          | ✗        |
| **Charging Sessions**            |
| Start session                    | ✓           | ✗         | ✗           | ✗         | ✗         | ✓          | ✓        |
| Stop session                     | ✓           | ✗         | ✗           | ✗         | ✗         | ✓          | ✓        |
| View own sessions                | ✓           | ✓         | ✓           | ✓         | ✓         | ✓          | ✓        |
| View all sessions                | ✓           | ✓         | ✓           | ✓         | ✓         | ✗          | ✗        |
| **Organization/Team Management** |
| Create team managers             | ✓           | ✓         | ✗           | ✓         | ✗         | ✗          | ✗        |
| Edit team managers               | ✓           | ✓         | ✗           | ✓         | ✗         | ✗          | ✗        |
| View team structure              | ✓           | ✓         | ✗           | ✓         | ✓         | ✗          | ✗        |
| Delete team managers             | ✓           | ✓         | ✗           | ✓         | ✗         | ✗          | ✗        |
| **Reporting & Analytics**        |
| View organization reports        | ✓           | ✓         | ✓           | ✓         | ✗         | ✗          | ✗        |
| View team reports                | ✓           | ✗         | ✗           | ✓         | ✓         | ✗          | ✗        |
| Generate reports                 | ✓           | ✓         | ✓           | ✓         | ✓         | ✗          | ✗        |
| **System Administration**        |
| Access system settings           | ✓           | ✗         | ✗           | ✗         | ✗         | ✗          | ✗        |
| Manage admins                    | ✓           | ✗         | ✗           | ✗         | ✗         | ✗          | ✗        |
| View audit logs                  | ✓           | ✓         | ✗           | ✓         | ✗         | ✗          | ✗        |

**Legend:**

- ✓ = Full access
- ✓\* = Can edit own organization only
- ✓\*\* = Can create pricing for own organization only
- ✗ = No access

---

## 7. Authentication & Role Context

### How Role Context Works

Each user has a context that determines their permissions and data access:

**Context Elements:**

- User ID (unique identifier)
- Role (super_admin, provider_admin, station_manager, etc.)
- Organization ID (which organization they belong to)
- Organization Type (ecs_provider, b2b, or null for B2C)
- Scope (what specific data they can access)

### Registration Paths

#### Path 1: B2B Driver Registration

A person registers to work for Uber as a driver:

- Email
- Password
- Name
- Organization Code (provided by Uber)
- User Type: b2b_driver

System assigns:

- Role: driver
- Organization: Uber India
- Scope: Can access their own sessions
- Context: B2B organization member

#### Path 2: B2C Individual Registration

A person registers as an individual EV owner:

- Email
- Password
- Name
- User Type: b2c

System assigns:

- Role: user (B2C)
- Organization: None
- Scope: Can access own sessions only
- Context: Independent user

#### Path 3: ECS Provider Admin Registration

A person registers as admin for Green Charging:

- Email
- Password
- Name
- Organization Name: Green Charging India
- Organization Type: ecs_provider

System creates:

- New organization (ecs_provider type)
- Assigns role: provider_admin
- Organization: Green Charging
- Scope: Can access entire provider network
- Context: Provider admin

---

### Role Context in JWT Token

When a user logs in, they receive a token containing their context:

```
{
  "userId": "user-123",
  "email": "user@example.com",
  "role": "driver",
  "organizationType": "b2b",
  "organizationId": "uber-india",
  "organizationName": "Uber India",
  "scope": {
    "drivers": ["self"],
    "stations": ["all"],
    "organizations": ["uber-india"]
  }
}
```

This context determines:

- What endpoints they can access
- What data they can view
- What actions they can perform

---

### Multi-Context Users

A single person can have multiple roles in different organizations:

**Example:**

- ECS Provider Admin at Green Charging India
- Fleet Manager at Uber India
- B2C individual user (personal vehicle)

The user switches between contexts to access different areas:

- Switch to Green Charging: Manage stations
- Switch to Uber: Manage driver team
- Switch to B2C: Charge personal vehicle

---

## 8. Key Architectural Principles

### Principle 1: Three Pillars Are Independent, Not Nested

**Correct Structure:**

```
Supply Side (ECS Providers)
    ↓
Kalpa Platform
    ↓
Demand Side (B2B + B2C)
```

Each pillar manages its own organization structure and users. They connect through Kalpa but remain independent.

### Principle 2: Aggregators Are NOT User Roles

Aggregators (Statiq, Spider Energy) are business layers that unify provider networks. They are never a user role in the system. Users don't interact with aggregators directly.

<div align="center">
  <img src="https://iili.io/KQJagbR.png" alt="Kalpa EV Logo" width="600"/>
</div>

**User roles in Kalpa:**

- Super Admin
- ECS Provider Admin
- Station Manager
- B2B Organization Admin
- B2B Fleet Manager
- B2B Driver
- B2C User

**Aggregators:**

- Business concept
- Optional layer
- Not a role

### Principle 3: Role Scope is Organization-Based

Each role's permissions are bounded by their organization:

- **ECS Provider Admin:** Can only manage their provider's data
- **B2B Organization Admin:** Can only manage their organization's data
- **Station Manager:** Can only manage assigned station(s)
- **Fleet Manager:** Can only manage assigned driver(s)
- **Driver/User:** Can only access personal data

This prevents:

- Cross-organization data leakage
- Accidental data modification
- Unauthorized access

### Principle 4: Role Hierarchy is Vertical Within Organization

Within each organization, roles form a hierarchy:

**ECS Provider:**

- Provider Admin (top)
- Station Manager (middle)
- Operational staff (bottom)

**B2B Organization:**

- Organization Admin (top)
- Fleet Manager (middle)
- Driver (bottom)

Each level can only manage users and data at their level or below within their organization.

### Principle 5: Permissions are Based on Need-to-Know

Each role has only the permissions necessary for their responsibilities:

- **Station Manager** doesn't need pricing permissions
- **Fleet Manager** doesn't need driver creation permissions
- **Driver** doesn't need team management permissions
- **B2C User** doesn't need organization access

This follows the principle of least privilege.

### Principle 6: Role Context is Stateless

Authentication is stateless using context-aware tokens. When a user logs in:

1. System verifies credentials
2. Retrieves all their roles and organizations
3. Issues token containing context
4. User includes token in every request
5. System validates token and enforces permissions

No session state needed on server.

### Principle 7: Organizations Determine Data Boundaries

Multi-tenancy is enforced at the organization level:

- ECS Provider Admin can't see other providers
- B2B Organization Admin can't see other organizations
- Station Manager can't see other stations (unless assigned)
- Fleet Manager can't see other teams

Database queries automatically filter by organization_id.

### Principle 8: Role Changes Require Admin Action

Regular users cannot change their own roles. Only admins can:

- Add users to organizations
- Assign roles to users
- Remove users from organizations
- Change user roles

This maintains security and prevents privilege escalation.

---

## Role Management Summary

### Quick Reference: All Six Roles

| Role                   | Organization | Reports To     | Manages            | Access            |
| ---------------------- | ------------ | -------------- | ------------------ | ----------------- |
| **Super Admin**        | System-wide  | External       | All orgs           | Everything        |
| **ECS Provider Admin** | ECS provider | CEO/Board      | Stations, managers | Own provider      |
| **Station Manager**    | ECS provider | Provider admin | Station ops        | Own station(s)    |
| **B2B Org Admin**      | B2B company  | Leadership     | Drivers, fleet     | Own organization  |
| **Fleet Manager**      | B2B company  | Org admin      | Driver team        | Own team          |
| **B2B Driver**         | B2B company  | Fleet manager  | Own charging       | Personal sessions |
| **B2C User**           | None         | No one         | Own charging       | Personal sessions |

---

## Key Takeaways

1. **Six distinct roles** with clear boundaries and responsibilities
2. **Three independent pillars** (Supply, B2B Demand, B2C Demand)
3. **Organization-based scope** ensures data isolation
4. **Hierarchical structure** within each organization
5. **Context-aware permissions** based on role and organization
6. **Principle of least privilege** for each role
7. **Stateless authentication** using context tokens
8. **No nested hierarchies** between pillars - they connect through platform

The system is designed for scalability, security, and clarity in role management across multiple business models.
