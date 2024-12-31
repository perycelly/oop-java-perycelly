// ASSIGNMENT

Vehicle Rental Management System Design (Java)

This Vehicle Rental Management System will demonstrate all key Object-Oriented Programming (OOP) principles, such as Encapsulation, Inheritance, Polymorphism, Abstraction, and Composition. Here's a detailed breakdown of how each principle is applied across the various components of the system:

1. Abstraction Principle

We will create an abstract base class Vehicle with abstract methods calculateRentalCost(int days) and isAvailableForRental(). Concrete subclasses will implement these methods based on the type of vehicle. public abstract class Vehicle { private String vehicleId; private String model; private double baseRentalRate; private boolean isAvailable;

// Constructor with validation
public Vehicle(String vehicleId, String model, double baseRentalRate) {
    if (vehicleId == null || model == null) throw new IllegalArgumentException("ID and Model cannot be null");
    if (baseRentalRate < 0) throw new IllegalArgumentException("Base rate cannot be negative");
    this.vehicleId = vehicleId;
    this.model = model;
    this.baseRentalRate = baseRentalRate;
    this.isAvailable = true; // Default to available
}

// Abstract methods
public abstract double calculateRentalCost(int days);

public abstract boolean isAvailableForRental();

// Getters and setters
public String getVehicleId() {
    return vehicleId;
}

public void setVehicleId(String vehicleId) {
    this.vehicleId = vehicleId;
}

public String getModel() {
    return model;
}

public void setModel(String model) {
    this.model = model;
}

public double getBaseRentalRate() {
    return baseRentalRate;
}

public void setBaseRentalRate(double baseRentalRate) {
    if (baseRentalRate < 0) throw new IllegalArgumentException("Base rental rate cannot be negative");
    this.baseRentalRate = baseRentalRate;
}

public boolean isAvailable() {
    return isAvailable;
}

public void setAvailable(boolean available) {
    this.isAvailable = available;
}
}

2. Inheritance Hierarchy

Each specific vehicle class (Car, Motorcycle, Truck) will inherit from Vehicle and implement the abstract methods. // Concrete Car class public class Car extends Vehicle { private boolean hasAirConditioning;

public Car(String vehicleId, String model, double baseRentalRate, boolean hasAirConditioning) {
    super(vehicleId, model, baseRentalRate);
    this.hasAirConditioning = hasAirConditioning;
}

@Override
public double calculateRentalCost(int days) {
    double cost = getBaseRentalRate() * days;
    if (hasAirConditioning) {
        cost += 10 * days; // Additional fee for air conditioning
    }
    return cost;
}

@Override
public boolean isAvailableForRental() {
    return isAvailable();
}

public boolean isHasAirConditioning() {
    return hasAirConditioning;
}

public void setHasAirConditioning(boolean hasAirConditioning) {
    this.hasAirConditioning = hasAirConditioning;
}
}

Similarly, we would implement Motorcycle and Truck classes, each with unique rental characteristics.

3. Encapsulation

Encapsulation ensures that sensitive data is protected. We use private fields, getters, and setters with validation where necessary.

For instance, in the Vehicle class, the base rental rate is validated to ensure it is non-negative. Similar validation is implemented for the vehicle's ID and model name.

4. Polymorphism Implementation

To implement polymorphism, we create an interface Rentable with methods like rent() and returnVehicle(). Then, we implement these methods in the vehicle classes. public interface Rentable { void rent(Customer customer, int days); void returnVehicle(); }

// Car class implements Rentable interface public class Car extends Vehicle implements Rentable { @Override

Pery Celly, [28/12/2024 10:36] public void rent(Customer customer, int days) { // Logic for renting a car System.out.println("Car rented to " + customer.getName() + " for " + days + " days."); }

@Override
public void returnVehicle() {
    // Logic for returning the car
    System.out.println("Car returned.");
}
}

Method Overloading and Overriding:

Method Overloading: We can overload methods such as rent() with different parameter types (e.g., rent a car for different durations).
Method Overriding: rent() and returnVehicle() will be overridden in the subclasses to provide specific implementations for each vehicle type.
5. Composition

In this case, the RentalAgency class will manage a fleet of vehicles and have a composition relationship with the Vehicle class. We will also introduce a Customer class and RentalTransaction class to handle the rental transactions. public class RentalAgency { private List vehicleFleet;

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

public class Customer { private String name; private List rentalHistory;

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

public class RentalTransaction { private Vehicle vehicle; private int daysRented;

public RentalTransaction(Vehicle vehicle, int daysRented) {
    this.vehicle = vehicle;
    this.daysRented = daysRented;
}

public double getRentalCost() {
    return vehicle.calculateRentalCost(daysRented);
}
}

Additional Features (Bonus)

Loyalty Program:
An interface LoyaltyProgram can be implemented by the Customer class to calculate discounts based on rental history.

Custom Exceptions:
We can create exceptions like VehicleNotAvailableException or InvalidRentalDurationException.

Vehicle Rating System:
A Rating class can be introduced to manage ratings given by customers for vehicles, storing ratings and reviews.

Complete Example of Inheritance, Polymorphism, and Abstraction

public class Main { public static void main(String[] args) { // Create rental agency RentalAgency agency = new RentalAgency();

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

Testing with JUnit

import static org.junit.jupiter.api.Assertions.*; import org.junit.jupiter.api.Test;

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

Evaluation Criteria

OOP Principles: Correctly implementing all principles: abstraction, encapsulation, inheritance, polymorphism, and composition.
    