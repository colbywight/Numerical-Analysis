# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**       l2Error(vector<int> &vector1, vector<int> &vector2)


**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  This routine will compute the two norm error for a vector of a given size in the form of a double.

**Input:** This routine requires two vectors as inputs. The routine will determine the size and do the needed calculations on the two vectors.


**Output:** This routine will output a single double precision number denoting the vector two norm error.


**Implementation/Code:** The following is the code for l2error:

 double l2Error(vector<int> &vector1, vector<int> &vector2) {
    int sum = 0;
    for (int i = 0; i < vector1.size(); i++) {
        sum+= abs(pow(vector1[i], 2)-pow(vector2[i],2));
    }
    return sqrt(sum);
}
  
**Code:** This code, similar to calculating the vector norm, takes the error in the norms to determine total error.

 

**Last Modified:** October/2017
