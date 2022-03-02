## Intro to pcap - 10 points

#### Description: 
*This is just the beginning so don't get too exited. Find the flag in the format cdc{"text here"} with the attached file*

#### Solution: 

We were given a wireshark file titled "test.pcappng"

There were 40 packets in the capture. Knowing that the format of the flag was "cdc".  We decided to query through the packets with "cdc" and searched through the available packet information we were given on the top left.

![[Pasted image 20220215223941.png]]

After selecting packet information, we were able to find the flag:
cdc{packets_hehe}