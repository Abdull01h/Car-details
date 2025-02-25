import json
import os

# শেয়ার্ড ফোল্ডারের লোকেশন
file_path = "/data/data/com.termux/files/home/storage/shared/CarData/data.json"

# ফাইল না থাকলে খালি ডাটা তৈরি করো
if not os.path.exists(file_path):
    with open(file_path, "w") as f:
        json.dump([], f)

# নতুন ডাটা সংরক্ষণ
def add_data():
    license_number = input("Enter Driving License Number: ")
    car_number = input("Enter Car Number: ")
    
    with open(file_path, "r") as f:
        data = json.load(f)

    data.append({"license_number": license_number, "car_number": car_number})

    with open(file_path, "w") as f:
        json.dump(data, f, indent=4)

    print("✅ Data Saved Successfully!")

# সমস্ত ডাটা দেখানো
def view_data():
    with open(file_path, "r") as f:
        data = json.load(f)

    for item in data:
        print(f"License: {item['license_number']}, Car: {item['car_number']}")

# মেনু
while True:
    print("\n🚗 Car & License Data Management")
    print("1️⃣ Add New Data")
    print("2️⃣ View All Data")
    print("3️⃣ Exit")

    choice = input("Select an option (1/2/3): ")

    if choice == "1":
        add_data()
    elif choice == "2":
        view_data()
    elif choice == "3":
        print("🔴 Exiting...")
        break
    else:
        print("❌ Invalid Choice! Try again.")
