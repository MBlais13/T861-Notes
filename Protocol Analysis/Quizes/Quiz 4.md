
Question 1

Which of the following display filters will display all email traffic?

		
smtp && pop && imap

 		
http || pop || imap

 		
smtp || pop || imap

 		
https && pop && imap



Question 2

Which of the following display filters can be used to match either the source or destination IP address to 192.168.81.112?

		
ip.addr == 192.168.81.112

 		
ip 192.168.81.112

 		
ip.src == 192.168.81.112

 		
ip.dst == 192.168.81.112



Question 3

To merge packets from within Wireshark you can use which menu option?

		
File > Merge and Save

 		
File > Merge

 		
Edit > Merge

 		
You can't merge in Wireshark



Question 4

Which of the following display filters will remove RDP traffic from the Wireshark packet list?

		
tcp.port == 3389

 		
!tcp.port == 3389

 		
!rdp

 		
http



Question 5

Which of the following is a display filter in Wireshark?

		
!(ip.src=192.168.81.112)

 		
dst host 192.168.81.112

 		
None of the above

 		
ip address 192.168.81.112 255.255.255.0




Question 6

Which of the following capture filters will display only TCP packets with the ACK flag set?

		
tcp.ack

 		
tcp[13] & 16 == 16

 		
tcp.flags.ack == 1

 		
ack



Question 7

Which operation's result is true when one of the inputs is true, but if they are both true its false.

		
NOT

 		
XOR

 		
OR

 		
AND



Question 8

Which of the following is a capture filter in Wireshark?

		
ip.host == 255.255.255.255

 		
ip address 192.168.81.112 255.255.255.0

 		
!(ip.src=192.168.81.112)

 		
dst host 192.168.81.112



Question 9

Which of the following formats does Wireshark support for exporting capture data?

		
PDF

 		
XML

 		
JSON

 		
HTML

 		
XLSX (Excel 2007+)

 		
DOCX

 		
PostScript

 		
CSV

 		
Plaintext 

 		
XLS



Question 10

The following filters will function the same.

!(ip.src == 192.168.81.112)

ip.src != 192.168.81.112

 True
 False



Question 11

One can search for a packet by hex value in Wireshark.

 True
 False



Question 12

Wireshark does not support additional columns outside of the default ones.

 True
 False



Question 13

The format for display filters in Wireshark is Berkeley Packet Filter (BPF).

 True
 False



Question 14

!ipv6

The capture filter above will show all non IPv6 traffic.

 True
 False



Question 15

port 80

The capture filter above will only show data with a destination port of 80.

 True
 False



Question 16

When using filesize for either auto stop or capture ring buffer options the maximum is 4 GiB.

 True
 False



Question 17

tshark -c Default

Will set the profile name to Default in command line.

 True
 False



Question 18

tshark -s 128

Will capture the first 128 bytes from each packet.

 True
 False



Question 19

One of the capture ring buffer options is filesize.

 True
 False



Question 20

One of the auto stop conditions for tshark is a specific date and time.

 True
 False



Question 21

Which of the following are generally true regarding packet length statistics?

		
Smaller packets are usually administrative traffic or deal with protocol control sequences

 		
When most of the packets are large you probably have a data breach in progress

 		
Larger packets are usually the transfer of data

 		
Small packets are generally wireless beacons

 		
Medium size packets are usually ARP requests

 		
Packet length means nothing as it is randomly defined by the sender



Question 22

Which of the following streams cannot be followed in Wireshark?

		
SSL

 		
HTTPS

 		
HTTP

 		
TCP

 		
UDP



Question 23

What is data segregated by when under the TCP tab of the Endpoint statistics in wireshark?

		
IP, UDP port

 		
IP, port

 		
IP, TCP port

 		
MAC, port



Question 24

What allows Wireshark to decode a protocol into various fields so the protocol can be displayed in the user interface?

		
Display filters

 		
Endpoints

 		
Protocol dissections

 		
Protocol Hierarchy



Question 25

What does a warning state in expert info mean?

		
Unusual packets that are most likely not part of normal communication

 		
An error packet or an error in the dissector interpreting it

 		
Basic information about the communication

 		
Unusual packets that may be part of normal communication



Question 26

Which of the following is required to view the contents in plaintext of an SSL stream to which you control the server?

		
Private Key

 		
Nothing Wireshark can decrypt SSL

 		
Public Key

 		
Use Editcap to decrypt SSL streams



Question 27

Which of the following Wireshark statistic windows best displays the highest talker regardless if there are multiple recipients?

		
Round Trip Time Graph

 		
Endpoint statistics

 		
Protocol Hierarchy 

 		
Conversations



Question 28

A flow graph is only useful to see data flowing in one direction.

 True
 False



Question 29

Round trip time graphs can be used to show latency with a particular conversation.

 True
 False



Question 30

Each device sending or receiving data on a network is called an endpoint.

 True
 False



Question 31

Communication between 3 or more endpoints is called a conversation.

 True
 False



Question 32

It is uncommon for companies to add a root certificate authority to the domain controller.

 True
 False



Question 33

tshark -i 3 -a duration:30 -w Iacobacci.pcap

What will the command above do?


		
Capture from interface 3, roll over to the next file after 30 seconds, and write to Iacobacci.pcap

 		
Capture from interface 3, capture for 30 seconds, and write to Iacobacci.pcap

 		
Capture from interface 1, roll over to the next file after 30 seconds, and write to Iacobacci.pcap 

 		
Read the first 30 packets from Iacobacci.pcap



Question 34

Which of the following will capture from the first device listed?

		
tshark -D 1

 		
tshark -I 1

 		
tshark -d 1

 		
tshark -i 1



Question 35

Which of the following command will display all devices available?

		
tshark -d

 		
tshark -i

 		
tshark -D

 		
tshark -I



Question 36

Which of the following command will allow you to merge all capture files that start with "Iacobacci" files together to IacobacciMerged.pcap?

		
mergecap -w IacobacciMerged.pcap Iacobacci*

 		
editcap -m -w IacobacciMerged.pcap Iacobacci*

 		
tshark -merge -w IacobacciMerged.pcap Iacobacci*

 		
tshark -m-w IacobacciMerged.pcap Iacobacci* 



Question 37

tshark -i 1 -b duration:30 -w Iacobacci.pcap

What will the command above do?


		
Read the first 30 packets from Iacobacci.pcap

 		
Capture from interface 3, roll over to the next file after 30 seconds, and write to Iacobacci.pcap

 		
Capture from interface 1, roll over to the next file after 30 seconds, and write to Iacobacci.pcap 

 		
Capture from interface 1, capture for 30 seconds, and write to Iacobacci.pcap



Question 38

Which of the following command will read Iacobacci.pcap and extract the packets 300-450 and write them to Iacobacci150.pcap?

		
tshark -w Iacobacci150.pcap -r Iacobacci.pcap -c150

 		
splitcap -w Iacobacci150.pcap Iacobacci.pcap 300-450

 		
editcap -r Iacobacci.pcap Iacobacci150.pcap 300-450

 		
tshark -w Iacobacci150.pcap -r Iacobacci.pcap -c300-450



Question 39

Which of the following tshark commands will write to output.pcap?

		
tshark -w output.pcap

 		
tshark output.pcap

 		
tshark -W output.pcap

 		
tshark --write output.pcap



