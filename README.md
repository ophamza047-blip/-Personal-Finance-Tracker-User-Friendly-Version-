# -Personal-Finance-Tracker-User-Friendly-Version-
# Personal Finance Tracker (User-Friendly Version)

incomes = []
expenses = []

# Function to add income
def add_income():
    print("\n--- Add Income ---")
    date = input("Enter date (YYYY-MM-DD): ")
    amount = float(input("Enter income amount: "))
    description = input("Enter income source (e.g., Salary, Bonus): ")
    incomes.append((date, amount, description))
    print("Income added successfully!")

# Function to add expense
def add_expense():
    print("\n--- Add Expense ---")
    date = input("Enter date (YYYY-MM-DD): ")
    amount = float(input("Enter expense amount: "))
    category = input("Enter expense category (e.g., Food, Rent, Shopping): ")
    description = input("Enter description: ")
    expenses.append((date, amount, category, description))
    print("Expense added successfully!")

# Function to view balance
def view_balance():
    total_income = sum([amt for d, amt, desc in incomes])
    total_expense = sum([amt for d, amt, cat, desc in expenses])
    balance = total_income - total_expense
    print("\n--- Balance Summary ---")
    print(f"Total Income: {total_income}")
    print(f"Total Expense: {total_expense}")
    print(f"Remaining Balance (Savings): {balance}")

# Function to view all transactions with details
def view_transactions():
    print("\n--- All Incomes ---")
    for d, amt, desc in incomes:
        print(f"{d} | + {amt} | {desc}")
    print("\n--- All Expenses ---")
    for d, amt, cat, desc in expenses:
        print(f"{d} | - {amt} | {cat} | {desc}")

# Function to show summary report
def summary_report():
    if not incomes:
        print("\nNo income records found.")
        return
    if not expenses:
        print("\nNo expense records found.")
        return

    total_income = sum([amt for d, amt, desc in incomes])
    total_expense = sum([amt for d, amt, cat, desc in expenses])
    balance = total_income - total_expense

    print("\n====== Expense Summary ======")
    category_totals = {}
    for d, amt, cat, desc in expenses:
        category_totals[cat] = category_totals.get(cat, 0) + amt
        print(f"{d} | {cat} | {desc} | {amt}")

    print("\n--- Expense Breakdown by Category ---")
    for cat, amt in category_totals.items():
        percent = (amt / total_expense) * 100
        print(f"{cat}: {amt} ({percent:.2f}%)")

    print("\n--- Final Summary ---")
    print(f"Total Income: {total_income}")
    print(f"Total Expenses: {total_expense}")
    print(f"Remaining Balance (Savings): {balance}")

    # Smart tips based on spending
    print("\n--- Smart Tips for Better Future ---")
    for cat, amt in category_totals.items():
        percent = (amt / total_expense) * 100
        if cat.lower() == "food" and percent > 40:
            print("🍔 You are spending too much on Food. Try cooking at home more often.")
        if cat.lower() == "rent" and percent > 50:
            print("🏠 Rent is too high. Consider shared accommodation or cheaper housing.")
        if cat.lower() == "shopping" and percent > 30:
            print("🛍️ Too much on Shopping! Try controlling impulse buying.")

    if balance < (0.2 * total_income):
        print("💰 Your savings are less than 20% of income. Try to save more for emergencies.")

# Main program loop
while True:
    print("\n==== Personal Finance Tracker ====")
    print("1. Add Income")
    print("2. Add Expense")
    print("3. View Balance")
    print("4. View All Transactions")
    print("5. View Summary Report (with tips)")
    print("6. Exit")
    
    choice = input("Choose an option (1-6): ")
    
    if choice == "1":
        add_income()
    elif choice == "2":
        add_expense()
    elif choice == "3":
        view_balance()
    elif choice == "4":
        view_transactions()
    elif choice == "5":
        summary_report()
    elif choice == "6":
        print("Exiting program. Goodbye!")
        break
    else:
        print("Invalid choice! Please try again.")
