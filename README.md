# Program-Documentation
#include <iostream>
#include <iomanip>
using namespace std;

// Named Constants
const double SAVINGS_SERVICE_CHARGE = 10.00;
const double CURRENT_SERVICE_CHARGE = 25.00;
const double SAVINGS_INTEREST_RATE = 0.04;
const double CURRENT_LOW_INTEREST_RATE = 0.03;
const double CURRENT_HIGH_INTEREST_RATE = 0.05;
const double CURRENT_INTEREST_THRESHOLD = 5000.00;


int main() {
    int accountNumber;
    char accountType;
    double minBalance, currentBalance;

    cout << "Enter account number, type (S/C), min balance, and current balance:\n";
    if (!(cin >> accountNumber)) {
        cout << "Invalid account number.\n";
        return 1;
    }
    
	cin >> accountType >> minBalance >> currentBalance;

    double interestRate;
    double serviceCharge;

    if (accountType == 'S' || accountType == 's') {
        serviceCharge = SAVINGS_SERVICE_CHARGE;
        interestRate = SAVINGS_INTEREST_RATE;
    } else {
        serviceCharge = CURRENT_SERVICE_CHARGE;
        interestRate = (currentBalance >= minBalance + CURRENT_INTEREST_THRESHOLD) ? CURRENT_HIGH_INTEREST_RATE : CURRENT_LOW_INTEREST_RATE;
    }

    if (currentBalance < minBalance) {
        currentBalance -= serviceCharge;
        cout << "Account Number: " << accountNumber << "\n";
        cout << "Account Type: " << (accountType == 'S' || accountType == 's' ? "Savings" : "Current") << "\n";
        cout << "You failed to maintain minimum balance. Service Charges = $ " << fixed << setprecision(2) << serviceCharge << "\n";
        cout << "Current Balance = $ " << currentBalance << "\n";
    } else {
        double interest = currentBalance * interestRate;
        currentBalance += interest;
        cout << "Account Number: " << accountNumber << "\n";
        cout << "Account Type: " << (accountType == 'S' || accountType == 's' ? "Savings" : "Current") << "\n";
        cout << "You received interest = $ " << fixed << setprecision(2) << interest << " @ " << interestRate*100 << "%\n";
        cout << "Current Balance = $ " << currentBalance << "\n";
    }

    return 0;
}
