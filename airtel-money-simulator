import json
import os

ACCOUNTS_FILE = 'accounts.json'

def load_accounts():
    if not os.path.exists(ACCOUNTS_FILE):
        return {}
    with open(ACCOUNTS_FILE, 'r') as f:
        return json.load(f)

def save_accounts(accounts):
    with open(ACCOUNTS_FILE, 'w') as f:
        json.dump(accounts, f, indent=2)

def create_account():
    accounts = load_accounts()
    print("\n--- Create a New Airtel Money Account ---")
    name = input("Enter your full name: ")
    phone = input("Enter your 09XXXXXXXX phone number: ")

    if phone in accounts:
        print("⚠️ This phone number is already registered.")
        return

    pin = input("Set a secure 4-digit PIN: ")

    accounts[phone] = {
        "name": name,
        "pin": pin,
        "balance": 0.0
    }

    save_accounts(accounts)
    print("✅ Account created successfully!")

def login():
    accounts = load_accounts()
    phone = input("  Enter your phone number:\n  ____ ")

    if phone not in accounts:
        print("❌ No account found with this number.")
        return

    pin = input("  Enter your PIN:\n  ____ ")
    if pin != accounts[phone]["pin"]:
        print("❌ Incorrect PIN.")
        return

    print(f"\n👋 Welcome, {accounts[phone]['name']}!")
    user_menu(phone)

def verify_pin(accounts, phone):
    pin = input("  🔐 Please enter your PIN to confirm.\n  ____ ")
    return pin == accounts[phone]['pin']

def user_menu(phone):
    while True:
        print("\n=== Airtel Money Menu ===")
        print("1. Check Balance")
        print("2. Deposit Money")
        print("3. Withdraw Money")
        print("4. Buy Data Bundle")
        print("5. Find Help")
        print("6. Logout")

        choice = input("Select an option (1-6): ")

        if choice == "1":
            check_balance(phone)
        elif choice == "2":
            deposit(phone)
        elif choice == "3":
            withdraw(phone)
        elif choice == "4":
            buy_bundle(phone)
        elif choice == "5":
            find_help()
        elif choice == "6":
            print("✅ You have successfully logged out. Goodbye!")
            break
        else:
            print("⚠️ Invalid selection. Please try again.")

def check_balance(phone):
    accounts = load_accounts()
    print(f"\n💰 Your current balance is: MK {accounts[phone]['balance']:.2f}")

def deposit(phone):
    accounts = load_accounts()
    try:
        amount = float(input("Enter amount to deposit (MK): "))
        if amount <= 0:
            print("⚠️ Amount must be greater than zero.")
            return
        accounts[phone]['balance'] += amount
        save_accounts(accounts)
        print(f"✅ Deposit successful! New balance: MK {accounts[phone]['balance']:.2f}")
    except ValueError:
        print("❌ Invalid input. Please enter a valid amount.")

def withdraw(phone):
    accounts = load_accounts()
    try:
        amount = float(input("Enter amount to withdraw (MK): "))
        if amount <= 0:
            print("⚠️ Amount must be greater than zero.")
            return
        if accounts[phone]['balance'] < amount:
            print("❌ Insufficient balance.")
            return
        if not verify_pin(accounts, phone):
            print("❌ PIN verification failed.")
            return
        accounts[phone]['balance'] -= amount
        save_accounts(accounts)
        print(f"✅ Withdrawal successful. Remaining balance: MK {accounts[phone]['balance']:.2f}")
    except ValueError:
        print("❌ Invalid input. Please enter a valid amount.")

def buy_bundle(phone):
    accounts = load_accounts()
    print("\n=== Available Data Bundles ===")
    print("1. Daily Bundle (MK 250 for 90MB)")
    print("2. Weekly Bundle (MK 1,000 for 800MB)")
    print("3. Monthly Bundle (MK 2,500 for 5GB)")
    print("4. Cancel")

    bundles = {
        "1": ("Daily Bundle", 250),
        "2": ("Weekly Bundle", 1000),
        "3": ("Monthly Bundle", 2500)
    }

    choice = input("Select a bundle (1-4): ")
    if choice == "4":
        return
    if choice not in bundles:
        print("⚠️ Invalid selection.")
        return

    bundle_name, cost = bundles[choice]
    if accounts[phone]['balance'] < cost:
        print("❌ Insufficient funds to purchase this bundle.")
        return

    if not verify_pin(accounts, phone):
        print("❌ PIN verification failed.")
        return

    accounts[phone]['balance'] -= cost
    save_accounts(accounts)
    print(f"✅ {bundle_name} purchased successfully! Remaining balance: MK {accounts[phone]['balance']:.2f}")

def find_help():
    print("\n📘 === Help & Support ===")
    print("  Welcome to the Airtel Money Help Center. Here are some things you can do:")
    print("  • 💡 To create an account, go back to the main menu and select 'Create Account'.")
    print("  • 🔐 Always keep your PIN safe. Do not share it with anyone.")
    print("  • 💵 You can deposit or withdraw money after logging in.")
    print("  • 📲 Data bundles are available in Daily, Weekly, and Monthly options.")
    print("  • 🆘 For support, visit an Airtel store or call 121 (placeholder).")
    print("\n  To return to the menu, just select the 'Logout' option and log in again.")


def main():
  name = "Welcome To Airtel Money"
  space = " " * 18
  print (space + "_" * 24 + space)
  print ("")
  print (space + name.upper()) 
  print (space + "_" * 24 +space)
  print ("")
  
  choice = input("  This is a simple version.Enter *211# to get started.\n  ____ ")
  
  if choice == "*211#":
    while True:
        print("1. Create Account")
        print("2. Login")
        print("3. Find Help")
        print("4. Exit")

        option = input("  Please choose an option (1-3).\n  ____ ")

        if option == "1":
            create_account()
        elif option == "2":
            login()
        elif option == "3":
            find_help()
        elif option == "4":
            print("\n  👋 Thank you for using Airtel Money. See you again!")
            break
        else:
            print("\n  ⚠️ Invalid choice. Please select 1, 2, or 3.")
  else:
   print("\n  ⚠️ Invalid input!")

if __name__ == '__main__':
    main()
