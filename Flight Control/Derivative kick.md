step input causes step change of error, the derivative of the error will be a spike (very large value). If we feed this spike into controller, our output will also have this spike, definitely not ideal.

The solution to this problem :
$$
\frac{de}{dt}=\frac{d(setpoint)}{dt}-\frac{d(current)}{dt} \\ \\
\text{when setpoint is a constant, leads to :}\\
\frac{de}{dt}=-\frac{d(current)}{dt} \\
$$
