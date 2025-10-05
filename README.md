# project-1
TOTAL_SEATS = 20

def main( ):
    seats = [0] * TOTAL_SEATS  # 0: available, 1: booked
    
     # Define stops and cumulative adult prices (from start to each stop)
    stops = [
        "vidyaranyapura",
        "bel circle",
        "rmv 2nd stage",
        "dollars colony devasandra",
        "ramaiah college",
        "sadashivanagar police station",
        "malleshwaram 8th cross",
        "malleshwaram 11th cross",
        "malleshwaram 15th cross",
        "malleshwaram 18th cross",
        "majestic bus stop"
    ]
    
    cumulative_adult_prices = {
        "vidyaranyapura": 0,
        "bel circle": 10,
        "rmv 2nd stage": 12,
        "dollars colony devasandra": 14,
        "ramaiah college": 16,
        "sadashivanagar police station": 18,
        "malleshwaram 8th cross": 20,
        "malleshwaram 11th cross": 22,
        "malleshwaram 15th cross": 24,
        "malleshwaram 18th cross": 26,
        "majestic bus stop": 28
    }
    
    while True:
        print("\n=== Bus Reservation System ===")
        print("1. View Available Seats")
        print("2. Book a Seat")
        print("3. Cancel Booking")
        print("4. Calculate Ticket Price (Enter departure/destination/age)")
        print("5. View Route Information and Prices")
        choice = input("Enter your choice (1-5): ")
        
        if not choice.isdigit():
            print("Invalid choice! Please enter a number.")
            continue
        choice = int(choice)

        if choice == 1:
            print("\nSeating Arrangement:")
            for i in range(TOTAL_SEATS):
                status = "Available" if seats[i] == 0 else "Booked"
                print(f"Seat {i+1}: {status}")
        
        elif choice == 2:
            seat_input = input(f"\nEnter seat number (1-{TOTAL_SEATS}): ")
            if not seat_input.isdigit():
                print("Invalid seat number!")
                continue
            seatNum = int(seat_input)
            
            if seatNum < 1 or seatNum > TOTAL_SEATS:
                print("Invalid seat number!")
            elif seats[seatNum-1] == 1:
                print("Seat already booked!")
            else:
                seats[seatNum-1] = 1
                print(f"Seat {seatNum} booked successfully!")
        
        elif choice == 3:
            seat_input = input(f"\nEnter seat number to cancel (1-{TOTAL_SEATS}): ")
            if not seat_input.isdigit():
                print("Invalid seat number!")
                continue
            seatNum = int(seat_input)
            
            if seatNum < 1 or seatNum > TOTAL_SEATS:
                print("Invalid seat number!")
            elif seats[seatNum-1] == 0:
                print("Seat is not booked!")
            else:
                seats[seatNum-1] = 0
                print(f"Booking cancelled for seat {seatNum}!")
        
        elif choice == 4:
            # Get departure, destination, and age
            print("\nAvailable Stops:")
            for stop in stops:
                print(f"- {stop.title()}")
                
            departure = input("\nEnter departure stop: ").strip().lower()
            destination = input("Enter destination stop: ").strip().lower()
            age_input = input("Enter passenger age: ").strip()
            
            # Validate inputs
            if not age_input.isdigit():
                print("Invalid age! Please enter a number.")
                continue
            age = int(age_input)
            
            if departure not in cumulative_adult_prices:
                print(f"Invalid departure stop! Available stops: {', '.join(stops)}")
                continue
                
            if destination not in cumulative_adult_prices:
                print(f"Invalid destination stop! Available stops: {', '.join(stops)}")
                continue
                
            if cumulative_adult_prices[departure] > cumulative_adult_prices[destination]:
                print("Error: Departure stop must come before destination stop.")
                continue
                
            # Calculate adult price for the journey
            adult_price = cumulative_adult_prices[destination] - cumulative_adult_prices[departure]
            
            # Calculate price based on age category
            if age < 5:
                print("Children under 5 travel free!")
                price = 0
            elif age < 10:
                # Kids (5-10 years): proportional to adult price
                price = max(1, round(adult_price * (5/28)))
                print(f"\nTicket price for the journey: Rs {price}")
            elif age < 18:
                # Students: require ID validation
                student_id = input("Enter 6-digit Student ID: ").strip()
                if not student_id.isdigit() or len(student_id) != 6:
                    print("Invalid Student ID! Must be 6 digits. Charging adult fare.")
                    price = adult_price
                else:
                    price = max(1, round(adult_price * (23/28)))
                print(f"\nTicket price for the journey: Rs {price}")
            elif age >= 60:
                # Senior citizens: require ID validation
                senior_id = input("Enter 8-digit Senior Citizen ID: ").strip()
                if not senior_id.isdigit() or len(senior_id) != 8:
                    print("Invalid Senior Citizen ID! Must be 8 digits. Charging adult fare.")
                    price = adult_price
                else:
                    price = max(1, round(adult_price * (25/28)))
                print(f"\nTicket price for the journey: Rs {price}")
            else:
                # Adults (18-59 years)
                price = adult_price
                print(f"\nTicket price for the journey: Rs {price}")
        
        elif choice == 5:
            # Display route information
            print("\nDeparture: Vidyaranyapura")
            print("Destination: Majestic Bus Stop")
            print("Total Journey Price for Adults: Rs 28")
            print("\nRoute Details with Cumulative Prices:")
            print("NOTE: Prices shown are cumulative from Vidyaranyapura")
            print("------------------------------------------------------")
            print("1. Bel circle: Rs 10 (Adults), Rs 2 (Kids), Rs 5 (Students), Rs 7 (Seniors)")
            print("2. RMV 2nd stage: Rs 12 (Adults), Rs 4 (Kids), Rs 7 (Students), Rs 9 (Seniors)")
            print("3. Dollars colony Devasandra: Rs 14 (Adults), Rs 6 (Kids), Rs 9 (Students), Rs 11 (Seniors)")
            print("4. Ramaiah college: Rs 16 (Adults), Rs 8 (Kids), Rs 11 (Students), Rs 13 (Seniors)")
            print("5. Sadashivanagar police station: Rs 18 (Adults), Rs 10 (Kids), Rs 13 (Students), Rs 15 (Seniors)")
            print("6. Malleshwaram 8th cross: Rs 20 (Adults), Rs 12 (Kids), Rs 15 (Students), Rs 17 (Seniors)")
            print("7. Malleshwaram 11th cross: Rs 22 (Adults), Rs 14 (Kids), Rs 17 (Students), Rs 19 (Seniors)")
            print("8. Malleshwaram 15th cross: Rs 24 (Adults), Rs 16 (Kids), Rs 19 (Students), Rs 21 (Seniors)")
            print("9. Malleshwaram 18th cross: Rs 26 (Adults), Rs 18 (Kids), Rs 21 (Students), Rs 23 (Seniors)")
            print("10. Majestic Bus stop: Rs 28 (Adults), Rs 20 (Kids), Rs 23 (Students), Rs 25 (Seniors)")
            print("\nNote: Students and seniors must show valid ID for discounted fares.")
            break
        
        else:
            print("Invalid choice! Please enter a number between 1-5.")

if __name__ == "__main__":
    main( )
TOTAL_SEATS = 20

def main( ):
    seats = [0] * TOTAL_SEATS  # 0: available, 1: booked
    
     # Define stops and cumulative adult prices (from start to each stop)
    stops = [
        "vidyaranyapura",
        "bel circle",
        "rmv 2nd stage",
        "dollars colony devasandra",
        "ramaiah college",
        "sadashivanagar police station",
        "malleshwaram 8th cross",
        "malleshwaram 11th cross",
        "malleshwaram 15th cross",
        "malleshwaram 18th cross",
        "majestic bus stop"
    ]
    
    cumulative_adult_prices = {
        "vidyaranyapura": 0,
        "bel circle": 10,
        "rmv 2nd stage": 12,
        "dollars colony devasandra": 14,
        "ramaiah college": 16,
        "sadashivanagar police station": 18,
        "malleshwaram 8th cross": 20,
        "malleshwaram 11th cross": 22,
        "malleshwaram 15th cross": 24,
        "malleshwaram 18th cross": 26,
        "majestic bus stop": 28
    }
    
    while True:
        print("\n=== Bus Reservation System ===")
        print("1. View Available Seats")
        print("2. Book a Seat")
        print("3. Cancel Booking")
        print("4. Calculate Ticket Price (Enter departure/destination/age)")
        print("5. View Route Information and Prices")
        choice = input("Enter your choice (1-5): ")
        
        if not choice.isdigit():
            print("Invalid choice! Please enter a number.")
            continue
        choice = int(choice)

        if choice == 1:
            print("\nSeating Arrangement:")
            for i in range(TOTAL_SEATS):
                status = "Available" if seats[i] == 0 else "Booked"
                print(f"Seat {i+1}: {status}")
        
        elif choice == 2:
            seat_input = input(f"\nEnter seat number (1-{TOTAL_SEATS}): ")
            if not seat_input.isdigit():
                print("Invalid seat number!")
                continue
            seatNum = int(seat_input)
            
            if seatNum < 1 or seatNum > TOTAL_SEATS:
                print("Invalid seat number!")
            elif seats[seatNum-1] == 1:
                print("Seat already booked!")
            else:
                seats[seatNum-1] = 1
                print(f"Seat {seatNum} booked successfully!")
        
        elif choice == 3:
            seat_input = input(f"\nEnter seat number to cancel (1-{TOTAL_SEATS}): ")
            if not seat_input.isdigit():
                print("Invalid seat number!")
                continue
            seatNum = int(seat_input)
            
            if seatNum < 1 or seatNum > TOTAL_SEATS:
                print("Invalid seat number!")
            elif seats[seatNum-1] == 0:
                print("Seat is not booked!")
            else:
                seats[seatNum-1] = 0
                print(f"Booking cancelled for seat {seatNum}!")
        
        elif choice == 4:
            # Get departure, destination, and age
            print("\nAvailable Stops:")
            for stop in stops:
                print(f"- {stop.title()}")
                
            departure = input("\nEnter departure stop: ").strip().lower()
            destination = input("Enter destination stop: ").strip().lower()
            age_input = input("Enter passenger age: ").strip()
            
            # Validate inputs
            if not age_input.isdigit():
                print("Invalid age! Please enter a number.")
                continue
            age = int(age_input)
            
            if departure not in cumulative_adult_prices:
                print(f"Invalid departure stop! Available stops: {', '.join(stops)}")
                continue
                
            if destination not in cumulative_adult_prices:
                print(f"Invalid destination stop! Available stops: {', '.join(stops)}")
                continue
                
            if cumulative_adult_prices[departure] > cumulative_adult_prices[destination]:
                print("Error: Departure stop must come before destination stop.")
                continue
                
            # Calculate adult price for the journey
            adult_price = cumulative_adult_prices[destination] - cumulative_adult_prices[departure]
            
            # Calculate price based on age category
            if age < 5:
                print("Children under 5 travel free!")
                price = 0
            elif age < 10:
                # Kids (5-10 years): proportional to adult price
                price = max(1, round(adult_price * (5/28)))
                print(f"\nTicket price for the journey: Rs {price}")
            elif age < 18:
                # Students: require ID validation
                student_id = input("Enter 6-digit Student ID: ").strip()
                if not student_id.isdigit() or len(student_id) != 6:
                    print("Invalid Student ID! Must be 6 digits. Charging adult fare.")
                    price = adult_price
                else:
                    price = max(1, round(adult_price * (23/28)))
                print(f"\nTicket price for the journey: Rs {price}")
            elif age >= 60:
                # Senior citizens: require ID validation
                senior_id = input("Enter 8-digit Senior Citizen ID: ").strip()
                if not senior_id.isdigit() or len(senior_id) != 8:
                    print("Invalid Senior Citizen ID! Must be 8 digits. Charging adult fare.")
                    price = adult_price
                else:
                    price = max(1, round(adult_price * (25/28)))
                print(f"\nTicket price for the journey: Rs {price}")
            else:
                # Adults (18-59 years)
                price = adult_price
                print(f"\nTicket price for the journey: Rs {price}")
        
        elif choice == 5:
            # Display route information
            print("\nDeparture: Vidyaranyapura")
            print("Destination: Majestic Bus Stop")
            print("Total Journey Price for Adults: Rs 28")
            print("\nRoute Details with Cumulative Prices:")
            print("NOTE: Prices shown are cumulative from Vidyaranyapura")
            print("------------------------------------------------------")
            print("1. Bel circle: Rs 10 (Adults), Rs 2 (Kids), Rs 5 (Students), Rs 7 (Seniors)")
            print("2. RMV 2nd stage: Rs 12 (Adults), Rs 4 (Kids), Rs 7 (Students), Rs 9 (Seniors)")
            print("3. Dollars colony Devasandra: Rs 14 (Adults), Rs 6 (Kids), Rs 9 (Students), Rs 11 (Seniors)")
            print("4. Ramaiah college: Rs 16 (Adults), Rs 8 (Kids), Rs 11 (Students), Rs 13 (Seniors)")
            print("5. Sadashivanagar police station: Rs 18 (Adults), Rs 10 (Kids), Rs 13 (Students), Rs 15 (Seniors)")
            print("6. Malleshwaram 8th cross: Rs 20 (Adults), Rs 12 (Kids), Rs 15 (Students), Rs 17 (Seniors)")
            print("7. Malleshwaram 11th cross: Rs 22 (Adults), Rs 14 (Kids), Rs 17 (Students), Rs 19 (Seniors)")
            print("8. Malleshwaram 15th cross: Rs 24 (Adults), Rs 16 (Kids), Rs 19 (Students), Rs 21 (Seniors)")
            print("9. Malleshwaram 18th cross: Rs 26 (Adults), Rs 18 (Kids), Rs 21 (Students), Rs 23 (Seniors)")
            print("10. Majestic Bus stop: Rs 28 (Adults), Rs 20 (Kids), Rs 23 (Students), Rs 25 (Seniors)")
            print("\nNote: Students and seniors must show valid ID for discounted fares.")
            break
        
        else:
            print("Invalid choice! Please enter a number between 1-5.")

if __name__ == "__main__":
    main( )

