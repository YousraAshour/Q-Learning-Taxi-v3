# Q-Learning-Taxi-v3
The Taxi Problem from “Hierarchical Reinforcement Learning with the MAXQ Value Function Decomposition” by Tom Dietterich.
https://www.gymlibrary.ml/environments/toy_text/taxi/?highlight=taxi

# Description
There are four designated locations in the grid world indicated by R(ed), G(reen), Y(ellow), and B(lue). When the episode starts, the taxi starts off at a random square and the passenger is at a random location. The taxi drives to the passenger’s location, picks up the passenger, drives to the passenger’s destination (another one of the four specified locations), and then drops off the passenger. Once the passenger is dropped off, the episode ends.

Map:

+---------+<br/>
|R: | : :G|<br/>
| : | : : |<br/>
| : : : : |<br/>
| | : | : |<br/>
|Y| : |B: |<br/>
+---------+

# Actions
There are 6 discrete deterministic actions:

0: move south<br/>
1: move north<br/>
2: move east<br/>
3: move west<br/>
4: pickup passenger<br/>
5: drop off passenger<br/>

# Observations
There are 500 discrete states since there are 25 taxi positions, 5 possible locations of the passenger (including the case when the passenger is in the taxi), and 4 destination locations.
Note that there are 400 states that can actually be reached during an episode. The missing states correspond to situations in which the passenger is at the same location as their destination, as this typically signals the end of an episode. Four additional states can be observed right after a successful episodes, when both the passenger and the taxi are at the destination. This gives a total of 404 reachable discrete states.
Each state space is represented by the tuple: (taxi_row, taxi_col, passenger_location, destination)
An observation is an integer that encodes the corresponding state. The state tuple can then be decoded with the “decode” method.

Passenger locations:

0: R(ed)<br/>
1: G(reen)<br/>
2: Y(ellow)<br/>
3: B(lue)<br/>
4: in taxi<br/>

Destinations:

0: R(ed)<br/>
1: G(reen)<br/>
2: Y(ellow)<br/>
3: B(lue)<br/>

# Rewards:

-1 per step unless other reward is triggered.<br/>
+20 delivering passenger.<br/>
-10 executing “pickup” and “drop-off” actions illegally.<br/>
