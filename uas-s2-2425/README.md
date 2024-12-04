# UAS S2 24-25 
Analisis menggunakan Wireshark pada file [_tcp-ethereal-trace-1_](./assets/tcp-ethereal-trace-1) di dalam [.zip](http://gaia.cs.umass.edu/wireshark-labs/wireshark-traces.zip)

## Question 1
What is the IP address and TCP port number used by your client computer (source) to transfer the file to gaia.cs.umass.edu?

![Q1 IP Source](./assets/q1-ip-source.png)
IP Address : `192.168.1.102` <br>
TCP Port : `1161`

## Question 2
What does gaia.cs.umass.edu use the IP address and port number to receive the file. (Attach the screenshot of your Wireshark's display)

![Q1 IP Source](./assets/q1-ip-source.png)
IP Address : `128.119.245.12` <br>
TCP Port : `80`

## Question 3
What is the sequence number of the TCP SYN segment that is used to initiate the TCP connection between the client computer and gaia.cs.umass.edu? What is it in the segment that identifies the segment as a SYN segment? (Attach the screenshot of your Wireshark's display)

![Q1 IP Source](./assets/q3-syn-flag.png)
Attention **red square** on the image above. <br>
1. First of all, select the **first row** packet.
2. Then expand packet TCP
3. Look at field `FLags` value
<br>
Sequence Number : `0` <br>
Flags : `SYN` (Proof the segment identifies as a SYN segment)
<br>
Video penjelasan: <br>
<video src="./assets/q3-syn.mp4" width="640" height="320" controls></video>


## Question 4
What is the sequence number of the SYNACK segment sent by gaia.cs.umass.edu to the client computer in reply to the SYN? What is the value of the ACKnowledgement field in the SYNACK segment? How did gaia.cs.umass.edu determine that value? What is it in the segment that identifies the segment as a SYNACK segment? (Attach the screenshot of your Wireshark's display)

![Q1 IP Source](./assets/q4-synack-value.png)
Attention **red square** on the image above. <br>
1. First of all, select the **second row** packet.
2. Then expand packet TCP
<br><br>
Sequence Number : `0` <br>
Acknowledgement Number : `1` <br>
Flags : `SYN`, `ACK` (Proof the segment identifies as a SYN, ACK segment) <br>
> The Acknowledgement Number (ACK) in a TCP header is the next number/byte (**Sequence Number from sender/response previously + 1**) of segment.

## Question 5
What is the sequence number of the TCP segment containing the HTTP POST command? Note that in order to find the POST command, you’ll need to dig into the packet content field at the bottom of the Wireshark window, looking for a segment with a “POST” within its DATA field.(Attach the screenshot of your Wireshark's display)

![Q1 IP Source](./assets/q5-post.png)
Attention **red square** on the image above. <br>
1. First of all, select the **4th row** packet.
2. Then expand packet TCP
<br>
<br>
Sequence Number : `1` <br>
The Client send POST command with `Flags` `PSH`, `ACK`

## Question 6
Consider the TCP segment containing the HTTP POST as the first segment in the TCP connection. What are the sequence numbers of the first six TCP connection segments (including the HTTP POST segment)? At what time was each segment sent? When was the ACK for each segment received? Given the difference between when each TCP segment was sent, and when its acknowledgement was received, what is the RTT value for each of the six segments? What is the EstimatedRTT value (see page 237 in textbook) after the receipt of each ACK? Assume that the value of the EstimatedRTT is equal to the measured RTT for the first segment, and then is computed using the EstimatedRTT equation on page 237 for all subsequent segments.

> Note: Wireshark has a nice feature that allows you to plot the RTT for each of the TCP segments sent. Select a TCP segment in the “listing of captured packets” window that is being sent from the client to the gaia.cs.umass.edu server. Then select: Statistics->TCP Stream Graph->Round Trip Time Graph.

![Q1 IP Source](./assets/q6-6th-first-segment.png)
The Sequence number first six TCP Connection (include HTTP POST) from Client to Server : <br>
1<sup>st</sup> Sequence : `1`<br>
2<sup>nd</sup> Sequence : `566`<br>
3<sup>rd</sup> Sequence : `2026`<br>
4<sup>th</sup> Sequence : `3486`<br>
5<sup>th</sup> Sequence : `4946`<br>
6<sup>th</sup> Sequence : `6406`<br>
<br>
Each segment was sent when the receiver sent `Flag` `ACK` number = next `byte`
<br>
Time each six segment sent is ACK from Server to Client:<br>
1<sup>st</sup> Time : `0,053937`<br>
2<sup>nd</sup> Time : `0,077294`<br>
3<sup>rd</sup> Time : `0,124085`<br>
4<sup>th</sup> Time : `0,169118`<br>
5<sup>th</sup> Time : `0,217299`<br>
6<sup>th</sup> Time : `0,267802`<br>
<br>
![Q1 IP Source](./assets/q6-6th-rtt.png)
RTT value: <br>
1<sup>st</sup> Time : `27,5ms`<br>
2<sup>nd</sup> Time : `35,5ms`<br>
3<sup>rd</sup> Time : `70ms`<br>
4<sup>th</sup> Time : `114,5ms`<br>
5<sup>th</sup> Time : `139,9ms`<br>
6<sup>th</sup> Time : `189,8ms`<br>

## Question 7
What is the length of each of the first six TCP segments?(Attach the screenshot of your Wireshark's display)
![Q1 IP Source](./assets/q7-len.png)
Len value: <br>
1<sup>st</sup> Len : `565`<br>
2<sup>nd</sup> Len : `1460` <br>
3<sup>rd</sup> Len : `1460` <br>
4<sup>th</sup> Len : `1460` <br>
5<sup>th</sup> Len : `1460` <br>
6<sup>th</sup> Len : `1460` <br>

