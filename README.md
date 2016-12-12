# eco-state-machine
Finite State Machine script for Godot Engine

This component is a standalone script with no dependency. It is compatible with every Godot version that supports signals and vcall.

## Conditional links
This component features a state machine that can handle states and conditional links between them. It is possible to manually set a state or to let the machine determine is there's a state change (by calling its method "process(delta)").
If a condition is given, it can be of 2 kinds : 
* condition : calls a method of a node and compare it with an expected value.
* timeout : do the transition after a certain time.
and it is possible to combine a condition and a timer:
* timed condition : do the transition only if the condition is filled AND the timer is out.
It is possible to define multiple conditions for the same link, by simply adding more links between the same states. It will then act like a logical "OR".
Timers are either the time passed since the last state change or a custom defined timer. 

## States
States are merely objects with a name and attributes. 
They must be declared before making a link between them.

## Groups
States can be regrouped in groups. Those groups can have conditional links to a state too. If a condition of a group whithin which the current state is located, the transition is made regardless the conditions of the current state.
It is possible to imbricate groups in other groups, without limit of depth.
Groups can have attributes and a custom timer, like states.
Groups must be declared before they can be used.

## Priorities
If two or more conditions are fulfilled at the same time, the link with highest priority will be used for the transition.
The priority is automatically set in the same order of creation of the links. Links for groups have however more priority that state links. The top level group has the highest priority. States have the lowest priority. But within a same group/state, the first defined link will have the highest priority and the last defined link will have the lowest priority. 

## Timers
There a 2 kinds of timers: one automatically started when there's a change of state, and custom timers. The custom timers are defined with a name. Their typical usage is for groups, where it's sometimes whished to make a condition on the time passed since the group is entered.
Custom timers can be used by states and groups by adding them in their constructor.
Timers must be declared before they can be used.