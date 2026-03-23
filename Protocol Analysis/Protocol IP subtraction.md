
128 64 32 16 8 4 2 1

10.52.18.0 /23
10.52.17.0 /24
10.52.20.0 /22

00010010
00010001
00010100

00010 common
5 numbers are same
8.8.5.0 add them all
=21
10.52.16.0/21
The reason it's 16 is because of the common value: `00010` 
128 64 32 **16**



**Find to remove**

10.52.18.0 /23
10.52.17.0 /24
10.52.20.0 /22

Find ranges of networks
18.1 - 19.255
17.1 - 17.255
20.1 - 23.255


`ip.address == 10.52.16.0/21 && !(ip.addr == 10.52.16.0/24)`

