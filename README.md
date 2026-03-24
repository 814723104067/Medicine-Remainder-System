import time
from datetime import datetime

def add_medicine():
    name = input("Enter medicine name: ")
    time_input = input("Enter time (HH:MM format): ")

    with open("medicines.txt", "a") as file:
        file.write(f"{name},{time_input}\n")

    print("✅ Medicine added successfully!")

def view_medicines():
    try:
        with open("medicines.txt", "r") as file:
            print("\n📋 Medicine Schedule:")
            for line in file:
                name, time_input = line.strip().split(",")
                print(f"{name} at {time_input}")
    except FileNotFoundError:
        print("No medicines found!")

def check_reminders():
    print("⏰ Reminder system started... (Press Ctrl+C to stop)")
    
    while True:
        now = datetime.now().strftime("%H:%M")
        
        try:
            with open("medicines.txt", "r") as file:
                for line in file:
                    name, time_input = line.strip().split(",")
                    
                    if now == time_input:
                        print(f"\n🔔 Time to take your medicine: {name}")
        
        except FileNotFoundError:
            pass
        
        time.sleep(60)  # Check every minute

def main():
    while True:
        print("\n💊 MEDICINE REMINDER SYSTEM")
        print("1. Add Medicine")
        print("2. View Medicines")
        print("3. Start Reminder")
        print("4. Exit")

        choice = input("Enter choice: ")

        if choice == "1":
            add_medicine()
        elif choice == "2":
            view_medicines()
        elif choice == "3":
            check_reminders()
        elif choice == "4":
            print("Exiting... 👋")
            break
        else:
            print("Invalid choice!")

if __name__ == "__main__":
    main()
