
# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  dotProd

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  The purpose of this routine is to compute the dot product of two vectors. 

**Input:** The requried input is two vectors. The program will determine the size of the vectors and return an error message if the vectors are not of the same size.

**Output:** This routine will output the resulting scalar quantitie from the operation.

**Usage/Example:**

Here we have two vectos of size two with enteirs 2 and their dot product.

    cout << "Dot product: \n";
    double resultDotProd = dotProd(vectB, vectB);
    cout << resultDotProd << endl;
      

Output from the lines above:

    Dot product: 
    8


**Implementation/Code:** The code is as follows:

    double dotProd(vector<double> vect1, vector<double> vect2) {
    double result = 0;
    if (vect1.size() != vect2.size())
        cout << "Please use vecotrs of same length" << endl;
    else {
        for (int i = 0; i < vect1.size(); i++) {
            result = result + vect1[i]*vect2[i];
        }
    }
    return result;
    }  

**Last Modified:** October/2017
