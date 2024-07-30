# OSPF-CONFIGUARTION-FOR-MULTIPLE-AREAS
### OSPF Configuration for Multiple Areas Using Loopback Addresses

The provided topology consists of multiple routers configured in different OSPF areas. Below is a detailed guide on configuring OSPF for multiple areas using loopback addresses and the `ip ospf` interface command method.

#### Topology Overview:
- **Routers:** Multiple routers in different OSPF areas (Area 0, Area 50, Area 60, Area 70)
- **OSPF Areas:**
  - Area 0: Backbone area
  - Area 50, Area 60, Area 70: Other OSPF areas

### Step-by-Step Configuration

#### Step 1: Assign IP Addresses and Loopback Addresses
Assign IP addresses to each router interface and configure loopback addresses as per the topology. Below is an example for each router:

**Router1 (Area 0):**
```shell
Router1> enable
Router1# configure terminal
Router1(config)# interface gigabitEthernet 0/0
Router1(config-if)# ip address 192.168.55.1 255.255.255.0
Router1(config-if)# no shutdown
Router1(config-if)# exit
Router1(config)# interface gigabitEthernet 0/1
Router1(config-if)# ip address 192.168.78.1 255.255.255.0
Router1(config-if)# no shutdown
Router1(config-if)# exit
Router1(config)# interface loopback 0
Router1(config-if)# ip address 192.168.100.1 255.255.255.255
Router1(config-if)# exit
```

**Router2 (Area 0, 60, 70):**
```shell
Router2> enable
Router2# configure terminal
Router2(config)# interface gigabitEthernet 0/0
Router2(config-if)# ip address 192.168.55.2 255.255.255.0
Router2(config-if)# no shutdown
Router2(config-if)# exit
Router2(config)# interface gigabitEthernet 0/1
Router2(config-if)# ip address 192.168.45.1 255.255.255.0
Router2(config-if)# no shutdown
Router2(config-if)# exit
Router2(config)# interface gigabitEthernet 0/2
Router2(config-if)# ip address 192.168.46.1 255.255.255.0
Router2(config-if)# no shutdown
Router2(config-if)# exit
Router2(config)# interface loopback 0
Router2(config-if)# ip address 192.168.100.2 255.255.255.255
Router2(config-if)# exit
```

**Router3 (Area 0):**
```shell
Router3> enable
Router3# configure terminal
Router3(config)# interface gigabitEthernet 0/0
Router3(config-if)# ip address 192.168.55.3 255.255.255.0
Router3(config-if)# no shutdown
Router3(config-if)# exit
Router3(config)# interface loopback 0
Router3(config-if)# ip address 192.168.100.3 255.255.255.255
Router3(config-if)# exit
```

**Router4 (Area 60):**
```shell
Router4> enable
Router4# configure terminal
Router4(config)# interface gigabitEthernet 0/0
Router4(config-if)# ip address 192.168.45.2 255.255.255.0
Router4(config-if)# no shutdown
Router4(config-if)# exit
Router4(config)# interface loopback 0
Router4(config-if)# ip address 192.168.100.4 255.255.255.255
Router4(config-if)# exit
```

**Router5 (Area 70):**
```shell
Router5> enable
Router5# configure terminal
Router5(config)# interface gigabitEthernet 0/0
Router5(config-if)# ip address 192.168.46.2 255.255.255.0
Router5(config-if)# no shutdown
Router5(config-if)# exit
Router5(config)# interface loopback 0
Router5(config-if)# ip address 192.168.100.5 255.255.255.255
Router5(config-if)# exit
```

#### Step 2: Configure OSPF on Routers
Enable OSPF and advertise the networks on each router using the `ip ospf` interface command.

**Router1 (Area 0):**
```shell
Router1> enable
Router1# configure terminal
Router1(config)# router ospf 1
Router1(config-router)# exit
Router1(config)# interface gigabitEthernet 0/0
Router1(config-if)# ip ospf 1 area 0
Router1(config-if)# exit
Router1(config)# interface gigabitEthernet 0/1
Router1(config-if)# ip ospf 1 area 50
Router1(config-if)# exit
Router1(config)# interface loopback 0
Router1(config-if)# ip ospf 1 area 0
Router1(config-if)# exit
```

**Router2 (Area 0, 60, 70):**
```shell
Router2> enable
Router2# configure terminal
Router2(config)# router ospf 1
Router2(config-router)# exit
Router2(config)# interface gigabitEthernet 0/0
Router2(config-if)# ip ospf 1 area 0
Router2(config-if)# exit
Router2(config)# interface gigabitEthernet 0/1
Router2(config-if)# ip ospf 1 area 60
Router2(config-if)# exit
Router2(config)# interface gigabitEthernet 0/2
Router2(config-if)# ip ospf 1 area 70
Router2(config-if)# exit
Router2(config)# interface loopback 0
Router2(config-if)# ip ospf 1 area 0
Router2(config-if)# exit
```

**Router3 (Area 0):**
```shell
Router3> enable
Router3# configure terminal
Router3(config)# router ospf 1
Router3(config-router)# exit
Router3(config)# interface gigabitEthernet 0/0
Router3(config-if)# ip ospf 1 area 0
Router3(config-if)# exit
Router3(config)# interface loopback 0
Router3(config-if)# ip ospf 1 area 0
Router3(config-if)# exit
```

**Router4 (Area 60):**
```shell
Router4> enable
Router4# configure terminal
Router4(config)# router ospf 1
Router4(config-router)# exit
Router4(config)# interface gigabitEthernet 0/0
Router4(config-if)# ip ospf 1 area 60
Router4(config-if)# exit
Router4(config)# interface loopback 0
Router4(config-if)# ip ospf 1 area 60
Router4(config-if)# exit
```

**Router5 (Area 70):**
```shell
Router5> enable
Router5# configure terminal
Router5(config)# router ospf 1
Router5(config-router)# exit
Router5(config)# interface gigabitEthernet 0/0
Router5(config-if)# ip ospf 1 area 70
Router5(config-if)# exit
Router5(config)# interface loopback 0
Router5(config-if)# ip ospf 1 area 70
Router5(config-if)# exit
```

#### Step 3: Verify Configuration
Use the following commands to verify the OSPF configuration and connectivity:

**Check OSPF Neighbors:**
```shell
Router# show ip ospf neighbor
```

**Check OSPF Routes:**
```shell
Router# show ip route ospf
```

**Ping from one network to another:**
```shell
Router# ping 192.168.100.3
```

By following these steps, you can configure the provided network topology in Cisco Packet Tracer, ensuring efficient routing and connectivity using OSPF in multiple areas with loopback addresses and interface-specific OSPF commands.
