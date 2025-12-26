# DHCP-Relay-added-to-VLAN-Segmented-network.
I used an existing network I created, added a DHCP, configured the services needed on the server, assigned trunk and access ports and ensured networking connectivity using ICMP traffic.
<img width="1084" height="518" alt="image" src="https://github.com/user-attachments/assets/a8735d69-4522-418e-a6e3-2ed897d2ce66" />


This lab is a continuation/built upon my last one. I added a central DHCP server to dynamically assign IP address to my end host devices for real enterprise similarity.

To do so I first configured in the switch terminal a VLAN for the server itself assigning it a name of "management" using commands "Enable" "configure terminal" "Vlan 99" "name management". The server itself had a static IP address because I do not want services that are used often to always have changing IP addresses in case I need to troubleshoot issues related to that server. 

The first problem I ran into was the DHCP server could not ping the router after I configured it. To troubleshoot this the first step I did was go to my router and ensure it could ping itself, and then the same for the server. Both times the router and the DHCP server could ping themselves so I knew there was a disconnect somewhere between the ICMP traffic between the router and server. This led me to trying to understand what configuration mistake I made on the switch. Long story short, I accidentally configured the server on the same port as the switch which was blocking traffic from reaching the router. I had to assign the server its own access port so that internet traffic could travel to the switch and then I configured the trunking port to attach from the switch to the router. This allowed inter VLAN routing so the VLANs could communicate with each other in the network. 

After that, I was able to verify internet connectivity between the DHCP server and router by pinging each device. 

My second problem came from the DHCP server failing to assign IP addresses. I configured DHCP relay on the router using the "IP Helper-address" command and this made it possible for the other vlan devices to reach the central. It was necessary because DHCP uses broadcast and cannot send traffic/addresses across VLANs. The server failed the first time because the DHCP service was not on, but I did not know because Packet tracer makes it difficult to see the toggle for ON/OFF on the service. 


What I learned from this lab :)

I learned what DHCP relay is and why its important. 
I learned how to configure DHCP relay. 
This lab deepened my understanding of trunking ports and access ports. 
I learned to troubleshoot misconfigurations based on assigned trunking and access ports. 

* Everything I type is from documentation I jot down while doing the labs and when I dont understand something completely I use AI to describe the concept to me. I do have Network+ so not everything is new but I am also studying for CCNA to deepen my networking understanding. I hope you enjoyed this write up.

