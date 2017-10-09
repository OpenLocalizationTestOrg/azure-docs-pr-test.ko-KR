hello 접근 방식을 tooAzure 끝점 약간 다르게 작동 hello 리소스 관리자 및 클래식 배포 모델 합니다. Hello 리소스 관리자 배포 모델에서 이제 Vm 내부 및 외부로 트래픽의 hello 흐름을 제어 하는 hello 유연성 toocreate 네트워크 필터가 있는 합니다. 이러한 필터를 사용 하면 toocreate 복잡 한 네트워킹 환경을 hello 클래식 배포 모델에서와 같이 간단한 끝점을 초과 합니다. 이 문서는 네트워크 보안 그룹과 클래식 끝점 사용 및 필터링 규칙 및 샘플 배포 시나리오 만들기와의 차이점을 간략히 설명합니다.

## <a name="overview-of-resource-manager-deployments"></a>리소스 관리자 배포 개요
Hello 클래식 배포 모델에서 끝점 네트워크 보안 그룹으로 대체 하 고 액세스 제어 목록 (ACL) 규칙입니다. 네트워크 보안 그룹 ACL 규칙 구현을 위한 빠른 단계는 다음과 같습니다.

* 네트워크 보안 그룹을 만듭니다.
* tooallow 트래픽을 거부 하거나, 네트워크 보안 그룹 ACL 규칙을 정의 합니다.
* 네트워크 보안 그룹 tooa 네트워크 인터페이스 또는 가상 네트워크 서브넷을 할당 합니다.

Tooalso 부호 포트 전달을 수행, 부하 분산 장치 tooplace VM 앞에 필요 하 고 NAT 규칙을 사용 합니다. 부하 분산 장치 및 NAT 규칙 구현을 위한 빠른 단계는 다음과 같습니다.

* 부하 분산 장치를 만듭니다.
* 백 엔드 풀을 만들고 Vm toohello 풀을 추가 합니다.
* 필요한 hello 포트 전달에 대 한 NAT 규칙을 정의 합니다.
* NAT 규칙 tooyour Vm을 할당 합니다.

## <a name="network-security-group-overview"></a>네트워크 보안 그룹 개요
네트워크 보안 그룹 Vm 서브넷 tooaccess 및 계층 있습니다 tooallow 특정 포트에 대 한 보안을 제공합니다. 일반적으로 항상 있는 Vm과 hello 외부 세계 간의 보안이 계층으로 제공 하는 네트워크 보안 그룹입니다. 네트워크 보안 그룹에는 적용 된 tooa 가상 네트워크 서브넷 또는 VM에 대 한 특정 네트워크 인터페이스 수 있습니다. 이제는 끝점 ACL 규칙을 만드는 대신에 네트워크 보안 그룹 ACL 규칙을 만듭니다. 이러한 ACL 규칙 단순히 끝점 tooforward 특정된 포트를 만드는 것 보다 많은 큰 제어를 제공 합니다. 자세한 내용은 [NSG(네트워크 보안 그룹)란?](../articles/virtual-network/virtual-networks-nsg.md)을 참조하세요.

> [!TIP]
> 네트워크 보안 그룹 toomultiple 서브넷 또는 네트워크 인터페이스를 할당할 수 있습니다. 1:1 매핑은 없습니다. 네트워크 보안 그룹 ACL 규칙의 공통 집합으로 만들고 toomultiple 서브넷 또는 네트워크 인터페이스를 적용할 수 있습니다. 네트워크 보안 그룹을 구독 전체에서는 tooresources 적용된 될 수 또한 (기반 [역할 기반 액세스 제어](../articles/active-directory/role-based-access-control-what-is.md)합니다.

## <a name="load-balancers-overview"></a>부하 분산 장치 개요
Hello 클래식 배포 모델에서 Azure 모든 hello 네트워크 주소 변환 (NAT)를 수행 하 고 포트 수에 대 한 클라우드 서비스에 전달 합니다. 끝점을 만들 때 hello 내부 포트 toodirect 트래픽의 함께 hello 외부 포트 tooexpose을 지정 합니다. 네트워크 보안 그룹은 단독으로 이 동일한 NAT 및 포트 전달을 수행하지 않습니다. 

tooallow 리소스 그룹에는 Azure 부하 분산 장치를 만들 전달, 이러한 포트에 대 한 NAT 규칙 toocreate 있습니다. Hello 부하 분산 장치는 세분화 된 다시 필요한 경우 충분 한 tooonly toospecific Vm을 적용 합니다. Azure hello 훨씬 더 많은 유연성 및 제어를 클라우드 서비스 끝점을 사용 하 여 달성 가능한 것 보다 네트워크 보안 그룹 ACL 규칙 tooprovide 함께 분산 장치 NAT 규칙 작업을 로드 합니다. 자세한 내용은 참조 hello [부하 분산 장치 개요](../articles/load-balancer/load-balancer-overview.md)합니다.

## <a name="network-security-group-acl-rules"></a>네트워크 보안 그룹 ACL 규칙
ACL 규칙을 통해 특정 포트, 포트 범위 또는 프로토콜을 기반으로 하는 VM 간에 전달될 수 있는 트래픽을 정의할 수 있습니다. 규칙은 tooindividual Vm 또는 tooa 서브넷에 할당 됩니다. 다음 스크린 샷 hello은 일반적인 웹 서버에 대 한 ACL 규칙의 예:

![네트워크 보안 그룹 ACL 규칙 목록](./media/virtual-machines-common-endpoints-in-resource-manager/example-acl-rules.png)

ACL 규칙 우선 순위 하는 메트릭을 지정-hello 값을 높게 hello, hello hello 우선 순위가 낮은에 따라 적용 됩니다. 모든 네트워크 보안 그룹에는 세 가지 기본 규칙을 명시적으로 Azure 네트워킹 트래픽을 toohandle hello 흐름 설계 `DenyAllInbound` hello 최종 원칙으로 합니다. 기본 ACL 규칙은 우선 순위가 낮은 toonot 지정한에 영향을 작성 한 규칙.

## <a name="assigning-network-security-groups"></a>네트워크 보안 그룹 지정
네트워크 보안 그룹 tooa 서브넷 또는 네트워크 인터페이스를 할당 합니다. 이 방법을 사용 하면 toobe tooonly가 특정 VM을 규칙에 ACL을 적용 하는 경우 필요에 따라 세분화 또는 공통 집합을 보장 액세스 제어 목록 규칙은 적용 된 tooall 서브넷의 Vm 일부:

![Nsg toonetwork 인터페이스 또는 서브넷을 적용](./media/virtual-machines-common-endpoints-in-resource-manager/apply-nsg-to-resources.png)

hello 네트워크 보안 그룹의 hello 동작 tooa 서브넷 또는 네트워크 인터페이스 할당에 따라 변경 되지 않습니다. 일반적인 배포 시나리오에 네트워크 보안 그룹의 모든 Vm 연결 된 toothat 서브넷 tooa 서브넷 tooensure 규정 준수를 할당 하는 hello 있습니다. 자세한 내용은 참조 [tooresources 그룹화 네트워크 보안을 적용](../articles/virtual-network/virtual-networks-nsg.md#associating-nsgs)합니다.

## <a name="default-behavior-of-network-security-groups"></a>네트워크 보안 그룹의 기본 동작
방법 및 시기를 네트워크 보안 그룹을 만드는에 따라 Windows Vm toopermit RDP 액세스 TCP 포트 3389에 대해 기본 규칙을 만들 수 있습니다. Linux VM에 대한 기본 규칙은 TCP 포트 22에 대한 SSH 액세스를 허용합니다. 이러한 자동 ACL 규칙은 다음 조건 hello에서 만들어집니다.

* Hello 포털을 통해 Windows VM을 만들고 hello 기본 동작 toocreate 네트워크 보안 그룹에 동의 하는 경우 ACL 규칙 tooallow TCP 포트 3389 (RDP)이 생성 됩니다.
* Hello 포털을 통해 Linux VM을 만들고 hello 기본 동작 toocreate 네트워크 보안 그룹에 동의 하는 경우에 ACL 규칙 tooallow TCP 포트 22 (SSH) 만들어집니다.

기타 모든 조건에서는 이러한 기본 ACL 규칙이 만들어지지 않습니다. Hello 적절 한 ACL 규칙을 만들지 않고 tooyour VM을 연결할 수 없습니다. 이러한 조건은 일반 동작을 수행 하는 hello를 같습니다.

* 별도 작업 toocreating hello VM으로 hello 포털을 통해 네트워크 보안 그룹을 만듭니다.
* PowerShell, Azure CLI, Rest Api 등을 통해 프로그래밍 방식으로 네트워크 보안 그룹 만들기.
* VM을 만들고 tooan 네트워크 보안 그룹에 아직 없는 hello 적절 한 ACL 규칙 정의 하는 기존 할당 합니다.

경우 앞에 오는 모든 hello, 해야 toocreate ACL 규칙 VM tooallow hello 적절 한 원격 관리 연결에 대 한 합니다.

## <a name="default-behavior-of-a-vm-without-a-network-security-group"></a>네트워크 보안 그룹이 없는 VM의 기본 동작
네트워크 보안 그룹을 만들지 않고 VM을 만들 수 있습니다. 이러한 상황에서는 tooyour VM을 연결할 수 있는 ACL 규칙을 만들지 않고 RDP 또는 SSH를 사용 하 여 합니다. 마찬가지로, 웹 서비스를 포트 80에 설치한 경우, 해당 서비스를 원격으로 자동 액세스할 수 있습니다. hello VM에는 모든 포트가 열려 있습니다.

> [!NOTE]
> 모든 원격 연결에 대 한 순서는 공용 IP 주소 할당 tooa VM toohave를 보내야합니다. Hello 서브넷 또는 네트워크 인터페이스에 대 한 네트워크 보안 그룹 고 다니지 않아도 hello VM tooany 외부 트래픽이 노출 하지 않습니다. hello 기본 동작은 hello 포털을 통해 VM을 만들 때에 새 공용 IP toocreate입니다. PowerShell, Azure CLI 또는 Resource Manager 템플릿과 같은 기타 모든 형식의 VM을 만드는 경우 명시적으로 요청하지 않으면 공용 IP를 자동으로 생성하지 않습니다. 네트워크 보안 그룹 toocreate hello 포털을 통해 hello 기본 동작 이기도합니다. 이 기본 작업은 노출된 VM에 네트워크 필터링이 준비되지 않은 상황에 빠지지 않아야 함을 의미합니다.

## <a name="understanding-load-balancers-and-nat-rules"></a>부하 분산 장치 및 NAT 규칙 이해
Hello 클래식 배포 모델에서 포트 전달도 수행 하는 끝점을 만들 수 있습니다. Hello 클래식 배포 모델에는 VM을 만들 때 RDP 또는 SSH에 대 한 ACL 규칙이 자동으로 만들어집니다. 이러한 규칙은 TCP 포트 3389 또는 TCP 포트 22 각각 노출 하지 외부 세계 toohello 합니다. 대신, 우선 순위가 높은 TCP 포트를 노출지 않습니다 toohello 적절 한 내부 포트를 매핑하는. 비슷한 방식으로 사용자 고유의 ACL 규칙을 만들 수도 수, 노출 같은 TCP에 대 한 웹 서버는 외부 세계 4280 toohello 포트. 이러한 ACL 규칙 및 hello 스크린 샷 hello 클래식 포털에서 다음에 포트 매핑을 확인할 수 있습니다.

![클래식 끝점을 사용하여 포트 전달](./media/virtual-machines-common-endpoints-in-resource-manager/classic-endpoints-port-forwarding.png)

네트워크 보안 그룹을 사용하는 경우 포트 전달 함수는 부하 분산 장치에서 처리합니다. 자세한 내용은 [Azure의 부하 분산 장치](../articles/load-balancer/load-balancer-overview.md)를 참조하세요. hello 다음 보여 주는 예제는 부하 분산 장치 NAT 규칙 tooperform 포트 전달을 TCP 포트 4222 toohello 내부 TCP 포트 22 VM:

![포트 전달에 대한 부하 분산 장치 NAT 규칙](./media/virtual-machines-common-endpoints-in-resource-manager/load-balancer-nat-rules.png)

> [!NOTE]
> 부하 분산 장치를 구현할 때 일반적으로 할당 하지 않으면 hello VM 자체 공용 IP 주소입니다. 대신, hello 부하 분산 장치에 공용 IP 주소 할당 tooit 있습니다. 보내야 toocreate에 네트워크 보안 그룹 및 ACL 규칙 toodefine hello 트래픽 흐름을 VM 축소 합니다. hello 부하 분산 장치 NAT 규칙은 어떤 포트 hello 부하 분산 장치 및 hello 백 엔드 Vm 간에 어떻게 분포 get을 통해 허용 된 toodefine 하기만 합니다. 따라서 toocreate NAT 규칙 hello 부하 분산 장치를 통해 트래픽 tooflow 필요합니다. tooallow hello 트래픽 tooreach hello VM을 네트워크 보안 그룹 ACL 규칙을 만듭니다.
