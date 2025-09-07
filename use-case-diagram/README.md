# Use Case Diagram - Airbnb Clone System

## Overview
This use case diagram visualizes the interactions between different actors (users and external systems) and the Airbnb Clone system. It captures all key functionalities and shows how different types of users interact with the system to accomplish their goals.

## Actors

### Primary Actors (Human Users)

#### 1. Guest
**Description:** A user who searches for and books accommodations
**Primary Goals:**
- Find suitable accommodations
- Book properties for specific dates
- Complete secure payments
- Communicate with hosts
- Share feedback through reviews

#### 2. Host  
**Description:** A user who lists and manages rental properties
**Primary Goals:**
- List properties on the platform
- Manage bookings and availability
- Communicate with potential guests
- Receive payments for bookings
- Maintain property information and pricing

#### 3. Admin
**Description:** System administrator who manages the platform
**Primary Goals:**
- Oversee platform operations
- Manage user accounts and content
- Resolve disputes and issues
- Monitor system performance
- Generate business reports

### Secondary Actors (External Systems)

#### 4. Payment Gateway (Stripe/PayPal)
**Description:** External payment processing service
**Role:** Handles secure payment transactions, refunds, and payouts

#### 5. Email Service (SendGrid/Mailgun)
**Description:** External email delivery service
**Role:** Sends transactional emails, notifications, and confirmations

#### 6. Map Service (Google Maps/Mapbox)
**Description:** External mapping and location service
**Role:** Provides location data, mapping, and geolocation services

## Use Cases by Actor

### Guest Use Cases

| Use Case | Description | Priority |
|----------|-------------|----------|
| **Register Account** | Create a new user account with email verification | High |
| **Login/Logout** | Authenticate and access account or securely exit | High |
| **Search Properties** | Find accommodations based on location, dates, and filters | High |
| **View Property Details** | See comprehensive property information, photos, reviews | High |
| **Make Booking** | Reserve a property for specific dates with guest details | High |
| **Make Payment** | Complete secure payment for booking confirmation | High |
| **Manage Booking** | View, modify, or cancel existing reservations | Medium |
| **Leave Review** | Rate and review properties and hosts after stay | Medium |
| **Send Messages** | Communicate with hosts about bookings and questions | Medium |
| **Manage Profile** | Update personal information, preferences, and settings | Low |
| **View Booking History** | Access past and upcoming reservation details | Low |

### Host Use Cases

| Use Case | Description | Priority |
|----------|-------------|----------|
| **Register as Host** | Create host account with additional verification | High |
| **Create Property Listing** | Add new rental property with details and photos | High |
| **Manage Property** | Update property information, amenities, and photos | High |
| **Set Availability** | Define available dates using calendar management | High |
| **Set Pricing** | Configure base rates, seasonal pricing, and discounts | High |
| **Respond to Bookings** | Accept or decline booking requests | High |
| **Receive Payments** | Get payouts for confirmed bookings | High |
| **Communicate with Guests** | Message guests before, during, and after stays | Medium |
| **Leave Guest Reviews** | Rate and review guests after their stay | Medium |
| **View Analytics** | Access booking statistics and performance metrics | Low |
| **Manage Calendar Sync** | Integrate with external calendar systems | Low |

### Admin Use Cases

| Use Case | Description | Priority |
|----------|-------------|----------|
| **Manage Users** | Create, update, suspend, or delete user accounts | High |
| **Monitor System** | Oversee platform performance and system health | High |
| **Handle Disputes** | Mediate conflicts between guests and hosts | High |
| **Generate Reports** | Create business intelligence and analytics reports | Medium |
| **Moderate Content** | Review and approve user-generated content | Medium |
| **Configure System** | Update platform settings and business rules | Medium |
| **Manage Payments** | Oversee financial transactions and resolve issues | Medium |
| **Send Announcements** | Communicate platform updates to all users | Low |

## Use Case Relationships

### Include Relationships
These represent mandatory sub-processes that are always executed:

- **Make Booking** includes **Authenticate User**
- **Make Payment** includes **Verify Payment Method**
- **Create Property Listing** includes **Verify Host Status**
- **Leave Review** includes **Verify Booking Completion**
- **Send Messages** includes **Authenticate User**

### Extend Relationships  
These represent optional behaviors that may occur:

- **Search Properties** extends with **Apply Advanced Filters**
- **Make Booking** extends with **Add Special Requests**
- **Make Payment** extends with **Apply Discount Code**
- **View Property Details** extends with **Save to Wishlist**
- **Manage Profile** extends with **Upload Profile Picture**

### Generalization Relationships
- **Host** is a specialized type of **Guest** (hosts can also book properties)
- **Premium Guest** extends **Guest** with additional privileges

## System Interactions

### Critical User Journeys

#### 1. Guest Booking Journey
```
Guest → Register Account → Search Properties → View Property Details 
→ Make Booking → Make Payment → Receive Confirmation
```

#### 2. Host Onboarding Journey
```
Host → Register as Host → Verify Identity → Create Property Listing 
→ Set Availability → Set Pricing → Publish Listing
```

#### 3. Booking Management Journey
```
Host → Receive Booking Request → Review Guest Profile → Respond to Booking 
→ Communicate with Guest → Receive Payment → Complete Stay
```

## External System Integration Points

### Payment Gateway Integration
- **Triggered by:** Make Payment, Process Refund, Send Payout
- **Data Exchange:** Payment details, transaction status, financial records
- **Security:** PCI DSS compliance, encrypted data transmission

### Email Service Integration  
- **Triggered by:** Account registration, booking confirmation, system notifications
- **Data Exchange:** Email templates, recipient information, delivery status
- **Features:** Transactional emails, bulk messaging, delivery tracking

### Map Service Integration
- **Triggered by:** Search Properties, View Property Details, Location Services
- **Data Exchange:** Coordinates, address data, map imagery
- **Features:** Geocoding, reverse geocoding, interactive maps

## Technical Implementation Notes

### Authentication & Authorization
- All use cases requiring user identification include authentication
- Role-based access control determines available use cases
- JWT tokens manage session state and permissions

### Data Validation
- Input validation occurs at use case entry points
- Business rule validation ensures data integrity
- Error handling provides meaningful user feedback

### Performance Considerations
- Search functionality requires optimized database queries
- Image handling needs CDN integration for property photos
- Real-time messaging requires WebSocket connections

### Security Measures
- Sensitive operations require additional verification
- Rate limiting prevents abuse of public endpoints
- Audit logging tracks all significant user actions

## Success Criteria

### Guest Experience
- ✅ Can complete booking process in under 5 minutes
- ✅ Search results load within 2 seconds
- ✅ Payment process is secure and intuitive
- ✅ Communication with hosts is seamless

### Host Experience  
- ✅ Can create complete listing in under 15 minutes
- ✅ Booking management is straightforward
- ✅ Payment processing is reliable and timely
- ✅ Analytics provide valuable insights

### System Performance
- ✅ 99.9% uptime during peak booking seasons
- ✅ All use cases handle concurrent users efficiently
- ✅ Data integrity maintained across all operations
- ✅ External integrations are reliable and fast

## Draw.io Implementation Guide

### Diagram Layout Structure
```
[Guest]     [Host]     [Admin]          [System Boundary]          [Payment Gateway]
   |          |          |                     |                        |
   |          |          |              [Use Cases Grid]                |
   |          |          |                     |                        |
   └----------└----------└─────────────────────┼────────────────────────┘
                                              |
                                    [Email Service] [Map Service]
```

### Visual Elements to Use
- **Actors:** Stick figures with clear labels
- **System Boundary:** Large rectangle containing all use cases  
- **Use Cases:** Ovals with concise, action-oriented names
- **Associations:** Solid lines connecting actors to use cases
- **Include/Extend:** Dashed arrows with stereotypes

### Color Coding Recommendations
- **Guest use cases:** Light blue (#E3F2FD)
- **Host use cases:** Light green (#E8F5E8)  
- **Admin use cases:** Light orange (#FFF3E0)
- **Shared use cases:** Light gray (#F5F5F5)
- **External actors:** Light yellow (#FFFDE7)

This comprehensive use case diagram will serve as a blueprint for understanding all system interactions and guide the development of user stories and system requirements.
