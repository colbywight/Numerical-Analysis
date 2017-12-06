# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  matVectMult

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  The purpose of this routine is to compute the resulting m by 1 vector that results from multiplying a matrix by a vector. 

**Input:** The requried input is a matrix and its dimensions, and a vecotr and its dimension. The matrix is of type vector<vector<double>>. This type is used because it is easy to pass in as parameter of a function. The dimensions of this matrix are then required to be input as integer values. The vector is simply of type vector and its length is reuired to be input as an integer as well. Note that the matrix col input and the vector length inputs must be equal or the funcion will not work.

**Output:** This routine will output the resulting vector from the multipication of type vector. This type is used because the result will always be an vecotr.


**Usage/Example:**

Here we have a 3 by 2 vector with entries of 2, and a vector with entries of 2 being multiplied together. The result is then output to console as follows.
```C++
    vector<double> result = matVectMult(matrixA, 3, 2, vectB, 2);
    cout << " Matrix Vector product: \n";
    for ( int i = 0; i < result.size(); i++) {
       cout << result[i] << " ";
    }
 ```     

Output from the lines above:
```C++
      Matrix Vector product: 
      8 8 8
```
The reulting vector is of size 3 with the correct entries.

**Implementation/Code:** Since we are doing matrix vector multiplication and not matrix matrix multiplication, we only need two for loops to complete this routine.
```C++
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
```
**Last Modified:** October/2017
