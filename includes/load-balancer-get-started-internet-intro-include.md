Azure 부하 분산 장치는 계층 4(TCP, UDP) 부하 분산 장치입니다. hello 부하 분산 장치 부하 분산 장치 집합의 가상 컴퓨터 또는 클라우드 서비스의 비정상 상태 서비스 인스턴스 간에 들어오는 트래픽을 분산 하 여 고가용성을 제공 합니다. Azure Load Balancer는 여러 포트, 여러 IP 주소 또는 둘 다에서 이러한 서비스를 제공할 수도 있습니다.

다음에 대해 부하 분산 장치를 구성할 수 있습니다.

* 컴퓨터의 부하를 분산 들어오는 인터넷 트래픽을 toovirtual (Vm). 이 시나리오에서 부하 분산 장치 tooa 이라고는 [인터넷 연결 부하 분산 장치](../articles/load-balancer/load-balancer-internet-overview.md)합니다.
* 가상 네트워크(VNet)의 VM 간, 클라우드 서비스의 VM 간 또는 크로스-프레미스 가상 네트워크의 온-프레미스 컴퓨터와 VM 간에 트래픽을 부하 분산합니다. 이 시나리오에서 부하 분산 장치 tooa 이라고는 [내부 부하 분산 장치 (ILB)](../articles/load-balancer/load-balancer-internal-overview.md)합니다.
* 외부 트래픽이 tooa 특정 VM 인스턴스를 전달 합니다.
