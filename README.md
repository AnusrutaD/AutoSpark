# AutoSpark

A pure car washing service

![Car Wash](src/main/resources/assets/images/car_wash.jpeg)

## Feature
- User can SignUp/LogIn
- View Profile
- Add cars
- View Service and pricing
- Add or remove slot
- Add or remove spot
- Assign Spot
- Assign Slot
- Book a ticket
- Do Payment

## UML Diagram

```plantuml
@startuml
    left to right direction
    actor Customer
    actor Attendant
    actor Admin
    
    rectangle AutoSpark{
        Customer -> (SignUp)
        Customer -> (LogIn)
        Admin -> (Profile Management)
        Customer -> (Add Cars)
        Customer -> (View Services & Pricing)
        Attendant -> (Assign Slot)
        Attendant -> (Assign Spot)
        Attendant -> (Book A Ticket)
        Customer -> (Do Payment)
    }
    
@enduml
```

## Entities & Attributes
- User
  - name
  - email
  - vehiclesList
  - userType
- Vehicle
  - vehicleNumber
  - vehicleType
- Shop
  - Name
  - location
  - spots
- Spot
  - SpotNumber
  - slotList
- Slot
  - Start
  - End
  - isBooked
- Ticket
  - user
  - vehicle
  - Spot
  - Slot
  - WashType
- Location
  - longitude
  - latitude
- Invoice
  - ticket
  - amount
- Payment
  - invoice
  - amount
  - paymentMode

## Class Diagram

```mermaid
classDiagram
    class User{
        <<abstract>>
        - String: name
        - String: email
        - String: phone
        - String: password

        + viewProfile() Profile
    }
    
    class Customer{
        - List~Vehicle~: vehicles
        
        + login() void
        + signup() Customer
        + addVehicle() Vehicle
        + makePayment() Payment
    }
    
    class Attendant{
        + chooseSpot() Spot
        + chooseSlot() slot
        + bookTicket(User, Vehicle, Spot, Slot) ticket
        + generateInvoice(ticket)
    }
    
    class Admin{
        + addShop(Shop) Shop
        + addSpot(Spot) Spot
        + addSlot(Slot) slot
    }
    
    class Profile{
        - String: name
        - String: email
        - String: Phone
        - String: role
        - List~Vehicle~: vehicles
        - List~History~: histories
    }
    
    class History{
        - Customer: customer
        - Vehicle: vehicle
        - Shop: shop
        - Spot: spot
        - Slot: slot
        - WashType: washType
        - Payment: payment
    }
    
    class Vehicle{
        - String: vehicleNumber;
        - VehicleType: vehicleType;
    }
    
    class VehicleType{
        SMALL,
        MEDIUM,
        HEAVY
    }
    
    class Shop{
        - String: name;
        - Location: location;
        - List~Spot~: spots
    }
    
    class Spot{
        - Integer: spotNumber
        - List~Slot~: slots
    }
    
    class Slot{
        - DateTime: start
        - DateTime: end
        - Boolean: isBooked
    }
    
    class Location{
        - String: longitude
        - String: latetude
    }
    
    class Ticket{
        - User: user
        - Vehicle: vehicle
        - Spot: spot
        - Slot: slot
        - WashType: washType
    }
    
    class WashType{
        <<enumeration>>
        REGULER,
        PREMIUM,
        WATERLESS
    }
    
    class Invoice{
        - Ticket: ticket
        - Double: amount
    }
    
    class Payment{
        - Invoice: invoice
        - Double: amount
        - PaymentMode: paymentMode
        - PaymentStatus: paymentStatus
    }
    
    class PaymentMode{
        <<enumeration>>
        CASH,
        CARD,
        UPI
    }
    
    class PaymentStatus{
        <<enumeration>>
        SUCCESS,
        PENDING
    }


    Customer --|> User
    Attendant --|> User
    Admin --|> User
    Customer "1" --o  "*" Vehicle
    Vehicle "1" --o  "*" VehicleType
    Profile "1" --o  "1" User
    Profile "1" --o  "*" History
    History "*" --o  "1" Customer
    History "*" --o  "1" Vehicle
    History "*" --o  "1" Shop
    History "*" --o  "1" Spot
    History "*" --o  "1" Slot
    History "1" --o  "1" WashType
    History "1" --o  "1" Payment
    Shop "1" --* "*" Spot
    Shop "1" --* "1" Location
    Spot "1" --* "*" Slot
    Ticket "1" --o "1" User
    Ticket "1" --o "1" Vehicle
    Ticket "1" --o "1" Shop
    Ticket "1" --o "1" Spot
    Ticket "1" --o "1" Slot
    Ticket "1" --o "1" WashType
    Invoice "1" --o "1" Ticket
    Payment "1" --o "1" Invoice
    Payment "1" --o "1" PaymentMode
    Payment "1" --o "1" PaymentStatus
    
```




