# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  smaceps

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  This routine computes the single precision machine epsilon.  This method uses a loop to determine when precision is lost in a floating point number.

**Input:** This method has no parameters.  It simply calculates the number of digits of accuracy of the systems floating point precision. 

**Output:** This method outputs a single number that indicates the number of decimal digits that are represented in a floating point number on the computer being used. 

**Usage/Example:** The routine was run on a macbook air and the results are as follows. 
```C++
    cout << "Single Precision Machine Epsilon: ";
    cout << smaceps() << endl;

```

Sample Output:

```C++
      Single Precision Machine Epsilon: 5.96046e-08
```
This simple program uses two floats to determine when accuracy is lost. 


**Implementation/Code:** The code is as follows:
```C++
    float smacepsTwoPointO(){
    float x = 2;
    while (x != 0){
        x/=2;
    }
    return x;
    }
```
**Last Modified:** December/2017
