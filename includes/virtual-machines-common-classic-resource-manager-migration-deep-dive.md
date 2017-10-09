## <a name="meaning-of-migration-of-iaas-resources-from-hello-classic-deployment-model-tooresource-manager"></a>Hello 클래식 배포 모델 tooResource 관리자에서에서 IaaS 리소스의 마이그레이션의 의미
Hello 세부 정보로 드릴 다운 म 전에 hello 차이 hello는 IaaS 리소스에 대 한 작업 데이터 평면과 관리 평면에서 살펴보겠습니다.

* *관리/제어 가능 평면* 리소스를 수정 하기 위한 hello 관리/제어 가능 평면 또는 hello API에 발생 하는 hello 호출에 설명 합니다. 예를 들어 VM 만들기, VM을 다시 시작 및 새 서브넷과 가상 네트워크를 업데이트 하는 등의 작업 리소스를 실행 하는 hello를 관리 합니다. Toohello 인스턴스 연결에 직접 영향을 하지 않습니다.
* *데이터 평면* (응용 프로그램) hello 응용 프로그램 자체의 hello 런타임을 설명 하 고 hello Azure API를 통해 이동 하지 못하는 인스턴스와 상호 작용을 포함 합니다. 웹 사이트에 액세스하거나 실행 중인 SQL Server 인스턴스 또는 mongoDB 서버에서 데이터를 가져오는 경우 데이터 평면 또는 응용 프로그램 상호 작용으로 간주됩니다. 저장소 계정에서 blob를 복사 하 고 hello 가상 컴퓨터에 공용 IP 주소 tooRDP 또는 SSH 액세스 데이터 평면은 있습니다. 이러한 작업 계산, 네트워킹 및 저장소에서 실행 하는 hello 응용 프로그램을 유지 합니다.

Hello 백그라운드 hello 데이터 평면 hello 클래식 배포 모델 및 리소스 관리자 스택의 간의 같은 hello 됩니다. 마이그레이션 프로세스 중 hello 리소스 관리자 스택의 hello 클래식 배포 모델 toothat에서 hello 리소스의 hello 표현으로 변환 했습니다. 결과적으로, 해야 합니다 toouse 새 도구, Api, Sdk toomanage hello 리소스 관리자 스택의 리소스.

![관리/제어 평면 및 데이터 평면 간의 차이를 보여주는 스크린샷](../articles/virtual-machines/media/virtual-machines-windows-migration-classic-resource-manager/data-control-plane.png)


> [!NOTE]
> 일부 마이그레이션 시나리오에서는 Azure 플랫폼 중지 hello 할당을 취소, 및 가상 컴퓨터를 다시 시작 합니다. 이 경우 데이터 평면 가동이 잠시 중지됩니다.
>

## <a name="hello-migration-experience"></a>hello 마이그레이션 환경
Hello 마이그레이션 경험을 시작 하기 전에 hello 다음 것이 좋습니다.

* 지원 되지 않는 기능이 나 구성 toomigrate hello 자원을 사용 하지 않는 것을 확인 합니다. 일반적으로 hello 플랫폼 이러한 문제를 감지 하 고 오류를 생성 합니다.
* Vm 가상 네트워크에 없는 경우 이러한 중지 되며 hello의 일부 준비 작업으로 할당 취소 합니다. Toolose hello 공용 IP 주소를 사용 하지 않으려는 경우 hello를 트리거하기 전에 hello IP 주소를 예약에 작업을 준비 합니다. 그러나 hello Vm 가상 네트워크에 있는 경우 하지 중지 되며 할당 취소 됩니다.
* 마이그레이션하는 동안 발생할 수 있는 예기치 않은 오류 tooaccommodate 업무 외 시간 동안 마이그레이션을 계획 합니다.
* PowerShell, CLI (명령줄 인터페이스) 명령 또는 REST Api toomake hello 준비 단계 후 유효성 검사에 대 한 보다 쉽게 완료 되기를 사용 하 여 hello Vm의 현재 구성을 다운로드 합니다.
* Hello 마이그레이션을 시작 하기 전에 자동화/해결해줍니다 스크립트 toohandle hello 리소스 관리자 배포 모델을 업데이트 합니다. 필요에 따라 수행할 수 있습니다 hello 리소스의 상태를 준비 하는 hello 경우 GET 작업입니다.
* Hello 클래식는 IaaS 리소스에 구성 된 하 고 hello 마이그레이션이 완료 된 후 계획 하는 hello RBAC 정책을 평가 합니다.

hello 마이그레이션 워크플로 다음과 같습니다.

![Hello 마이그레이션 워크플로 보여 주는 스크린샷](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-workflow.png)

> [!NOTE]
> Hello 다음 섹션에서에서 설명 하는 모든 hello 작업은 idempotent입니다. 지원 되지 않는 기능 또는 구성 오류 이외의 문제가 있는 경우 것이 좋습니다 hello을 다시 시도 준비, 중단 또는 작업을 커밋하기 합니다. Azure 플랫폼 hello hello 작업을 다시 시도합니다.
>
>

### <a name="validate"></a>유효성 검사
유효성 검사 작업 hello hello hello 마이그레이션 프로세스의 첫 번째 단계입니다. hello이 단계의 목적은 toomigrate hello 클래식 배포 모델에서 선택 하 고 hello 리소스를 마이그레이션 수 있는 경우 성공/실패를 반환 하는 hello 리소스의 tooanalyze hello 상태입니다.

선택 하면 hello 가상 네트워크는 클라우드 서비스 (가상 네트워크에 없는) 마이그레이션용 toovalidate 되도록 합니다.

* Hello 리소스의 마이그레이션 수 없는 경우 hello Azure 플랫폼 이유 마이그레이션에 지원 되지 않습니다에 대 한 모든 hello 이유를 나열 합니다.

#### <a name="checks-not-done-in-validate"></a>유효성 검사에서 수행되지 않은 검사

유효성 검사 작업에만 hello 클래식 배포 모델의 hello 리소스의 hello 상태 분석 합니다. 모든 오류 및 hello 클래식 배포 모델에서 toovarious 구성으로 인해 지원 되지 않는 시나리오에 대해 검사할 수 있습니다. Hello Azure 리소스 관리자를 마이그레이션하는 동안 스택 hello 리소스에 적용할 수 있습니다 하는 모든 문제에 대 한 가능한 toocheck는 없습니다. 이러한 문제는 hello 리소스 변환 hello 다음 단계에서의 마이그레이션, 즉, 준비를 진행 하는 경우에 확인 됩니다. hello 아래 표에 모든 hello 문제 체크 인 유효성 검사 되지 않습니다.


|유효성 검사에 없는 네트워킹 검사|
|-|
|ER 및 VPN Gateway를 포함한 Virtual Network|
|연결이 끊어진 상태의 Virtual Network 게이트웨이 연결|
|모든 ER 회선이 미리 마이그레이션된 tooAzure 리소스 관리자 스택에서 사용 되 고|
|고정 공용 IP, 동적 공용 IP, Load Balancer, 네트워크 보안 그룹, 경로 테이블, 네트워크 인터페이스 등 네트워킹 리소스에 대한 Azure 리소스 관리자 할당량 검사 |
| 모든 부하 분산 장치 규칙이 배포/VNET에서 유효한지 검사 |
| 동일한 hello에 중지-할당 취소 된 Vm 간에 충돌 하는 개인 Ip에 대 한 확인 VNET |

### <a name="prepare"></a>준비
hello 준비 작업이 hello hello 마이그레이션 프로세스의 두 번째 단계입니다. 이 단계의 목표 hello hello toosimulate hello 변환 클래식 배포 모델 tooResource Manager 리소스에서 리소스를 IaaS 됩니다 고 제공이 나란히 드립니다 toovisualize 합니다.

> [!NOTE] 
> 클래식 리소스는 이 단계에서 수정되지 않습니다. 안전 단계 toorun 마이그레이션을 시도 하는 경우입니다. 

Hello 가상 네트워크 또는 hello 클라우드 서비스 (경우 선택이 가상 네트워크) 마이그레이션에 대 한 tooprepare 되도록.

* Hello 리소스의 마이그레이션 수 없는 경우 Azure 플랫폼 hello hello 마이그레이션 프로세스를 중지 하 고 hello 이유 hello 작업이 실패 했습니다 준비 하는 이유를 나열 합니다.
* Hello 리소스 마이그레이션 수 있는 경우 hello Azure 플랫폼을 먼저 마이그레이션되고 hello 리소스에 대 한 hello 관리 평면 작업 아래로 잠급니다. 예를 들어 수 tooadd 마이그레이션되고 데이터 디스크 tooa VM 없는 합니다.

hello Azure 플랫폼 다음 메타 데이터의 마이그레이션만 hello에서에서 시작 hello 리소스를 마이그레이션에 대 한 클래식 배포 모델 tooResource 관리자 합니다.

Hello 준비 후 작업이 완료 된를 클래식 배포 모델 및 리소스 관리자 모두의 hello 리소스 시각화 hello 선택할 수 있습니다. Hello 클래식 배포 모델의 모든 클라우드 서비스에 대 한 hello Azure 플랫폼 만듭니다 hello 패턴이 있는 리소스 그룹 이름은 `cloud-service-name>-Migrated`합니다.

> [!NOTE]
> 마이그레이션된 리소스에 대 한 만든 리소스 그룹의 가능한 tooselect hello 이름이 아닙니다 (예: "-마이그레이션") 하지만 마이그레이션이 완료 된 후에 Azure 리소스 관리자 이동 기능 toomove 리소스 tooany 리소스 그룹을 사용할 수 있습니다. 이 참조에 대 한 자세한 tooread [리소스 toonew 리소스 그룹이 나 구독 이동](../articles/resource-group-move-resources.md)

다음은 성공적 준비 작업 후 hello 결과 보여 주는 두 개의 화면입니다. 첫 번째 화면 hello 원래 클라우드 서비스를 포함 하는 리소스 그룹을 보여 줍니다. 두 번째 화면 hello에 새로운 표시 "-마이그레이션" hello 해당 하는 Azure 리소스 관리자 리소스를 포함 하는 리소스 그룹입니다.

![포털 클래식 클라우드 서비스를 보여 주는 스크린샷](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-classic.png)

![준비 중인 포털 Azure Resource Manager 리소스를 보여주는 스크린샷](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-arm.png)

Hello 준비 단계 완료 된 후 리소스 백그라운드를 살펴보면 다음과 같습니다. Hello 리소스는 hello 데이터 평면 같은 hello 됩니다. Hello 관리 평면 (클래식 배포 모델) 및 hello 제어 평면 (리소스 관리자)에 표시 됩니다.

![준비 단계에 대 한 hello 백그라운드](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-prepare.png)

> [!NOTE]
> 클래식 Virtual Network에 없는 Virtual Machines는 이 마이그레이션 단계에서 중지 또는 할당 취소됩니다.
>

### <a name="check-manual-or-scripted"></a>검사(수동 또는 스크립트)
Hello 확인 단계에서 이전 toovalidate hello 마이그레이션 제대로 표시 되는지를 다운로드 한 hello 구성을 선택적으로 사용할 수 있습니다. Toohello 포털과 자리를 검사 hello 속성 및 리소스 toovalidate 메타 데이터 마이그레이션 좋아 보입니다에 서명할 수 있습니다.

가상 네트워크를 마이그레이션하는 경우 가상 컴퓨터의 구성이 대부분 다시 시작됩니다. 해당 Vm에서 응용 프로그램에 대 한 hello 응용 프로그램을 여전히 실행 되 고 있는지 확인할 수 있습니다.

모니터링/자동화 및 작업 스크립트 toosee hello Vm 및 업데이트 된 스크립트가 올바르게 작동 하는 경우 예상 대로 작동 되 면 테스트할 수 있습니다. Hello 리소스의 상태를 준비 하는 hello 경우 GET 작업 에서만 지원 됩니다.

Toocommit hello 마이그레이션이 필요 하면 되기까지의 집합 시간 창이 있습니다. 이 상태를 원하는 시간 동안 유지할 수 있습니다. 그러나 hello 관리 평면 중단 하거나 커밋할 때까지 이러한 리소스에 대해 잠겨 있습니다.

모든 문제를 참조 하는 경우 항상 hello 마이그레이션 중단 고 이동할 수 있습니다 다시 toohello 클래식 배포 모델입니다. 이전 단계로 이동 후 hello 클래식 배포 모델에서 해당 Vm에 대 한 일반 작업을 다시 시작할 수 있도록 hello Azure 플랫폼이 hello 리소스에 대 한 hello 평면 관리 작업을 열립니다.

### <a name="abort"></a>중단
중단은 toorevert 변경 toohello 클래식 배포 모델을 사용 하 고 hello 마이그레이션을 중지할 수 있는 단계는 선택 사항입니다. 이 작업에는 hello hello 이전 준비 단계에서 만든 리소스 관리자 메타 데이터 리소스를 삭제 합니다. 

![중단 단계에 대 한 hello 백그라운드](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-abort.png)


> [!NOTE]
> Hello 커밋 작업이 발생 한 후이 작업을 실행할 수 없습니다.     
>

### <a name="commit"></a>커밋
Hello 유효성 검사를 완료 한 후에 hello 마이그레이션을 커밋할 수 있습니다. 리소스 클래식 배포 모델에 더 이상 표시 되지 않습니다 및 hello 리소스 관리자 배포 모델 에서만 사용할 수 있습니다. hello 마이그레이션된 해당 리소스를 관리할 수 있습니다 hello 새 포털에만.

> [!NOTE]
> 이 작업은 멱등원 작업입니다. 실패 한 경우 hello 작업을 다시 시도 하는 것이 좋습니다. Toofail를 계속 하는 경우 지원 티켓을 만드세요 만들거나 포럼 게시물의 ClassicIaaSMigration 태그와 우리의 [VM 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows)합니다.
>
>

![커밋 단계에 대 한 hello 백그라운드](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-commit.png)

## <a name="where-toobegin-migration"></a>여기서 toobegin 마이그레이션?

다음은 보여 주는 순서도 방법을 tooproceed 마이그레이션

![Hello 마이그레이션 단계를 보여 주는 스크린샷](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="translation-of-classic-deployment-model-tooazure-resource-manager-resources"></a>클래식 배포 모델 tooAzure 리소스 관리자 리소스의 번역
다음 표에 hello에 hello 클래식 배포 모델 및 hello 리소스를 나타내는 리소스 관리자를 찾을 수 있습니다. 다른 기능 및 리소스는 현재 지원되지 않습니다.

| 클래식 표현 | Resource Manager 표현 | 자세한 정보 |
| --- | --- | --- |
| 클라우드 서비스 이름 |DNS 이름 |마이그레이션하는 동안 새 리소스 그룹 이름 지정 패턴 hello 포함 된 모든 클라우드 서비스에 대 한 만들어집니다 `<cloudservicename>-migrated`합니다. 이 리소스 그룹에는 모든 리소스가 포함됩니다. hello 클라우드 서비스 이름은 hello 공용 IP 주소와 연결 된 DNS 이름이 됩니다. |
| 가상 컴퓨터 |가상 컴퓨터 |VM 관련 속성은 변경되지 않고 마이그레이션됩니다. 컴퓨터 이름 처럼 특정 osProfile 정보 hello 클래식 배포 모델에 저장 되지 않으므로 및 마이그레이션 후 빈 상태로 유지 합니다. |
| 디스크 리소스 tooVM 연결 |연결 된 암시적 디스크 tooVM |디스크는 hello 리소스 관리자 배포 모델의 최상위 리소스 그룹으로 모델링 되지 않았습니다. Hello VM에서 디스크를 암시적으로 마이그레이션됩니다. 디스크를 연결 tooa VM은 현재 지원 됩니다. 리소스 관리자 Vm을 사용할 수 클래식 저장소 계정을 포함 하지 않는 hello 디스크 toobe 손쉽게 마이그레이션할 수 있도록 해줍니다. |
| VM 확장 |VM 확장 |XML 확장을 제외한 모든 hello 리소스 확장 hello 클래식 배포 모델에서 마이그레이션됩니다. |
| 가상 컴퓨터 인증서 |Azure Key Vault의 인증서 |클라우드 서비스는 서비스 인증서를 새 Azure 키 자격 증명 모음 클라우드 서비스 당 있고 hello 인증서 hello 주요 자격 증명 모음으로 이동 합니다. hello Vm은 hello 키 자격 증명 모음에서 업데이트 된 tooreference hello 인증서입니다. <br><br> **참고:** 를 삭제 하지 마세요 hello keyvault 대로 실패 한 상태로 hello VM toogo 발생할 수 있습니다. 자격 증명 모음 키를 안전 하 게 삭제 하거나 VM tooa 새 구독 hello 함께 이동 수 있도록 hello 백 엔드에 대 한 작업을 개선 하는 중입니다. |
| WinRM 구성 |osProfile 하의 WinRM 구성 |Windows 원격 관리 구성 이동 hello 마이그레이션의 일부로 변경 않습니다. |
| 가용성 집합 속성 |가용성 집합 리소스 | 가용성 집합 사양에서 hello VM hello 클래식 배포 모델에 대 한 속성. 가용성 집합 hello 마이그레이션의 일환으로 최상위 리소스를 수 있습니다. hello 다음 구성은 지원 되지 않습니다: 여러 클라우드 서비스 당 가용성 집합 또는 함께 사용할 수 있는 클라우드 서비스에서 설정에 없는 Vm 하나 이상의 가용성을 설정 합니다. |
| VM의 네트워크 구성 |기본 네트워크 인터페이스 |VM의 네트워크 구성은 마이그레이션 후 hello 주 네트워크 인터페이스 리소스로 표시 됩니다. Vm의 가상 네트워크에 없는 경우 마이그레이션 중 hello 내부 IP 주소로 변경 합니다. |
| VM의 여러 네트워크 인터페이스 |네트워크 인터페이스 |VM에 연결 된 여러 네트워크 인터페이스가 있는 경우 각 네트워크 인터페이스는 모든 hello 속성과 함께 hello 리소스 관리자 배포 모델에서 hello 마이그레이션의 일환으로 최상위 리소스가 됩니다. |
| 부하 분산된 끝점 집합 |부하 분산 장치 |Hello 클래식 배포 모델 hello 플랫폼 모든 클라우드 서비스에서 암시적 부하 분산 장치를 할당 합니다. 마이그레이션하는 동안 새 부하 분산 장치 리소스를 만들고 hello 부하 분산 끝점 집합은 부하 분산 장치 규칙입니다. |
| 인바운드 NAT 규칙 |인바운드 NAT 규칙 |Hello VM에 정의 된 입력된 끝점은 hello 마이그레이션하는 동안 hello 부하 분산 장치에서 변환 된 tooinbound 네트워크 주소 변환 규칙입니다. |
| VIP 주소 |DNS 이름이 포함된 공용 IP 주소 |hello 가상 IP 주소는 공용 IP 주소를 되 고 hello 부하 분산 장치와 연결 된. 가상 IP 할당 tooit 입력된 끝점이 없을 경우에 마이그레이션할 수 있습니다. |
| 가상 네트워크 |가상 네트워크 |가상 네트워크 hello 마이그레이션되는 속성은 모두 toohello 리소스 관리자 배포 모델입니다. Hello 이름으로 새 리소스 그룹이 만들어질 `-migrated`합니다. |
| 예약된 IP |정적 할당 방법의 공용 IP 주소 |Hello 클라우드 서비스 또는 hello 가상 컴퓨터의 hello 마이그레이션 함께 hello 부하 분산 장치와 연결 된 예약 된 Ip이 마이그레이션됩니다. 연결되지 않고 예약된 IP 마이그레이션은 현재 지원되지 않습니다. |
| VM당 공용 IP 주소 |동적 할당 방법의 공용 IP 주소 |hello 공용 IP 주소에 연결 된 hello VM hello 할당 메서드 집합 toostatic와 공용 IP 주소 리소스를로 변환 됩니다. |
| NSG |NSG |서브넷과 연결 된 네트워크 보안 그룹 hello 마이그레이션 toohello 리소스 관리자 배포 모델의 일부분으로 복제 됩니다. hello 클래식 배포 모델에 NSG hello는 hello 마이그레이션하는 동안 제거 되지 않습니다. 그러나 hello 마이그레이션이 진행 중인 NSG hello에 대 한 hello 관리 평면 작업 차단 됩니다. |
| DNS 서버 |DNS 서버 |가상 네트워크와 연결 된 DNS 서버 또는 VM hello 마이그레이션의 일환으로 hello 해당 리소스를 모든 hello 속성과 함께 마이그레이션됩니다. |
| UDR |UDR |서브넷과 연결 된 사용자 정의 경로 hello 마이그레이션 toohello 리소스 관리자 배포 모델의 일부분으로 복제 됩니다. hello 마이그레이션하는 동안 hello UDR hello 클래식 배포 모델에서 제거 되지 않습니다. hello 마이그레이션이 진행 중인 UDR hello에 대 한 hello 관리 평면 작업 차단 됩니다. |
| VM 네트워크 구성의 IP 전달 속성 |IP 속성 hello NIC에 전달 합니다. |VM에서 hello IP 전달을 속성은 hello 마이그레이션하는 동안 hello 네트워크 인터페이스에서 변환 된 tooa 속성입니다. |
| 여러 IP가 포함된 부하 분산 장치 |여러 공용 IP 리소스가 포함된 부하 분산 장치 |부하 분산 장치 hello와 관련 된 모든 공용 IP는 변환 된 tooa 공용 IP 리소스 및 마이그레이션 후 hello 부하 분산 장치 관련 합니다. |
| Hello VM에 내부 DNS 이름 |Hello NIC에 내부 DNS 이름 |마이그레이션하는 동안 hello hello Vm에 대 한 내부 DNS 접미사는 "InternalDomainNameSuffix" hello NIC. 라는 마이그레이션된 tooa 읽기 전용 속성 hello 접미사 마이그레이션 후 변경 되지 않습니다 및 VM 해상도 계속 toowork 앞에서 설명 합니다. |
| Virtual Network 게이트웨이 |Virtual Network 게이트웨이 |Virtual Network 게이트웨이 속성은 변경되지 않고 마이그레이션됩니다. hello hello 게이트웨이에 연결 된 VIP 중 하나를 변경 하지 않습니다. |
| 로컬 네트워크 사이트 |로컬 네트워크 게이트웨이 |로컬 네트워크 사이트 속성은 로컬 네트워크 게이트웨이 호출 하는 변경 되지 않은 마이그레이션된 tooa 새 리소스입니다. 이는 온-프레미스 주소 접두사 및 원격 게이트웨이 IP를 나타냅니다. |
| 연결 참조 |연결 |네트워크 구성에서 게이트웨이 및 로컬 네트워크 사이트 간 연결 참조는 마이그레이션 후에 리소스 관리자에서 [Connection]이라는 새로 만든 리소스에 의해 표시됩니다. 네트워크 구성 파일에서 연결 참조의 모든 속성은 새로 만든 변경 되지 않은 toohello 복사 된 연결 리소스입니다. 두 개의 IPsec 터널 hello Vnet을 나타내는 toolocal 네트워크 사이트를 만들어 기본에서 VNet tooVNet 연결이 이루어집니다. 이 변환 된 tooVnet2Vnet 연결 로컬 네트워크 게이트웨이 요구 하지 않고 리소스 관리자 모델의 형식입니다. |

## <a name="changes-tooyour-automation-and-tooling-after-migration"></a>Tooyour 자동화 및 마이그레이션 후 도구 변경
Hello 클래식 배포 모델 toohello 리소스 관리자 배포 모델에서 리소스를 마이그레이션의 일환으로, 기존 자동화 또는 도구 tooensure hello 마이그레이션 후 toowork 계속 되도록 tooupdate 있어야 합니다.
