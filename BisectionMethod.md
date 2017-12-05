# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  bisect

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  A function that implements the bisection method to find a real root of a function.  The root satisfies the equations f(x) = 0. In order for this method to work the function values of the boundary inputs a and b are required.

**Input:** (double a, double b, double tol, int maxIter) where a and b are two boundary points that when evaluated at f(a) and f(b), f(a) * f(b) < 0. The variable tol is for the desired tolerance and the finally variable specifies the maximum allowed iterations. 

**Output:** The function returns a double that is an approximation of a real root between the parameters input. 

**Usage/Example:**


```C++

double eFunct(double x)
{
    return x * pow(e, -x);
}

double sinFunct(double x)
{
    return 3 * std::sin(10 * x);
}


std::cout << bisect(1, 7, .001,100);
```

Output from the lines above:

```C++
      3.14087
 ```

This is the desired result.

**Implementation/Code:**

```C++
    double bisect(double a, double b, double tol, int maxIter)
 {
     double error = 10.0 * tol;
     double fa = sinFunct(a);
     double fb = sinFunct(b);
     double fc;
     double c = 0;


     if ((fa * fb) >= 0.0)
     {
         std::cout << "error" << std::endl;
     }

     int cnt = 0;

     while(error > tol && cnt < maxIter) {

         {
             c = 0.5 * (a + b);
             fc = sinFunct(c);
         }

         if (fa * fc < 0.0) {
             b = c;
             fb = fc;
         }
         else {
             a = c;
             fa = fc;
         }
         error = b - a;
         cnt++;
     }
return c;
}
```
**Last Modified:** December/2017
