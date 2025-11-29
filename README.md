# windPower_modules

Developed from windpower related Fortran code in repository fortranPractise. Takes the working file wp24.f90 and added modules 
via external files. Organized as:

## code organization

main program -|
              |_wp25.f90_
                         |
                         |_module mod_wind_power.f90_
                                                     |
                                                     |_module mod_procedures.f90_
                                                                                 |
                                                                                 |_module mod_meteo.f90_


## compilation steps

gfortran -c mod_wind_power.f90
gfortran -c mod_meteo.f90
gfortran -c mod_procedures.f90
gfortran -c wp25.f90
gfortran -Wall -O2 mod_wind_power.o mod_procedures.o mod_meteo.o wp25.o -o runwp25
