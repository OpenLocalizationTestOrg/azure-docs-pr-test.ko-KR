# <a name="platform-supported-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 마이그레이션 플랫폼 지원
이 문서에서는 어떻게 우리는 마이그레이션할 수 있도록 인프라의 hello 클래식 tooResource 관리자 배포 모델에서 서비스 (IaaS) 리소스 그룹으로 설명 합니다. [Azure Resource Manager 기능 및 이점](../articles/azure-resource-manager/resource-group-overview.md)에 대해 자세히 알아볼 수 있습니다. 에서는 가상를 사용 하 여 구독에서 함께 사용 하는 hello 두 가지 배포 모델에서 tooconnect 리소스 네트워크 사이트 간 게이트웨이 방법을 자세히 설명 합니다.

## <a name="goal-for-migration"></a>마이그레이션 목표
Resource Manager는 템플릿을 사용하여 복잡한 응용 프로그램을 배포할 수 있도록 지원하며 VM 확장을 사용하여 가상 컴퓨터를 구성하고 액세스 관리와 태깅을 통합합니다. Azure Resource Manager는 가용성 집합에 가상 컴퓨터에 대해 확장성 있는 병렬 배포를 포함합니다. 새로운 배포 모델이 hello도 제공 하지 계산, 네트워크 및 저장소의 수명 주기 관리 독립적으로 합니다. 마지막으로 가상 네트워크의 가상 컴퓨터의 hello 적용 함께 기본적으로 보안 설정에 대 한 포커스가입니다.

계산, 네트워크 및 Azure 리소스 관리자에서 저장소에 대 한 hello 클래식 배포 모델에서 거의 모든 hello 기능을 사용할 수 있습니다. hello 새로운 기능이 Azure 리소스 관리자에서 toobenefit, 기존 hello 클래식 배포 모델에서 배포를 마이그레이션할 수 있습니다.

## <a name="supported-resources-for-migration"></a>마이그레이션에 지원되는 리소스
이들 클래식 IaaS 리소스는 마이그레이션 시 지원됩니다.

* 가상 컴퓨터
* 가용성 집합
* 클라우드 서비스
* 저장소 계정
* 가상 네트워크
* VPN 게이트웨이
* Express 경로 게이트웨이 _(hello에만 가상 네트워크와 동일한 구독)_
* 네트워크 보안 그룹 
* 경로 테이블 
* 예약된 IP 

## <a name="supported-scopes-of-migration"></a>지원되는 마이그레이션 범위
계산, 네트워크 및 저장소 리소스의 toocomplete 마이그레이션은 4 가지가 있습니다. 다음과 같습니다. 

* 가상 컴퓨터 마이그레이션(가상 네트워크가 아님)
* 가상 컴퓨터 마이그레이션(가상 네트워크에서)
* 저장소 계정 마이그레이션
* 연결되지 않은 리소스(네트워크 보안 그룹, 경로 테이블 및 예약된 IP)

### <a name="migration-of-virtual-machines-not-in-a-virtual-network"></a>가상 컴퓨터 마이그레이션(가상 네트워크가 아님)
Hello 리소스 관리자 배포 모델에서 보안은 기본적으로 응용 프로그램에 적용 됩니다. 모든 Vm toobe hello 리소스 관리자 모델에는 가상 네트워크에 필요합니다. Azure 플랫폼 다시 시작 hello (`Stop`, `Deallocate`, 및 `Start`) hello 마이그레이션의 일환으로 Vm을 hello 합니다. 가상 컴퓨터를 hello hello 가상 네트워크 계정으로 마이그레이션에 대 한 두 가지 옵션이 있습니다.

* Hello 플랫폼 toocreate 새 가상 네트워크를 요청 하 고 hello 새 가상 네트워크로 hello 가상 컴퓨터를 마이그레이션할 수 있습니다.
* 리소스 관리자의 기존 가상 네트워크에 hello 가상 컴퓨터를 마이그레이션할 수 있습니다.

> [!NOTE]
> 이 마이그레이션 범위에 평면 관리 작업 둘 다 hello 및 데이터 평면 작업 hello hello 마이그레이션 중 한 기간에 대 한 허용 되지 않습니다.
>
>

### <a name="migration-of-virtual-machines-in-a-virtual-network"></a>가상 컴퓨터 마이그레이션(가상 네트워크에서)
대부분의 VM 구성에 대 한 hello 메타 데이터만 hello 리소스 관리자 및 클래식 배포 모델 간의 마이그레이션 중입니다. 실행 중인 기본 Vm hello hello 동일한 하드웨어에 동일한 네트워크, 항목과 동일 hello hello 저장소입니다. hello 평면 관리 작업이 시간 hello 마이그레이션 중의 특정 기간에 대 한 허용 되지 않을 수 있습니다. 그러나 hello 데이터 평면 toowork를 계속합니다. 즉, Vm (클래식) 상에 서 실행 되는 응용 프로그램 hello 마이그레이션하는 동안 가동 중지 시간을 유발 하지 않습니다.

구성을 따르고 hello 현재 지원 되지 않습니다. 이 구성의 일부 Vm 가동 중지 시간이 발생할 수 지원 hello 앞에 추가 되 면 (이동 중지를 통해 할당을 취소 하 고 VM 작업을 다시 시작)입니다.

* 단일 클라우드 서비스에 둘 이상의 가용성 집합이 있습니다.
* 단일 클라우드 서비스에서 하나 이상의 가용성 집합과 가용성 집합에 없는 VM이 있습니다.

> [!NOTE]
> 이 마이그레이션 범위에 hello 관리 평면 hello 마이그레이션 중 한 기간에 허용 되지 않을 수 있습니다. 앞서 설명한 특정 구성의 경우 데이터 평면 가동 중지 시간이 발생합니다.
>
>

### <a name="storage-accounts-migration"></a>저장소 계정 마이그레이션
tooallow 원활 하 게 마이그레이션할 클래식 저장소 계정에서 리소스 관리자 Vm을 배포할 수 있습니다. 이 기능을 사용하면 계산 및 네트워크 리소스를 저장소 계정과 상관없이 마이그레이션할 수 있으며 이러한 방식이 바람직합니다. 가상 컴퓨터와 가상 네트워크를 통해 마이그레이션한 후 저장소 계정 toocomplete hello 마이그레이션 프로세스를 통해 toomigrate가 필요 합니다.

> [!NOTE]
> hello 리소스 관리자 배포 모델에는 기본 이미지와 디스크의 hello 개념이 되어 있지 않습니다. Hello 저장소 계정 마이그레이션된, 클래식 이미지에 있고 디스크 hello 리소스 관리자 스택에서 하지만 백업 hello에 표시 되지 않는 경우 Vhd hello 저장소 계정에 남아 있습니다.
>
>

### <a name="unattached-resources-network-security-groups-route-tables--reserved-ips"></a>연결되지 않은 리소스(네트워크 보안 그룹, 경로 테이블 및 예약된 IP)
네트워크 보안 그룹, 경로 테이블 및 하지 않은 예약 된 Ip tooany 가상 컴퓨터와 가상 네트워크가 마이그레이션할 수 있습니다 독립적으로 연결 합니다.

<br>

## <a name="unsupported-features-and-configurations"></a>지원되지 않는 기능 및 구성
현재는 일부 기능 및 구성 집합을 지원하지 않습니다. hello 다음 섹션으로 권장 되는 주위를 설명 합니다.

### <a name="unsupported-features"></a>지원되지 않는 기능
같은 기능 hello 현재 지원 되지 않습니다. 필요에 따라 이러한 설정을 제거 지정, hello Vm 마이그레이션 및 다음 hello 리소스 관리자 배포 모델에서 hello 설정을 다시 설정 합니다.

| 리소스 공급자 | 기능 | 권장 사항 |
| --- | --- | --- |
| Compute |연결되지 않은 가상 컴퓨터 디스크 | 이러한 디스크 뒤 hello VHD blob hello 저장소 계정에서 마이그레이션할 때 마이그레이션된 됩니다. |
| 계산 |가상 컴퓨터 이미지 | 이러한 디스크 뒤 hello VHD blob hello 저장소 계정에서 마이그레이션할 때 마이그레이션된 됩니다. |
| 네트워크 |끝점 ACL. | 끝점 ACL을 제거하고 마이그레이션을 다시 시도합니다. |
| 네트워크 |ExpressRoute 게이트웨이와 VPN Gateway가 모두 있는 가상 네트워크  | 마이그레이션을 시작 하기 전에 hello VPN 게이트웨이 제거 하 고 마이그레이션이 완료 되 면 hello VPN 게이트웨이 다시 만듭니다. [ExpressRoute 마이그레이션](../articles/expressroute/expressroute-migration-classic-resource-manager.md)에 대해 자세히 알아봅니다.|
| 네트워크 |권한 부여 링크를 사용하는 ExpressRoute  | 마이그레이션을 시작 하기 전에 hello ExpressRoute 회로 toovirtaul 네트워크 연결을 제거한 다음 마이그레이션이 완료 되 면 hello 연결을 다시 만드십시오. [ExpressRoute 마이그레이션](../articles/expressroute/expressroute-migration-classic-resource-manager.md)에 대해 자세히 알아봅니다. |
| 네트워크 |응용 프로그램 게이트웨이 | 마이그레이션을 시작 하기 전에 hello 응용 프로그램 게이트웨이 제거 하 고 마이그레이션이 완료 되 면 hello 응용 프로그램 게이트웨이 다시 만듭니다. |
| 네트워크 |VNet 피어링을 사용하는 가상 네트워크 | 가상 네트워크 tooResource 관리자 마이그레이션합니다 다음 피어 투 피어 합니다. [VNet 피어링](../articles/virtual-network/virtual-network-peering-overview.md)에 대해 자세히 알아보세요. | 

### <a name="unsupported-configurations"></a>지원되지 않는 구성
구성을 따르고 hello 현재 지원 되지 않습니다.

| 부여 | 구성 | 권장 사항 |
| --- | --- | --- |
| 리소스 관리자 |클래식 리소스에 대한 RBAC(역할 기반 액세스 제어) |Hello hello 리소스의 URI가 마이그레이션 후 수정 하므로 마이그레이션 후 toohappen 해야 하는 hello RBAC 정책 업데이트를 계획 하는 것이 좋습니다. |
| 계산 |VM과 연결된 여러 서브넷 |Hello 서브넷 configuration tooreference만 서브넷을 업데이트 합니다. |
| 계산 |Tooa 가상 네트워크에 속해 있지만 할당 하는 명시적 서브넷이 없는 가상 컴퓨터 |필요에 따라 VM hello를 삭제할 수 있습니다. |
| 계산 |경고, 자동 크기 조정 정책이 있는 가상 컴퓨터 |hello 마이그레이션을 통해 이동 하 고 이러한 설정이 삭제 됩니다. 마이그레이션 hello 수행 전에 사용자 환경을 평가 하는 것이 좋습니다. 또는 마이그레이션이 완료 된 후 hello 경고 설정을 재구성할 수 있습니다. |
| 계산 |XML VM 확장(BGInfo 1.*, Visual Studio 디버거, 웹 배포 및 원격 디버깅) |이 기능은 지원되지 않습니다. Hello, toocontinue 마이그레이션 가상 컴퓨터에서에서 이러한 확장을 제거 하거나 hello 마이그레이션 프로세스 중 자동으로 삭제 것이 좋습니다. |
| 계산 |프리미엄 저장소를 사용한 부팅 진단 |마이그레이션을 사용 하 여 계속 하기 전에 hello Vm에 대 한 부트 진단 기능을 사용 하지 않도록 설정 합니다. Hello 리소스 관리자 스택에서 부트 진단을 hello 마이그레이션이 완료 된 후에 다시 활성화할 수 있습니다. 또한 스크린샷 및 직렬 로그에 대해 사용되는 blob은 그러한 blob에 대해 요금이 부과되지 않도록 삭제해야 합니다. |
| 계산 |웹/작업자 역할이 포함된 클라우드 서비스 |현재는 지원되지 않습니다. |
| 네트워크 |가상 컴퓨터와 웹/작업자 역할이 포함된 가상 네트워크 |현재는 지원되지 않습니다. |
| Azure 앱 서비스 |앱 서비스 환경이 포함된 가상 네트워크 |현재는 지원되지 않습니다. |
| Azure HDInsight |HDInsight Services가 포함된 가상 네트워크 |현재는 지원되지 않습니다. |
| Microsoft Dynamics Lifecycle Services |Dynamics Lifecycle Services에서 관리하는 가상 컴퓨터가 포함된 가상 네트워크 |현재는 지원되지 않습니다. |
| Azure AD Domain Services |Azure AD Domain Services가 포함된 가상 네트워크 |현재는 지원되지 않습니다. |
| Azure RemoteApp |Azure RemoteApp 배포가 포함된 가상 네트워크 |현재는 지원되지 않습니다. |
| Azure API 관리 |Azure API Management 배포가 포함된 가상 네트워크 |현재는 지원되지 않습니다. toomigrate hello IaaS VNET hello VNET의 hello 가동 중지 시간 없는 작업 인 API 관리 배포를 변경 하십시오. |
| 계산 |온-프레미스 DNS 서버에서 전송 연결 중인 VPN Gateway 또는 ExpressRoute 게이트웨이가 있는 VNET을 포함하는 Azure Security Center 확장 |자동으로 azure 보안 센터의 보안에 가상 컴퓨터 toomonitor 확장을 설치 하 고 경고를 생성 합니다. 이러한 확장 일반적으로 가져올 경우 자동으로 설치 hello 구독에서 Azure 보안 센터 정책 hello를 사용 합니다. ExpressRoute 게이트웨이 마이그레이션은 현재 지원되지 않고 전송 연결된 VPN Gateway는 온-프레미스 액세스를 상실합니다. 게이트웨이 또는 전송 연결 VPN 게이트웨이 마이그레이션 인터넷 액세스 tooVM 저장소 계정 toobe hello 마이그레이션 커밋으로 계속 하는 경우 손실 하면 express 경로 삭제 합니다. 대로 hello 게스트 에이전트 상태 blob 채울 수 없습니다. 이런 경우에 hello 마이그레이션 진행 되지 않습니다. Hello 구독에서 Azure 보안 센터 정책을 toodisable 마이그레이션 사용 하 여 계속 진행 하기 전에 3 시간 좋습니다. |

