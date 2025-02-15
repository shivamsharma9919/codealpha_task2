# codealpha_task2
banking system
import java.util.*;
class Account {
            private String accountNumber;
            private String customerName;
            private double balance;

            public Account(String accountNumber, String customerName) {
                this.accountNumber = accountNumber;
                this.customerName = customerName;
                this.balance = 0.0;
            }

            public String getAccountNumber() {
                return accountNumber;
            }

            public String getCustomerName() {
                return customerName;
            }

            public double getBalance() {
                return balance;
            }

            public void deposit(double amount) {
                if (amount > 0) {
                    balance += amount;
                    System.out.println("Deposited: " + amount);
                } else {
                    System.out.println("Deposit amount must be positive.");
                }
            }

            public void withdraw(double amount) {
                if (amount <= balance) {
                    balance -= amount;
                    System.out.println("Withdrawn: " + amount);
                } else {
                    System.out.println("Insufficient balance.");
                }
            }

            @Override
            public String toString() {
                return "Account Number: " + accountNumber + ", Customer Name: " + customerName + ", Balance: " + balance;
            }
        }

        class Bank {
            private List<Account> accounts;

            public Bank() {
                accounts = new ArrayList<>();
            }

            public void createAccount(String accountNumber, String customerName) {
                Account newAccount = new Account(accountNumber, customerName);
                accounts.add(newAccount);
                System.out.println("Account created for: " + customerName);
            }

            public Account findAccount(String accountNumber) {
                for (Account account : accounts) {
                    if (account.getAccountNumber().equals(accountNumber)) {
                        return account;
                    }
                }
                return null;
            }

            public void deposit(String accountNumber, double amount) {
                Account account = findAccount(accountNumber);
                if (account != null) {
                    account.deposit(amount);
                } else {
                    System.out.println("Account not found.");
                }
            }

            public void withdraw(String accountNumber, double amount) {
                Account account = findAccount(accountNumber);
                if (account != null) {
                    account.withdraw(amount);
                } else {
                    System.out.println("Account not found.");
                }
            }

            public void displayAccounts() {
                for (Account account : accounts) {
                    System.out.println(account);
                }
            }
        }

        public class bankingsystem {
            public static void main(String[] args) {
                Scanner scanner = new Scanner(System.in);
                Bank bank = new Bank();
                int choice;

                do {
                    System.out.println("\n--- Banking Management System ---");
                    System.out.println("1. Create Account");
                    System.out.println("2. Deposit");
                    System.out.println("3. Withdraw");
                    System.out.println("4. Display All Accounts");
                    System.out.println("5. Exit");
                    System.out.print("Enter your choice: ");
                    choice = scanner.nextInt();
                    scanner.nextLine(); // Consume newline

                    switch (choice) {
                        case 1:
                            System.out.print("Enter account number: ");
                            String accountNumber = scanner.nextLine();
                            System.out.print("Enter customer name: ");
                            String customerName = scanner.nextLine();
                            bank.createAccount(accountNumber, customerName);
                            break;

                        case 2:
                            System.out.print("Enter account number: ");
                            accountNumber = scanner.nextLine();
                            System.out.print("Enter amount to deposit: ");
                            double depositAmount = scanner.nextDouble();
                            bank.deposit(accountNumber, depositAmount);
                            break;

                        case 3:
                            System.out.print("Enter account number: ");
                            accountNumber = scanner.nextLine();
                            System.out.print("Enter amount to withdraw: ");
                            double withdrawAmount = scanner.nextDouble();
                            bank.withdraw(accountNumber, withdrawAmount);
                            break;

                        case 4:
                            bank.displayAccounts();
                            break;

                        case 5:
                            System.out.println("Exiting...");
                            break;

                        default:
                            System.out.println("Invalid choice. Please try again.");
                    }
                } while (choice != 5);

                scanner.close();
            }
        }

