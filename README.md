# windPower_modules

Developed from windpower related Fortran code in repository https://github.com/astroJarHead/Fortran-practise
Takes the working file wp24.f90 and added modules 
via external files. Organized as:

## code organization

```
main program -|
              |_wp25.f90_
                         |
                         |_module mod_wind_power.f90_
                                                     |
                                                     |_module mod_procedures.f90_
                                                                                 |
                                                                                 |_module mod_meteo.f90_
```

## compilation steps

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

   ...

   saveresults:  Write to disk and screen the wind power potential


  Root of sounding file is: porthardy                     

  Output filename will be: porthardy.out.txt             

 power =    868213248.00 Watts
 power =    868213.25 kWatts
 power =    868.21 MegaWatts
 CPU Time =    4.942E-03 seconds.
 **********PROGRAM Wind Power FINISHED**********
```

