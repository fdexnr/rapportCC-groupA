# rapportCC-groupA

# Bridge Network with VirtualBox

  # Principle :
Thank's to a Specific Driver installed on the host PC, VirtualBox is "connected" to a network interface of this host computer (like eth0 of the physic machine). This enables VirtualBox to do two things:
1. Intercept packets coming from the Internet. It checks the IP Addresses of the packets. If the IP Address matches : VirtualBox replaces the MAC address in the header of the IP packet with the VM's MAC address and then delivers the packet to the VM.
and redirect them to the VMs if the IP Address matches. 
2. Inject Data : VirtualBox can write packets and send them through the interface chosen.

  # Interfaces concerned : 
Globally you can choose whether an Ethernet interface of a Wi-Fi interface. In the first case they are no problems, but with Wi-Fi : if the Host is a Macintosh or a Linux system, VirtualBox supports only IPv4 and IPv6 protocols, but not IPX.

  # Uses :
* Contrary to the NAT network, with bridge network your VMs get a real IP address so they can act like servers, which is impossible in the NAT network system (clients away for the private network can't send packets to the VM because they don't have it's IP Address).
* If the VMs are not supposed to be connected from away computers, Bridge Network could be a bad idea in a security-based point of view, as NAT network can be used as a firewall and protect your VMs better. 
