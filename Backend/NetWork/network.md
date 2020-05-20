# Network

## Router
컴퓨터간에 통신을 위해서 `ip address`가 필요하다. 
일반적으로 가정에서 인터넷에 연결할 때는 통신사와의 계약을 통해서 회선을 부여받고, 그에 따라서 ip가 주어진다.   
*하지만 인터넷을 연결하는 장비가 많아진다면?*  
공유기를 사용하게 된다. 그럼 공유기에 ip가 부여된다.  
공유기에는 WAN과 LAN선을 연결할 수 있다. 이 둘 사이를 연결한다.  
* WAN (Wide Area Network)  
* LAN (Local Area Network)   
Local로 형성된 네트워크 내부의 기기들도 ip주소를 가지게 되고, 공유기 또한 ip 주소를 가지게 되는데 공유기가 가지는 ip 주소를 `Gateway address` or `Router address`라고 한다.

* public ip address

* private ip address
## NAT (Network Address Translation)
private ip address를 가지고 있는 기기로 외부의 네트워크에 접속하려고 하면, Gateway address를 가진 기기로 신호를 보낸다.  
1. 공유기는 private ip address를 기록
2. 그리고 public ip address로 변환 후 외부 네트워크 접속. 이 후 response가 오면 기록을 참고하여 전달. 
## IP

* dynamic addres 
* static address 

### version 
* Ipv4

* Ipv6

## Port 
하나의 컴퓨터에는 여러 개의 서버가 존재한다.  
* 22 SSH
* 80 HTTP 
* 0~1023 Well-known port
* 1024~ 65535 

### URI 
`scheme:[//authority]path[?query][#fragment]`

## Port fowarding 


## DHCP (Dynamic Host Configuration Protocol)
DHCP Server, DHCP Client  
1. DHCP Client가 DHCP Server에게 MAC address를 알려준다. 
2. DHCP Server가 DHCP Client에게 ip address를 대여.
3. DHCP Client --OK--> DHCP Server 