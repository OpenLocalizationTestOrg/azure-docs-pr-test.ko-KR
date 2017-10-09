IaaS 가상 컴퓨터 (Vm)와 가상 네트워크에 PaaS 역할 인스턴스와 자동으로 수신 개인 IP 주소 범위에서 지정 하는 hello 서브넷에 연결 되어 있는에 기반 합니다. 해당 주소는 서비스 해제 된 전까지 hello Vm 및 역할 인스턴스에 의해 유지 됩니다. Hello Azure 포털 또는 PowerShell을 hello Azure CLI에서 중지 하 여 VM 또는 역할 인스턴스를 서비스 해제 있습니다. 이러한 경우 hello hello 않을 수도 있는 Azure 인프라에서에서 사용 가능한 IP 주소 받도록 hello VM 또는 역할 인스턴스 다시 시작 되 면 동일한 이전에 이었습니다. Hello VM 또는 hello 게스트 운영 체제에서 역할 인스턴스를 종료 하면 이전의 hello IP 주소가 유지 됩니다.  

경우에 따라 대상 VM 또는 역할 인스턴스 toohave 고정 IP 주소 예를 들어 VM은 toorun DNS 또는 도메인 컨트롤러가 될입니다. 이렇게 하려면 고정 개인 IP 주소를 설정합니다.

