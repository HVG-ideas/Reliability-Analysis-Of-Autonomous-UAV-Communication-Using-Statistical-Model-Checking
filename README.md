To open the file please use the uppaal-4.1.20-stratego-7 tool. 
The file include the templates for all the models used in our framework. 
The declerations template contains all the global variables that can be accessed by all the templates. The following parameters is used to indicate:
1. 	`scrub_time`    -----> This variable can change the scrubbing time for the transmitter and receiever. ![image](https://user-images.githubusercontent.com/68142141/120345051-22eae800-c2c8-11eb-934f-15c088ede37a.png)

2.  `time_in_state` -----> This variable refers to the transmission delay for the data exchange template. ![image](https://user-images.githubusercontent.com/68142141/120345346-647b9300-c2c8-11eb-80c2-f188ed6af144.png)

3.  `pass_count`    -----> This variable can change the number of messages exchanged for the experiment. ![image](https://user-images.githubusercontent.com/68142141/120345424-75c49f80-c2c8-11eb-9050-41273f6c7926.png)
4.  `transmitter_gain`    -----> This variable changes the transmitter gain. ![image](https://user-images.githubusercontent.com/68142141/120347865-a4dc1080-c2ca-11eb-8e7b-e85007af6d2b.png)

5.  `rec_gain`    -----> This variable changes the receiever gain. ![image](https://user-images.githubusercontent.com/68142141/120347938-b6bdb380-c2ca-11eb-8eec-a5726a863096.png)

7.   The `x_pos, y_pos, z_pos`     variables are used to initialize the position of UAV 2 in the x,y, and z axis. Changing this variable will change the initale coordiantes of UAV 1.
8.   The `x_pos2, y_pos2, z_pos2`  variables are used to initialize the position of UAV 2 in the x,y, and z axis. Changing this variable will change the initale coordiantes of UAV 2.

![image](https://user-images.githubusercontent.com/68142141/120348162-ec629c80-c2ca-11eb-80b6-31eb8f443d65.png)

8.  The random value in the `rand_s` variable is used to change the maximum movement speed of the UAV. ![image](https://user-images.githubusercontent.com/68142141/120348518-42374480-c2cb-11eb-94e3-404a999316d5.png)
9. The `pos_prob and neg_prob` changes the failure probability (P) for the Tr and Rec templates.  
![image](https://user-images.githubusercontent.com/68142141/120350553-16b55980-c2cd-11eb-8b1a-5eae3db1149e.png)
10. `thresh_power_recieved`    -----> This variable changes the threshold for the receiever sensitivity based on the telemetry device specifications.
 
11. ![image](https://user-images.githubusercontent.com/68142141/120349609-3ef08880-c2cc-11eb-9338-3a625babe40f.png)
12. The value of the transmitted power can be changed using the `power_transmitted` variable. The maximum `power_transmitted` depends on the telemetry device specifications 

![image](https://user-images.githubusercontent.com/68142141/120350413-f7b6c780-c2cc-11eb-84f2-147358e800ec.png)
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Functions (Guards) :
1. UAV movement function: In this void function the distance moved by a UAV is calculated based on a random value defined before the experiment and is stored in the locally declared `rand_s` variable. `rand_s` is converted to an integer using the `fint` function embedded in the UPPAAL-SMC tool. The variable value is then added to the corresponding position variable based on the state in the dr1 and dr2 templates. 

![image](https://user-images.githubusercontent.com/68142141/120420685-d4266800-c332-11eb-8d05-cf1e4415a8fd.png)

2. Power Calculation function: The `int pr ()` function returns the receiever sensitivity for the given `transmitter_gain`, `rec_gain`, `power_transmitted` and calculated distance between UAV1 and UAV2 `distance_diff` in integer.
![image](https://user-images.githubusercontent.com/68142141/120421367-25832700-c334-11eb-956d-889feb4535cc.png)

4. Receiever sensistivity boolean functions : These boolean guards are used to compare the sensitivy threshold of a communication device to the calculated reciever power sensitivty. `crr` is a boolean variable used to compare whether Pr is withing reciever sensitivity threshold and is initalized to false. The if statement returns "true" if `pr()`  is less than or equal to the `thresh_power_recieved` variable. However, if the calculated `pr()` is greater than `thresh_power_recieved` the function returns false. 

![image](https://user-images.githubusercontent.com/68142141/120422366-1ac99180-c336-11eb-9e91-36e9c594db9b.png)

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Propoerties (queries) : 
The query file ""  includes the propoerty used for the paper can be checked under the verifier tab. This propoerty checks whether the replacement template will reach the Replacement_fail at any given moment within the time limit. ![image](https://user-images.githubusercontent.com/68142141/120423172-e48d1180-c337-11eb-9d93-4a5f5cc95e59.png)
Properites such as ![image](https://user-images.githubusercontent.com/68142141/120423333-36ce3280-c338-11eb-98c8-8e90bb858f38.png)
 can also be checked to ensure than the system does not have any deadlocks.
