# fabinoccifact
EB3/61539/22  MUTINDA MUSYOKI

#include <iostream>
#include <chrono>

using namespace std;
using namespace std::chrono;

long long factorial_recursive(int n) {
    return (n <= 1) ? 1 : n * factorial_recursive(n - 1);
}

long long factorial_iterative(int n) {
    long long result = 1;
    for (int i = 2; i <= n; i++) {
        result *= i;
    }
    return result;
}

long long fibonacci_recursive(int n) {
    return (n <= 1) ? n : fibonacci_recursive(n - 1) + fibonacci_recursive(n - 2);
}

long long fibonacci_iterative(int n) {
    if (n <= 1) return n;
    long long a = 0, b = 1, temp;
    for (int i = 2; i <= n; i++) {
        temp = a + b;
        a = b;
        b = temp;
    }
    return b;
}

template<typename Func, typename... Args>
long long measure_time(Func func, Args... args) {
    auto start = high_resolution_clock::now();
    func(args...);
    auto stop = high_resolution_clock::now();
    return duration_cast<nanoseconds>(stop - start).count();
}

int main() {
    int n;
    cout << "Enter a number: ";
    cin >> n;

    cout << "\nFactorial (" << n << "):" << endl;
    long long factorial_rec_time = measure_time(factorial_recursive, n);
    long long factorial_itr_time = measure_time(factorial_iterative, n);
    cout << "Recursive Result: " << factorial_recursive(n) << endl;
    cout << "Iterative Result: " << factorial_iterative(n) << endl;
    cout << "Recursive Time: " << factorial_rec_time << " ns" << endl;
    cout << "Iterative Time: " << factorial_itr_time << " ns" << endl;

    cout << "\nFibonacci (" << n << "):" << endl;
    long long fibonacci_rec_time = measure_time(fibonacci_recursive, n);
    long long fibonacci_itr_time = measure_time(fibonacci_iterative, n);
    cout << "Recursive Result: " << fibonacci_recursive(n) << endl;
    cout << "Iterative Result: " << fibonacci_iterative(n) << endl;
    cout << "Recursive Time: " << fibonacci_rec_time << " ns" << endl;
    cout << "Iterative Time: " << fibonacci_itr_time << " ns" << endl;

    return 0;
}
