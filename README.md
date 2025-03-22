# Practical.cpp

**practical__1**
```
#include <iostream>
#include <cstdlib> // For atoi
using namespace std;

// Function to compute the alternating series sum
double computeSeriesSum(int n) {
    double series_sum = 0.0;    
    
    for (int i = 1; i <= n; i++) {
        // Add or subtract based on whether i is odd or even
        if (i % 2 == 1) {
            series_sum += 1.0 / (i * i); // Add for odd i
        } else {
            series_sum -= 1.0 / (i * i); // Subtract for even i
        }
    }    
    return series_sum;
}

int main(int argc, char* argv[]) {
    int n;

    // Check if a command-line argument is provided
    if (argc > 1) {
        n = atoi(argv[1]); // Convert argument to integer
        if (n <= 0) { // Check if n is positive
            cout << "Please enter a positive integer." << endl;
            return 1; // Exit with an error code
        }
    } else {
        // Prompt user for input
        cout << "Enter the number of terms (n): ";
        cin >> n;

        // Validate user input
        while (n <= 0) {
            cout << "Please enter a positive integer: ";
            cin >> n;
        }
    }

    // Compute the series sum
    double result = computeSeriesSum(n);
    cout << "The sum of the first " << n << " terms of the series is: " << result << endl;
    return 0;
}

```
