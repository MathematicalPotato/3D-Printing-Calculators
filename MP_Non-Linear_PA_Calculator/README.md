# Non-Linear PA Calculator
This is a calculator that can be used to approximate non-linear pressure advance parameters based on known PA values at different speeds/flowrates.  Non-Linear PA is a part of [dmbutyugin's advanced-features](https://github.com/DangerKlippers/danger-klipper/pull/69).  It autoadjusts pressure advance parameters to compensate for necessary changes in in the effective pressure advance at different speeds/flowrates;.

It is recommended to have the [Solver Add-In](https://support.microsoft.com/en-us/office/load-the-solver-add-in-in-excel-612926fc-d53b-46b4-872c-e24772f078ca) installed for this calculator.  You can manually adjust the parameters to get them to line up, but running Solver first typically gets pretty good values.

## Instructions

### Blue "Fixed/Calculations" Cells
These cells take up the majority of the sheet and should not need to be modified.  They are used for fixed values or for calculations.

### Yellow "Input" Cells
![MP-Non-Linear-PA-Pic001](MP_Non-Linear_PA_Calculator//yellow-inputs.png)

Filament diameter, line width, and layer height need to be added to approximate the flowrate and pa_velocity values used for calculations.

Pressure Advance values will need to be measured and input for a few different speeds/flowrates across the range intended for printing.  These values can be captured with standard Pressure Advance by running a PA tuning tool or by manually adjusting PA by eye during normal printing until you are satisfied.  Both will need to be done at specific print speeds.  It is recommended to input as many as values as possible, but decent data should be possible with 5-6 measured values as long as values are captured throughout the full speed range intended for printing.


### Green "Output/Variable" Cells
![MP-Non-Linear-PA-Pic002](MP_Non-Linear_PA_Calculator/Images/green-outputs.png)

These are the non-linear PA parameters.  There are two sets, one for the TANH model and one for the RECIP model.  Either model can be used, but RECIP drops off faster in the lower speed/flowrate range which is generally less ideal for printing.  From testing it seems like most have have better success with the TANH model.

These cells will be the variable cells that can be manipulated either automatically with the Solver Add-in or manually.  Manually adjusting the values can be useful to help visualize how the different parameters impact the effective PA curves of the non-linear models.

Solver will take whatever is in these cells prior to running as starting points and then approximate the non-linear PA parameters into the same cells.  It is recommended to be fairly close (order of magnitude), otherwise Solver may have issues convergeing.  Ideally the nonlinear plots (pink and blue lines) will line up with/overlap the measured PA values (green points) on the plot.  Non-linear PA parameters can be manually modified to get closer to overlapping if Solver does not converge to satisfactory values.  There are recommended starting values for the parameters with smooth_time: 0.015.  For other setups you may need to raise the starting values.
![MP-Non-Linear-PA-Pic003](MP_Non-Linear_PA_Calculator/Images/range.png)

To run Solver go to the "Data" tab in Excel and it will be on the right side of the toolbar in the "Analysis" Section:
![MP-Non-Linear-PA-Pic003](MP_Non-Linear_PA_Calculator/Images/solver-location.png)

Once Solver is open just click "Solve" and it will run:
![MP-Non-Linear-PA-Pic003](MP_Non-Linear_PA_Calculator/Images/solver-location.png)

### Warning
This model is just an approximation and given that PA won't have much of a measurable difference beyond the thousandths place with two significant figures (0.0XX) this model will get close, but likely will not be "perfect" compared to and the measured values.  This also means that Solver will likely give this error when it converges:
![MP-Non-Linear-PA-Pic003](MP_Non-Linear_PA_Calculator/Images/solver-error.png)

If this happens (in testing this error occurs almost every time) click "OK" to save the values or "Cancel" to revert them to the starting values.  During testing if the residual cells were calculated to be small enough to avoid the error the models would converge with the parameters not changing at all.  If the non-linear model plots overlap the measured points, it is recommended to just click "OK" and use the values as these parameters are likely as close as possible. 

### Example of a good plot
![MP-Non-Linear-PA-Pic003](MP_Non-Linear_PA_Calculator/Images/plot1.png)

## Updates

### 2024-01-18

Initial upload of the Non-Linear PA Calculator.
