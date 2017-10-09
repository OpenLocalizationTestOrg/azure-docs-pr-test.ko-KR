Azure 가상 컴퓨터에 대 한 업데이트 tooimprove hello 안정성, 성능 및 hello 호스트 인프라의 보안을 정기적으로 수행합니다. 이러한 업데이트 범위 패치 hello 호스팅 환경 (예: 운영 체제, 하이퍼바이저 및 hello 호스트에 배포 하는 다양 한 에이전트)의 소프트웨어 구성 요소에서 네트워킹 구성 요소를 업그레이드 toohardware 서비스 해제 합니다. hello 대부분의 이러한 업데이트는 모든 영향 toohello 호스트 가상 컴퓨터 없이 수행 됩니다. 그러나 업데이트가 다음 항목에 영향을 미치는 경우가 있습니다.

- Hello 유지 관리에는 다시 부팅이 필요 하지 않지만 hello 호스트 업데이트에 Azure VM에서 현재 위치 마이그레이션 toopause hello를 사용 합니다.

- 유지 관리 컴퓨터를 다시 부팅을 필요한 경우 hello 유지 관리가 계획 되어 때에 대 한 공지를 가져옵니다. 이러한 경우 있습니다 합니다 단위도 시작할 수 있는 hello 유지 관리, 직접에 한 번에 기간입니다.

이 페이지에서는 Microsoft Azure에서 모든 종류의 유지 관리를 수행하는 방법을 설명합니다. 계획 되지 않은 이벤트 (중단)에 대 한 자세한 내용은 가상 컴퓨터의 관리 hello 가용성 [창]에 대 한 참조 (... / articles/virtual-machines/windows/manage-availability.md) 또는 [Linux](../articles/virtual-machines/linux/manage-availability.md)합니다.

가상 컴퓨터에서 실행 중인 응용 프로그램 수를 사용 하 여 예정 된 업데이트에 대 한 정보 수집 hello에 대 한 메타 데이터 서비스를 Azure [Windows](../articles/virtual-machines/windows/instance-metadata-service.md) 또는 [Linux] (... / articles/virtual-machines/linux/instance-metadata-service.md).

## <a name="in-place-vm-migration"></a>바로 VM 마이그레이션

업데이트에 전체 다시 부팅이 필요하지 않는 경우 바로 실시간 마이그레이션을 사용합니다. Hello 업데이트 하는 동안 hello 가상 컴퓨터 호스팅 환경 hello hello 필요한 업데이트 및 패치를 적용 하는 동안 RAM에 hello 메모리 유지 30 초 정도 일시 중지 됩니다. hello 가상 컴퓨터를 다시 시작 후 및 hello 클록 hello 가상 컴퓨터에 자동으로 동기화 됩니다.

가용성 집합에서 VM의 경우 업데이트 도메인은 한 번에 하나씩 업데이트됩니다. 하나의 업데이트 도메인 (UD)에 있는 모든 Vm 일시 중지, 업데이트 및 toohello에 이동 하는 계획 된 유지 관리 하기 전에 다시 시작 후 다음 UD 합니다.

일부 응용 프로그램은 이러한 종류의 업데이트에 영향을 받을 수 있습니다. 미디어 스트리밍 또는 코드 변환, 또는 처리량이 높은 네트워킹 시나리오를 처리 하는 실시간 이벤트를 수행 하는 응용 프로그램 디자인 된 tootolerate 30 초 일시 중지에 없을 수도 있습니다. <!-- sooooo, what should they do? --> 


## <a name="maintenance-requiring-a-reboot"></a>다시 부팅이 필요한 유지 관리

Vm 계획 된 유지 관리에 대 한 다시 부팅 toobe을 할 때 미리 알림을 받습니다. 계획 된 유지 관리는 두 단계: 셀프 서비스 기간과 예약 된 유지 관리 기간을 hello 합니다.

hello **셀프 서비스 창** Vm에 대 한 hello 유지 관리를 시작할 수 있습니다. 이 시간 동안 각 VM toosee의 상태를 쿼리할 수 있으며 마지막 유지 관리 요청의 hello 결과 확인할 수 있습니다.

셀프 서비스 유지 관리를 시작 하면 VM는 이미 업데이트 하 고 다시 켜져 있는 이동된 tooa 노드입니다. Hello VM 다시 부팅 때문에 hello 임시 디스크 손실 되며 가상 네트워크 인터페이스와 연결 된 동적 IP 주소는 업데이트 됩니다.

셀프 서비스 유지 관리를 시작 하는 경우 hello 프로세스 중 오류가 발생 하는 hello 작업이 중지 되 면 VM를 업데이트 하지 않으면 hello 및 것도 hello 계획 된 유지 관리 반복에서 제거 됩니다. 새 일정에 나중에 접속 선택한 새 기회 toodo 셀프 서비스 유지 관리를 제공 합니다. 

Hello 셀프 서비스 창에 전달 되는 경우 hello **예약된 유지 관리 기간** 시작 합니다. 이 기간 동안 hello 유지 관리 기간을 쿼리할 수 있지만 직접 수 toostart hello 유지 관리를 수 없습니다.

## <a name="availability-considerations-during-planned-maintenance"></a>계획된 유지 관리 동안의 가용성 고려 사항 

Toowait hello 계획 유지 관리 기간이 될 때까지 기능을 결정 하는 경우 Vm의 hello 가장 높은 가용성을 유지 관리 하기 위한 몇 가지 tooconsider가 있습니다. 

### <a name="paired-regions"></a>쌍을 이루는 지역

각 Azure 영역의 다른 영역 hello 내와 쌍을 이루는 동일한 지역, 지역 쌍 만드는 함께 합니다. 계획 된 유지 관리 하는 동안 Azure hello Vm 지역 쌍의 단일 영역에만 업데이트 됩니다. 예를 들어 hello 북 중미의 가상 컴퓨터를 업데이트할 때 Azure 업데이트 되지 것입니다: 미국 중남부에서 모든 가상 컴퓨터 hello에서 같은 시간입니다. 그러나 다른 영역에서 유지 관리 유럽 북부 수와 같은 hello 동일 미국 동부로 시간입니다. 지역 쌍의 작동 방식을 이해하면 지역에 VM을 더 잘 배포할 수 있습니다. 자세한 내용은 [Azure 지역 쌍](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)을 참조하세요.

### <a name="availability-sets-and-scale-sets"></a>가용성 집합 및 확장 집합

Azure Vm에서 작업 부하를 배포 하는 경우에 가용성 집합 tooprovide 고가용성 tooyour 응용 프로그램 내에서 hello Vm을 만들 수 있습니다. 이를 통해 가동 중단 또는 유지 관리 이벤트 중에도 하나 이상의 가상 컴퓨터를 사용할 수 있습니다.

가용성 집합 내에서 개별 Vm too20 업데이트 도메인 (Ud)을 분산 됩니다. 계획된 유지 관리 동안에는 단일 업데이트 도메인만 지정된 시간에 영향을 받습니다. 업데이트 도메인 영향 받고의 hello 순서는 반드시 이루어지지 순차적으로 알아야 합니다. 

가상 컴퓨터 크기 집합 toodeploy 하는 Azure 계산 리소스를 사용 하면 되 고 단일 리소스로 동일한 Vm 집합이 관리 합니다. hello 크기 집합 Vm 가용성 집합에 같은 업데이트 도메인에 걸쳐 자동으로 배포 됩니다. 지정된 시점에서는 가용성 집합과 마찬가지로 확장 집합에서 단일 업데이트 도메인만 영향을 받습니다.

고가용성을 위해 가상 컴퓨터를 구성 하는 방법에 대 한 자세한 내용은 가상 컴퓨터의 관리 hello 가용성 Windows에 대 한 참조 (... / articles/virtual-machines/windows/manage-availability.md) 또는 [Linux](../articles/virtual-machines/linux/manage-availability.md)합니다.
