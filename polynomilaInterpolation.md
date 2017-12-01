# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  polyEval

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  The purpose of this code is to use the computed divided difference table to evaluate a polynomial at a vector of points not in the data set. 

**Input:** We are given a data set, and the point we want to evaluate at. This set is requried to be in the form of a vector array. One for the x values and one for the y values at the appropriate indecies of the array.

**Output:** This routine will return the evaluation of the point given in the form of a double.

**Usage/Example:**  This routine will take the given two vectors as the data set. We wanted to find the value at 5, and the program output 1 which is correct. 

```C++
   int main() {
    Vect x = { 1, 2, 4 };
    Vect y = { 1, 3, 3};
    Vect c = divDif(x, y);
    cout << "The resulting coefficients are: " << endl;
    printVect(c);
    cout << "The evaluation at the given value is:  " << endl;
    cout << polyEval(x, y, 5) << endl;
    return 0;
}
```

Output from the lines above:

```C++
   The resulting coefficients are: 
   1 2 -0.666667 
   The evaluation at the given value is:  
   1
```

**Implementation/Code:** The code is as follows:
```C++
    double polyEval(Vect x, Vect y, double x0) {
    Vect c= divDif(x, y);
    double sum = 0;
    int n = x.size();
    for (int i = 0; i < n; i++) {
        double temp = c[i];
        for ( int j = 0; j < i; j++) {
            temp *= x0 - x[j];
        }
        sum += temp;
    }
    return sum;
}
```
**Last Modified:** November/2017
