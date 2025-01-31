#cisco #book
year1
### Configure a router: step-by-step

Router > enable
Router# config term
Router(config)# hostname S1
S1(config)# banner motd # no entry #

#### Configure Password
S1(config)# enable secret cisco
S1(config)# line console 0
S1(config-line)# password 1234
S1(config-line)# login
S1(config-line)# exit

#### Configure Interface
S1(config)# interface f0/0
S1(config-if)# ip address 172.16.10.1 255.255.255.0
S1(config-if)# no shutdown
S1(config-if)# interface S0/2/0
S1(config-if)# ip address 172.16.20.1 255.255.255.0
S1(config-if)# no shutdown
S1(config-if)# exit
