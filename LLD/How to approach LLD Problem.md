
1. Clarify requirements
2. Identify entities (core objects)
	- Anything that has state + behaviour
	- Example: 
		- ParkingLot
		- ParkingFloor
		- ParkingSpot
		- Vehicle
		- Ticket
3. Define Relationships
	- ParkingLot -> has Floors
	- Floor -> has Slots
	- Slot -> holds Vehicles
4. Define Responsibilities (**most important**)
	- **Who Should do what?**
	- Example:
		- Slot → knows if free or occupied
		- ParkingLot → should NOT handle everything
		- Separate service for allocation
5. Identify abstractions (very very important)
	- You shouldn't be using `if verhicleType == 1` everywhere
	- Generalize where needed:
		- Vehicle -> Bike, Car, Truck
		- Slot -> Different slots
6. Apply design principles (SOLID)
	1. Single responsibility?
7. Introduce design patterns (only if needed)
	- Example:
		- Strategy -> pricing
		- Factory -> vehicle creation
	- Important: **WE SHOULD'NT BE FORCING DESIGN PATTERNS FOR THE SAKE OF IT**
8. Define flow
	- Vehicle enters -> slot assigned -> ticket generated -> exit -> payment
9. Code
	- Interfaces
	- Classes
	- Implementations
	- Clean Methods, etc.
10. Review
	- Ask:
		- Can I add EV slots easily?
		- Can pricing change without breaking code?