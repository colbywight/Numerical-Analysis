# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  fixedIter

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  A function that implements the fixed point iteration method to to find a real root of a function.  The root satisfies the equations f(x) = 0. This method is simple to code.

**Input:** (double x0, double tol, int maxIter) In order to use this function to find a root of a desired function f(x) = 0, another function g(x) = x is required to be found. Another stipulation is that x0 must be a guess of a root that is close enough to the actual root to have fast enough convergence. 

**Output:** The function returns a double that is an approximation of a real root of the given function.  

**Usage/Example:** Here is an example of the output for a root of the function f(x) = x^2 : fixedIter(3, .1, 100); and g(x) is input as g(x) = pow(x, .5).


```C++
double eFunct(double x)
{
    return x * pow(e, -x);
}

double sinFunct(double x)
{
    return 3 * std::sin(10 * x);
}

double g(double x) // when f(x) = x^2
{
    return pow(x, .5);
}

int main()
{
    std::cout << fixedIter(3, .1, 100);

    return 0;
}
```

Output from the lines above:

```C++
      0
 ```

This is the desired result.

**Implementation/Code:**

```C++
 double fixedIter( double x0, double tol, int maxIter)

{
    int count = 0;
    double x;

    x = g(x0);

    if(fabs(x - x0) < tol)
    {
     return x;
    }
    else
    {
        count++;
    }
}
```
**Last Modified:** December/2017
