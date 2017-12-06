# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  secantMeth

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  This is another numerical method used to obtain a real root of a given function. This method uses the function to find the real root in a fast (quadratic) convergence rate. This method is similar to Newton’s Method in that aspect.  One key difference is that in the secant method the derivative is not require.  However, the user must specify two points rather than one for this method to work.  This is a great method and can be used in functions of more dimensions than two. 
 

**Input:** The inputs require for this method are the function and, two guesses relatively close to the approximate root. The other two parameters are the standard tolerance and limit for the maximum iterations allowed.  

**Output:** The function returns a double that is an approximation of a real root of the given function.    

**Usage/Example:** When secantMeth(55, 56, "1", .001, 1000) is run the program in very few iterations come up with an excellent approximation for the quadratic function x^2 – 4. The output is: 2. which is within the desired tolerance of the actual value of the root which is 2. The two guess were experimented with and any positive integer less than 100 was sufficient in obtaining this result.

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

    cout << secantMeth(0, 2, "3", .01, 100) << endl;
    return 0;
}
```

Output from the lines above:

```C++
      2
 ```

This function takes in a string input denoting number associated with desired function to be tested.  An if statement assesses which function to be used.  In the example we have a simple quadratic function being used. The inputs must be sufficient or the output will be undesired.  


**Implementation/Code:**

```C++
 double secantMeth(double x0, double x1, string f, double tol, int maxIter) {
    double error = 10 * tol;
    int cnt = 0;
    double x2 = 0;

    if (f == "1") {
        double fx0 = functionQuadratic(x0);
        double fx1 = functionQuadratic(x1);

        while ( error > tol && cnt < maxIter) {

            x2 = x1 - (fx1 * (x1 - x0)) / (fx1 - fx0);
            error = abs(x2 - x1);
            x0 = x1;
            x1 = x2;
            fx0 = functionQuadratic(x0);
            fx1 = functionQuadratic(x1);
            cnt++;
        }
        return x2;
    }
    else if (f == "3") {
        double fx0 = measureConvergence(x0);
        double fx1 = measureConvergence(x1);

        while ( error > tol && cnt < maxIter) {

            x2 = x1 - (fx1 * (x1 - x0)) / (fx1 - fx0);
            error = abs(x2 - x1);
            x0 = x1;
            x1 = x2;
            fx0 = measureConvergence(x0);
            fx1 = measureConvergence(x1);
            cnt++;
        }
        cout << "Secant Method Iterations: " << cnt << endl;

        return x2;
    }
```
**Last Modified:** December/2017
