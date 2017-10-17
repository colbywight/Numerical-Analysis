
# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  matMatMult

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  The purpose of this routine is to compute the resulting m by n vector that results from multiplying a matrix by a matrix. 

**Input:** The requried input is two matricies and their dimensions. The matricies are of type vector<vector<double>>. This type is used because it is easy to pass in as parameter of a function. The dimensions of the matricies are then required to be input as integer values. Note that the matrixA colA input and matrixB rowB inputs must be equal or the funcion will not work.

**Output:** This routine will output the resulting matrix from the multipication.

**Usage/Example:**

Here we have a 3 by 2 vector with entries of 2, and a 2 by 3 matrix with entries of 2 being multiplied together. The result is then output to console as follows.

    cout << "Matrix Matrix product: \n";
    vector<vector<double>> resultMat(3, vector<double>(3));
    resultMat = matMatMult(matrixA, 3, 2, matrixB, 2, 3);
    printMatrix(resultMat, 3, 3);
      

Output from the lines above:

      Matrix Matrix product: 
      8 8 8 
      8 8 8 
      8 8 8

The reulting vector is of size 3 by 3 with the correct entries.

**Implementation/Code:** 
     vector<vector<double>> matMatMult(vector<vector<double>> matA, int rowA, int colA, vector<vector<double>> matB, int rowB,      int colB) {
     vector<vector<double>> resultMat(rowA, vector<double>(colB));
     for (int i = 0; i < rowA; i++)
     {
        for (int j = 0; j < colB; j++) {
            resultMat[i][j] = 0;
            for (int k = 0; k < colA; k++) {
                resultMat[i][j] = resultMat[i][j] + matA[i][k] * matB[k][j];
            }
        }
     }
     return resultMat;
     }

**Last Modified:** October/2017
