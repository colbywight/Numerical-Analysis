# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**       lInfinityError(vector<int> &vector1, vector<int> &vector2)

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  This routine will compute the infinity norm error for a vector of a given size in the form of a double.

**Input:** This routine requires two vectors as inputs. The routine will determine the size and do the needed calculations on the two vectors.


**Output:** This routine will output a single double precision number denoting the vector infinity norm error.


**Implementation/Code:** The following is the code for lInfinityerror:

 double lInfinityError(vector<int> &vector1, vector<int> &vector2) {
    return abs(*max_element(vector1.begin(), vector1.end()) - *max_element(vector2.begin(), vector2.end()));
}

**Code:** This code, similar to calculating the vector norm, takes the error in the norms to determine total error.

 

**Last Modified:** October/2017
