
# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  steepest

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  The purpose of this routine is to the appoximate solution the the linear equation Ax = b. In oreder for assured convergence to a solution we can use a symetric positive definite matrix.

**Input:** The required inputs for this routine are A, b, x0, tol and maxIter. Where we have A as a nxn (square) matrix. We will mainly use this code on not only square but large symetric positive definite matricies as this routine works well for thindin the soultion to these types of problems. b and x0 are vectors of lenght n as well. b is the solution vector and x0 will be our initial guess for our x vector. As usuall we will use tol and maxIter to break out of a loop when either out desired tolerance level is met or the maximum allowable interations has been tried.

**Output:** This routine will return the final vector apporximation of x after it end the while loop. We also have modified this code to tell us the number of iterations that were required to come to our approximation.

**Usage/Example:**

This routine was first tested simply for verifiaction purposes on a 2x2 matrix. Then a symetric positive definite matrix creator routine was implemented to test this routine on matricies of much larger size. The matrix was tested on a 1,000x1,000 matrix.

```C++
    
```

Output from the lines above:

```C++
     Run Gauss-Seidel Iteration test
     Print test solutions:
     2.008 1.99998
     Run Gauss-Seidel on n = 1000
     Complete
```

**Implementation/Code:** The code is as follows:
```C++
    vector<double> steepest(Matrix A, vector<double> b, vector<double> x0, double tol, int maxIter, vector<double> r0) {
    int n = (int)A.size();
    double delta0;
    double error = 10 * tol;
    double bDelta = dotProd(b, b);
    int cnt = 0;
    double alphaK;
    vector<double> x1(n);
    vector<double> r1(n);

    delta0 = dotProd(x0, x0);
    while (delta0 > error * error * bDelta && cnt < maxIter) {
        alphaK = dotProd(r0, r0) / l2Norm(r0);
        for ( int i = 0; i < n; i++) {
            r0[i] = r0[i] * alphaK;
        }
        for (int i = 0; i < n; i++) {
            x1[i] = x0[i] + r0[i];
        }
        for (int i = 0; i < n; i++) {
            r1[i] = b[i] + x1[i];
        }
        double diff;
        double sum = 0.0;
        for (int i = 0; i < n; i++) {
            diff = abs(x1[i] - x0[i]);
            sum = sum + diff*diff;
        }
        error = pow(sum, .5);
        for (int i = 0; i < n; i++) {
            x0[i] = x1[i];
        }
        cnt++;
        r0 = r1;
    }
}

```
**Last Modified:** November/2017
