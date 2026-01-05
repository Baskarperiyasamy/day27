

### SDN Network Topology Exploration with Mininet
 This project demonstrates the creation, visualization, and connectivity testing of different network topologies using Software Defined Networking (SDN) principles.

### Overview
~~~
The goal of this project was to instantiate various standard and custom network topologies to observe how SDN controllers (ONOS and Ryu) manage device discovery, link establishment, and packet forwarding.

Tools Used
Mininet: Network emulator for creating virtual hosts, switches, and links.

ONOS: Distributed SDN controller for topology visualization and flow management.

Ryu: Component-based SDN framework used for simple switch logic and packet-in monitoring.

OpenFlow 1.3: The protocol used for communication between the switches and the controller.
~~~
### Topologies Implemented
~~~
1. Single Topology
A simple star-like configuration where multiple hosts are connected to a single central switch.

Command: sudo mn --topo single,3 --mac --controller remote --switch ovsk

Results: Successfully performed pingall with 0% packet loss.

2. Linear Topology
Switches are connected in a line, with one host attached to each switch.

Configurations tested:

2-Switch Linear: sudo mn --topo linear,2

4-Switch Linear: sudo mn --topo linear,4

Observations: Verified multi-hop reachability across the chain. ONOS successfully mapped the linear path.

3. Tree Topology
A hierarchical structure defined by depth and fanout.

Small Tree: sudo mn --topo tree,depth=2,fanout=2

Large Tree: sudo mn --topo tree,depth=2,fanout=8 (Total 64 hosts).

Observations: Handled high-density host environments. The large tree test showed 4032/4032 successful pings.

4. Grid Topology (Attempted)
Tested the resilience of the CLI and controller when invoking non-standard topologies.

Status: Mininet default CLI does not support grid natively without a custom python script.
~~~
### Key Findings
~~~
Topology Visualization (ONOS)
Using the ONOS Web UI (localhost:8181/onos/ui), we verified:

Device Discovery: Switches (s1, s2, etc.) appearing as OpenFlow nodes.

Host Tracking: IP and MAC addresses of hosts (h1, h2...) becoming visible after the first ping.

Link Status: Real-time visualization of links between switches.

Packet Monitoring (Ryu)
By running the ryu.app.simple_switch application, we monitored "Packet-In" messages:

Captured MAC learning in real-time.

Observed how the controller handles ARP broadcasts (ff:ff:ff:ff:ff:ff) to discover host locations.
~~~
### How to Run
~~~
Start the Controller:

Bash
# For ONOS
./bin/onos-service start
# For Ryu
ryu-manager ryu.app.simple_switch
Launch Mininet:

Bash
sudo mn --topo <type> --controller remote,ip=127.0.0.1 --switch ovsk,protocols=OpenFlow13
Test Connectivity:

Bash
mininet> pingall
~~~

