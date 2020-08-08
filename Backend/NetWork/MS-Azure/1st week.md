## Cloud Computing
### 특징 
> 1. On-Demand Self Service - 원하는 서비스를 만들어서 사용한다.
> 2. Broad Network access - 네트워크를 통해서 사용한다.
> 3. Resource pooling - DataCenter의 리소스들이 풀링되어 있다. (Compute, Network, Storage)
> 가상화를 바탕으로 물리적인 각각의 서버를 하나로 pooling 시켜준다. 
> 4. Lower operational expenses - 온프레미스 환경보다 운영관리 비용이 저렴하다.
### public, private and hybird cloud
> public --> 벤더에서 제공하는<br/>
> private --> 회사 자체적으로 구축하는 클라우드 // window의 hyper-v <br/> 
> hybrid --> public과 private 유연성있게
### SaaS
### PaaS
### IaaS

## 클라우드의 정의
> 네트워크를 사용해서 받는 서비스를 총칭하는 말.<br/>
> Scalable and Elastic 해야한다. --> 물리적인 장비들이 pooling되어 있어야 한다. <br/>

## 가상화?
### Hyper-V 설치<br/>
windows enterprise 환경에서 설정-> 프로그램 기능에 탑재.

### Host OS: Hardware에 직접 설치된 OS(Windows 10 Enterprise)
### VM(Virtual MAchine): Hyper-V 환경에 설치된 OS(Windows Server 2016)
= Guest OS
1. 1세대 VM
>
2. 2세대 VM
>

### Virtual Switch
> -External(외부) : 실무에서 사용, VM에 Host OS의 네트워크 대역의 IP가 할당.(VM에 Public IP 할당 가능)
> -Internal(내부): 테스트나 개발, Private IP 할당. (Host OS와 VM과 통신 가능, NAT구성시 인터넷 연결)
> -Private(개인): 테스트나 개발, Private IP할당 (VM끼리만 통신 가능)

### Virtualization(가상화)
> -Type 1: 실무 환경에 사용(MS Hyper-V, Vmware ESX, CTRIX Zen) <br/>
>     CPU에서 가상화 지원, RAM의 DEP 지원 <br/> 
> -Type 2: 개발, 테스트(VMware workstation, Player, Oracle Virtual Box)
> 
### VHD Booting: VM을 Host OS 환경으로 구현
VM으로 만들면 다른 컴퓨터로 이식(?) 가능. <br/>
cf) .vhd || .vhdx 가상 하드디스크 파일??

### HDD Disk를 서버에 추가 시 <br/>
> (computer management, compmgmt.msc => Disk Management)
> 1. 초기화(MBR(2TB) , GPT(
> 2. 
### command
bcdboot: f\windows <br/>
msconfig <br/>
shutdown \r \t (/t second --> time option , /r reboot option  <br/>

## SSH <br/>
> 시큐어 셸(Secure Shell, SSH)은 네트워크 상의 다른 컴퓨터에 로그인하거나 원격 시스템에서 명령을 실행하고 다른 시스템으로 파일을 복사할 수 있도록 해 주는 응용 프로그램 또는 그 프로토콜을 가리킨다. 기존의 rsh, rlogin, 텔넷 등을 대체하기 위해 설계되었으며, 강력한 인증 방법 및 안전하지 못한 네트워크에서 안전하게 통신을 할 수 있는 기능을 제공한다. 기본적으로는 22번 포트를 사용한다.
## TCP/IP
### Dynamic Configuration(자동구성, 유동IP), (Client OS) : DHCP Server에서 할당 받아온다.
> APIPA(Automatic Private IP Address) : DHCP Server에서 IP를 못 받아올 경우
> OS에서 자동으로 할당하는 IP(169.254.x.x) - 자기 네트워크 내의 컴퓨터들과는 통신 가능. 인터넷 접속은 X
### Static Configuration(수동구성, 고정IP), (Server OS)
> IP: 
> Subnet Mask:
> Gateway:
> DNS:

### Public IP (공인 IP) <br/>
> IANA에서 라우팅 가능한 IP <br/>
cf) IANA? IP 관리하는 단체? 

### Private IP (사설 IP) <br/>
> IANA에서 누구나 사용 가능하도록 허용한 IP
> 적은 공인 IP로 많은 시스템을 인터넷 (NAT)
> 보안
> 10.x.x.x
> 172.16.x.x ~ 172.31.x.x
> 192.168.x.x

### Port <br/>
> 데이터가 전송되는 통로(0~65, 536), TCP or UDP (c:\windows\systems32\drivers\etc\services) 윈도우 기준 <br/>
> 1~1024 : 잘 알려진 포트 <br/>
> TCP 21 : FTP <br/>
> TCP 22 : SSH <br/>
> TCP 23 : Telnet <br/>
> TCP 25 : SMTP <br/>
> TCP 53 : DNS Zone Transfer <br/>
> UDP 53 : DNS Name Resolution <br/>
> UDP 67, 68 : DHCP <br/>
> TCP 80 : http <br/>
> TCP 443 : https <br/>
> TCP 110 : pop3 <br/>
> TCP 3389 : RDP(Remote Desktop Protocol) : window Server 원격 관리 
> 1025~ 5000: Application
## WS 2016
### role <br/>
서버 서비스(16, Web, FTP, DNS, DHCP, Hyper-V...)
### feature 
OS에서 지원해준느 기능(35)

## Linux
여러가지 버전이 있다.
### RedHat
> RedHat으로부터 기술 지원 O
### CentOS
> ReaHat 버전의 리눅스와 비슷. 기술 지원 X
### Debian
> 
### Ubuntu
> Debian 계열의 리눅스 OS.

<br/>


git