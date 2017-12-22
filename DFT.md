# Math 4610 Fundamentals of Computational Mathematics Software Manual Template File

**Routine Name:**       DFT_Coefficent

**Author:** Manish Bhojasia @ http://www.sanfoundry.com/cpp-program-compute-dft-coefficients-directly/ 

**Language:** C++


**Description/Purpose:** This is a C++ Program to compute the coefficients of the DFT (Discrete Fourier Transform) directly. In mathematics, the discrete Fourier transform (DFT) converts a finite list of equally spaced samples of a function into the list of coefficients of a finite combination of complex sinusoids, ordered by their frequencies, that has those same sample values. It can be said to convert the sampled function from its original domain (often time or position along a line) to the frequency domain.

**Input:** The inputs can be changed so that the code can be used for different variatinos.

**Output:** This routine will return the coefifcients for the DFT.

**Usage/Example:**

```C++

      #include<iostream>
      #include<math.h>

      using namespace std;

      #define PI 3.14159265

      class DFT_Coefficient {
          public:
              double real, img;
              DFT_Coefficient()
              {
                  real = 0.0;
                  img = 0.0;
              }
      };
      int main(int argc, char **argv) {
          int N = 10;
          cout << "Calculation DFT Coefficients\n";
          cout << "Enter the coefficient of simple linear function:\n";
          cout << "ax + by = c\n";
          double a, b, c;
          cin >> a >> b >> c;

          double function[N];
          for (int i = 0; i < N; i++) {
              function[i] = (((a * (double) i) + (b * (double) i)) - c);
              //System.out.print( "  "+function[i] + "  ");
          }

          cout << "Enter the max K value: ";
          int k;
          cin >> k;

          double cosine[N];
          double sine[N];

          for (int i = 0; i < N; i++) {
              cosine[i] = cos((2 * i * k * PI) / N);
              sine[i] = sin((2 * i * k * PI) / N);
          }

          DFT_Coefficient dft_val;
          cout << "The coefficients are: ";

          for (int i = 0; i < N; i++) {
              dft_val.real += function[i] * cosine[i];
              dft_val.img += function[i] * sine[i];
          }
          cout << "(" << dft_val.real << ") - " << "(" << dft_val.img << " i)";

       }
```

Output from the lines above:
```C++
      Calculation DFT Coefficients
      Enter the coefficient of simple linear funtion:
      ax + by = c
      1 2 3
      Enter the max K value: 
      2
      The coefficients are: (-15) - (-20.6457 i)
```



**Implementation/Code:** The code implementation is shown in the usage and example section.

      

**Last Modified:** December/2017
