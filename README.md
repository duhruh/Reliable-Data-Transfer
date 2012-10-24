Reliable-Data-Transfer
======================
`Due: Nov. 6th midnight`

This code implements the Alternating Bit Protocol (rdt3.0) simulating the client and server.

![A/B](http://www.cs.ucf.edu/~czou/CNT4704/PA-2.h1.gif)

* A_output(message),
  where message is a structure of type msg, containing data to be sent to the B-side.
  This routine will be called whenever the upper layer at the sending side (node A) has a message to send. It is the job of your protocol to insure that the data in such a message is delivered in-order, and correctly, to the receiving side upper layer. You should return a value of 1 if this data packet was accepted for transmission and -1 otherwise.

* A_input(packet),
  where packet is a structure of type pkt.
  This routine will be called whenever a packet sent from the B-side (i.e., as a result of a tolayer3()being done by a B-side procedure) arrives at the A-side. packetis the (possibly corrupted) packet sent from the B-side.

* A_timerinterrupt()
  This routine will be called when A's timer expires (thus generating a timer interrupt). You'll probably want to use this routine to control the retransmission of packets. See starttimer() and stoptimer() below for how the timer is started and stopped.

* A_init()
  This routine will be called once, before any of your other A-side routines are called. It can be used to do any required initialization.

* B_input(packet),
  where packet is a structure of type pkt.
  This routine will be called whenever a packet sent from the A-side (i.e., as a result of a tolayer3()being done by a A-side procedure) arrives at the B-side. packetis the (possibly corrupted) packet sent from the A-side.

* B_init()
  This routine will be called once, before any of your other B-side routines are called. It can be used to do any required initialization.
  
Software Interfaces
-------------------
The procedures described above are the ones that you will write. The textbook authors have written the following routines which can (and should) be called by your routines:

* starttimer(calling_entity,increment),
  where calling_entity is either 0 (for starting the A-side timer) or 1 (for starting the B side timer), and increment is a float value indicating the amount of time that will pass before the timer interrupts. A's timer should only be started (or stopped) by A-side routines, and similarly for the B-side timer.
  To give you an idea of the appropriate increment value to use: a packet sent into the network takes an average of 5 time units to arrive at the other side when there are no other messages in the medium.

* stoptimer(calling_entity),
  where calling_entity is either 0 (for stopping the A-side timer) or 1 (for stopping the B side timer).

* tolayer3(calling_entity,packet),
  where calling_entity is either 0 (for the A-side send) or 1 (for the B side send), and packet is a structure of type pkt.
  Calling this routine will cause the packet to be sent into the network, destined for the other entity.

* tolayer5(calling_entity,message),
  where calling_entity is either 0 (for A-side delivery to layer 5) or 1 (for B-side delivery to layer 5), and message is a structure of type msg. 
  Calling this routine will cause data to be passed up to layer 5. With unidirectional data transfer (which is what you have to implement), you would only be calling this routine with calling_entity equal to 1 (delivery to the B-side).