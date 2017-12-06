# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  newtsMethBells

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**   This is another numerical method used to obtain a real root of a given function. This method uses the function and the function derivative to find the real root in a fast (quadratic) convergence rate.  The downside of this method is that the second derivative must be continuous near the root and our guess for the value of the root must be sufficiently close to the actual root.  This is a great method and can be used in functions of more dimensions than two. This method incorporates error checking and uses if statements to make sure parameters are not exceeded and prompts user to try adjusting the inputs.  

**Input:** The inputs require for this method are the function and its derivative, a guess of the approximate root.  This guess must be chosen by the user to be sufficiently close to the real root value or the output may be incorrect. The other two parameters are the standard tolerance and limit for the maximum iterations allowed. 

**Output:** The function returns a double that is an approximation of a real root of the given function.  If the inputs are not sufficient in finding a root approximation with the desired tolerance, instead the output is a message that informs the user of the error.    

**Usage/Example:** 

```C++
double functionQuadratic(double x) {
    return pow(x, 2) - 4;
}
double functionQuadraticDeriv(double x) {
    return 2 * x;
}

double measureConvergence(double x) {
    return x * cos(10 * x);
}
double measureConvergenceDeriv(double x) {
    return x * (-1 * sin(10 * x) ) + cos(10 * x);
}

int main() {
cout << newtsMethBells(1000, "2", "2", .01, 100) << endl; 
    return 0;
}

```

Output from the lines above:

```C++
     Maximum Iterations Exceeded, 
     try another root approximation or 
     decrease tolerane
     Iterations required: 100
     1045.63
 ```

: This function takes in a string input denoting numbers associated with desired functions to be tested.  An if statement assesses which function to be used.  In the example we have a simple quadratic function being used. This program checks each iteration if the maximum iterations are exceeded. If this is the case the message is displayed along with the number of iterations attempted. 



**Implementation/Code:**

```C++
 double newtsMethBells(double x0, string function, string fPrime, double tol, int maxIter) {

    double error = 10 * tol;
    int cnt = 0;
    double x1 = 0;

    if (function == "1") {
        double f0 = functionQuadratic(x0);
        double df0 = functionQuadraticDeriv(x0);

        while ( error > tol && cnt < maxIter) {
            x1 = x0 - f0 / df0;
            error = abs(x1 - x0);
            x0 = x1;
            f0 = functionQuadratic(x0);
            df0 = functionQuadraticDeriv(x0);
            cnt++;
            if (cnt >= maxIter) {
                cout << "Maximum Iterations Exceeded, "
                        "try another root approximation or "
                        "decrease toleracne" << endl;
            }
        }
        cout << "Iterations requierd: " << cnt << " k" << endl;
        return x0;
    }
    else if (function == "2") {
        double f0 = measureConvergence(x0);
        double df0 = measureConvergenceDeriv(x0);

        while ( error > tol && cnt < maxIter) {
            x1 = x0 - f0 / df0;
            error = abs(x1 - x0);
            x0 = x1;
            f0 = measureConvergence(x0);
            df0 = measureConvergenceDeriv(x0);
            cnt++;
        }
        cout << "Iterations requierd: " << cnt << endl;
        return x0;

    }
}
```
**Last Modified:** December/2017
