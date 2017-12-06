# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**       matrixSub(vector<vector<double>> matrix1, vector<vector<double>> matrix2, int row, int col)


**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  This routine will compute the subtraction of two matrices.

**Input:** This routine requires two matrices as inputs. These must be of same dimensions.


**Output:** This routine will output a matrix of the same dimensions.


**Implementation/Code:** The following is the code for matrixSub():
```C++
    vector<vector<double>> matrixSub(vector<vector<double>> matrix1, vector<vector<double>> matrix2, int row, int col) {
    vector<vector<double>> subMatrix;
    for(int i = 0; i < row; i++) {
        for(int j = 0; j < col; j++) {
            subMatrix[i][j] = matrix1[i][j] - matrix2[i][j];
        }
    }
    return subMatrix;
    }
```

  
**Code:** This code uses two loops to subtract each element of each array one at a time and then puts the sum into the output array.


**Last Modified:** October/2017
