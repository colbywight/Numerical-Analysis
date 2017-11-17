# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  cGIter

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  The purpose of this routine is to the appoximate solution the the linear equation Ax = b. This is one of the most common . In order for assured convergence to a solution we can use a symetric positive definite matrix. This version is parallelized using openMP. This uses a pragma so that the code is run on the computers mulitple threads to decrease excecution time. Note we must include the header <omp.h> for it to work. This code in particular is a great candidate to paralellize we use the routines that compute matrix multiplcation. 

**Input:** The required inputs for this routine are A, b, x0, tol and maxIter. Where we have A as a nxn (square) matrix. We will mainly use this code on not only square but large symetric positive definite matricies as this routine works well for thindin the soultion to these types of problems. b and x0 are vectors of lenght n as well. b is the solution vector and x0 will be our initial guess for our x vector. As usuall we will use tol and maxIter to break out of a loop when either out desired tolerance level is met or the maximum allowable interations has been tried.

**Output:** This routine will return the final vector apporximation of x after it end the while loop. We also have modified this code to tell us the number of iterations that were required to come to our approximation.

**Usage/Example:**

This routine was first tested simply for verifiaction purposes on a 2x2 matrix. Then a symetric positive definite matrix creator routine was implemented to test this routine on matricies of much larger size. The matrix was tested on a 1,000x1,000 matrix. The first few entries of the solution vector are give for simplicity.

```C++
    cout <<"CG solution" << endl;
    Vector cGSolution = cGIter(A, b, x0, .01, 100);
    cout << cGSolution[0] << " " << cGSolution[1] << endl;
    Vector cG1000 = cGIter(B, b1, x01, .01, 100);
    cout << cG1000[0] << " " << cG1000[1] << " " << cG1000[100] << endl << endl;
```

Output from the lines above:

```C++
     CG solution
     number of iterations to convergence: 32
     2 2
     number of iterations to convergence: 92
     1.00398 1.00499 0.996028
```

**Implementation/Code:** The code is as follows:
```C++
    Vector cGIter(Matrix A, Vector b, Vector x0, double tol, int maxIter) {
    int n = (int)A.size();
    double delta1;
    double error = 10 * tol;
    double bDelta = dotProd(b, b);
    int cnt = 0;
    double alphaK;
    Vector x1(n);
    Vector r1(n);
    Vector s0(n);
    Vector r0 = vectorSub(b, matVectMult(A, n, n, x0));
    double delta0 = dotProd(r0, r0);

    Vector p0 = r0;
    Vector p1(n);

    while (delta0 > error * error * bDelta && cnt < maxIter) {
        s0 = matVectMult(A, n, n, p0);
        alphaK = delta0 / dotProd(p0, s0);
        x1 = vectorAdd(x0, scalarVect(alphaK, p0));
        r1 = vectorSub( r0, scalarVect(alphaK, s0));
        delta1 = dotProd(r1, r1);
        p1 = vectorAdd(r1, scalarVect((delta1/delta0), p0));
        cnt++;
        x0 = x1;
        p0 = p1;
        r0 = r1;
        delta0 = delta1;

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
    cout << "number of iterations to convergence: " << cnt << endl;
    return x0;
}

```
**Last Modified:** November/2017
