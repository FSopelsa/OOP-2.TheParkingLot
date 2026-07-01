# The Parking Lot

 - This project models a small parking lot in central Stockholm. 
    An attendant assigns arriving cars to free parking spots, creates tickets, closes tickets 
    when cars leave, prints the parked duration, and frees the spot again.


## Features

- Tracks free and occupied parking spots
- Assigns arriving cars to the first free spot
- Creates a ticket with spot number and arrival time
- Closes a ticket when the car leaves
- Prints how long the car was parked
- Handles a full parking lot with a clear message

## Design
- The **ParkingLot** owns a fixed number of **ParkingSpot** objects.
- The **Attendant** does not own the spots. The attendant only uses the parking lot to find a free spot, assign a car, and free the spot when the car leaves.
- The **Ticket** belongs to one parking session. It records the spot number, car registration, arrival time, and departure time.

```mermaid
classDiagram
    ParkingLot *-- "1..*" ParkingSpot : owns
    Attendant ..> ParkingLot : uses
    Attendant ..> ParkingSpot : assigns/frees
    Attendant ..> Ticket : creates/closes

    class ParkingLot {
        - spots: List~ParkingSpot~
        + ParkingLot(capacity int)
        + findFreeSpot() ParkingSpot
        + findSpotByNumber(spotNumber int) ParkingSpot
        + printStatus()
    }

    class ParkingSpot {
        - spotNumber: int
        - carRegistration: String
        + isFree() boolean
        + park(carRegistration String)
        + free()
    }

    class Ticket {
        - spotNumber: int
        - carRegistration: String
        - arrivalTime: LocalDateTime
        - departureTime: LocalDateTime
        + close()
        + getDuration() Duration
        + printDuration()
    }
```

---

## How To Run

### Build the project:
 - mvn package

### Run the app:
 - java -jar target\OOP-2.TheParkingLot.jar

### Or run directly with Maven:
 - mvn compile exec:java -Dexec.mainClass="se.lexicon.App"