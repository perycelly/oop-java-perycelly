[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/public void rent(Customer customer, int days) {
        // Logic for renting a car
        System.out.println("Car rented to " + customer.getName() + " for " + days + " days.");
    }

    @Override
    public void returnVehicle() {
        // Logic for returning the car
        System.out.println("Car returned.");
    }
}

Method Overloading and Overriding:

- Method Overloading: We can overload methods such as rent() with different parameter types (e.g., rent a car for different durations).
- Method Overriding: rent() and returnVehicle() will be overridden in the subclasses to provide specific implementations for each vehicle type.

---

### 5. Composition

In this case, the RentalAgency class will manage a fleet of vehicles and have a composition relationship with the Vehicle class. We will also introduce a Customer class and RentalTransaction class to handle the rental transactions.
public class RentalAgency {
    private List<Vehicle> vehicleFleet;

    public RentalAgency() {
        vehicleFleet = new ArrayList<>();
    }

    public void addVehicle(Vehicle vehicle) {
        vehicleFleet.add(vehicle);
    }

    public void rentVehicle(Vehicle vehicle, Customer customer, int days) {
        if (vehicle.isAvailableForRental()) {
            vehicle.rent(customer, days);
            vehicle.setAvailable(false);
        } else {
            System.out.println("Vehicle is not available.");
        }
    }
}

public class Customer {
    private String name;
    private List<RentalTransaction> rentalHistory;

    public Customer(String name) {
        this.name = name;
        rentalHistory = new ArrayList<>();
    }

    public void addRentalTransaction(RentalTransaction transaction) {
        rentalHistory.add(transaction);
    }

    public String getName() {
        return name;
    }
}

public class RentalTransaction {
    private Vehicle vehicle;
    private int daysRented;

    public RentalTransaction(Vehicle vehicle, int daysRented) {
        this.vehicle = vehicle;
        this.daysRented = daysRented;
    }

    public double getRentalCost() {
        return vehicle.calculateRentalCost(daysRented);
    }
}

---

### Additional Features (Bonus)

1. Loyalty Program:  
   An interface LoyaltyProgram can be implemented by the Customer class to calculate discounts based on rental history.

2. Custom Exceptions:  
   We can create exceptions like VehicleNotAvailableException or InvalidRentalDurationException.

3. Vehicle Rating System:  
   A Rating class can be introduced to manage ratings given by customers for vehicles, storing ratings and reviews.

---

### Complete Example of Inheritance, Polymorphism, and Abstraction
public class Main {
    public static void main(String[] args) {
        // Create rental agency
        RentalAgency agency = new RentalAgency();

        // Create vehicles
        Vehicle car1 = new Car("V001", "Toyota Corolla", 50, true);
        Vehicle motorcycle1 = new Motorcycle("V002", "Harley Davidson", 30, true);
        
        // Add vehicles to the fleet
        agency.addVehicle(car1);
        agency.addVehicle(motorcycle1);
        
        // Create customer
        Customer customer = new Customer("John Doe");
        
        // Rent vehicles
        agency.rentVehicle(car1, customer, 5);
        agency.rentVehicle(motorcycle1, customer, 2);
    }
}

---

### Testing with JUnit
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;

public class VehicleTest {
    
    @Test
    public void testCarRentalCost() {
        Vehicle car = new Car("V001", "Toyota Corolla", 50, true);
        assertEquals(250, car.calculateRentalCost(5));
    }

    @Test
    public void testMotorcycleRentalCost() {
        Vehicle motorcycle = new Motorcycle("V002", "Harley Davidson", 30, false);
        assertEquals(60, motorcycle.calculateRentalCost(2));
    }
}

---

### Evaluation Criteria

- OOP Principles: Correctly implementing all principles: abstraction, encapsulation, inheritance, polymorphism, and composition.

