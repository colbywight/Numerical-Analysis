# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**   luFactor

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  Implement the LU factorization with scaled partial pivoting insead of partial pivoting. Make sure this is effecient.

**Input:** This program requres a matrix and its demensions as its inputs. Depending on the entries of the matrix, this will give certain degree of a correct output matrix. Using scaled partial pivoting gives us the best chance at acheiving this.

**Output:** This progaram will return has the capability to return a LU structure which holds two matricies, a lower triangular and an upper triangular. 



**Implementation/Code:** The key part of this code is in its calculating the scale S sub i and then scaling the apropriate entries to help elimnate error.
```C++ 
    LU luFactor(Matrix matrix, int row, int col) {
    Matrix M(row, vector<double>(col));
    //Matrix uMatrix(row, vector<double>(col, 0));
    //Matrix lMatrix(row, vector<double>(col, 0));
    vector<double> s(row); // pivoting vecotr
    double val;

    for ( int i = 0; i < row; i++) {
        s[i] = 0;
        for (int j = 0; j < col; j++) {
            if (s[i] < matrix[i][j])
            s[i] = matrix[i][j];
        }
    }
    for (int k = 0; k < row; k++) {
        int maxRow = k;
        double maxVal = matrix[k][k] / s[k];
        for (int i = k + 1; i < row; i++) {
            val = matrix[i][k] / s[i];
            if (val > maxVal) {
                maxVal = val;
                maxRow = i;
            }
        }
        swap(matrix[maxRow], matrix[k]);
        swap(M[maxRow], M[k]);
        gaussStep(m,k);
    }
}
```

**Last Modified:** October/2017 
