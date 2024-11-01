# Airline_EMSystem
This is a a system that uses Python and OOP elements 

# Abstract Class
from abc import ABC, abstractmethod

class FlightBase(ABC):
    @abstractmethod
    def display_info(self):
        pass

class Flight(FlightBase):
    def __init__(self, flight_number, origin, destination, seats):
        self.flight_number = flight_number
        self.origin = origin
        self.destination = destination
        self._seats = seats   
        self.passengers = []

    def add_passenger(self, passenger):
        if len(self.passengers) < self._seats:
            self.passengers.append(passenger)
            print(f"Passenger {passenger.name} added to flight {self.flight_number}.")
        else:
            print(f"No available seats on flight {self.flight_number}.")

    def remove_passenger(self, passenger_id):
        self.passengers = [p for p in self.passengers if p.passenger_id != passenger_id]
        print(f"Passenger {passenger_id} removed from flight {self.flight_number}.")

    def display_info(self):
        print(f"Flight Number: {self.flight_number}, Origin: {self.origin}, Destination: {self.destination}, Available Seats: {self._seats - len(self.passengers)}")


# Subclass for International Flights
class InternationalFlight(Flight):
    def __init__(self, flight_number, origin, destination, seats, passport_required=True):
        super().__init__(flight_number, origin, destination, seats)
        self.passport_required = passport_required

    def display_info(self):  # Polymorphism - Overriding display_info method
        super().display_info()
        print("Passport Required: Yes" if self.passport_required else "Passport Required: No")

# Subclass for Domestic Flights
class DomesticFlight(Flight):
    def __init__(self, flight_number, origin, destination, seats):
        super().__init__(flight_number, origin, destination, seats)

    def display_info(self):  # Polymorphism
        super().display_info()
        print("Domestic Flight - No passport required.")
