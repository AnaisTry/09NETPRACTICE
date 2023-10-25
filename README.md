# Theory for NetPractice

## Ressources : ##

https://www.codequoi.com/en/internet-layered-network-architecture/

https://www.codequoi.com/en/ipv4-addresses-routing-and-subnet-masks/

Subnet calculators : 
https://www.calculator.net/ip-subnet-calculator.html
https://formulae.brew.sh/formula/ipcalc

Networking animated videos : https://www.youtube.com/playlist?list=PL7zRJGi6nMRzg0LdsR7F3olyLGoBcIvvg

Subnetting mastery :
https://www.youtube.com/playlist?list=PLIFyRwBY_4bQUE4IB5c4VPRyDoLgOdExE

## Notes : ##


### Classless Inter-Domain Routing (CIDR)

For example, 128.42.42.201/28 indicates that the 28 first bits of the address represent the subnetwork:
```
/28
in decimal : 255.255.255.240
in binary  : 11111111 11111111 11111111 11110000
```
 The formula to determine the number of possible addresses within a subnetwork is $2^(address length – mask)$. 
 This means that there are $2^(32-28) = 2^4 = 16$ possible IPv4 addresses in this 28-bit subnet range:

```
IP         : 10000000 00101010 00101010 11001001 : 128.42.42.201
Masque /28 : 11111111 11111111 11111111 11110000 : 255.255.255.240
IP min     : 10000000 00101010 00101010 11000000 : 128.42.42.192
IP max     : 10000000 00101010 00101010 11001111 : 128.42.42.207
```

### Reserved IPv4 Addresses :
```
Address Block		Range of Addresses			Number of Addresses		Use
0.0.0.0/8		0.0.0.0 – 0.255.255.255			16 777 	216			Software
10.0.0.0/8		10.0.0.0 – 10.255.255.255		16 777 216			Private network: local communications
100.64.0.0/10		100.64.0.0 – 100.127.255.255		4 194 304			Private network: ISP communications
127.0.0.0/8		127.0.0.0 – 127.255.255.255		16 777 216			Host: loopback addresses for localhost
169.254.0.0/16		169.254.0.0 – 169.254.255.255		65 536				Subnet: local communications between two hosts on a single link
172.16.0.0/12		172.16.0.0 – 172.31.255.255		1 048 576			Private network: local communications
192.0.0.0/24		192.0.0.0 – 192.0.0.255			256				Private network: IETF protocol assignments
192.0.2.0/24		192.0.2.0 – 192.0.2.255			256				Documentation: TEST-NET-1
192.88.99.0/24		192.88.99.0 – 192.88.99.255		256				Reserved: 6to4 relay
192.168.0.0/16		192.168.0.0 – 192.168.255.255		65 536				Private network: local communications
198.18.0.0/15		198.18.0.0 – 198.19.255.255		131 072				Private network: bench-marking between two connected subnets
198.51.100.0/24		198.51.100.0 – 198.51.100.255		256				Documentation: TEST-NET-2
203.0.113.0/24		203.0.113.0 – 203.0.113.255		256				Documentation: TEST-NET-3
224.0.0.0/4		224.0.0.0 – 239.255.255.255		268 435 456			Reserved: IPv4 multicast
233.252.0.0/24		233.252.0.0 – 233.252.0.255		256				Documentation: MCAST-TEST-NET
240.0.0.0/4		240.0.0.0 – 255.255.255.254		268 435 455			Reserved: for future use
255.255.255.255/32	255.255.255.255				1				Subnet: limited broadcast destination address
```

### Subnetting
```
Bitmask (Bits)	Dotted Decimal	Hexadecimal	Binary					Nb of networks	Nb of hosts	Group size
/0		0.0.0.0		0x00000000	00000000 00000000 00000000 00000000							
/1		128.0.0.0	0x80000000	10000000 00000000 00000000 00000000										
/2		192.0.0.0	0xc0000000	11000000 00000000 00000000 00000000			2147483646	2^31	
/3		224.0.0.0	0xe0000000	11100000 00000000 00000000 00000000
/4		240.0.0.0	0xf0000000	11110000 00000000 00000000 00000000
/5		248.0.0.0	0xf8000000	11111000 00000000 00000000 00000000
/6		252.0.0.0	0xfc000000	11111100 00000000 00000000 00000000
/7		254.0.0.0	0xfe000000	11111110 00000000 00000000 00000000
/8		255.0.0.0	0xff000000	11111111 00000000 00000000 00000000
/9		255.128.0.0	0xff800000	11111111 10000000 00000000 00000000
/10		255.192.0.0	0xffc00000	11111111 11000000 00000000 00000000
/11		255.224.0.0	0xffe00000	11111111 11100000 00000000 00000000
/12		255.240.0.0	0xfff00000	11111111 11110000 00000000 00000000
/13		255.248.0.0	0xfff80000	11111111 11111000 00000000 00000000
/14		255.252.0.0	0xfffc0000	11111111 11111100 00000000 00000000
/15		255.254.0.0	0xfffe0000	11111111 11111110 00000000 00000000
/16		255.255.0.0	0xffff0000	11111111 11111111 00000000 00000000
/17		255.255.128.0	0xffff8000	11111111 11111111 10000000 00000000
/18		255.255.192.0	0xffffc000	11111111 11111111 11000000 00000000
/19		255.255.224.0	0xffffe000	11111111 11111111 11100000 00000000
/20		255.255.240.0	0xfffff000	11111111 11111111 11110000 00000000
/21		255.255.248.0	0xfffff800	11111111 11111111 11111000 00000000
/22		255.255.252.0	0xfffffc00	11111111 11111111 11111100 00000000
/23		255.255.254.0	0xfffffe00	11111111 11111111 11111110 00000000			2046			2^11
/24		255.255.255.0	0xffffff00	11111111 11111111 11111111 00000000		1	254			256
/25		255.255.255.128	0xffffff80	11111111 11111111 11111111 10000000		2	126			128
/26		255.255.255.192	0xffffffc0	11111111 11111111 11111111 11000000		4	62			64	
/27		255.255.255.224	0xffffffe0	11111111 11111111 11111111 11100000		8	30			32
/28		255.255.255.240	0xfffffff0	11111111 11111111 11111111 11110000		16	14			16
/29		255.255.255.248	0xfffffff8	11111111 11111111 11111111 11111000		32	6			8
/30		255.255.255.252	0xfffffffc	11111111 11111111 11111111 11111100		64	2			4
/31		255.255.255.254	0xfffffffe	11111111 11111111 11111111 11111110		128	0			2
/32		255.255.255.255	0xffffffff	11111111 11111111 11111111 11111111		255				1 
```

### Some tips for levels 8 and 9 of netpractice :


```
8. 
All network should have the same group of ip with the range given in the modem's destination address
ex :
166.31.228.0/26 same destination for R1
addresses from 0 to 64
with a given mask of /28 (240) we have group sizes of 16 : 0-15 16-31 32-47 48-63 
R2 gives the hop (R13) of 62
```

```
9. 
4 separated networks
Left network (with switch) : the mask is given, take network of choice ex 0.0.0.1 and put it in the internet forwarding table
Routers network : mask is given pick network of choice ex 1.0.0.1, put the next hop in R1 forwarding table
Client D network : the mask and next hop are given so put them and implement the ip as destination for internet forwarding table and R1 forwarding table
Client C network : pick anything that doesn't overlap and is not a reserved ip address, implement as destination for both internet and R1
