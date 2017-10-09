VPN 연결을 통해 tooa 가상 컴퓨터를 연결 하는 데 문제가 hello 다음 사항을 확인.

- VPN 연결이 성공했는지 확인합니다.
- Toohello hello VM에 대 한 개인 IP 주소를 연결 하 고 있는지 확인 합니다.
- Toohello VM에 연결할 수 있는 경우 hello 개인 IP를 사용 하 여 주소, 하지만 컴퓨터 이름을 하지 hello을 DNS를 제대로 구성 했는지 확인 합니다. 이름 확인이 VM에서 작동하는 방법에 대한 자세한 내용은 [VM에서 이름 확인](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)을 참조하세요.

지점 및 사이트를 통해 연결할 때 다음 추가 항목 hello를 확인 합니다.

- 'Ipconfig' toocheck hello toohello 이더넷 어댑터 연결 중인 hello 컴퓨터에 할당 된 IPv4 주소를 사용 합니다. Hello IP 주소는 hello에 연결 하는 VNet의 hello 주소 범위 또는 프로그램 VPNClientAddressPool의 hello 주소 범위, 이것은 참조 tooas 겹치는 주소 공간입니다. 주소 공간은이 방식으로 중첩 하는 경우 네트워크 트래픽이 hello Azure까지 연장 되지 않으면, hello 로컬 네트워크의 상태를 유지 합니다.
- Hello DNS 서버 IP 주소는 hello VNet에 대해 지정 된 후 해당 hello VPN 클라이언트 구성 패키지 생성 된 것을 확인 합니다. Hello DNS 서버 IP 주소를 업데이트 한 경우 생성 하 고 새 VPN 클라이언트 구성 패키지를 설치 합니다.

RDP 연결 문제를 해결 하는 방법에 대 한 자세한 내용은 참조 [문제를 해결 하는 원격 데스크톱 연결 tooa VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)합니다.
