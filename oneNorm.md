# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**           double oneNorm(vector< vector<double> > matrix, int rows, int cols)

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  This routine will compute the one norm for a matrix of a given size in the form of a double.


**Input:** The matrix is requred as well as two intergers type numbers that specify the row and column size of the given matrix.


**Output:** This routine will output a single double precision number denoting the matrix one norm.


**Implementation/Code:** The following is the code for oneNorm:
```C++
    double oneNorm(vector< vector<double> > matrix, int rows, int cols) {
    vector<double> colSumVect{};
    for (int i = 0; i < cols; i++) {
        int colSum = 0;
        for (int j = 0; j < rows; j++) {
            colSum += matrix[i][j];
        }
        colSumVect.push_back(colSum);
    }
    return *max_element(colSumVect.begin(), colSumVect.end());
    }
    ```
  
**Code:** This code first puts the sum of each column of the matrix into an array and then determines the largest element.
 

**Last Modified:** October/2017
