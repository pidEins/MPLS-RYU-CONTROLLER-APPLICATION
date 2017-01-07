# MPLS-RYU-CONTROLLER-APPLICATION

It is MPLS application on RYU Controller. 

To run this application, please follow the below mentioned steps 

1. install ryu controller

   ./install-ryu.sh
   
2. Configure the ryu controller on the OVS. 

   ovs-vsctl set-controller br0 tcp:172.16.1.240:6633
   
3. Now run the application 

   ryu-manager --verbose rest_mpls.py
   
   
### Configuration using REST API:

1. This application provides the REST API interface to configure the addresses/prefix. 

   Now suppose, a OVS has two interfaces (eth0, eth1) and coressponding addresses (IP0, IP1) then user needs to configure  these addresses on the ryu controller by running the below mentioned command 

   curl -X POST -d '{"address":"10.10.1.2/24"}' http://localhost:8080/router/0000000000000001

   Here IP0 = 10.10.1.2/24 
      OVS1 id is "0000000000000001"
     
   Similarly user can configure the IP1 address. 

2. To configure the prefixes, user has to run this command

   curl -X POST -d '{ "prefix" : "10.10.1.0/24", "port" : "2", "router_type": "ler" }'       http://localhost:8080/router/0000000000000001

   Here 
   1.prefix means, OVS1 can reach "10.10.1.0/24" address through port number 
   2.router_type : it can be either edge (ler) or intermediate router (lsr). 

## Overall Desgin

