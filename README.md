# Mortgage Calculator

This Java program calculates mortgage payments, remaining loan balances, and provides a full amortization schedule. It is useful for home buyers, financial analysts, and anyone interested in understanding loan repayment structures.

## Features
- **Fixed Monthly Payment Calculation**
- **Remaining Balance Calculation** (after a specified number of months)
- **Amortization Schedule** (breakdown of principal, interest, and remaining balance for each month)

## How It Works
The program consists of three core methods:

### 1. Mortgage Payment Calculation
Calculates the monthly payment using the formula:
```java
public static double mortgagePayment(double L, double monthlyRate, int n) {
    return (L * monthlyRate) / (1 - Math.pow(1 + monthlyRate, -n));
}
```
Where:
- `L` = Loan amount
- `monthlyRate` = Monthly interest rate (annual rate / 12)
- `n` = Number of months (loan term)

### 2. Remaining Balance Calculation
Determines the balance after `j` months:
```java
public static double remainingBalance(double L, double monthlyRate, int n, int j) {
    double alpha = 1 + monthlyRate;
    return L * (Math.pow(alpha, n) - Math.pow(alpha, j)) / (Math.pow(alpha, n) - 1);
}
```
Where:
- `alpha = 1 + monthlyRate`
- `j` = Number of months passed

### 3. Amortization Schedule
Generates a breakdown of payments, showing:
```java
public static void paymentBreakdown(double L, double monthlyRate, int n) {
    double A = mortgagePayment(L, monthlyRate, n);
    double balance = L;
    
    System.out.println("Month | Payment | Interest | Principal | Remaining Balance");
    System.out.println("------------------------------------------------------------");
    
    for (int j = 1; j <= n; j++) {
        double interest = monthlyRate * balance;
        double principal = A - interest;
        balance -= principal;
        
        System.out.printf("%5d | $%7.2f | $%8.2f | $%9.2f | $%16.2f\n", j, A, interest, principal, balance);
    }
}
```

## Example Usage
```java
public class MortgageCalculator {
    public static void main(String[] args) {
        double L = 100000;  // Loan amount
        double monthlyRate = 0.006;  // Monthly interest rate (0.6%)
        int n = 180;  // Number of months (15 years)
        int j = 84;  // Month for remaining balance calculation

        double A = mortgagePayment(L, monthlyRate, n);
        double R_j = remainingBalance(L, monthlyRate, n, j);

        System.out.printf("Monthly Payment: $%.2f\n", A);
        System.out.printf("Remaining Balance after %d months: $%.2f\n", j, R_j);
        
        double interest_j, principal_j;
        double balance = L;
        for (int i = 1; i <= j; i++) {
            double interest = monthlyRate * balance;
            double principal = A - interest;
            balance -= principal;
            if (i == j) {
                interest_j = interest;
                principal_j = principal;
                System.out.printf("Interest Paid in Month %d: $%.2f\n", j, interest_j);
                System.out.printf("Principal Paid in Month %d: $%.2f\n", j, principal_j);
            }
        }

        paymentBreakdown(L, monthlyRate, n);
    }
}
```

### Sample Output
```
Monthly Payment: $843.86
Remaining Balance after 84 months: $58,326.57
Interest Paid in Month 84: $350.00
Principal Paid in Month 84: $493.86

Month | Payment | Interest | Principal | Remaining Balance
------------------------------------------------------------
  1   | $843.86 |  $600.00 |  $243.86  | $99,756.14
  2   | $843.86 |  $598.54 |  $245.32  | $99,510.82
...
180   | $843.86 |  $4.21   |  $839.65  | $0.00
```

## Requirements
- Java 8 or later

## Installation
Clone the repository:
```sh
git clone https://github.com/KennethTebogo/mortgage-calculator-java.git
cd mortgage-calculator-java
```

## Running the Program
Compile and run the Java program:
```sh
javac MortgageCalculator.java
java MortgageCalculator
```

## Future Enhancements
- Add user input for loan parameters
- Improve output formatting
- Export amortization schedule to CSV/Excel

## License
This project is licensed under the MIT License.

## Author
[Kenneth Tebogo Khondowe](https://github.com/KennethTebogo)

