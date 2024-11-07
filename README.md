def add_expense(expenses, item, amount):
    expenses.append((item, amount))
    print(f"Added expense: {item} - ${amount}")

def view_expenses(expenses):
    print("Expenses:")
    for i, (item, amount) in enumerate(expenses, 1):
        print(f"{i}. {item} - ${amount}")

def save_expenses(expenses, filename="expenses.txt"):
    with open(filename, "w") as file:
        for item, amount in expenses:
            file.write(f"{item},{amount}\n")
    print("Expenses saved to file.")

def load_expenses(filename="expenses.txt"):
    expenses = []
    try:
        with open(filename, "r") as file:
            for line in file:
                item, amount = line.strip().split(",")
                expenses.append((item, float(amount)))
        print("Expenses loaded from file.")
    except FileNotFoundError:
        print("No saved expenses found.")
    return expenses

expenses = load_expenses()
while True:
    action = input("Enter action (add/view/save/quit): ").lower()
    if action == "add":
        item = input("Enter expense item: ")
        amount = float(input("Enter expense amount: "))
        add_expense(expenses, item, amount)
    elif action == "view":
        view_expenses(expenses)
    elif action == "save":
        save_expenses(expenses)
    elif action == "quit":
        break
