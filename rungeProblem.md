# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  rungeFunct

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  To evaluate our polynomial interpolation code on Runge's Problem.

**Input:** We test various data sets using Runge's function to obtain our data set. 

**Output:** This routine will return the evaluation of the point given in the form of a double.

**Usage/Example:**  This routine will take the given two vectors as the data set. We wanted to find the value at 5, and the program output 1 which is correct. 

```C++
 
int main() {
    Vect x = { 1, 2, 4 };
    Vect y = { 1, 3, 3};
    Vect c = divDif(x, y);
    cout << "The resulting coefficients are: " << endl;
    printVect(c);
    Vect yRunge = rungeFunct(x);
    cout << polyEval(x, yRunge, 5) << endl;

    cout << polyEval( makeVect(5), rungeFunct(makeVect(5)), 6) << endl;
    cout << polyEval( makeVect(10), rungeFunct(makeVect(10)), 11) << endl;
    cout << polyEval( makeVect(50), rungeFunct(makeVect(50)), 60) << endl;
    cout << polyEval( makeVect(100), rungeFunct(makeVect(100)), 150) << endl;
    cout << polyEval( makeVect(500), rungeFunct(makeVect(500)), 50) << endl;

    return 0;
}
```

Output from the lines above:

```C++
 The resulting coefficients are: 
1 2 -0.666667 
0.0285852
4.65901
-9.15758
-5.59997e+10
-1.18363e+40
0.0532003
```

**Implementation/Code:** The code is as follows:
```C++
   Vect rungeFunct(Vect x){
    int n = x.size();
    Vect y(n);
    for (int i = 0; i < n; i++) {
        y[i] = 1 / ( 1 +25*pow(x[i], 2));
    }
    return y;
}
```
**Last Modified:** November/2017
