# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  newtsMeth

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  This is another numerical method used to obtain a real root of a given function. This method uses the function and the function derivative to find the real root in a fast (quadratic) convergence rate.  The downside of this method is that the second derivative must be continuous near the root and our guess for the value of the root must be sufficiently close to the actual root.  This is a great method and can be used in functions of more dimensions than two. 

**Input:** The inputs required for this method are the function and its derivative, a guess of the approximate root.  This guess must be chosen by the user to be sufficiently close to the real root value or the output may be incorrect. The other two parameters are the standard tolerance and limit for the maximum iterations allowed. 

**Output:** The function returns a double that is an approximation of a real root of the given function.    

**Usage/Example:** When newtsMeth(1, "1", "1", .1, 100) is run the program in very few iterations come up with an excellent approximation for the quadratic function x^2 – 4. The output is: 2.0006. which is within the desired tolerance of the actual value of the root which is 2.

```C++
double functionQuadratic(double x) {
    return pow(x, 2) - 4;
}
double functionQuadraticDeriv(double x) {
    return 2 * x;
}

double eFunct(double x)
{
    return x * pow(e, -x);
}
double eFunctDeriv(double x) {
    return -x * pow(e,-x) + pow(e, -x);
}

double measureConvergence(double x) {
    return x * cos(10 * x);
}
double measureConvergenceDeriv(double x) {
    return x * (-1 * sin(10 * x) ) + cos(10 * x);
}

int main() {
    cout << newtsMeth(.5, "3", "3", .01, 100) << endl;
 
    return 0;
}

```

Output from the lines above:

```C++
      2.0006
 ```

This function takes in a string input denoting numbers associated with desired functions to be tested.  An if statement assesses which function to be used.  In the example we have a simple quadratic function being used. This is a very basic program and runs very well if the user is knowledgeable about what they are looking for.  The inputs must be sufficient or the output will be undesired. 


**Implementation/Code:**

```C++
 double newtsMeth(double x0, string function, string fPrime, double tol, int maxIter) {

    if (function == "1") {
        double error = 10 * tol;
        double f0 = functionQuadratic(x0);
        double df0 = functionQuadraticDeriv(x0);
        int cnt = 0;
        double x1 = 0;

        while ( error > tol && cnt < maxIter) {
            x1 = x0 - f0 / df0;
            error = abs(x1 - x0);
            x0 = x1;
            f0 = functionQuadratic(x0);
            df0 = functionQuadraticDeriv(x0);
            cnt++;
        }
        cout << "Newtons Method Iterations: " << cnt << endl;
        return x0;
    }
    else if (function == "2") {
        double error = 10 * tol;
        double f0 = eFunct(x0);
        double df0 = eFunctDeriv(x0);
        int cnt = 0;
        double x1 = 0;

        while ( error > tol && cnt < maxIter) {
            x1 = x0 - f0 / df0;
            error = abs(x1 - x0);
            x0 = x1;
            f0 = eFunct(x0);
            df0 = eFunctDeriv(x0);
            cnt++;
        }
        cout << "Newtons Method Iterations: " << cnt << endl;
        return x0;
    }
    if (function == "3") {
        double error = 10 * tol;
        double f0 = measureConvergence(x0);
        double df0 = measureConvergenceDeriv(x0);
        int cnt = 0;
        double x1 = 0;

        while ( error > tol && cnt < maxIter) {
            x1 = x0 - f0 / df0;
            error = abs(x1 - x0);
            x0 = x1;
            f0 = measureConvergence(x0);
            df0 = measureConvergenceDeriv(x0);
            cnt++;
        }
       cout << "Newtons Method Iterations: " << cnt << endl;
        return x0;
    }
}
```
**Last Modified:** December/2017
