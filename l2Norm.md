# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**           l2Norm

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  This routine will compute the 2 norm for a vector of a given size in the form of a double.

**Input:** The only required input is a vector. The routine will determine the size and do the needed calculations.

**Output:** This routine will output a single double precision number denoting the vector two norm.


**Usage/Example:**

This routine uses a vector for the vector class' ease of use in passing it as a paramter of a function. In this example the vecor passed to this function was a vector containing three elements 1, 2, and 3.

      cout << "l2 Norm: " << l2Norm(vector1) << endl;
      

Output from the lines above:

      l2 Norm: 3.74166

This is the desired result.

**Implementation/Code:** The following is the code for l1Norm()

    double l2Norm(vector<int> &vector1) {
    int sum = 0;
    for (int i = 0; i < vector1.size(); i++) {
        sum+= abs(pow(vector1[i], 2));
    }
    return sqrt(sum);
}

**Last Modified:** October/2017
