# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  polyInter

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  The purpose of this code is to compute the divided difference table and return the coefficients of the Newton form. This can also be used for evaluation of the polynomial of a vector of points ino in the data set.

**Input:** We are only given a data set. This set is requried to be in the form of a vector array. One for the x values and one for the y values at the appropriate indecies of the array.

**Output:** This routine will return 

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
        #pragma omp parallel for
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < i; j++ ){
                x1[i] = b[i] - A[i][j] * x0[j];
            }
        }
        #pragma omp parallel for
        for (int i = 0; i < n; i++) {
            x1[i] = x1[i] / A[i][i];
        }
        double sum = 0.0;
        double diff;
        #pragma parallel for
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
**Last Modified:** November/2017
