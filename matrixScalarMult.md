# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**       scalarMult(double scalar, vector<vector<double>> matrix, int row, int col)


**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  This routine will compute the scalar product of a scalar and a matrix.


**Input:** This routine requires a matrix and a scalar value as inputs.


**Output:** This routine will output a matrix of the same dimensions as the input matrix.



**Implementation/Code:** The following is the code for scalarMult():
```C++
    vector<vector<double>> scalarMult(double scalar, vector<vector<double>> matrix, int row, int col) {
    vector<vector<double>> matrixMult;
    for(int i = 0; i < row; i++) {
        for(int j = 0; j < col; j++){
            matrixMult[i][j] = scalar * matrix[i][j];
        }
    }
    return matrixMult;
    }
```


  
**Code:** This code simply multipes each elemnt of the matrix by the scalar multiple and outputs the resulting matrix.


**Last Modified:** October/2017
