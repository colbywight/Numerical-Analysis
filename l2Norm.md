# Software Manual Entry

**Routine Name:**    l2Norm

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  The purpose of this routine is to calculate the l2-norm of a given vector. The l2-norm is alson know as the Euclidean lenath of a vector. Vector norms give us a scalar quantie as the solution. These are particualry helpful when trying to understand the error in algorithms as we can get the distance between to vectors and their error in approximation.

**Input:** The only required input is a vector. The routine will determine the size and do the needed calculations.

**Output:** This routine will output a single double precision number denoting the  l2-norm of the vector.


**Usage/Example:**

This routine uses a type vector for the vector class' ease of use. In c++ vectors are easy to manipulate such as passing them as parameters of a function. In this example parmeter to this function was a vector containing three elements 1, 2, and 3.
  ```C++
      vecotr<int> vector1 = {1, 2, 3}; 
      cout << "l2 Norm: " << l2Norm(vector1) << endl;
  ```

Output from the lines above:
```C++
      l2 Norm: 3.74166
```
This is the desired result.

**Implementation/Code:** The following is the code for l1Norm(). This code will first take the sum of the squares of each entry of the vector and then return the square root of that value.
```C++
    double l2Norm(vector<int> &vector1) {
    int sum = 0;
    for (int i = 0; i < vector1.size(); i++) {
        sum+= abs(pow(vector1[i], 2));
    }
    return sqrt(sum);
}
```

**Last Modified:** October/2017
