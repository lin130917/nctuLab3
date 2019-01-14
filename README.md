# Route Configuration

This repository is a lab for NCTU course "Introduction to Computer Networks 2018".

---
## Abstract

In this lab, we are going to write a Python program with Ryu SDN framework to build a simple software-defined network and compare the different between two forwarding rules.

---
## Objectives

1. Learn how to build a simple software-defined networking with Ryu SDN framework
2. Learn how to add forwarding rule into each OpenFlow switch

---
## Execution

1. Run topology with SimpleController.py
   - Run topo.py in one terminal first
      ```
      # Change the directory into /Route_Configuration/src/
      $ cd /root/Route_Configuration/src/
      # Run the topo.py with Mininet
      $ sudo mn --custom topo.py --topo topo --link tc --controller remote
      ```
   - Then, run SimpleController.py in another terminal
      ```
      # Change the directory into /Route_Configuration/src/
      $ cd /root/Route_Configuration/src/
      # Run the SimpleController.py with Ryu manager
      $ sudo ryu-manager SimpleController.py --observe-links
      ```
2. Measure the bandwidth
   - Use the following iPerf commands to measure the bandwidth in the network
      ```
      # Run in the iPerf command in Mininet CLI
      mininet> h1 iperf -s -u -i 1 -p 5566 > ./out/result1 &
      mininet> h2 iperf -c 10.0.0.1 -u -i 1 -p 5566
      ```
   - Leave topo.py in one terminal first
      ```
      # Leave the Mininet CLI
      mininet> exit
      ```
   - Then, leave SimpleController.py in another terminal
      ```
      # Leave the Mininet CLI
      Ctrl-z
      # Make sure “RTNETLINK” is clean indeed
      $ mn -c
      ```
   ![](/src/Capture1.PNG)
3. Run topology with controller.py
   - Run topo.py in one terminal first
      ```
      # Change the directory into /Route_Configuration/src/
      $ cd /root/Route_Configuration/src/
      # Run the topo.py with Mininet
      $ sudo mn --custom topo.py --topo topo --link tc --controller remote
      ```
   - Then, run controller.py in another terminal
      ```
      # Change the directory into /Route_Configuration/src/
      $ cd /root/Route_Configuration/src/
      # Run the controller.py with Ryu manager
      $ sudo ryu-manager controller.py --observe-links
      ```
4. Measure the bandwidth
   - Use the following iPerf commands to measure the bandwidth in the network
      ```
      # Run in the iPerf command in Mininet CLI
      mininet> h1 iperf -s -u -i 1 -p 5566 > ./out/result2 &
      mininet> h2 iperf -c 10.0.0.1 -u -i 1 -p 5566
      ```
   - Leave topo.py in one terminal first
      ```
      # Leave the Mininet CLI
      mininet> exit
      ```
   - Then, leave controller.py in another terminal
      ```
      # Leave the Mininet CLI
      Ctrl-z
      # Make sure “RTNETLINK” is clean indeed
      $ mn -c
      ```
   ![](/src/Capture2.PNG)

---
## Description

### Tasks

1. Environment Setup
   1. Join this lab on GitHub Classroom
      - Click the following link to join this lab
         - https://classroom.github.com/a/RHNMq4Td
      - Go to our GitHub group to see the repository
         - https://github.com/nctucn
   2. Login to the container using SSH
      ```
      # Open the terminal to connect to the container
      $ ssh -p 16203 root@140.113.195.69
      Password: 616203
      ```
   3. Clone the GitHub repository
      ```
      # Clone the GitHub repository to “Route_Configuration”
      $ git clone https://github.com/nctucn/lab3-lin130917.git Route_Configuration
      ```
   4. Run Mininet for testing
      ```
      # Start the service of Open vSwitch
      $ sudo service openvswitch-switch start
      # Run Mininet again!
      $ sudo mn
      ```
2. Example of Ryu SDN
   1. Login to the container in two terminals
      ```
      # Open the terminal to connect to the container
      $ ssh -p 16203 root@140.113.195.69
      Password: 616203
      ```
   2. Run Mininet topology
      - Run SimpleTopo.py in one terminal first
         ```
         # Change the directory into
         # /root/Route_Configuration/src/
         $ cd /root/Route_Configuration/src/
         # Run the SimpleTopo.py with Mininet
         $ sudo mn --custom SimpleTopo.py --topo topo --link tc --controller remote
         ```
   3. Run Ryu manager with controller
      - Run Ryu manager with controller
         ```
         # Change the directory into
         # /root/Route_Configuration/src/
         $ cd /root/Route_Configuration/src/
         # Run the SimpleController.py with Ryu manager
         $ sudo ryu-manager SimpleController.py --observelinks
         ```
   4. How to leave the Ryu controller?
      - Leave SimpleTopo.py in one terminal first
         ```
         # Leave the Mininet CLI
         mininet> exit
         ```
      - Then, leave SimpleController.py in another terminal
         ```
         # Leave the Mininet CLI
         Ctrl-z
         # Make sure “RTNETLINK” is clean indeed
         $ mn -c
         ```
3. Mininet Topology
   1. Build the topology via Mininet
      - Duplicate the example code SimpleTopo.py and name it topo.py
         ```
         # Make sure the current directory is
         # /root/Route_Configuration/src/
         $ cp SimpleTopo.py topo.py
         ```
      - Add the constraints (e.g., bandwidth, delay, and loss rate) by /Route_Configuration/src/topo/ topo.png
   2. Run Mininet topology and controller
      - Run topo.py in one terminal first
         ```
         # Run the topo.py with Mininet
         $ sudo mn --custom topo.py --topo topo --link tc --controller remote
         ```
      - Then, run SimpleController.py in another terminal
         ```
         # Run the SimpleController.py with Ryu manager
         $ sudo ryu-manager SimpleController.py --observe-links
         ```
4. Ryu Controller
   1. Trace the code of Ryu controller
      - Trace the example code SimpleController.py and modify switch_feature_handler
         ```
         # Handle the initial feature of each switch
         def switch_features_handler(self, ev):
         ```
   2. Write another Ryu controller
      - Duplicate the example code SimpleController.py and name it controller.py
      - Follow the the forwarding rules in the next slide and modify controller.py
      - ONLY need to modify the method switch_features_handler(self, ev)
5. Measurement
   1. Run topology with SimpleController.py
      - Run topo.py in one terminal first
         ```
         # Run the topo.py with Mininet
         $ sudo mn --custom topo.py --topo topo --link tc --controller remote
         ```
      - Then, run SimpleController.py in another terminal
         ```
         # Run the SimpleController.py with Ryu manager
         sudo ryu-manager SimpleController.py --observe-links
         ```
   2. Measure the bandwidth
      - Use the following iPerf commands to measure the bandwidth in the network
         ```
         # Run in the iPerf command in Mininet CLI
         mininet> h1 iperf -s -u -i 1 -p 5566 > ./out/result1 &
         mininet> h2 iperf -c 10.0.0.1 -u -i 1 -p 5566
         ```
      - Leave topo.py in one terminal first
         ```
         # Leave the Mininet CLI
         mininet> exit
         ```
      - Then, leave SimpleController.py in another terminal
         ```
         # Leave the Mininet CLI
         Ctrl-z
         # Make sure “RTNETLINK” is clean indeed
         $ mn -c
         ```
   3. Run topology with controller.py
      - Run topo.py in one terminal first
         ```
         $ sudo mn --custom topo.py --topo topo --link tc --controller remote
         ```
      - Then, run controller.py in another terminal
         ```
         # Run the controller.py with Ryu manager
         sudo ryu-manager controller.py --observe-links
         ```
   4. Measure the bandwidth
      - Use the following iPerf commands to measure the bandwidth in the network
         ```
         # Run in the iPerf command in Mininet CLI
         mininet> h1 iperf -s -u -i 1 -p 5566 > ./out/result2 &
         mininet> h2 iperf -c 10.0.0.1 -u -i 1 -p 5566
         ```
      - Leave topo.py in one terminal first
         ```
         # Leave the Mininet CLI
         mininet> exit
         ```
      - Then, leave controller.py in another terminal
         ```
         # Leave the Mininet CLI
         Ctrl-z
         # Make sure “RTNETLINK” is clean indeed
         $ mn -c
         ```

### Discussion

1. Describe the difference between packet-in and packet-out in detail.
   - packet-in: Transfers the received packets to the controller
   - packet-out: Transfers the packets forwarded by the controller from the specified port
   
2. What is “table-miss” in SDN?

   If a packet does not match a flow entry in a flow table, this is a table miss.
   
3. Why is "`(app_manager.RyuApp)`" adding after the declaration of class in `controller.py`?

   In order to inherit from app_manager.RyuApp.
   
4. Explain the following code in `controller.py`.
    ```python
    @set_ev_cls(ofp_event.EventOFPPacketIn, MAIN_DISPATCHER)
    ```
    This is a decorator for Ryu application to declare an event handler.This decorator tells Ryu when the decorated function should be called. The first argument of the decorator indicates which type of event this function should be called for. As you might expect, every time Ryu gets a packet_in message, this function is called. The second argument indicates the state of the switch. You probably want to ignore packet_in messages before the negotiation between Ryu and the switch is finished. Using 'MAIN_DISPATCHER' as the second argument means this function is called only after the negotiation completes.

5. What is the meaning of “datapath” in `controller.py`?

   the switch in the topology using OpenFlow
   
6. Why need to set "`ip_proto=17`" in the flow entry?

   Because UDP is better.
   
7. Compare the differences between the iPerf results of `SimpleController.py` and `controller.py` in detail.

   In the result of controller.py, bandwidth is slightly better than the result of SimpleController.py and loss is less than the result of SimpleController.py .
   
8. Which forwarding rule is better? Why?

   The forwarding rule of controller.py is better because loss is less than the result of Simplecontroller.py.

---
## References

* **Ryu SDN**
    * [Ryubook Documentation](https://osrg.github.io/ryu-book/en/html/)
    * [Ryubook [PDF]](https://osrg.github.io/ryu-book/en/Ryubook.pdf)
    * [Ryu 4.30 Documentation](https://github.com/mininet/mininet/wiki/Introduction-to-Mininet)
    * [Ryu Controller Tutorial](http://sdnhub.org/tutorials/ryu/)
    * [OpenFlow 1.3 Switch Specification](https://www.opennetworking.org/wp-content/uploads/2014/10/openflow-spec-v1.3.0.pdf)
    * [Ryubook 說明文件](https://osrg.github.io/ryu-book/zh_tw/html/)
    * [GitHub - Ryu Controller 教學專案](https://github.com/OSE-Lab/Learning-SDN/blob/master/Controller/Ryu/README.md)
    * [Ryu SDN 指南 – Pengfei Ni](https://feisky.gitbooks.io/sdn/sdn/ryu.html)
    * [OpenFlow 通訊協定](https://osrg.github.io/ryu-book/zh_tw/html/openflow_protocol.html)
* **Python**
    * [Python 2.7.15 Standard Library](https://docs.python.org/2/library/index.html)
    * [Python Tutorial - Tutorialspoint](https://www.tutorialspoint.com/python/)
* **Others**
    * [Cheat Sheet of Markdown Syntax](https://www.markdownguide.org/cheat-sheet)
    * [Vim Tutorial – Tutorialspoint](https://www.tutorialspoint.com/vim/index.htm)
    * [鳥哥的 Linux 私房菜 – 第九章、vim 程式編輯器](http://linux.vbird.org/linux_basic/0310vi.php)

---
## Contributors

* [林詩哲](https://github.com/lin130917)
* [David Lu](https://github.com/yungshenglu)

---
## License

GNU GENERAL PUBLIC LICENSE Version 3
