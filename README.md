# Calendar-app
This code is used to creat an electronic calendar that can set dates, add events and  can help you keep track of what day  it is

import calendar
import datetime
import json
import os

# File where events will be stored
EVENT_FILE = "events.json"

# Load events from file
def load_events():
    if os.path.exists(EVENT_FILE):
        with open(EVENT_FILE, "r") as file:
            return json.load(file)
    return {}

# Save events to file
def save_events(events):
    with open(EVENT_FILE, "w") as file:
        json.dump(events, file, indent=4)

# Display monthly calendar
def show_calendar():
    year = int(input("Enter year (e.g., 2026): "))
    month = int(input("Enter month (1-12): "))
    print("\n")
    print(calendar.month(year, month))

# Add event
def add_event(events):
    date = input("Enter date (YYYY-MM-DD): ")
    event = input("Enter event description: ")

    if date in events:
        events[date].append(event)
    else:
        events[date] = [event]

    save_events(events)
    print("✅ Event added successfully!")

# View events
def view_events(events):
    date = input("Enter date (YYYY-MM-DD) to view events: ")

    if date in events:
        print(f"\nEvents on {date}:")
        for i, event in enumerate(events[date], start=1):
            print(f"{i}. {event}")
    else:
        print("No events found for this date.")

# Main menu
def main():
    events = load_events()

    while True:
        print("\n=== Electronic Calendar ===")
        print("1. View Monthly Calendar")
        print("2. Add Event")
        print("3. View Events")
        print("4. Exit")

        choice = input("Choose an option (1-4): ")

        if choice == "1":
            show_calendar()
        elif choice == "2":
            add_event(events)
        elif choice == "3":
            view_events(events)
        elif choice == "4":
            print("Goodbye!")
            break
        else:
            print("Invalid choice. Try again.")

if __name__ == "__main__":
    main()
