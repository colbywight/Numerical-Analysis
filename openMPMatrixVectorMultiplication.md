# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  matVectMultMP

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  Implement an OpenMP version of a matrix-vector multiplication that runs faster than the sequential version. OpenMP offers a way to utilize the multiple processors of a computer and parallize the operations of a program. The matrix-vector calculation is a prime example of an operation that can benifit greatly in faster computation time from paralization

**Input:** This program requires the same inputs as the program to do matrix-vector multplication without openMP, in fact most of the code is the same as well with a few key exeptions. The inputs are a matriix and a vector and their dimensions.

**Output:** This progaram will return a Matrix of type vector<vector<double>>.


**Usage/Example:**  In this example we multiplied a matrix of dimension 10,000 by 10,000 and a vector of dimension 10,000 by 1.

    cout << "Matrix Vector product: \n";
    vector<double> result = matVectMultMP(matrixA, 10000, 10000, vectorA, 10000);
    cout << "done" << endl;
      

Output from the lines above:

    Matrix Vector product: 
    done

here we output the first line before the multiplications begins and then the second line we print directly after the multlication has finished. This allows us to time the multiplication operation. 

**Implementation/Code:** The key difference in this code is the #pragma statment that is put before the for loops. This will allow openMP to paralellize the operations required for multiplication. Note that <omp.h> must be inclued for this capablity to be accessible.

    vector<double> matVectMultMP(vector<vector<double>> matA, int rowA, int colA, vector<double> vectB, int colB) {
    vector<double> resultVect(rowA);
    #pragma omp parallel for
    for (int i = 0; i < rowA; i++)
    {
        resultVect[i] = 0;
    #pragma omp parallel for
        for (int j = 0; j < colA; j++)
        {
            resultVect[i] = resultVect[i] + matA[i][j] * vectB[j];
        } 
    }
    return resultVect;
    }
    
**Time Testing** The following code was tested with and without using parallization. The results, contrary to what was hypothesised, indicated no real gain in time for the operation. This was not the case in matrix-matrix multiplicaiton. The error may have come from improper use of onpenMP in paralelizing the loops. The vector multipication was very fast.

**Last Modified:** October/2017
