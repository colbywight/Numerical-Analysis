# Math 4610 Fundamentals of Computational Mathematics Software Manual Entry

**Routine Name:**  smaceps

**Author:** Colby Wight

**Language:** C++

**Description/Purpose:**  This is a method that computes the single precision machine epsilon.  This method uses a loop to determine when precision is lost in a floating point number.

**Input:** This method has no parameters.  It simply calculates the number of digits of accuracy of any floating point number.

**Output:** This method outputs a single number that indicates the number of decimal digits that are represented in a floating point number on the computer being used. 
**Usage/Example:**
Sample Output: 8; on the computer used this program returned the number 8.
   

```C++
      8
```
This simple program uses two floats to determine when accuracy is lost. The counter variable keeps track of how many times the float is accurate and up to how many bits. Each number is cast to a float to ensure that no numbers become double precision.


**Implementation/Code:** The code is as follows:
```C++
    int smaceps()
    {
    float n  = 1.0;
    float x;
    float y;
    int counter = 0;

    for (int i = 0; i < 8; i++)
    {
        n *= 2.0;
        x = static_cast<float>(1.0) - static_cast<float>(1.0) / static_cast<float>(n);

        y = static_cast<float>(1.0) - static_cast<float>(x);
        counter++;
    }
    return counter;
    }
```
**Last Modified:** December/2017
