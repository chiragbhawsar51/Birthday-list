# Birthday-list
import datetime

# dictionary to store the friend/family birthdays
birthdays = {}

def add_birthday():
    name = input("Enter friend/family member's name: ")
    birthday_str = input("Enter birthday (format: yyyy-mm-dd): ")
    birthday = datetime.datetime.strptime(birthday_str, '%Y-%m-%d').date()
    birthdays[name] = birthday
    print("Birthday added successfully.")

def display_birthday_list():
    if not birthdays:
        print("Birthday list is empty.")
    else:
        print("Upcoming birthdays:")
        sorted_birthdays = sorted(birthdays.items(), key=lambda x: x[1])
        today = datetime.date.today()
        for name, birthday in sorted_birthdays:
            if birthday >= today:
                days_until_birthday = (birthday - today).days
                print(f"{name} - {birthday.strftime('%B %d')}, {days_until_birthday} days until birthday.")

def search_birthday():
    name = input("Enter friend/family member's name to search for: ")
    if name in birthdays:
        birthday = birthdays[name]
        print(f"{name}'s birthday is on {birthday.strftime('%B %d')}.")
    else:
        print(f"No birthday found for {name}.")

def display_monthly_birthdays():
    today = datetime.date.today()
    upcoming_birthdays = []
    for name, birthday in birthdays.items():
        if birthday.month == today.month:
            upcoming_birthdays.append((name, birthday))
    if not upcoming_birthdays:
        print("No birthdays this month.")
    else:
        print(f"Upcoming birthdays for {today.strftime('%B')}:")
        for name, birthday in upcoming_birthdays[:5]:
            days_until_birthday = (birthday - today).days
            print(f"{name} - {birthday.strftime('%B %d')}, {days_until_birthday} days until birthday.")
