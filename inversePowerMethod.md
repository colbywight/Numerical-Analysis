# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  inveresPowerMethod

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  The purpose of this routine is to the appoximate solution the the eigenvalue problem Av = (lambda)v. This method will calculate the least dominant eigenvalue and eigenvector of a matrix. We will assume that the matrix has a full set of eigenvalues for this routine. This is very similar to the power method except that we will use A inverse in the routine.

**Input:** The required inputs for this routine are A, v0, tol and maxIter. Where we have A as a nxn (square) matrix. v0 is the vector guess. As usuall we will use tol and maxIter to break out of a loop when either out desired tolerance level is met or the maximum allowable interations has been tried.

**Output:** This routine will return a struct which holds both the eigenvalue and the eigenvector.  These are both associated with the greateds eigen value.  

**Usage/Example:** 


```C++
int main() {

    Matrix A(32, Vect (32));
    Vect v0(32);


    for (int i = 0; i < 32; i++) {
        A[i][i] = i+1;
        v0[i] = 1;
    }
    Matrix B = A;
    B[30][30] = 30.0;


    inversePowerMethod(B, v0, .001, 100); cout << endl;
    inversePowerMethod(A, v0, .001, 100); cout << endl;

    return 0;
}
```

Output from the lines above:

```C++
      0.999877
      0.999877
```

**Implementation/Code:** The code is as follows: (the Conjugate Gradient routine was also used refer to the software manual section on Iterative methods for this code, it was excluded dp to its size.
```C++
lambdaVector inversePowerMethod(Matrix A, Vect v0, double tol, int maxIter){
    lambdaVector result;
    int n = v0.size();
    Vect y(n);
    Vect x(n);
    Vect s(n);
    double lambdaNew;
    y = cGIter(A, v0, v0, tol, maxIter);
    double lambdaOld = 0.0;
    double error = tol * 10;
    int cnt = 0;
    double yNorm;
    lambdaNew = 0;
    while (error > tol && cnt < maxIter) {

        yNorm = l2Norm(y);
        for (int i = 0; i < n; i++){
            x[i] = y[i] / yNorm;
        }

        y = cGIter(A, x, x, tol, maxIter);
        lambdaNew = dotProd(x, y);
        error = abs(lambdaOld - lambdaNew);
        cnt++;

        lambdaOld = lambdaNew;
    }
    cout << 1/lambdaNew;
    result.Lambda = 1/lambdaNew;
    result.x = x;
    return result;

}
Vect matVectMult(Matrix matA, int rowA, int colA, Vect vectB) {

    Vect resultVect(rowA);
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
