# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  divDif

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  The purpose of this code is to compute the divided difference table and return the coefficients of the Newton form. This code simply uses a matrix to store the needed componetnts of the divided difference table. To obtain the coefficients, we simply take the entries stored along a diagonal of the matrix. 

**Input:** We are only given a data set. This set is requried to be in the form of a vector array. One for the x values and one for the y values at the appropriate indecies of the array.

**Output:** This routine will return the coefficients of the polynmoial in the form of a vector. 

**Usage/Example:** This routine was first tested on a 3 point data set, then another data point was added and the program was run again. It is interesting to note that when the point was added the fourth coefficient did contain a larger error than thought.

```C++
    int main() {
    Vect x = { 1, 2, 4 };
    Vect y = { 1, 3, 3};
    Vect c = divDif(x, y);
    cout << "The resulting coefficients are: " << endl;
    printVect(c);
    cout << "After adding another data point: " << endl;
    x.push_back(5);
    y.push_back(4);
    printVect(divDif(x,y));
    return 0;
}
```

Output from the lines above:

```C++
     The resulting coefficients are: 
     1 2 -0.666667 
     After adding another data point: 
     1 2 -0.666667 0.182292 
```

**Implementation/Code:** The code is as follows:
```C++
    Vect divDif(Vect x, Vect y){
    int n = x.size();
    Vect c(n); // Coefficient vector
    Matrix divDifTable(n, Vect(n + 1));
    for (int i = 0; i < n; i++){
        divDifTable[i][0] = x[i];
        divDifTable[i][1] = y[i];
    }
    for (int j = 2; j < n+1; j++) {
        for (int k = 1; k < n; k++) {
            for (int i = k; i < n; i++) {
                divDifTable[i][j] = (divDifTable[i][j-1] - divDifTable[i-1][j-1]) / (divDifTable[i][0] - divDifTable[i-k][0]);
            }
        }
    }
    for (int i = 0; i < n; i++) {
        c[i] = divDifTable[i][i+1];
    }
    return c;
}
```
**Last Modified:** November/2017
