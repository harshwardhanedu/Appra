
@echo off
:loop
echo.
echo Please enter q to exit or press any other key to continue...
set /p input=

if /I "%input%"=="q" (
    echo Exiting...
    exit
) else (
    echo You entered %input%, let's continue.
    goto loop
)
