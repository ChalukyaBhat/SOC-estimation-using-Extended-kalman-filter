# SOC-estimation-using-Extended-kalman-filter


Run the main.mlx file to obtain view the results of EKF based SOC estimation \
The EKF_SOC_Estimation.mlx consists of the SOC-estimation-using-Extended-kalman-filter algorithm 

INPUT REQUIRED :
- Measured current values
- Measured Terminal voltage values
- Measured Temperature values
- R0, R1, R2, C1, C2 values for the respective battery (These values are a function of temperature and SOC)

A second order RC equivalent circuit is used to estimate state of charge and battery terminal voltage using Extended kalman filter. Extended kalman filter requires two sets of equations:
- State Equation
- Measurement equation

For SOC estimation, The state and measurement equations are as follows:

## State Equation:

![image](https://user-images.githubusercontent.com/79139644/163665213-69aaf5df-2038-48b1-bd6f-c4132f0e8912.png) \
![image](https://user-images.githubusercontent.com/79139644/163665227-f94e3df8-9720-4bfa-8122-2804660c4a65.png)

In the above expressions,
- k represents time stamp
- i(k) - current at time k
- V1(k) - voltage across R1 
- V2(k) - voltage across R2

## Measurement Equation:

![image](https://user-images.githubusercontent.com/79139644/163665523-273d7269-3276-48fa-8597-f625b4c395c5.png)

The general representation of State and measurement equations are,

![image](https://user-images.githubusercontent.com/79139644/163665603-adf9bedb-366e-433a-8d12-4cac1ed09052.png)

where,

![image](https://user-images.githubusercontent.com/79139644/163665689-7313b202-bde8-4247-b88e-0d006515c349.png) \
![image](https://user-images.githubusercontent.com/79139644/163665665-56d63ad8-76ab-400a-9c0d-70c6931b0ec9.png) \
![image](https://user-images.githubusercontent.com/79139644/163665621-063fa89c-7a7b-4c17-aa61-a415597e7c6e.png) \
![image](https://user-images.githubusercontent.com/79139644/163665633-2e57dd53-e022-4a5f-a162-77a3387c7a58.png)

## Steps to perform SOC estimation:

- To perform SOC estimation, The initial guess for SOC, V1 and V2 is provided along with measurement error covariance P, Process error covariance Q, and output covariance R.
- SOC(k+1), V1(k+1) and V2(k+1)  values are calculated from the state equations and corresponding error covariances are calcultaed using the following expression. These are the predicted values [x(k+1)] of time step (k+1). \
![image](https://user-images.githubusercontent.com/79139644/163665985-8ef84221-5a97-49a2-8d10-e1c8f511cc9b.png) 
- similarly Vt(k+1) is calculated using the measurement equations.
- Kalman gain is calculated using the following expression. \
![image](https://user-images.githubusercontent.com/79139644/163666009-76cdc097-0eed-42d2-9370-1ba84e0e23e1.png) 
- Now, the predicted values [x(k+1)] of time step is updated using the following expression, \
![image](https://user-images.githubusercontent.com/79139644/163666091-cf3f10fc-8ec5-4416-ac08-d3e0d8b83b2b.png) 
- The error covarience "P" of time step (k+1) is also updated , \
![image](https://user-images.githubusercontent.com/79139644/163666111-ac45b31c-e675-4a20-92bd-937c0383b09f.png) 
- With the updated values of time step (k+1), the values of SOC(k+2), V1(k+2) and V2(k+2) are predicted and the cycle repeats.




