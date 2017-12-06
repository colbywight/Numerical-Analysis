# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  dmaceps

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  This is a method that computes the double precision machine epsilon.  This method uses a loop to determine when precision is lost in a double precision number.


**Input:** This method has no parameters.  It simply calculates the number of digits of accuracy of any double precision number.

**Output:** This method outputs a single number that indicates the number of decimal digits that are represented in a double type on the computer being used. 
 
**Usage/Example:**
Sample Output: 16
   

```C++
      16
```
This simple program uses two double values to determine when accuracy is lost. The counter variable keeps track of how many times the double is accurate and up to how many bits. 



**Implementation/Code:** The code is as follows:
```C++
   int dmaceps()
   {
    double n  = 1.0;
    double x;
    double y;
    int counter = 0;

    for (int i = 0; i < 16; i++)
    {
        n *= 2.0;
        x = 1.0 - 1.0 / n;

        y = 1.0 - x;
        counter++;
    }
    return counter;
    }
```
**Last Modified:** December/2017
