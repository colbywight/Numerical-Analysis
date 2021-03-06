
# Software Manual Entry

**Routine Name:**  gausIter

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  The purpose of this routine, similar to Jacobi iteration, is to the appoximate solution the the linear equation Ax = b. This is one of the first simple iterative methods we will implement. In order for assured convergence to a solution, we can use a symetric positive definite matrix. This routine is useful in that it is easy to code.

**Input:** The required inputs for this routine are A, b, x0, tol, and maxIter. Where we have A as a nxn (square) matrix. We will mainly use this code on not only square but large symetric positive definite matricies as this routine works well for thindin the soultion to these types of problems. b and x0 are vectors of lenght n as well. b is the solution vector and x0 will be our initial guess for our x vector. As usuall we will use tol and maxIter to break out of a loop when either out desired tolerance level is met or the maximum allowable interations has been tried.

**Output:** This routine will return the final vector apporximation of x after it end the while loop. We also have modified this code to tell us the number of iterations that were required to come to our approximation.

**Usage/Example:**

This routine was first tested simply for verifiaction purposes on a 2x2 matrix. Then a symetric positive definite matrix creator routine was implemented to test this routine on matricies of much larger size. The matrix was tested on a 1,000x1,000 matrix.

```C++
    cout << "Run Gauss-Seidel Iteration test" << endl;
    vector<double> x2 = gausIter(A, b, x0, .01, 100);
    cout << "Print test solutions:" << endl;
    cout << x2[0] << " " << x2[1] << endl;

    cout << "Run Gauss-Seidel on n = 1000" << endl;
    vector<double> x12 = jacobiIter(B, b1, x01, .01, 100);
    cout << "Complete" << endl;
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
    vector<double> gausIter(Matrix A, vector<double> b, vector<double> x0, double tol, int maxIter) {
    int n = (int)A.size();
    double error = tol*10;
    int cnt = 0;
    vector<double> x1(n, 0);

    while (error > tol && cnt < maxIter) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < i; j++ ){
                x1[i] = b[i] - A[i][j] * x0[j];
            }
        }
        for (int i = 0; i < n; i++) {
            x1[i] = x1[i] / A[i][i];
        }
        double sum = 0.0;
        double diff;
        for (int i = n - 1; i >= 0; i--){
            for (int j = i; j < n; j++) {
                sum = sum + A[i][j] * x1[j];
            }
            x1[i] = sum / A[i][i];
        }
        for (int i = 0; i < n; i++) {
            diff = abs(x1[i] - x0[i]);
            sum = sum + diff*diff;
        }
        error = pow(sum, .5);
        for (int i = 0; i < n; i++) {
            x0[i] = x1[i];
        }
        cnt++;
    }
    return x0;
}
```
**Last Modified:** March/2018
