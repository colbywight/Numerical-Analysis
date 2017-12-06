# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**           lInfNorm

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  This routine will compute the Infinity norm for a vector of a given size in the form of a double.

**Input:** The only required input is a vector. The routine will determine the size and do the needed calculations.

**Output:** This routine will output a single double precision number denoting the vector infinity norm.


**Usage/Example:**

This routine uses a vector for the vector class' ease of use in passing it as a paramter of a function. In this example the vecor passed to this function was a vector containing three elements 1, 2, and 3.
```C++
      cout << "lInfinity Norm: " << l2Norm(vector1) << endl;
```      

Output from the lines above:
```C++
      lInfinity Norm: 3
```
This is the desired result.

**Implementation/Code:** The following is the code for lInfinityNorm(). Note that in order to use the max_element method, the algorithm header must be included.
```C++
    double lInfNorm(vector<int> &vector1) {
    return *max_element(vector1.begin(), vector1.end());
    } 
```    

**Last Modified:** October/2017
