
이 문서의 Azure 문제 해결 되지 않으면 방문 하 여 hello [MSDN 및 스택 오버플로 Azure 포럼](https://azure.microsoft.com/support/forums/)합니다. 이러한 포럼에 문제를 게시할 수 있습니다 또는 too@AzureSupport Twitter에서. 또한 선택 하 여 Azure 지원 요청을 제출할 수 있습니다 **지원을 받는** hello에 [Azure 지원](https://azure.microsoft.com/support/options/) 사이트입니다.

## <a name="general-troubleshooting-steps"></a>일반적인 문제 해결 단계
### <a name="troubleshoot-common-allocation-failures-in-hello-classic-deployment-model"></a>Hello 클래식 배포 모델의 일반 할당 오류 해결
이 단계는 가상 컴퓨터의 다양한 할당 문제를 해결하는 데 도움이 됩니다.

* Hello VM tooa 다른 VM 크기를 조정 합니다.<br>
    **모두 찾아보기** > **Virtual Machines(클래식)** > 사용자의 가상 컴퓨터 > **설정** > **크기**를 차례로 클릭합니다. 자세한 내용은 참조 [hello 가상 컴퓨터 크기를 조정한](https://msdn.microsoft.com/library/dn168976.aspx)합니다.
* Hello 클라우드 서비스에서 모든 Vm을 삭제 하 고 다시 Vm을 만듭니다.<br>
    **모두 찾아보기** > **Virtual Machines(클래식)** > 사용자의 가상 컴퓨터 > **삭제**를 차례로 클릭합니다. 그런 다음 **새로 만들기** > **계산** > [가상 컴퓨터 이미지]를 클릭합니다.

### <a name="troubleshoot-common-allocation-failures-in-hello-azure-resource-manager-deployment-model"></a>Hello Azure 리소스 관리자 배포 모델의 일반 할당 오류 해결
이 단계는 가상 컴퓨터의 다양한 할당 문제를 해결하는 데 도움이 됩니다.

* 중지 (할당 취소)의 모든 Vm에서 hello 동일한 가용성을 설정한 다음 다시 시작 합니다.<br>
    toostop: 클릭 **리소스 그룹** > 리소스 그룹 > **리소스** > 가용성 집합 > **가상 컴퓨터** > 가상 컴퓨터 >  **중지**합니다.
  
    선택 첫 번째 VM hello 모든 Vm을 중지 한 후를 클릭 하 고 **시작**합니다.

## <a name="background-information"></a>배경 정보
### <a name="how-allocation-works"></a>할당의 작동 원리
Azure 데이터 센터의 hello 서버 클러스터로 분할 됩니다. 일반적으로 여러 개의 클러스터에 할당 요청 시도 하지만 클라이언트 컴퓨터를 hello 할당 요청에서 특정 제약 조건을 강제로 hello 하나의 클러스터에 Azure 플랫폼 tooattempt hello 요청 수입니다. 이 문서에서는 지칭 toothis "고정 된 tooa 클러스터." 아래의 다이어그램 1에서는 여러 개의 클러스터에 시도 된 일반 할당 hello 대/소문자를 보여 줍니다. 다이어그램 2는 할당의 hello 대/소문자를 보여 줍니다. 하는 클라우드 서비스 CS_1 또는 가용성 집합을 기존 hello 호스트 되는 위치 이기 때문에 고정 된 tooCluster 2가 있습니다.
![할당 다이어그램](./media/virtual-machines-common-allocation-failure/Allocation1.png)

### <a name="why-allocation-failures-happen"></a>할당 오류가 발생하는 이유
고정 된 tooa 클러스터 할당 요청을 사용 하는 경우 hello 사용 가능한 리소스 풀은 더 작은 이후 toofind 무료 리소스를 실패의 높은 가능성이 높습니다. 또한 할당 요청은 고정 된 tooa 클러스터 hello 유형의 요청한 리소스가 해당 클러스터에서 지원 되지 않습니다 되지만 hello 클러스터에 리소스를 해제 하는 경우에 요청이 실패 합니다. 아래의 다이어그램 3 고정된 할당 hello 유일한 후보 클러스터에 리소스를 해제 없기 때문에 실패 하는 hello 경우를 보여 줍니다. 다이어그램 4 hello 유일한 후보 클러스터를 지원 하지 않으므로 고정된 할당 실패 하는 hello 경우를 보여 줍니다. hello hello 클러스터에 리소스를 해제 하는 경우에 VM 크기를 요청 했습니다.

![고정된 할당 오류](./media/virtual-machines-common-allocation-failure/Allocation2.png)

## <a name="detailed-troubleshoot-steps-specific-allocation-failure-scenarios-in-hello-classic-deployment-model"></a>자세한 hello 클래식 배포 모델에서 단계 특정 할당 오류 시나리오 문제 해결
다음은 고정 한 할당 요청 toobe 발생 하는 일반적인 할당 시나리오입니다. 이 문서의 뒷 부분에서 각 시나리오에 대해 자세히 알아봅니다.

* VM 크기를 조정 하거나 Vm 또는 역할 인스턴스 tooan 기존 클라우드 서비스를 추가 합니다.
* 부분적으로 중지(할당 취소)된 VM 다시 시작
* 완전히 중지(할당 취소)된 VM 다시 시작
* 스테이징/프로덕션 배포(Platform as a Service 전용)
* 선호도 그룹(VM/서비스 근접)
* 선호도-그룹-기반 가상 네트워크

할당 오류가 발생 하는 경우 설명 hello 시나리오 중 하나라도 충족할 tooyour 오류 표시 됩니다. Hello Azure 플랫폼 tooidentify hello 해당 시나리오에 따라 반환 된 hello 할당 오류를 사용 합니다. 요청이 고정 하는 경우 일부 제거 hello 고정 제약 조건 tooopen 할당 성공 hello 가능성이 길어지는 요청 toomore 클러스터.

일반적으로 hello 오류 "hello VM 크기가 지원 되지 않음이 필요" 나타내지 않습니다,으로 항상 다시 시도할 수 있습니다는 나중에 충분 한 리소스가 것 처럼 요청 hello 클러스터 tooaccommodate에서 해제 합니다. Hello 문제가 발생 한 경우 해당 hello 요청한 VM 크기를 지원 하지 않습니다, 다른 VM 크기를 시도 하십시오. 그렇지 않으면 hello 유일한 옵션은 제약 조건 고정 tooremove hello 있습니다.

두 가지 일반적인 오류 시나리오는 관련된 tooaffinity 그룹. 지난 hello, 선호도 그룹 사용된 tooprovide 근접 tooVMs/서비스 인스턴스, 되었거나 가상 네트워크 사용된 tooenable hello 생성 했습니다. 지역 가상 네트워크의 hello 소개, 선호도 그룹은 더 이상 필요 toocreate 가상 네트워크입니다. Hello Azure 인프라의 네트워크 대기 시간 감소와 VM/서비스 근접 한 hello 권장 toouse 선호도 그룹 변경 되었습니다.

다이어그램 아래 5 (고정) hello 할당 시나리오의 hello 분류를 표시합니다.
![고정된 할당 분류법](./media/virtual-machines-common-allocation-failure/Allocation3.png)

> [!NOTE]
> 각 할당 시나리오에 나열 된 hello 오류 약식 표현입니다. Toohello 참조 [오류 문자열 조회](#Error string lookup) 자세한 오류 문자열에 대 한 합니다.
> 
> 

## <a name="allocation-scenario-resize-a-vm-or-add-vms-or-role-instances-tooan-existing-cloud-service"></a>할당 시나리오: VM 크기를 조정 하거나 추가 Vm 또는 역할 인스턴스 tooan 기존 클라우드 서비스
**오류**

Upgrade_VMSizeNotSupported 또는 GeneralError

**클러스터 고정의 원인**

역할 인스턴스 tooan 기존 클라우드 서비스는 hello 기존 클라우드 서비스를 호스팅하는 hello 원본 클러스터에서 시도한 toobe 또는 A 요청 tooresize VM 또는 VM을 추가 합니다. 새 클라우드 서비스를 만들면 다른 클러스터를 리소스 또는 사용자가 요청한 hello VM 크기를 지 원하는 hello Azure 플랫폼 toofind 있습니다.

**해결 방법**

이면 hello 오류 Upgrade_VMSizeNotSupported * 다른 VM 크기를 시도 합니다. 이 옵션을만 허용 가능한 다른 가상 IP 주소 (VIP) toouse 경우 만들 다른 VM 크기를 사용 하 여 새 클라우드 서비스 toohost 새 VM hello 하 고 hello 새 클라우드 서비스 toohello 지역 가상 네트워크 hello 기존 Vm 실행 되 고 있는 추가 합니다. 기존 클라우드 서비스는 지역 가상 네트워크를 사용 하지 않는 경우 여전히 hello 새 클라우드 서비스에 대 한 새 가상 네트워크를 만들고 수 다음 연결 프로그램 [기존 가상 네트워크 toohello 새 가상 네트워크](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/)합니다. [지역 가상 네트워크](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/)에 대한 자세한 내용을 참조하세요.

이면 hello 오류 GeneralError * 가능성이 hello 유형의 리소스 (예: 특정 VM 크기) hello 클러스터에서 사용할 수 있지만 hello 클러스터 hello 순간에 리소스가 없는 됩니다. 새 클라우드 서비스 (참고 hello 새 클라우드 서비스에 toouse 다른 VIP)를 만드는 과정 hello 필요한 계산 리소스를 추가 하 고 지역 가상 네트워크 tooconnect 클라우드 서비스를 사용 하는 시나리오에서는 위의 비슷한 toohello 합니다.

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>할당 시나리오: 부분적으로 중지(할당 취소)된 VM 다시 시작
**오류**

GeneralError*

**클러스터 고정의 원인**

일부 할당 취소란 클라우드 서비스에서 하나 이상을 중지(할당 취소)했지만 모든 VM을 중지한 것은 아니라는 의미입니다. 중지 하면 (할당 취소) VM을 연결 하는 hello 리소스가 해제 됩니다. 따라서 중지(할당 취소)한 VM을 재시작하는 것은 새로운 할당 요청입니다. 해당 tooadding Vm tooan 기존 클라우드 서비스는 부분적으로 할당이 해제 된 클라우드 서비스에서 Vm을 다시 시작 합니다. hello 할당 요청에 toobe hello 기존 클라우드 서비스를 호스팅하는 hello 원래 클러스터에 시도 되었습니다. 다른 클라우드 서비스를 만들면 사용자가 요청한 hello VM 크기를 지 원하는 무료 리소스 또는 다른 클러스터를 hello Azure 플랫폼 toofind 있습니다.

**해결 방법**

허용 되는 경우 toouse 삭제 hello 다른 VIP hello 연결 된 디스크 유지) (않음 (할당 취소) Vm을 중지 하 고 다른 클라우드 서비스를 통해 다시 hello Vm을 추가 합니다. 지역 가상 네트워크 tooconnect 클라우드 서비스를 사용 합니다.

* 새 클라우드 서비스 toohello hello 추가 하면 기존 클라우드 서비스는 지역 가상 네트워크를 사용 하는 경우 동일한 가상 네트워크입니다.
* 기존 클라우드 서비스는 지역 가상 네트워크를 사용 하지 않는 경우 hello 새 클라우드 서비스에 대 한 새 가상 네트워크를 만드는 다음 [기존 가상 네트워크 toohello 새로운 가상 네트워크 연결](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/)합니다. [지역 가상 네트워크](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/)에 대한 자세한 내용을 참조하세요.

## <a name="allocation-scenario-restart-fully-stopped-deallocated-vms"></a>할당 시나리오: 완전히 중지(할당 취소)된 VM 다시 시작
**오류**

GeneralError*

**클러스터 고정의 원인**

전체 할당 취소란 클라우드 서비스의 모든 VM을 중지(할당 취소)했다는 의미입니다. 이러한 Vm가 hello 클라우드 서비스를 호스팅하는 hello 원본 클러스터에서 시도한 toobe toorestart hello 할당을 요청 합니다. 새 클라우드 서비스를 만들면 다른 클러스터를 리소스 또는 사용자가 요청한 hello VM 크기를 지 원하는 hello Azure 플랫폼 toofind 있습니다.

**해결 방법**

허용 가능한 toouse 다른 VIP를 삭제 hello 원래 hello 연결 된 디스크 유지) (않음 (할당 취소) Vm 중지 되 고 hello 해당 클라우드 서비스 중지 (할당 취소) 하는 경우에 이미 리소스 릴리스된 (hello 관련 된 계산 삭제 hello Vm)입니다. 새 클라우드 서비스 tooadd hello Vm을 다시 만듭니다.

## <a name="allocation-scenario-stagingproduction-deployments-platform-as-a-service-only"></a>할당 시나리오: 스테이징/프로덕션 배포(Platform as a Service 전용)
**오류**

New_General* 또는 New_VMSizeNotSupported*

**클러스터 고정의 원인**

배포 및 클라우드 서비스의 hello 프로덕션 배포를 준비 하는 hello hello에서 호스팅되는 동일한 클러스터입니다. Hello 두 번째 배포에 추가 하면 hello 해당 할당 요청을 호스팅하는 동일한 클러스터 hello 첫 번째 배포 된 hello에 시도 됩니다.

**해결 방법**

첫 번째 배포 hello 및 hello 원래 클라우드 서비스를 삭제 하 고 hello 클라우드 서비스를 다시 배포 합니다. 이 작업을 지 원하는 클러스터를 사용자가 요청한 hello VM 크기 또는 두 배포 모두 만큼 충분 한 리소스를 해제 toofit에 있는 클러스터에 hello 첫 번째 배포를 배치 될 수 있습니다.

## <a name="allocation-scenario-affinity-group-vmservice-proximity"></a>할당 시나리오: 선호도 그룹(VM/서비스 근접성)
**오류**

New_General* 또는 New_VMSizeNotSupported*

**클러스터 고정의 원인**

할당 된 tooan 선호도 그룹은 모든 계산 리소스 tooone 클러스터 연결 되어 있습니다. Hello hello 기존 리소스 호스팅되는 동일한 클러스터에 해당 선호도 그룹에서 새 계산 리소스 요청 시도 됩니다. 마찬가지 기존 클라우드 서비스 또는 새 클라우드 서비스를 통해 hello 새 리소스가 생성 여부입니다.

**해결 방법**

선호도 그룹이 필요하지 않으면 선호도 그룹을 사용하지 않거나 여러 선호도 그룹의 계산 리소스를 그룹화합니다.

## <a name="allocation-scenario-affinity-group-based-virtual-network"></a>할당 시나리오: 선호도-그룹-기반 가상 네트워크
**오류**

New_General* 또는 New_VMSizeNotSupported*

**클러스터 고정의 원인**

지역 가상 네트워크를 도입 하기 전에 필요한 tooassociate 선호도 그룹과 가상 네트워크 있었습니다. 결과적으로, 선호도 그룹에 배치 하는 계산 리소스에 의해 바인딩된 hello에 설명 된 대로 동일한 제약 조건을 hello "할당 시나리오: 선호도 그룹 (VM/서비스 영역)" 섹션. hello 계산 리소스가 동률된 tooone 클러스터입니다.

**해결 방법**

선호도 그룹을 필요 하지 않은 경우 hello에 대 한 새 지역 가상 네트워크 추가 하는 새 리소스를 만들고 다음 [기존 가상 네트워크 toohello 새로운 가상 네트워크 연결](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/)합니다. [지역 가상 네트워크](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/)에 대한 자세한 내용을 참조하세요.

수 또는 [가상 네트워크를 선호도 그룹 기반 tooa 지역 가상 네트워크 마이그레이션](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/), 한 다음 원하는 hello 리소스를 다시 추가 합니다.

## <a name="detailed-troubleshooting-steps-specific-allocation-failure-scenarios-in-hello-azure-resource-manager-deployment-model"></a>자세한 단계 특정 할당 오류 시나리오 hello Azure 리소스 관리자 배포 모델에서 문제 해결
다음은 고정 한 할당 요청 toobe 발생 하는 일반적인 할당 시나리오입니다. 이 문서의 뒷 부분에서 각 시나리오에 대해 자세히 알아봅니다.

* VM 크기를 조정 하거나 Vm 또는 역할 인스턴스 tooan 기존 클라우드 서비스를 추가 합니다.
* 부분적으로 중지(할당 취소)된 VM 다시 시작
* 완전히 중지(할당 취소)된 VM 다시 시작

할당 오류가 발생 하는 경우 설명 hello 시나리오 중 하나라도 충족할 tooyour 오류 표시 됩니다. Hello Azure 플랫폼 tooidentify hello 해당 시나리오에 따라 반환 된 hello 할당 오류를 사용 합니다. 고정 된 tooan 기존 클러스터 사용자의 요청을 사용 하는 경우 일부 제거 hello 고정 제약 조건 tooopen 할당 성공 hello 가능성이 길어지는 요청 toomore 클러스터.

일반적으로 hello 오류 "hello VM 크기가 지원 되지 않음이 필요" 나타내지 않습니다,으로 항상 다시 시도할 수 있습니다는 나중에 충분 한 리소스가 것 처럼 요청 hello 클러스터 tooaccommodate에서 해제 합니다. 해결 방법에 대 한 hello 문제가 발생 한 경우 해당 hello 요청한 VM 크기를 지원 하지 않습니다, 아래 참조.

## <a name="allocation-scenario-resize-a-vm-or-add-vms-tooan-existing-availability-set"></a>할당 시나리오: VM 크기를 조정 하거나 추가 Vm tooan 기존 가용성 집합
**오류**

Upgrade_VMSizeNotSupported* 또는 GeneralError*

**클러스터 고정의 원인**

A tooresize VM을 요청 하거나 기존 가용성 집합 VM tooan hello 기존 가용성 집합을 호스팅하는 hello 원본 클러스터에서 시도한 toobe에 추가 합니다. 새 가용성 집합을 만들면 리소스 또는 사용자가 요청한 hello VM 크기를 지 원하는 다른 클러스터를 hello Azure 플랫폼 toofind 있습니다.

**해결 방법**

이면 hello 오류 Upgrade_VMSizeNotSupported * 다른 VM 크기를 시도 합니다. 다른 VM 크기를 사용 하는 옵션을 없으면 hello 가용성 집합에 있는 모든 Vm을 중지 합니다. 원하는 VM 크기는 hello VM tooa 지 원하는 클러스터를 hello가 할당 hello 가상 컴퓨터의 hello 크기를 변경 하는 다음 할 수 있습니다.

이면 hello 오류 GeneralError * 가능성이 hello 유형의 리소스 (예: 특정 VM 크기) hello 클러스터에서 사용할 수 있지만 hello 클러스터 hello 순간에 리소스가 없는 됩니다. Hello VM에는 다른 가용성 집합의 일부가 될 수, 하는 경우 다른 가용성 집합에 새 VM을 만듭니다 (hello에 동일한 지역). 이 새 VM을 추가할 수 있습니다 toohello 동일한 가상 네트워크입니다.  

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>할당 시나리오: 부분적으로 중지(할당 취소)된 VM 다시 시작
**오류**

GeneralError*

**클러스터 고정의 원인**

일부 할당 취소란 가용성 집합에서 하나 이상을 중지(할당 취소)했지만 모든 VM을 중지한 것은 아니라는 의미입니다. 중지 하면 (할당 취소) VM을 연결 하는 hello 리소스가 해제 됩니다. 따라서 중지(할당 취소)한 VM을 재시작하는 것은 새로운 할당 요청입니다. 부분적으로 할당이 해제 된 가용성 집합에 Vm을 다시 시작은 해당 tooadding Vm tooan 기존 가용성 설정 됩니다. hello 할당 요청에 toobe hello 기존 가용성 집합을 호스트 하는 hello 원래 클러스터에 시도 되었습니다.

**해결 방법**

첫 번째 hello를 다시 시작 하기 전에 설정 hello 사용 가능한 모든 Vm을 중지 합니다. 이렇게 하면 새로운 할당 시도가 실행되고 사용 가능한 용량이 있는 새 클러스터가 선택될 수 있습니다.

## <a name="allocation-scenario-restart-fully-stopped-deallocated"></a>할당 시나리오: 완전히 중지(할당 취소)된 VM 다시 시작
**오류**

GeneralError*

**클러스터 고정의 원인**

전체 할당 취소란 가용성 집합의 모든 VM을 중지(할당 취소)했다는 의미입니다. hello 할당 요청을 이러한 Vm를 지 원하는 모든 클러스터를 대상 toorestart hello 원하는 크기입니다.

**해결 방법**

새 VM 크기 tooallocate를 선택 합니다. 작동하지 않는 경우 나중에 다시 시도하세요.

## <a name="error-string-lookup"></a>오류 문자열 조회
**New_VMSizeNotSupported***

"hello VM 크기 (또는 VM 크기 조합)이이 배포에 필요한 구축할 수 없으므로 toodeployment 요청 제약 조건 때문입니다. 가능 하면 tooa 호스팅된 서비스에 없는 다른 배포와 함께 배포 되는 가상 네트워크 바인딩과 같은 제약 조건을 완화해 보거나 하십시오 tooa 다른 선호도 그룹 또는 선호도 그룹 또는 try 없이 tooa 다른 영역을 배포 하 고 있습니다. "

**New_General***

"를 할당 하지 못했습니다. 요청에 없습니다 toosatisfy 제약 조건입니다. hello 요청 된 새 서비스 배포 바인딩된 tooan 선호도 그룹 또는 가상 네트워크를 대상으로 발생 하거나이 호스팅된 서비스에서 기존 배포 합니다. 이러한 조건 중 하나가 제한 hello 새 배포 toospecific Azure 리소스입니다. 나중에 다시 시도 하거나 hello VM 크기 또는 역할 인스턴스 수를 줄여 보십시오. 또는 가능한 경우 hello 앞에서 언급 한 제약 조건을 제거 하거나 tooa 다른 지역에 배포 해 보십시오. "

**Upgrade_VMSizeNotSupported***

"Hello 배포 tooupgrade 수 없습니다. hello 요청한 VM 크기 XXX를 hello 기존 배포를 지 원하는 hello 리소스에서 확인할 수 있습니다. 나중에 다시 시도하거나, 다른 VM 크기 또는 적은 수의 역할 인스턴스로 시도하거나 새 선호도 그룹 또는 선호도 그룹 바인딩 없이 빈 호스티드 서비스에 배포를 만듭니다.”

**GeneralError***

"hello 서버에서 내부 오류가 발생 하는 데 사용 합니다. Hello 요청 시도 하십시오. " 또는 "실패 tooproduce hello 서비스에 대 한 할당 합니다."

