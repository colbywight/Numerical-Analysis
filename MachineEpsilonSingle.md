# Software Manual Entry

**Routine Name:**  smaceps

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  This routine computes the single precision machine epsilon.  This method uses a loop to determine when precision is lost in a floating point number.

**Input:** This method has no parameters.  It simply calculates the number of digits of accuracy of the systems floating point. 

**Output:** This method outputs a single number that indicates the number of decimal digits that are represented in a floating point number on the computer being used. 

**Usage/Example:** The routine was run on a macbook air and the results are as follows. This simple program uses two floats to determine when accuracy is lost. 

```C++
    cout << "Single Precision Machine Epsilon: ";
    cout << smaceps() << endl;

```

Sample Output:

```C++
      Single Precision Machine Epsilon: 5.96046e-08
```
The result is as expected, our precision is up to about 8 decimal places for a float. 

**Implementation/Code:** The code is as follows:
```C++
    float smaceps(){
    float x = 1;
    float x0 = 1;
    while (x + x0 != 1){
        x0/=2;
    }
    return x0;
    }
```
**Last Modified:** January/2018
