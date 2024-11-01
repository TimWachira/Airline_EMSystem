# Abstract Class to help in the OOP concepts

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
        self._seats = seats   # Private attribute to enforce encapsulation
        self.passengers = []   # List to hold passengers
        self.crew = {"pilots": [], "attendants": []}  # Dictionary to hold crew members

    def add_passenger(self, passenger):
        if len(self.passengers) < self._seats:
            self.passengers.append(passenger)
            print(f"Passenger {passenger.name} added to flight {self.flight_number}.")
        else:
            print(f"No available seats on flight {self.flight_number}.")

    def remove_passenger(self, passenger_id):
        self.passengers = [p for p in self.passengers if p.passenger_id != passenger_id]
        print(f"Passenger {passenger_id} removed from flight {self.flight_number}.")

    def add_crew_member(self, crew_member):
        if isinstance(crew_member, Pilot):
            self.crew["pilots"].append(crew_member)
            print(f"Pilot {crew_member.name} added to flight {self.flight_number}.")
        elif isinstance(crew_member, FlightAttendant):
            self.crew["attendants"].append(crew_member)
            print(f"Flight Attendant {crew_member.name} added to flight {self.flight_number}.")

    def display_info(self):
        print(f"Flight Number: {self.flight_number}, Origin: {self.origin}, Destination: {self.destination}, Available Seats: {self._seats - len(self.passengers)}")
        print("Crew Information:")
        for pilot in self.crew["pilots"]:
            pilot.display_info()
        for attendant in self.crew["attendants"]:
            attendant.display_info()

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

    def display_info(self):  # Polymorphism - Overriding display_info method
        super().display_info()
        print("Domestic Flight - No passport required.")




# Created Booking Class
    class Booking:
    def __init__(self):
        self.bookings = []

    def create_booking(self, flight, passenger):
        flight.add_passenger(passenger)
        self.bookings.append((flight, passenger))

    def cancel_booking(self, flight, passenger_id):
        flight.remove_passenger(passenger_id)
        self.bookings = [b for b in self.bookings if b[1].passenger_id != passenger_id]

    def show_bookings(self):
        for flight, passenger in self.bookings:
            print(f"Booking: {passenger.name} on Flight {flight.flight_number}")




# Created CrewMembers Class
    class Pilot:
    def __init__(self, pilot_id, name, experience_years, rank):
        self.pilot_id = pilot_id
        self.name = name
        self.experience_years = experience_years
        self.rank = rank

    def display_info(self):
        print(f"Pilot ID: {self.pilot_id}, Name: {self.name}, Experience: {self.experience_years} years, Rank: {self.rank}")

    class FlightAttendant:
    def __init__(self, attendant_id, name, language):
        self.attendant_id = attendant_id
        self.name = name
        self.language = language

    def display_info(self):
        print(f"Attendant ID: {self.attendant_id}, Name: {self.name}, Language: {self.language}")



# Main EMS Class
    def main():
    flight1 = InternationalFlight("KQ001", "Nairobi", "New York", 250)
    flight2 = DomesticFlight("KQ650", "Nairobi", "Mombasa", 100)

    passenger1 = passenger("001", "Liam Hemsworth", "27")
    passenger2 =pPassenger("002", "Jennifer Lawrence", "25")

    pilotP1 = pilot("P231", "Tom Cruise", "45", "Captain")
    pilotP2 = pilot("P232", "John Travolta", "50", "First Officer")

    attendantA1 = FlightAttendant("A321", "Angelina Jolie", "English")
    attendantA2 = FlightAttendant("A322", "Brad Pitt", "French")

    # Assigning crew members to flights
    flight1.add_crew_member(pilotP1)
    flight1.add_crew_member(attendantA1)
    flight2.add_crew_member(pilotP2)
    flight2.add_crew_member(attendantA2)

    # Creating the  booking system
    booking_system = Booking()

    # Add bookings (Update)
    booking_system.create_booking(flight1, passenger1)
    booking_system.create_booking(flight2, passenger2)
    booking_system.create_booking(flight1, passenger3)  # No seat available for 3rd passenger

    # Show bookings (Read)
    booking_system.show_bookings()

    # Cancel booking (Delete)
    booking_system.cancel_booking(flight1, passenger1.passenger_id)

    # Display flight, passenger, and crew information 
    print("\nFlight Info:")
    flight1.display_info()
    flight2.display_info()

    print("\nPassenger Info:")
    passenger1.display_info()
    passenger2.display_info()
    passenger3.display_info()

    if __name__ == "__main__":
    main()
    


