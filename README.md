# windPower_modules

Developed from windpower related Fortran code in repository https://github.com/astroJarHead/Fortran-practise.
Takes the working file wp24.f90 which is now version wp25.f90 and added modules 
via external files. Organized as:

## code organization

```
main program -
|__wp25.f90 # main program
|
modules -
|__mod_wind_power.f90  # module with shared variables, constants
|
|__mod_procedures.f90  # contains five (5) subroutines called by main program
|
|__mod_meteo.f90       # contains two (2) functions called by subroutines in module procedures

```

## compilation steps

A Makefile is included in this repository. Use the file Makefile as the other Makefiles are archived 
versions of developmental versions that led to Makefile. For individual steps at the command line 
without using a Makefile see the following step by step instructions using gfortran.

```
gfortran -c mod_wind_power.f90

gfortran -c mod_meteo.f90

gfortran -c mod_procedures.f90

gfortran -c wp25.f90

gfortran -Wall -O2 mod_wind_power.o mod_procedures.o mod_meteo.o wp25.o -o runwp25
```
Compiled with gcc version 15.2.0. OS is Ubuntu Linux (UbuntuMate) on an IBM ThinkPad corei7. 

## Example to test

At the command line:

```
.runwp25

Welcome to Wind Power

 getturbinespecs: Get specifications of the wind turbine.
   Enter hub height (m) AGL: 270

     Enter turbine radius (m): 180
 **********Hub and radius parameters**********
 hub height (m) AGL =  270.00
 and radius (m) =  180.00

 getsounding:  Get the file holding the input sounding
   Enter the name of the sounding file: porthardy.txt

   ... more output and then ...

   saveresults:  Write to disk and screen the wind power potential


  Root of sounding file is: porthardy                     

  Output filename will be: porthardy.out.txt             

 power =    868213248.00 Watts
 power =    868213.25 kWatts
 power =    868.21 MegaWatts
 CPU Time =    4.942E-03 seconds.
 **********PROGRAM Wind Power FINISHED**********
```

## A test case

Vestas, https://www.vestas.com/en , a sustainable energy company, has turbines in service that provide a helpful example to test the code against a real world case. Their EnVentus V172-7.2 turbine with a hub height of 166 m and a rotor diameter of 172 m with an average wind speed of 6 m/sec would generate about 1.9 MegaWatts per day. The Darwin weather data averaged over the heights samped by this turbine has an average wind speed of 4.9 m/sec, and with 50 rectangles the code predicts a power output 1.78 MegaWatts. The code using pi*r^2 over-estimates the turbine blade area, and thus I think EnVentus accounts for the part of the hub that does not sample the wind. 

### Conclusion

The algorithm and my implementation of the code provides a reasonable estimate of wind turbine power output against one real world example. 
