# Practical.cpp

# Practical 01
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

![Screenshot (76)](https://github.com/user-attachments/assets/7632d12f-c306-4d6f-be47-854c76169492)

# PRACTICAL-02
```

#include <iostream>
#include <unordered_set>
#include <vector>
using namespace std;

// Function to remove duplicates from the array
void removeDuplicates(vector<int>& arr) {
    unordered_set<int> uniqueElements; // Set to store unique elements
    int index = 0; // Index to keep track of the new array without duplicates

    for (int i = 0; i < arr.size(); i++) {
        // If the element is not already in the set, add it
        if (uniqueElements.find(arr[i]) == uniqueElements.end()) {
            uniqueElements.insert(arr[i]);
            arr[index++] = arr[i]; // Place the unique element in the new position
        }
    }

    // Resize the vector to contain only unique elements
    arr.resize(index);
}

// Function to print the elements of the array
void printArray(const vector<int>& arr) {
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
}

int main() {
    int n;

    cout << "Enter the number of elements in the array: ";
    cin >> n;

    // Input validation for the number of elements
    while (n <= 0) {
        cout << "Please enter a positive integer for the number of elements: ";
        cin >> n;
    }

    vector<int> arr(n); // Use vector for dynamic array allocation

    cout << "Enter the elements of the array: ";
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    removeDuplicates(arr); // Remove duplicates from the array

    cout << "Array after removing duplicates: ";
    printArray(arr); // Print the modified array
    return 0;
}

```

![Screenshot (52)](https://github.com/user-attachments/assets/cce4f3e0-fe01-4b19-aff6-6ce283f17310)


# PRACTICAL-03
```
#include <iostream>
#include <cctype>
#include <string>
#include <map>
#include <sstream> // For std::ostringstream
using namespace std;

// Function to count occurrences of each alphabet letter in the given text
void countAlphabetOccurrences(const string& text) {
    map<char, int> frequency;

    // Count occurrences of each letter
    for (char ch : text) {
        ch = tolower(ch); // Convert to lowercase
        if (isalpha(ch)) {
            frequency[ch]++; // Increment the count for the letter
        }
    }

    // Print the table of occurrences
    cout << "Alphabet Occurrences:" << endl;
    cout << "Letter | Occurrences" << endl;
    cout << "----------------------" << endl;
    for (char letter = 'a'; letter <= 'z'; letter++) {
        cout << letter << "      | " << frequency[letter] << endl; // Print occurrences
    }
}

int main() {
    string text;

    cout << "Enter text: ";
    getline(cin, text); // Read a line of text from the user

    // Check if the text is empty
    if (text.empty()) {
        cout << "The provided text is empty." << endl;
        return 1;
    }

    countAlphabetOccurrences(text); // Count and display occurrences
    return 0;
}

```

![Screenshot (54)](https://github.com/user-attachments/assets/c23c1251-1ef7-4f11-9c89-99fe37606738)

# PRACTICAL-04
```
#include <iostream>
#include <cstring>
using namespace std;


void showCharacterAddresses(const char* str) {
    cout << "Addresses of each character in the string:" << endl;
    while (*str != '\0') {
        cout << (void*)str << " -> " << *str << endl;
        str++;
    }
}


void concatenateStrings(char* str1, const char* str2) {
    while (*str1 != '\0') {
        str1++;
    }
    while (*str2 != '\0') {
        *str1 = *str2;
        str1++;
        str2++;
    }
    *str1 = '\0'; 
}


int compareStrings(const char* str1, const char* str2) {
    while (*str1 != '\0' && *str2 != '\0') {
        if (*str1 != *str2) {
            return (*str1 - *str2); 
        }
        str1++;
        str2++;
    }
    return (*str1 - *str2);  
}


int calculateLength(const char* str) {
    const char* ptr = str;
    int length = 0;
    while (*ptr != '\0') {
        length++;
        ptr++;
    }
    return length;
}

 
void convertToUppercase(char* str) {
    while (*str != '\0') {
        if (*str >= 'a' && *str <= 'z') {
            *str = *str - 'a' + 'A'; 
        }
        str++;
    }
}


void reverseString(char* str) {
    int length = calculateLength(str);
    int start = 0, end = length - 1;
    while (start < end) {
       
        char temp = str[start];
        str[start] = str[end];
        str[end] = temp;
        start++;
        end--;
    }
}

// Function to insert a string at a user-specified position
void insertStringAtPosition(char* str1, const char* str2, int position) {
    int length1 = calculateLength(str1);
    int length2 = calculateLength(str2);
   
    for (int i = length1; i >= position; i--) {
        str1[i + length2] = str1[i];
    }
  
    for (int i = 0; i < length2; i++) {
        str1[position + i] = str2[i];
    }
    str1[length1 + length2] = '\0'; 
}

int main() {
    int choice;
    char str1[100], str2[100];
    int position;
    int result; 

    do {
        cout << "\nMenu: \n";
        cout << "1. Show address of each character in string\n";
        cout << "2. Concatenate two strings\n";
        cout << "3. Compare two strings\n";
        cout << "4. Calculate length of the string\n";
        cout << "5. Convert all lowercase characters to uppercase\n";
        cout << "6. Reverse the string\n";
        cout << "7. Insert a string in another string at a user-specified position\n";
        cout << "8. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;
        cin.ignore(); 

        switch (choice) {
            case 1:
                cout << "Enter a string: ";
                cin.getline(str1, 100);
                showCharacterAddresses(str1);
                break;
            case 2:
                cout << "Enter first string: ";
                cin.getline(str1, 100);
                cout << "Enter second string: ";
                cin.getline(str2, 100);
                concatenateStrings(str1, str2);
                cout << "Concatenated string: " << str1 << endl;
                break;
            case 3:
                cout << "Enter first string: ";
                cin.getline(str1, 100);
                cout << "Enter second string: ";
                cin.getline(str2, 100);
                result = compareStrings(str1, str2); 
                if (result == 0) {
                    cout << "The strings are equal." << endl;
                } else if (result < 0) {
                    cout << "The first string is lexicographically smaller." << endl;
                } else {
                    cout << "The first string is lexicographically larger." << endl;
                }
                break;
            case 4:
                cout << "Enter a string: ";
                cin.getline(str1, 100);
                cout << "Length of the string: " << calculateLength(str1) << endl;
                break;
            case 5:
                cout << "Enter a string: ";
                cin.getline(str1, 100);
                convertToUppercase(str1);
                cout << "String after conversion to uppercase: " << str1 << endl;
                break;
            case 6:
                cout << "Enter a string: ";
                cin.getline(str1, 100);
                reverseString(str1);
                cout << "Reversed string: " << str1 << endl;
                break;
            case 7:
                cout << "Enter the string: ";
                cin.getline(str1, 100);
                cout << "Enter the string to insert: ";
                cin.getline(str2, 100);
                cout << "Enter the position to insert: ";
                cin >> position;
                insertStringAtPosition(str1, str2, position);
                cout << "String after insertion: " << str1 << endl;
                break;
            case 8:
                cout << "Exiting program." << endl;
                break;
            default:
                cout << "Invalid choice. Please try again." << endl;
        }
    } while (choice != 8);
    
    return 0;
}

```

![Screenshot (55)](https://github.com/user-attachments/assets/cf418726-18ae-4dc3-bf0c-201c317c3cda)

![Screenshot (56)](https://github.com/user-attachments/assets/9182732f-7860-4812-a37e-762e1bb3f1e9)


![Screenshot (57)](https://github.com/user-attachments/assets/7a90705b-fcef-4478-8769-77178f00700d)


![Screenshot (58)](https://github.com/user-attachments/assets/d251396d-2732-487b-9382-943717fb477e)


# PRACTICAL-05
**b. with recursion**
```
#include <iostream>
#include <vector> // Include vector for dynamic array allocation
using namespace std;

// Function to merge two sorted arrays into a single sorted array
void mergeArrays(const vector<int>& arr1, const vector<int>& arr2, vector<int>& merged) {
    int i = 0, j = 0, k = 0;

    // Merge the two arrays
    while (i < arr1.size() && j < arr2.size()) {
        if (arr1[i] < arr2[j]) {
            merged[k++] = arr1[i++];
        } else {
            merged[k++] = arr2[j++];
        }
    }
    // If there are remaining elements in arr1, add them
    while (i < arr1.size()) {
        merged[k++] = arr1[i++];
    }
    // If there are remaining elements in arr2, add them
    while (j < arr2.size()) {
        merged[k++] = arr2[j++];
    }
}

// Function to print the elements of an array
void printArray(const vector<int>& arr) {
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
}

int main() {
    int n1, n2;

    cout << "Enter the size of the first array: ";
    cin >> n1;
    // Input validation for the first array size
    while (n1 <= 0) {
        cout << "Please enter a positive integer for the size of the first array: ";
        cin >> n1;
    }
    vector<int> arr1(n1); // Use vector for dynamic array allocation
    cout << "Enter the elements of the first array in sorted order: ";
    for (int i = 0; i < n1; i++) {
        cin >> arr1[i];
    }

    cout << "Enter the size of the second array: ";
    cin >> n2;
    // Input validation for the second array size
    while (n2 <= 0) {
        cout << "Please enter a positive integer for the size of the second array: ";
        cin >> n2;
    }
    vector<int> arr2(n2); // Use vector for dynamic array allocation
    cout << "Enter the elements of the second array in sorted order: ";
    for (int i = 0; i < n2; i++) {
        cin >> arr2[i];
    }

    vector<int> merged(n1 + n2); // Create a vector to hold the merged array

    mergeArrays(arr1, arr2, merged); // Merge the two arrays

    cout << "Merged array: ";
    printArray(merged); // Print the merged array
    return 0;
}
```



![Screenshot (59)](https://github.com/user-attachments/assets/e98612b7-9892-4b09-b965-b382c8638ebc)

**a. without recursion**
```
#include <iostream>
#include <vector> // Include vector for dynamic array allocation
using namespace std;

// Function to perform binary search recursively
int binarySearchRecursive(const vector<int>& arr, int low, int high, int target) {
    if (low > high) {
        return -1; // Target not found
    }

    int mid = low + (high - low) / 2;

    if (arr[mid] == target) {
        return mid; // Target found
    } else if (arr[mid] > target) {
        return binarySearchRecursive(arr, low, mid - 1, target); // Search in the left half
    } else {
        return binarySearchRecursive(arr, mid + 1, high, target); // Search in the right half
    }
}

int main() {
    int n, target;

    cout << "Enter the number of elements: ";
    cin >> n;

    // Input validation for the number of elements
    while (n <= 0) {
        cout << "Please enter a positive integer for the number of elements: ";
        cin >> n;
    }

    vector<int> arr(n); // Use vector for dynamic array allocation

    cout << "Enter the sorted elements: ";
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    cout << "Enter the element to search for: ";
    cin >> target;

    int resultRecursive = binarySearchRecursive(arr, 0, n - 1, target);
    if (resultRecursive != -1) {
        cout << "Element found at index (recursive): " << resultRecursive << endl;
    } else {
        cout << "Element not found (recursive)." << endl;
    }

    return 0;
}

```

![Screenshot (60)](https://github.com/user-attachments/assets/7f92b327-632f-433b-b2c5-3200422d9098)



# PRACTICAL-06
```
#include <iostream>
#include <vector> // Include vector for dynamic array allocation
using namespace std;

// Function to perform binary search iteratively
int binarySearchIterative(const vector<int>& arr, int n, int target) {
    int low = 0, high = n - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == target) {
            return mid; // Target found
        } else if (arr[mid] > target) {
            high = mid - 1; // Search in the left half
        } else {
            low = mid + 1; // Search in the right half
        }
    }

    return -1; // Target not found
}

int main() {
    int n, target;

    cout << "Enter the number of elements: ";
    cin >> n;

    // Input validation for the number of elements
    while (n <= 0) {
        cout << "Please enter a positive integer for the number of elements: ";
        cin >> n;
    }

    vector<int> arr(n); // Use vector for dynamic array allocation

    cout << "Enter the sorted elements: ";
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    cout << "Enter the element to search for: ";
    cin >> target;

    int resultIterative = binarySearchIterative(arr, n, target);
    if (resultIterative != -1) {
        cout << "Element found at index (iterative): " << resultIterative << endl;
    } else {
        cout << "Element not found (iterative)." << endl;
    }

    return 0;
}
```


![Screenshot (62)](https://github.com/user-attachments/assets/7cacf63b-5b49-4fca-b10e-fe0005a4ec90)


# PRACTICAL-07
**a. with recursion**

```
#include <iostream>
#include <cstdlib> // For std::abs
using namespace std;

// Recursive function to calculate GCD using the Euclidean algorithm
int gcdRecursive(int a, int b) {
    // Base case: If b is 0, the GCD is a
    if (b == 0) {
        return a;
    }
    // Recursive case: Call gcd on b and the remainder of a divided by b
    return gcdRecursive(b, a % b);
}

int main() {
    int a, b;

    cout << "Enter two numbers: ";
    cin >> a >> b;

    // Input validation
    if (cin.fail()) {
        cout << "Invalid input. Please enter two integers." << endl;
        return 1; // Exit with an error code
    }

    // Use absolute values to handle negative numbers
    a = abs(a);
    b = abs(b);

    int result = gcdRecursive(a, b);
    cout << "GCD of " << a << " and " << b << " is: " << result << endl;

    return 0;
}
```

![Screenshot (64)](https://github.com/user-attachments/assets/2b703693-a21c-478d-96bc-e7fbb4abc50e)


**b. without recursion**
```
#include <iostream>
#include <cstdlib> // For std::abs
using namespace std;

// Recursive function to calculate GCD using the Euclidean algorithm
int gcdRecursive(int a, int b) {
    // Base case: If b is 0, the GCD is a
    if (b == 0) {
        return a;
    }
    // Recursive case: Call gcd on b and the remainder of a divided by b
    return gcdRecursive(b, a % b);
}

int main() {
    int a, b;

    cout << "Enter two numbers: ";
    cin >> a >> b;

    // Input validation
    if (cin.fail()) {
        cout << "Invalid input. Please enter two integers." << endl;
        return 1; // Exit with an error code
    }

    // Use absolute values to handle negative numbers
    a = abs(a);
    b = abs(b);

    int result = gcdRecursive(a, b);
    cout << "GCD of " << a << " and " << b << " is: " << result << endl;

    return 0;
}

```


![Screenshot (65)](https://github.com/user-attachments/assets/429f6935-2874-4241-ad61-e0d700a6c5c3)


# PRACTICAL-08
```
#include <iostream>
#include <vector>
#include <stdexcept>
#include <memory> // For smart pointers
using namespace std;

class Matrix {
private:
    int rows, cols;
    vector<vector<int>> mat;

public:
    // Constructor to initialize the matrix with given dimensions
    Matrix(int r, int c) : rows(r), cols(c) {
        mat.resize(rows, vector<int>(cols, 0)); // Initialize with zeros
    }

    // Function to input matrix elements
    void inputMatrix() {
        cout << "Enter elements of the matrix (" << rows << "x" << cols << "):\n";
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                cin >> mat[i][j];
            }
        }
    }

    // Function to display the matrix
    void displayMatrix() const {
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                cout << mat[i][j] << " ";
            }
            cout << endl;
        }
    }

    // Function to add two matrices
    Matrix add(const Matrix& m) {
        if (rows != m.rows || cols != m.cols) {
            throw invalid_argument("Matrices dimensions do not match for addition.");
        }
        Matrix result(rows, cols);
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                result.mat[i][j] = mat[i][j] + m.mat[i][j];
            }
        }
        return result;
    }

    // Function to multiply two matrices
    Matrix multiply(const Matrix& m) {
        if (cols != m.rows) {
            throw invalid_argument("Matrices dimensions are incompatible for multiplication.");
        }
        Matrix result(rows, m.cols);
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < m.cols; j++) {
                result.mat[i][j] = 0;
                for (int k = 0; k < cols; k++) {
                    result.mat[i][j] += mat[i][k] * m.mat[k][j];
                }
            }
        }
        return result;
    }

    // Function to transpose the matrix
    Matrix transpose() {
        Matrix result(cols, rows);
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                result.mat[j][i] = mat[i][j];
            }
        }
        return result;
    }
};

int main() {
    int choice;
    unique_ptr<Matrix> m1 = nullptr;
    unique_ptr<Matrix> m2 = nullptr;

    while (true) {
        cout << "\nMatrix Operations Menu:\n";
        cout << "1. Add Matrices\n";
        cout << "2. Multiply Matrices\n";
        cout << "3. Transpose Matrix\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1: {
                int r, c;
                cout << "Enter dimensions of matrix 1 (rows columns): ";
                cin >> r >> c;
                m1 = make_unique<Matrix>(r, c);
                m1->inputMatrix();

                cout << "Enter dimensions of matrix 2 (rows columns): ";
                cin >> r >> c;
                m2 = make_unique<Matrix>(r, c);
                m2->inputMatrix();
                try {
                    Matrix result = m1->add(*m2);
                    cout << "Result of addition:\n";
                    result.displayMatrix();
                } catch (const invalid_argument& e) {
                    cout << "Error: " << e.what() << endl;
                }
                break;
            }
            case 2: {
                int r1, c1, r2, c2;
                cout << "Enter dimensions of matrix 1 (rows columns): ";
                cin >> r1 >> c1;
                m1 = make_unique<Matrix>(r1, c1);
                m1->inputMatrix();
                cout << "Enter dimensions of matrix 2 (rows columns): ";
                cin >> r2 >> c2;
                m2 = make_unique<Matrix>(r2, c2);
                m2->inputMatrix();
                try {
                    Matrix result = m1->multiply(*m2);
                    cout << "Result of multiplication:\n";
                    result.displayMatrix();
                } catch (const invalid_argument& e) {
                    cout << "Error: " << e.what() << endl;
                }
                break;
            }
            case 3: {
                int r, c;
                cout << "Enter dimensions of matrix (rows columns): ";
                cin >> r >> c;
                m1 = make_unique<Matrix>(r, c);
                m1->inputMatrix();
                Matrix result = m1->transpose();
                cout << "Transpose of the matrix:\n";
                result.displayMatrix();
                break;
            }
            case 4: { // Exit
                cout << "Exiting program.\n";
                return 0;
            }
            default:
                cout << "Invalid choice, please try again.\n";
                break;
        }
    }
    return 0;
}
```


![Screenshot (67)](https://github.com/user-attachments/assets/7ffa0b1e-0a71-4f2c-9688-d228872c3769)

![Screenshot (68)](https://github.com/user-attachments/assets/bea898c8-a886-4f5f-b2f4-9388bca251b7)


# PRACTICAL-09
```
#include <iostream>
#include <string>
#include <memory> // For smart pointers
using namespace std;

class Person {
protected:
    string name;
public:
    // Constructor to initialize the name
    Person(string n) : name(n) {}

    // Virtual function to display person details
    virtual void display() {
        cout << "Name: " << name << endl;
    }

    // Virtual destructor
    virtual ~Person() {}
};

class Student : public Person {
private:
    string course;
    float marks;
    int year;
public:
    // Constructor to initialize student details
    Student(string n, string c, float m, int y) : Person(n), course(c), marks(m), year(y) {}

    // Override display function to show student details
    void display() override {
        cout << "Student Name: " << name << endl;
        cout << "Course: " << course << endl;
        cout << "Marks: " << marks << endl;
        cout << "Year: " << year << endl;
    }
};

class Employee : public Person {
private:
    string department;
    float salary;
public:
    // Constructor to initialize employee details
    Employee(string n, string d, float s) : Person(n), department(d), salary(s) {}

    // Override display function to show employee details
    void display() override {
        cout << "Employee Name: " << name << endl;
        cout << "Department: " << department << endl;
        cout << "Salary: " << salary << endl;
    }
};

// Main function
int main() {
    // Use smart pointers for automatic memory management
    unique_ptr<Person> p1 = make_unique<Student>("Alice", "Computer Science", 88.5, 2);
    unique_ptr<Person> p2 = make_unique<Employee>("Bob", "IT", 50000);

    cout << "Displaying Student details:" << endl;
    p1->display();
    cout << "\nDisplaying Employee details:" << endl;
    p2->display();

    // No need to manually delete, smart pointers handle it
    return 0;
}
```

![Screenshot (69)](https://github.com/user-attachments/assets/ae18b2cb-0439-4bca-9595-a764001b1d04)



# PRACTICAL-10
```
#include <iostream>
#include <cmath>
#include <stdexcept>
using namespace std;

class Triangle {
private:
    double side1, side2, side3;

public:
    // Constructor to initialize the triangle sides
    Triangle(double s1, double s2, double s3) : side1(s1), side2(s2), side3(s3) {
        if (s1 <= 0 || s2 <= 0 || s3 <= 0) {
            throw invalid_argument("Sides must be greater than 0.");
        }
        if (s1 + s2 <= s3 || s1 + s3 <= s2 || s2 + s3 <= s1) {
            throw invalid_argument("Sum of any two sides must be greater than the third side.");
        }
    }

    // Calculate area for right-angled triangle
    double calculateArea() const {
        if (isRightAngled()) {
            return 0.5 * side1 * side2; // Assuming side1 and side2 are the base and height
        }
        throw invalid_argument("Not a right-angled triangle.");
    }

    // Calculate area using Heron's formula
    double calculateAreaUsingHeronsFormula() const {
        double s = (side1 + side2 + side3) / 2; // Semi-perimeter
        return sqrt(s * (s - side1) * (s - side2) * (s - side3));
    }

    // Check if the triangle is right-angled
    bool isRightAngled() const {
        double a = side1, b = side2, c = side3;
        return (a * a + b * b == c * c || a * a + c * c == b * b || b * b + c * c == a * a);
    }

    // Assignment operator
    Triangle& operator=(const Triangle& other) {
        if (this != &other) {
            side1 = other.side1;
            side2 = other.side2;
            side3 = other.side3;
        }
        return *this;
    }

    // Equality operator
    bool operator==(const Triangle& other) const {
        return (side1 == other.side1 && side2 == other.side2 && side3 == other.side3);
    }

    // Display triangle sides
    void display() const {
        cout << "Sides of the triangle: " << side1 << ", " << side2 << ", " << side3 << endl;
    }
};

int main() {
    try {
        Triangle t1(3, 4, 5); // Right-angled triangle
        t1.display();
        cout << "Area of the right-angled triangle: " << t1.calculateArea() << endl;

        Triangle t2(5, 6, 7); // General triangle
        t2.display();
        cout << "Area using Heron's formula: " << t2.calculateAreaUsingHeronsFormula() << endl;

        Triangle t3(0, 0, 0); // Initializing with dummy values
        t3 = t1; 
        cout << "\nAfter assignment, t3 is:\n";
        t3.display();

        if (t1 == t3) {
            cout << "\nt1 and t3 are equal." << endl;
        } else {
            cout << "\nt1 and t3 are not equal." << endl;
        }
    }
    catch (const invalid_argument& e) {
        cout << "Error: " << e.what() << endl;
    }
    return 0;
}
```


![Screenshot (70)](https://github.com/user-attachments/assets/c377a3c4-73cb-4790-8c7e-350a9eaebce7)


# PRACTICAL-11
```

#include <iostream>
#include <fstream>
#include <string>
using namespace std;

class Student {
private:
    int rollNo;
    string name;
    string studentClass;
    int year;
    float totalMarks;

public:
    // Constructor to initialize student details
    Student(int r, string n, string c, int y, float t) 
        : rollNo(r), name(n), studentClass(c), year(y), totalMarks(t) {}

    // Default constructor for reading from file
    Student() : rollNo(0), year(0), totalMarks(0.0) {}

    // Write student details to a file
    void writeToFile(ofstream &file) {
        file << rollNo << endl;
        file << name << endl;
        file << studentClass << endl;
        file << year << endl;
        file << totalMarks << endl;
    }

    // Read student details from a file
    void readFromFile(ifstream &file) {
        file >> rollNo;
        file.ignore(); // Ignore the newline character after the integer
        getline(file, name);
        getline(file, studentClass);
        file >> year;
        file >> totalMarks;
    }

    // Display student details
    void display() const {
        cout << "Roll No: " << rollNo << endl;
        cout << "Name: " << name << endl;
        cout << "Class: " << studentClass << endl;
        cout << "Year: " << year << endl;
        cout << "Total Marks: " << totalMarks << endl;
    }
};

int main() {
    // Open file for writing
    ofstream outFile("students.txt");
    if (!outFile) {
        cerr << "File could not be opened for writing!" << endl;
        return 1;
    }

    // Create student objects
    Student students[] = {
        Student(1, "Alice", "Math", 2023, 450),
        Student(2, "Bob", "Science", 2023, 400),
        Student(3, "Charlie", "History", 2023, 480),
        Student(4, "David", "English", 2023, 470),
        Student(5, "Eve", "Computer Science", 2023, 490)
    };

    // Write student records to file
    for (Student& student : students) { // Use non-const reference
        student.writeToFile(outFile);
    }

    outFile.close();

    // Open file for reading
    ifstream inFile("students.txt");
    if (!inFile) {
        cerr << "File could not be opened for reading!" << endl;
        return 1;
    }

    cout << "\nStudent records retrieved from file:\n";

    Student tempStudent; // Use default constructor
    // Read student records from file until the end
    while (inFile.peek() != EOF) {
        tempStudent.readFromFile(inFile);
        tempStudent.display();
        cout << "-------------------------------\n";
    }

    inFile.close();
    return 0;
}
```



![Screenshot (71)](https://github.com/user-attachments/assets/f7bf36d8-09b9-4ecb-ac85-bf74fa9b0feb)



# PRACTICAL-12
```
#include <iostream>
#include <fstream>
#include <cctype>  
using namespace std;

int main() {
    string inputFile = "input.txt";  // Input file name
    string outputFile = "output.txt"; // Output file name

    // Open the input file
    ifstream inFile(inputFile);
    if (!inFile) {
        cerr << "Error: Unable to open input file!" << endl;
        return 1; // Exit with error code
    }

    // Open the output file
    ofstream outFile(outputFile);
    if (!outFile) {
        cerr << "Error: Unable to open output file!" << endl;
        return 1; // Exit with error code
    }

    char ch; // Variable to hold each character

    // Read characters from the input file
    while (inFile.get(ch)) {
        // Write the character to the output file if it's not a whitespace
        if (!isspace(ch)) {
            outFile.put(ch);
        }
    }

    // Close the file streams
    inFile.close();
    outFile.close();

    cout << "File contents copied successfully without whitespaces." << endl;
    return 0; // Exit successfully
}

```

![Screenshot (73)](https://github.com/user-attachments/assets/87cc30ee-36ed-4c2e-a46c-33dc189ca8e3)


![Screenshot (74)](https://github.com/user-attachments/assets/11a6b62b-27c1-4d3b-86aa-c4bf01901c19)

# PRACTICAL-13
```
#include <iostream>
#include <stdexcept>
#include <limits> // Include this header for numeric_limits
using namespace std;

int main() {
    double p, q;

    while (true) {
        cout << "Enter two numbers (p and q): ";
        cin >> p >> q;

        // Check if the input is valid
        if (cin.fail()) {
            cin.clear(); // Clear the error flag
            cin.ignore(numeric_limits<streamsize>::max(), '\n'); // Discard invalid input
            cout << "Invalid input. Please enter numeric values." << endl;
            continue; // Retry the input
        }

        try {
            // Check for division by zero
            if (q == 0) {
                throw runtime_error("Error: Division by zero is not allowed.");
            }

            // Perform the division
            double result = p / q;
            cout << "Result of " << p << " / " << q << " = " << result << endl;
            break; // Exit the loop after successful calculation
        }
        catch (const runtime_error& e) {
            // Handle division by zero error
            cout << e.what() << endl;
        }
    }

    return 0;
}

```



![Screenshot (75)](https://github.com/user-attachments/assets/8d3c052e-e276-41c9-9b71-b2ff7cd96d30)





























































