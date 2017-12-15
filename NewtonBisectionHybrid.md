# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  hybridMeth

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  This root finding method uses two previously defined methods to help find a root if the parameters we put in are not sufficiently close. This method used the bisection method to get closer to a root so we can then use newton’s method to obtain a faster convergence. We will do four iterations of the biscetion method and one try at newtonds method until we are sufficiently close. We will then use newtons method to quickly approximate the root.
 

**Input:** The inputs require for this method are the function and its derivative, a guess of the approximate root. We will also need guesses for a and b to use the bisection method.  This guess must be chosen by the user to be sufficiently close to the real root value or the output may be incorrect. The other two parameters are the standard tolerance and limit for the maximum iterations allowed.  

**Output:** The function returns a double that is an approximation of a real root of the given function.      

**Usage/Example:**  For this example we succeful found a root of a quadratic function. Our modified bisection method is alsoe provided.

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
    double number = hybridMeth( .5, 0, 4, "1", "1", .001, 100);
    cout << number;


    return 0;
}
```

**Ouput**
```C++
     2
 ```


**Implementation/Code:**

```C++
   double hybridMeth(double x0, double a, double b, string function, string fPrime, double tol, int maxIter){
    if (function == "1") {
        double error = 10 * tol;
        double newError;
        double f0 = functionQuadratic(x0);
        double df0 = functionQuadraticDeriv(x0);
        Vect vect = bisectMod(a, b, "1");
        int cnt = 0;
        double x1 = 0;

        // do four iterations of bisect and then one of newtons method
        // to see if the error becomes smaller.
        while (error > newError  && cnt < maxIter) {
            //for (int i = 0; i < 4; i++){
            vect = bisectMod(a, b, "1");

            a = vect[0];
            b = vect[1];
            x0 = vect[2];
            f0 = functionQuadratic(x0);
            df0 = functionQuadraticDeriv(x0);
            x1 = x0 - f0 / df0;
            newError = abs(x1 - x0);
        }
        // if newtons method is converging continue using newtons method

        while ( error > tol && cnt < maxIter) {
            x1 = x0 - f0 / df0;
            x0 = x1;
            f0 = functionQuadratic(x0);
            df0 = functionQuadraticDeriv(x0);
            cnt++;
        }
        return x0;
    }

}

}
```
**Last Modified:** December/2017
