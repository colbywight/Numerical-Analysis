# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**      double infinityNorm(vector< vector<double> > matrix, int rows, int cols)

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  This routine will compute the infinity norm for a matrix of a given size in the form of a double.


**Input:** The matrix is requred as well as two intergers type numbers that specify the row and column size of the given matrix.


**Output:** This routine will output a single double precision number denoting the matrix infinity norm.


**Implementation/Code:** The following is the code for infinityNorm:
   
     double infityNorm(vector< vector<double> > matrix, int rows, int cols){
     vector<double> rowSumVect{};
     for (int i = 0; i < rows; i++) {
        int rowSum = 0;
        for (int j = 0; j < cols; j++) {
            rowSum += matrix[i][j];
        }
        rowSumVect.push_back(rowSum);
     }
     return *max_element(rowSumVect.begin(), rowSumVect.end());
     }
     
**Code:** This code first puts the sum of each row of the matrix into an array and then determines the largest element.
 

**Last Modified:** October/2017
