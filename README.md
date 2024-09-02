JavaScript implementation using a linked list to manage bank accounts, facilitate money transfers, and simplify the account creation process. This includes account creation, balance checking, and transaction functionalities.
Linked List Node and Linked List Implementation
First, let’s define the ListNode and LinkedList classes:
JavaScript:
class ListNode {
    constructor(data) {
        this.data = data;
        this.next = null;
    }
}

class LinkedList {
    constructor() {
        this.head = null;
    }

    add(data) {
        const newNode = new ListNode(data);
        if (!this.head) {
            this.head = newNode;
        } else {
            let current = this.head;
            while (current.next) {
                current = current.next;
            }
            current.next = newNode;
        }
    }


    find(accountNumber) {
        let current = this.head;
        while (current) {
            if (current.data.accountNumber === accountNumber) {
                return current.data;
            }
            current = current.next;
        }
        return null;
    }
}
 
Bank Account Class
Next, let’s create the BankAccount class with methods for depositing, withdrawing, and transferring money:
JavaScript:
class BankAccount {
    constructor(accountNumber, accountHolderName, balance = 0) {
        this.accountNumber = accountNumber;
        this.accountHolderName = accountHolderName;
        this.balance = balance;
    }

    deposit(amount) {
        this.balance += amount;
        console.log(`Amount $${amount} deposited into account ${this.accountNumber}.`);
    }

    withdraw(amount) {
        if (amount <= this.balance) {
            this.balance -= amount;
            console.log(`Amount $${amount} withdrawn from account ${this.accountNumber}.`);
        } else {
            console.log(`Insufficient balance in account ${this.accountNumber}.`);
        }
    }

    transfer(amount, recipientAccount) {
        if (amount <= this.balance) {
            this.balance -= amount;
            recipientAccount.deposit(amount);
            console.log(`Amount $${amount} transferred from account ${this.accountNumber} to account ${recipientAccount.accountNumber}.`);
        } else {
            console.log(`Insufficient balance in account ${this.accountNumber} for transfer.`);
        }
    }

    displayBalance() {
        console.log(`Account ${this.accountNumber} balance: $${this.balance}`);
    }
}
 
Bank Management System
Finally, let’s create the bank management system using the linked list to manage accounts:
JavaScript:
class Bank {
    constructor() {
        this.accounts = new LinkedList();
    }


    createAccount(accountNumber, accountHolderName, initialBalance = 0) {
        const newAccount = new BankAccount(accountNumber, accountHolderName, initialBalance);
        this.accounts.add(newAccount);
        console.log(`Account ${accountNumber} created for ${accountHolderName}.`);
    }

    getAccount(accountNumber) {
        return this.accounts.find(accountNumber);
    }

    performTransaction(accountNumber, type, amount, recipientAccountNumber = null) {
        const account = this.getAccount(accountNumber);
        if (!account) {
            console.log(`Account ${accountNumber} not found.`);
            return;
        }

        switch (type) {
            case 'deposit':
                account.deposit(amount);
                break;
            case 'withdraw':
                account.withdraw(amount);
                break;
            case 'transfer':
                const recipientAccount = this.getAccount(recipientAccountNumber);
                if (recipientAccount) {
                    account.transfer(amount, recipientAccount);
                } else {
                    console.log(`Recipient account ${recipientAccountNumber} not found.`);
                }
                break;
            default:
                console.log('Invalid transaction type.');
        }
    }

    displayAccountBalance(accountNumber) {
        const account = this.getAccount(accountNumber);
        if (account) {
            account.displayBalance();
        } else {
            console.log(`Account ${accountNumber} not found.`);
        }
    }
}

// Example usage
const bank = new Bank();
bank.createAccount('001', 'Rajashri', 5000);
bank.createAccount('002', 'Abhi', 2000);

bank.displayAccountBalance('001');
bank.performTransaction('001', 'deposit', 500);
bank.performTransaction('001', 'withdraw', 100);
bank.performTransaction('001', 'transfer', 1000, '002');

bank.displayAccountBalance('001');
bank.displayAccountBalance('002');

 
This code defines a simple bank management system using a linked list to store and manage bank accounts. You can create accounts, check balances, and perform transactions such as deposits, withdrawals, and transfers. This example integrates both linear (linked list) and non-linear (bank account operations) data structures.

