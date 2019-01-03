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
   - Use the following iPerf commands to measure the bandwidth in your network
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
   - Use the following iPerf commands to measure the bandwidth in your network
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

2. Example of Ryu SDN

3. Mininet Topology

4. Ryu Controller

5. Measurement

### Discussion

1. Describe the difference between packet-in and packet-out in detail.
   
2. What is “table-miss” in SDN?
   
3. Why is "`(app_manager.RyuApp)`" adding after the declaration of class in `controller.py`?
   
4. Explain the following code in `controller.py`.
    ```python
    @set_ev_cls(ofp_event.EventOFPPacketIn, CONFIG_DISPATCHER)
    ```

5. What is the meaning of “datapath” in `controller.py`?
   
6. Why need to set "`ip_proto=17`" in the flow entry?
   
7. Compare the differences between the iPerf results of `SimpleController.py` and `controller.py` in detail.
   
8. Which forwarding rule is better? Why?

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
