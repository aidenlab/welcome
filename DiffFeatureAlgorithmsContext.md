# Differential Feature Finding Algorithms

There are currently 3 differential feature finding algorithms implemented within the Aiden Lab codebase:
* DiffHiCCUPS
* RECAP
* HOTSPOT

Each of these algorithms take different approaches in finding these differential features. DiffHiCCUPS and RECAP take a "top-down" approach than HOTSPOT in the sense that they both make use of loop lists as input and only evaluate Hi-C maps at the specified locations within the loop lists. Comparing across a select number of locations allows for a greater degree of granularity in these assessments and comparisons (note: these loop lists are often generated with great precision using loop-finding neural networks). On the other hand, HOTSPOT uses more of a 'bottom-up' approach in the sense that it evaluates every pixel of each Hi-C map and compares it across the other maps to determine its degree of difference. HOTSPOT ultimately filters out all locations that either don't have enough variation or don't appear to be significant features for loop comparison purposes (the main super diagonal, translocations, etc.). While missing out on these advantages of granularity and loop-finding precision, HOTSPOT, in theory, offers the advantage of being more equipped to detect differentiations of weak signals by assessing every pixel location. These types of weak signals may not be detected as loops using the loop-finding neural networks, meaning they'll therefore never be assessed in the first place by DiffHiCCUPS or RECAP. 

## Differences Between RECAP and DiffHiCCUPS

...