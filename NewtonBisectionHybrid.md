# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  hybridMeth

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  This root finding method uses two previously defined methods to help find a root if the parameters we put in are not sufficiently close. This method used the bisection method to get closer to a root so we can then use newton’s method to obtain a faster convergence. 
 

**Input:** The inputs require for this method are the function and its derivative, a guess of the approximate root.  This guess must be chosen by the user to be sufficiently close to the real root value or the output may be incorrect. The other two parameters are the standard tolerance and limit for the maximum iterations allowed.  

**Output:** The function returns a double that is an approximation of a real root of the given function.      

**Usage/Example:** 

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

    return 0;
}
```


This method takes in the parameters and puts them directly in to newton’s method for 4 iterations. If the root is not found it then used the bisection method to get closer to the roots and goes back and fourth until the root if found.  


**Implementation/Code:**

```C++
   double hybridMeth(double x0, string function, string fPrime, double tol, int maxIter) {
    // try Newtons method for 4 iterations
    int cnt = 0;
    double approximation = 0;
    double actual = 2;

    while (approximation != actual && cnt < maxIter) {

        // try Newtons method for 4 iterations
        approximation = newtsMeth(x0, function, fPrime, tol, 4);

        // if the root is not found use bisect method to get closer to root
        approximation = bisect(x0 + 10, x0 - 10, function, tol, 4);

        // use our new apporxiation and try Newton's method again
        approximation = newtsMeth(approximation, function, fPrime, tol, 4);
    }

    return approximation;
}
```
**Last Modified:** December/2017
