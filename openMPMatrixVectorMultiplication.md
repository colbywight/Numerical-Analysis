# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  Implement an OpenMP version of a matrix-vector multiplication that runs faster than the sequential version. Plot the timing.

**Input:** 

**Output:** 


**Usage/Example:**



    vector<double> result = matVectMult(matrixA, 3, 2, vectB, 2);
    cout << " Matrix Vector product: \n";
    for ( int i = 0; i < result.size(); i++) {
       cout << result[i] << " ";
    }
      

Output from the lines above:

      Matrix Vector product: 
      8 8 8

The reulting vector is of size 3 with the correct entries.

**Implementation/Code:** Since we are doing matrix vector multiplication and not matrix matrix multiplication, we only need two for loops to complete this routine.

    vector<double> matVectMult(vector<vector<double>> matA, int rowA, int colA, vector<double> vectB, int colB) {
    vector<double> resultVect(rowA);
    for (int i = 0; i < rowA; i++)
    {
            resultVect[i] = 0;
            for (int j = 0; j < colA; j++)
            {
                resultVect[i] = resultVect[i] + matA[i][j] * vectB[j];
            }

    }
    return resultVect;
    }

**Last Modified:** October/2017
