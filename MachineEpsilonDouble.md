# Software Manual Entry

**Routine Name:**  dmaceps

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  This routine computes the double precision machine epsilon.  This method uses a loop to determine when precision is lost in a double precision number.

**Input:** This method has no parameters.  It simply calculates the number of digits of accuracy of the systems double type. 

**Output:** This method will output the number at which accuracy is lost.  

**Usage/Example:** The routine was run on a macbook air and the results are as follows. This simple program uses two doubles to determine when accuracy is lost. 

```C++
    cout << "Double Precision Machine Epsilon: ";
    cout << dmaceps() << endl;

```

Sample Output:

```C++
      Double Precision Machine Epsilon: 1.11022e-16
```
The result is as expected, our precision is up to about 16 decimal places for a float. 

**Implementation/Code:** The code is as follows:
```C++
    double dmaceps(){
    double x = 1;
    double x0 = 1;
    while (x + x0 != 1){
        x0/=2;
    }
    return x0;
    }
```
**Last Modified:** January/2018
