# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  hybridMethSecant

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  This root finding method uses two previously defined methods to help find a root if the parameters we put in are not sufficiently close. This method used the bisection method to get closer to a root so we can then use secant method to obtain a faster convergence. We will first use the biscection method, and then test one iteration of the secant method to test if we are close enogh to continue using the secant method. 
 

**Input:** The inputs require for this method are the function and two guesses of the approximate root.  This guess must be chosen by the user to be sufficiently close to the real root value or the output may be incorrect. The other two parameters are the standard tolerance and limit for the maximum iterations allowed. 
 

**Output:** The function returns a double that is an approximation of a real root of the given function.      

**Usage/Example:** 

```C++
double functionQuadratic(double x) {
    return pow(x, 2) - 4;
}
double functionQuadraticDeriv(double x) {
    return 2 * x;
}

Vect bisectMod(double a, double b, string funct){
    Vect vect;
    if (funct == "1"){
        double error = 10.0 * .00001;
        double fa = functionQuadratic(a);
        double fb = functionQuadratic(b);
        double fc;
        double c = 0;

        if ((fa * fb) >= 0.0) {
            std::cout << "error, no root is guratneed here, function values are same sign" << std::endl;
        }

        for (int i = 0; i < 4; i++){
            c = (a + b) / 2;
            fc = functionQuadratic(c);
            if ( fa*fc < 0){
                b = c;
                fb = fc;
            }
            else{
                a = c;
                fa =fc;
            }
        }
        vect.push_back(a);
        vect.push_back(b);
        vect.push_back(c);
    }

    return vect;
}

int main() {
    double number1 = hybridMethSecant( 0, 4, 0, 4, "1",  .001, 100);
    cout << number1;

    return 0;
}
```

**Output**
```C++
     2
 ```

**Implementation/Code:**

```C++
    double hybridMethSecant(double x0, double x1, double a, double b, string f, double tol, int maxIter) {
    double error = 10 * tol;
    double newError;
    int cnt = 0;
    double x2 = 0;
    Vect vect;

     if (f == "1") {
        double f0 = functionQuadratic(x0);
        double f1 = functionQuadratic(x1);

        // do bisect method until we know we are close enough with secant test
        while (error > newError  && cnt < maxIter) {
            //for (int i = 0; i < 4; i++){
            vect = bisectMod(a, b, "1");

            a = vect[0];
            b = vect[1];
            x0 = vect[2];
            x2 = x1 - (f1 * (x1 - x0)) / (f1 - f0);
            newError = abs(x2 - x1);
            f0 = functionQuadratic(x0);
            f1 = functionQuadratic(x1);

        }
        
        // finish using secant method 
        while ( error > tol && cnt < maxIter) {

            x2 = x1 - (f1 * (x1 - x0)) / (f1 - f0);
            error = abs(x2 - x1);
            x0 = x1;
            x1 = x2;
            f0 = functionQuadratic(x0);
            f1 = functionQuadratic(x1);
            cnt++;
        }
        return x2;
    }

}
```
**Last Modified:** December/2017
