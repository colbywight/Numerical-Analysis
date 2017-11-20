# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  inveresPowerMethod

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  The purpose of this routine is to the appoximate solution the the eigenvalue problem Av = (lambda)v. This method will calculate the least dominant eigenvalue and eigenvector of a matrix. We will assume that the matrix has a full set of eigenvalues for this routine. This is very similar to the power method except that we will use A inverse int the routine.  This routine is optimized to run on multiple thread using OMP. We will parallelized the matrix multiplicaiton operations. 

**Input:** The required inputs for this routine are A, v0, tol and maxIter. Where we have A as a nxn (square) matrix. v0 is the vector guess. As usuall we will use tol and maxIter to break out of a loop when either out desired tolerance level is met or the maximum allowable interations has been tried.

**Output:** This routine will return a struct which holds both the eigenvalue and the eigenvector.  These are both associated with the greateds eigen value.  

**Usage/Example:**

This routine was first tested simply for verifiaction purposes on a 3x3 matrix. The matrix was tested on a 1,000x1,000 matrix.

```C++
     Matrix a( (3), vector<double>(3));
    a[0][0]=-2;
    a[0][1]=-4;
    a[0][2]=2;
    a[1][0]=-2;
    a[1][1]=1;
    a[1][2]=2;
    a[2][0]=4;
    a[2][1]=2;
    a[2][2]=5;
    Vect v = {1, 2, 3};
    lambdaVector result = powerMethod(a, v, .01, 100);

    cout << result.Lambda;
```

Output from the lines above:

```C++
     9.6097
```

**Implementation/Code:** The code is as follows:
```C++
lambdaVector powerMethod(Matrix A, Vect v0, double tol, int maxIter){
    lambdaVector result;
    int n = v0.size();
    Vect y(n);
    Vect x(n);
    Vect s(n);
    double lambdaNew;
    y = matVectMult(A, n, n, v0);
    double lambdaOld = 0.0;
    double error = tol * 10;
    int cnt = 0;
    double yNorm;
    while (error > tol && cnt < maxIter) {
        lambdaNew = 0;
        yNorm = l2Norm(y);
        x = scalarVect(1/yNorm, y);
        s = matVectMult(A, n, n, x);
        for (int i = 0; i < n; i++) {
            lambdaNew += x[i] + s[i];
        }
        error = abs(lambdaOld - lambdaNew);
        cnt++;
        y = s;
        lambdaOld = lambdaNew;
    }
    result.Lambda = lambdaNew;
    result.x = x;
    return result;

}
Vect matVectMult(Matrix matA, int rowA, int colA, Vect vectB) {

    Vect resultVect(rowA);
    # pragma omp parallel for
    for (int i = 0; i < rowA; i++) {
        resultVect[i] = 0;
        for (int j = 0; j < colA; j++) {
            resultVect[i] = resultVect[i] + matA[i][j] * vectB[j];
        }
    }
    return resultVect;
}

double l2Norm(Vect vector1) {
    int sum = 0;
    for (int i = 0; i < vector1.size(); i++) {
        sum+= abs(pow(vector1[i], 2))
        }
    return sqrt(sum);
}

Vect scalarVect(double a, Vect b) {
    for (int i = 0; i < b.size(); i++){
        b[i] = a * b[i];
    }
    return b;
}
```
**Last Modified:** October/2017
