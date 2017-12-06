# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  matMatMultMP

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  Implement an OpenMP version of a matrix-matrix multiplication that runs faster than the sequential version. OpenMP offers a way to utilize the multiple processors of a computer and parallize the operations of a program. The matrix-matrix calculation is a prime example of an operation that can benifit greatly in faster computation from paralization

**Input:** This program requires the same inputs as the program to do matrix multplication without openMP, in fact most of the code is the same as well with a few key exeptions. The inputs are two matricies and their dimensions

**Output:** This progaram will return a Matrix of type vector<vector<double>> the program can also be specified to print out the clocked time from start to finish of the program for testing purposes. 


**Usage/Example:**  Here we simply enable the clock run time print option and use it to tell us when the matrix matrix multiplication is complete on the given matricies. In this example we multiplied two matrices of dimension 1500 by 1500.


```C++
     cout << "Matrix Matrix product: \n";
     vector<vector<double>> resultMat(1500, vector<double>(1500));
     resultMat = matMatMultMP(matrixA, 1500, 1500, matrixB, 1500, 1500);
     cout << "done" << endl;
```      

Output from the lines above:
```C++
      Matrix Matrix product: 
      382.703
      done
```
The number and string done are output only after the matrix matrix operations have been completed. The number is related to the clock speed of the computer and are then computed to seconds.

**Implementation/Code:** The key difference in this code is the #pragma statment that is put before the for loops. This will allow openMP to paralellize the operations required for multiplication. Note that <omp.h> must be inclued for this capablity to be accessible.
```C++
     vector<vector<double>> matMatMultMP(vector<vector<double>> matA, int rowA, int colA, vector<vector<double>> matB, int rowB, int colB) {
    double startTime = clock();
    vector<vector<double>> resultMat(rowA, vector<double>(colB));
    #pragma omp parallel for
    for (int i = 0; i < rowA; i++)
    {
        for (int j = 0; j < colB; j++) {
            resultMat[i][j] = 0;
            for (int k = 0; k < colA; k++) {
                resultMat[i][j] = resultMat[i][j] + matA[i][k] * matB[k][j];
            }
        }
        
    }
    double endTime = clock();
    double totalTime = (endTime - startTime) / CLOCKS_PER_SEC;
    cout << totalTime << endl;
    
    return resultMat;
    }
```    
**Time Testing** The following code was tested with and without using parallization. The results of multipliction of square matrices of size 500, 1000, and 1500 were tested and times recorded. The smaller matrices had less of a gap between time difference with 2.67 seconds versus 4.46 seconds being the diffence. When matricies were much larger the paralliztion had a larger effect. the 1500 by 1500 matrix multiplicaiton took 4 minuets and 27 seconds withoug paralleization and only 1 minuet and 39 seconds to complete with the computer being used. 

**Last Modified:** October/2017
