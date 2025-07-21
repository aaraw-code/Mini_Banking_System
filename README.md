# Mini_Banking_System
Basic banking application in Python 

class BankAccount():
    def __init__(self,name,acc_no,balance):
        self.name = name
        self.acc_no = acc_no
        self.balance = balance

    def deposit(self,amount):
        self.balance += amount
        print("Rs", amount, " was credit")
        print("Total balance = ", self.get_balance())

    def withdraw(self,amount):
        if amount > self.balance:
            print("Insufficient balance!")
        else:
            self.balance -= amount
            print("Rs", amount, "was withdrawn")
            print("Total balance = ", self.get_balance())

    def show_details(self):
        print("Account holder: ", self.name)
        print("Account number", self.acc_no)
        print("Balance: Rs", self.balance)

    def get_balance(self):                                   # this return the current balance
        return self.balance
    

accounts = {}

while True:
    print("1. Create account")
    print("2. Deposit")
    print("3. Withdraw")
    print("4. Show account details")
    print("5. Exit")

    ask = input("Enter your choice (1-5): ")

    if ask == "1":
        acc_no = input("Enter your account number: ")
        if acc_no in accounts:                                             # its check account nuber exists in disctionary(accounts)
            print("Account with this number already exists!")
        else:
            name = input("Enter your name: ")
            balance = float(input("Enter initial balance: "))
            new_account = BankAccount(name,acc_no,balance)
            accounts[acc_no] = new_account
            print("Account created succesfully!")

            with open("account.json","w") as f:
                json.dump({acc_no: account.__dict__ for acc_no, account in accounts.items()},f,indent="4")
    if ask == "2":
        acc_no = input("Enter your account number: ")
        if acc_no in accounts:
            account = accounts[acc_no]                                       #User ke account number se uska pura account object le rahe hain.
            print(f"Account holder: {account.name}")
            print(f"Current balance: {account.balance}")
            amount = float(input("Enter amount to deposit: "))
            account.deposit(amount)
        else:
            print("Account not found!")

    if ask == "3":
        acc_no = input("Enter your account number: ")
        if acc_no in accounts:
            account = accounts[acc_no]
            amount = float(input("Enter withdraw amount: "))
            account.withdraw(amount)
        else:
            print("Account not found.")

    if ask == "4":
        acc_no = input("Enter account number to see details: ")
        if acc_no in accounts:
            account = accounts[acc_no]
            account.show_details()                                             # help to display the details of user
        else:
            print("Account not found.")

                
    if ask == "5":
        print("Thank you for using the Bank Management System!")
        break






        




