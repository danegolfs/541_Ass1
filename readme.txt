Group: Dane Walton and Alexander Perry

For assignment 7, we have a model for the customer and the barber.

- Barber
The barber has three states: sleep, check, and cut
The barber only sleeps if none of the waiting seats are taken.
In order to go to the cut stage, it has to recieve a 'sit' sync from a customer who is in a waiting chair.
When in cut, a timer runs for 20 ticks and then sends a 'done' sync. 
The customer uses that 'done' sync to move to a different stage

-Customer
The customer has 5 stages: outsideBarb, insideBarb, waiting, takeTurn, and cut.
The process is as follows:
A customer starts at outsideBarb and waits a unique amount of time before coming back in the barbershop.
When one comes in, it checks if the 'seat' value is less than three (where 'seat' is the number of taken waiting seats)
If less than three, incremenet seat and move to the waiting room. Else go back outside.
When in the waiting room, a customer checks if the barber chair ('seated') is taken. 
If it's zero, decrement seat and go to the committed location takeTurn which immediately sends a sit! sync and takes the 'seated' mutex. It then is in the cut stage where the barber cuts their hair. When it receives a 'done?' from the barber, it goes back outside to eventually come back.