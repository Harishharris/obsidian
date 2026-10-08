#### Requirements
- the parkinglot supports multiple parking floors
- each parkinglot able to part multiple types of vehicles
- the vehicle should be assigned a nearest place
#### Entities
- ParkingLot
- ParkingFloor
- FloorConfiguration
- ParkingSpot
- Vehicle
- Ticket
#### Relationships
- ParkingLot -> floors
- ParkingFloor -> spots
- ParkingSpot -? vehicle
- Ticket -> Vehicle
#### Responsibilities
- The parking lot is an orchestrator for the entire system
- the parking floor will handle all the parking spots in the particular floor
- the parking spot will park the vehicle
- the ticket will hold the vehicle
#### Abstractions
- Vehicle will hold Bike, Car, Truck, etc
- Pricing Strategy will be different for each vehicle type
#### Design Principles
#### Design Patterns
- Strategy Pattern for price calculation
- Factory pattern for vehicle creation
#### Flow
- Vehicle enters into our system
- Check if there is any space
- Generate the ticket and park the vehicle
- Vehicle will exit the system
- Calculates the fare
- Payment
