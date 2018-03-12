RapportCC - Group A
# VirtualBox Networks
VirtualBox allows different virtual network options for its VMs, each with its own authorizations and limitations. Depending on the selected network some of the communications between the network elements will be allowed or not.
There are four main networks:
1. NAT
2. Bridge
3. Internal network
4. Host-only  

It is also possible to isolate the guest by choosing not to connect it.

# NAT (Network  Address Translation)
This configuration is the default one. It is like creating a private network : the VMs are given a private IP Address which make outsiders unable to access them directly. However, the contrary is possible : the VM sends a packet to a server (as an example). The VirtualBox network Engine will transform the source IP Address and port (replaces by the host's Addresses). When a packet comes, it goes to VirtualBox and it's engine manage to replace the adresses correctly and follows the message to the VM.

  ## Principle:
This configuration is the default one. It is like creating a private network : the VMs are given a private IP Address which make outsiders unable to access them directly. However, the contrary is possible : the VM sends a packet to a server (as an example). The VirtualBox network Engine will transform the source IP Address and port (replaces by the host's Addresses). When a packet comes, it goes to VirtualBox and it's engine manage to replace the adresses correctly and follows the message to the VM.
  
  ## Uses:
If the VMs are destinated to be clients or if the services aren't all meant to be connected to the internet, NAT is a good solution.
  
  ##Limits:
Some protocols are not supported (only UDP and TCP are)
Can't assign <1024 ports on the host side.
UDP broadcasting not reliable (VMs go to sleep few seconds after having sent packet so you can't be sure the VM listened the message).


# Bridged networking
In this mode the guest can access the external network through the host and inversely. Obviously communication between the host and the guest is also possible.

  ## Principle:
Thank's to a Specific Driver installed on the host PC, VirtualBox is "connected" to a network interface of this host computer (like eth0 of the physic machine). This enables VirtualBox to do two things:
1. Intercept packets coming from the Internet. It checks the IP Addresses of the packets. If the IP Address matches : VirtualBox replaces the MAC address in the header of the IP packet with the VM's MAC address and then delivers the packet to the VM.
and redirect them to the VMs if the IP Address matches. 
2. Inject Data : VirtualBox can write packets and send them through the interface chosen.

  ## Interfaces concerned: 
Globally you can choose whether an Ethernet interface of a Wi-Fi interface. In the first case they are no problems, but with Wi-Fi : if the Host is a Macintosh or a Linux system, VirtualBox supports only IPv4 and IPv6 protocols, but not IPX.

  ## Uses:
* Contrary to the NAT network, with bridge network your VMs get a real IP address so they can act like servers, which is impossible in the NAT network system (clients away for the private network can't send packets to the VM because they don't have it's IP Address).
* If the VMs are not supposed to be connected from away computers, Bridge Network could be a bad idea in a security-based point of view, as NAT network can be used as a firewall and protect your VMs better. 


# Internal networking
This network only allows communications between selected guests.

  ## Principle:
The VirtualBox driver will act like a Switch and enables VM-to-VM communication. To attach a VM’s network card to the network : go to the settings, in “Networking”, “internal networking”, select the name of an existing internal network and you’re done. (Each Internal network is defined by its name)

  ## Uses:
You can do less things than with bridged network but if you’re looking only for VM-to-VM communication, this solution is safer (the host system can’t observe the data transferred).


# Host-only networking
This mode only allows communication between the host and guests.

  ## Principle:
It’s a sort of merge of Bridge Network and Internal Network :
VirtualBox creates on the host a new software interface which appears like any other network interface.
It creates VM-to-VM communication. The difference with Internal Network is that the host can intercept exchanges and so on watch their communications.  
  # Uses:
Imagine you have : 1 databaseVM, 1 VM hosting a website (webVM) and you want to have an overview of the exchanges from your host Machine. You create 2 networks :
 BridgeNetwork with the webVM
Host-OnlyNetwork with the dataVM
People from outside can’t corrupt your database, and you can examine the exchanges from your host computer.

  ## Sources
- https://www.virtualbox.org/manual/ch06.html
- https://www.thomas-krenn.com/en/wiki/Network_Configuration_in_VirtualBox
