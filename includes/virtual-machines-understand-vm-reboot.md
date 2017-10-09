Azure 가상 컴퓨터 (Vm) 프로그램 시작 hello 다시 부팅 작업의 증명 정보 없이 명확한 이유 없이 다시 부팅 경우가 될 수 있습니다. 이 문서에서는 hello 동작과 Vm tooreboot 하면이 고 tooavoid 예기치 않은 문제를 다시 부팅 또는 이러한 문제의 hello 영향을 줄이는 방법에 대 한 정보를 제공 하는 이벤트를 나열 합니다.

## <a name="configure-hello-vms-for-high-availability"></a>고가용성에 대 한 hello Vm 구성
hello 가장 좋은 방법은 tooprotect VM에 대해 Azure에서 실행 되는 응용 프로그램을 다시 부팅 되며 가동 중지 시간 tooconfigure hello Vm 가용성을 높이기 위한 있습니다.

tooprovide이 수준에서 중복 tooyour 응용 프로그램의 확인을 가용성 집합에 두 개 이상의 Vm을 그룹화 하는 것이 좋습니다. 이 구성을 사용 하면 계획 되거나 계획 되지 않은 유지 관리 이벤트 중 하나에서 하나 이상의 VM를 사용할 수 있는 충족 hello 99.95% [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_5/)합니다.

가용성 집합에 대 한 자세한 내용은 다음 문서는 hello 참조:

- [Vm의 hello 가용성 관리](../articles/virtual-machines/windows/manage-availability.md)
- [VM의 가용성 구성](../articles/virtual-machines/windows/classic/configure-availability.md)

## <a name="resource-health-information"></a>Resource Health 정보 
Azure 리소스 상태는 개별 Azure 리소스의 hello 상태를 노출 하 고 문제 해결을 위한 조치 가능한 지침을 제공 하는 서비스입니다. 여기서 않다면 가능한 toodirectly 액세스 서버나 인프라 요소는 클라우드 환경에서 리소스 상태 hello 목표는 문제를 해결 하는 데 소요 된 tooreduce hello 시간입니다. 특히 hello 목적은 tooreduce hello 시간에 있는지 여부를 hello 문제의 hello 루트 hello 내에 이벤트 또는 hello 응용 프로그램에서 Azure 플랫폼 결정을 소비 하는입니다. 자세한 내용은 [Resource Health 이해 및 사용](../articles/resource-health/resource-health-overview.md)을 참조하세요.

## <a name="actions-and-events-that-can-cause-hello-vm-tooreboot"></a>동작 및 이벤트를 발생 시킬 수 있는 VM tooreboot hello

### <a name="planned-maintenance"></a>계획된 유지 보수
Microsoft Azure hello 구형 tooimprove hello 안정성, 성능 및 Vm의 기반이 되는 hello 호스트 인프라의 보안을 통해 업데이트를 주기적으로 수행 합니다. 메모리 보존 업데이트를 비롯한 이러한 많은 업데이트는 VM 또는 클라우드 서비스에 영향을 주지 않고 수행됩니다.

그러나 일부 업데이트는 재부팅이 필요하지 않습니다. 이러한 경우 hello Vm hello 인프라 패치 म hello Vm은 다시 시작 하는 동안 종료 됩니다.

toounderstand 어떤 Azure 계획 된 유지 관리 방법을 Linux Vm의 가용성을 hello 나오는지 참조 여기에 나열 된 hello 문서. hello 문서 hello 영향을 줄이는 hello Azure의 계획 된 유지 관리 프로세스에 대 한 배경 및 tooschedule toofurther 유지 관리를 계획 하는 방법을 제공 합니다.

- [Azure에서 VM에 대한 계획된 유지 관리](../articles/virtual-machines/windows/planned-maintenance.md)
- [Tooschedule는 Azure Vm에서 유지 관리를 계획 하는 방법](../articles/virtual-machines/windows/classic/planned-maintenance-schedule.md)

### <a name="memory-preserving-updates"></a>메모리 유지 업데이트   
Microsoft Azure의 이 업데이트 클래스는 사용자가 실행 중인 VM에는 아무런 영향도 주지 않습니다. 이러한 많은 업데이트는 toocomponents 또는 인스턴스를 실행 하는 hello를 방해 하지 않고 업데이트할 수 있는 서비스입니다. 일부는 hello Vm 재부팅 하지 않고 적용 될 수 있는 hello 호스트 운영 체제에서 플랫폼 인프라 업데이트입니다.

이러한 메모리 보존 업데이트는 바로 실시간 마이그레이션을 가능하게 하는 기술을 통해 수행됩니다. Hello VM에 위치한가 업데이트 되는 경우는 *일시 중지* 상태입니다. 이 상태는 hello 기본 호스트 운영 체제 hello 필요한 업데이트 및 패치를 수신 하는 동안 RAM에 hello 메모리를 유지 합니다. 일시 중지 되 고 30 초 이내 hello VM 다시 시작 됩니다. VM이 다시 시작 하는 hello, 후의 시계 자동으로 동기화 됩니다.

Hello 짧은 일시 중지 기간으로 인해 hello Vm에 미치는 영향을 hello 줄어듭니다 크게이 메커니즘을 통해 업데이트를 배포 합니다. 그러나 모든 업데이트를 이러한 방식으로 배포할 수는 없습니다. 

다중 인스턴스 업데이트(가용성 집합의 VM인 경우)는 한 번에 하나의 업데이트 도메인에 적용됩니다.

> [!NOTE]
> 이전 커널 버전이 설치된 Linux 컴퓨터는 이 업데이트 메서드 중에 커널 패닉의 영향을 받습니다. tooavoid이 문제점, 업데이트 tookernel 버전 3.10.0-327.10.1 이상. 자세한 내용은 [호스트 노드 업그레이드 후에 3.10 기반 커널 패닉인 Azure Linux VM](https://support.microsoft.com/help/3212236)을 참조하세요.     
    
### <a name="user-initiated-reboot-or-shutdown-actions"></a>사용자 시작 재부팅 또는 종료 작업
 
Hello Azure 포털, Azure PowerShell, 명령줄 인터페이스 또는 API를 다시 설정에서 컴퓨터를 다시 부팅을 수행 하는 경우 hello에서 hello 이벤트를 찾을 수 있습니다 [Azure 활동 로그](../articles/monitoring-and-diagnostics/monitoring-overview-activity-logs.md)합니다.

Hello VM의 운영 체제에서 hello 동작을 수행 하는 경우에 hello 시스템 로그에 hello 이벤트를 찾을 수 있습니다.

일반적으로 hello VM tooreboot 시키는 다른 시나리오에는 여러 구성 변경 작업이 포함 됩니다. 일반적으로 특정 작업을 실행 하는지 여부를 나타내는 경고 메시지가 hello VM의 다시 부팅 하면 볼 수 있습니다. 예로 모든 VM 크기 조정 작업에 hello 관리 계정의 hello 암호를 변경 하 고 정적 IP 주소를 설정 합니다.

### <a name="azure-security-center-and-windows-update"></a>Azure Security Center 및 Windows 업데이트
Azure Security Center는 누락된 운영 체제 업데이트가 있는지 매일 Windows 및 Linux VM을 모니터링합니다. 보안 센터는 Windows VM에서 구성된 서비스에 따라 Windows 업데이트 또는 WSUS(Windows Server Update Services)에서 사용 가능한 보안 및 중요 업데이트의 목록을 검색합니다. 보안 센터 hello Linux 시스템에 대 한 최신 업데이트를 확인합니다. VM이 시스템 업데이트를 누락하는 경우 Security Center는 시스템 업데이트 적용을 권장합니다. 이러한 시스템 업데이트를 적용 hello hello Azure 포털에에서 hello 보안 센터를 통해 제어 됩니다. 일부 업데이트를 적용한 후 VM을 재부팅해야 할 수 있습니다. 자세한 내용은 [Azure Security Center의 시스템 업데이트 적용](../articles/security-center/security-center-apply-system-updates.md)을 참조하세요.

온-프레미스 서버와 마찬가지로 Azure 밀어 넣지 않습니다 업데이트가 Windows 업데이트 tooWindows Azure Vm에서에서 이러한 컴퓨터는 해당 사용자가 관리 되는 의도 한 toobe 때문에 있습니다. 그러나는 tooleave hello 자동 Windows 업데이트 설정을 사용을 권장 합니다. Windows Update에서 업데이트의 자동 설치는 hello 업데이트가 적용 된 후 재부팅 toooccur를 발생할 수 있습니다. 자세한 내용은 [Windows 업데이트 FAQ](https://support.microsoft.com/help/12373/windows-update-faq)를 참조하세요.

### <a name="other-situations-affecting-hello-availability-of-your-vm"></a>VM의 hello 가용성에 영향을 주는 다른 경우
Azure VM의 hello 사용 중단 적극적으로 수 다른 경우가 있습니다. 받을 수 전자 메일 알림을이 작업을 수행 하기 전에 기본 문제를 hello 기회 tooresolve 볼 수 있도록 합니다. VM 가용성에 영향을 주는 문제의 예로 보안 위반 및 지불 방법 hello 만료를 들 수 있습니다.

### <a name="host-server-faults"></a>호스트 서버 오류 
hello VM은 Azure 데이터 센터 내에서 실행 되는 실제 서버에서 호스트 됩니다. 에이전트가 hello 물리적 서버 실행 Azure 다른 몇 가지 구성 요소 추가 tooa에 hello 호스트 에이전트를 호출 합니다. Hello 물리적 서버에 이러한 Azure 소프트웨어 구성 요소는 응답 하지 않을, 시스템을 모니터링 하는 hello hello 호스트 서버 tooattempt 복구를 다시 부팅을 트리거합니다. hello VM은 5 분 내에 다시 일반적으로 사용할 수 및 hello 동일한 이전에 호스트에서 toolive 계속 합니다.

서버 오류는 일반적으로 하드 디스크 또는 반도체 드라이브의 hello 실패 등의 하드웨어 오류로 인해 발생 합니다. Azure는 지속적으로 모니터링 이러한 경우, hello 기본 버그를 식별 하 고 hello 완화 구현 되어 테스트 후에서는 업데이트.

일부 호스트 서버에 오류가 발생 특정 toothat 서버 일 수 있으므로 수동으로 hello VM tooanother 호스트 서버를 다시 배포 하 여 반복 되는 VM 재부팅 상황을 향상 시킬 수 있습니다. Hello를 사용 하 여이 작업을 트리거할 수 **다시 배포** hello VM의 hello 세부 정보 페이지에서 옵션 또는 중지 및 다시 시작 하 여 hello Azure 포털에서에서 VM을 환영 합니다.

### <a name="auto-recovery"></a>자동 복구
호스트 서버 hello 수 없는 컴퓨터를 다시 부팅 어떤 이유로 든 hello Azure 플랫폼 추가 조사를 위해 순환 순서에서 한 자동 복구 동작 tootake hello 결함이 있는 호스트 서버를 시작 합니다. 

해당 호스트에서 모든 Vm에 자동으로 재배치 tooa 다른, 정상 호스트 서버 됩니다. 이 프로세스는 15분 이내에 일반적으로 완료됩니다. hello 자동 복구 프로세스에 대해 자세히 toolearn 참조 [Vm의 자동 복구](https://azure.microsoft.com/blog/service-healing-auto-recovery-of-virtual-machines)합니다.

### <a name="unplanned-maintenance"></a>계획되지 않은 유지 관리
드문 경우 이지만 수 필요 tooperform 유지 관리 활동 tooensure hello hello Azure 플랫폼의 전반적인 상태 Azure 운영 팀을 hello 합니다. 이 동작은 VM 가용성에 영향을 줄 수 있습니다 및 일반적으로 발생 hello 동일 앞에서 설명한 대로 자동 복구 작업입니다.  

계획 되지 않은 maintenances hello 다음과를 같습니다.

- 긴급 노드 조각 모음
- 긴급 네트워크 스위치 업데이트

### <a name="vm-crashes"></a>VM 충돌
Hello VM 자체 내에서 문제로 인해 Vm 다시 시작할 수 있습니다. hello 작업 부하 또는 hello VM에서 실행 중인 역할 hello 게스트 운영 체제 내 버그 검사를 트리거할 수 있습니다. Hello 크래시에 대 한 hello 이유를 결정 하는 데 도움이 필요한 경우 Windows Vm에 대 한 hello 시스템 및 응용 프로그램 로그를 확인 하 고 Linux Vm에 대 한 직렬 로그 hello 합니다.

### <a name="storage-related-forced-shutdowns"></a>Storage 관련 강제 종료
Azure의 Vm 운영 체제 및 hello Azure 저장소 인프라에서 호스트 되는 데이터 저장소에 대 한 가상 디스크에 의존 합니다. Hello 가용성 또는 hello VM 및 연결 된 hello 가상 디스크를 연결할 영향을 받는 120 초 넘게 때마다 hello Azure 플랫폼 hello Vm tooavoid 데이터 손상의 강제 종료를 수행 합니다. hello Vm 저장소 연결 복원 된 후에 자동으로 다시 제공 됩니다. 

hello 종료의 hello 기간 5 분으로 짧게 될 수 있지만 훨씬 길어질 수 있습니다. hello 다음 연결 강제 종료 저장소 관련 된 hello 특정 사례 중 하나입니다. 

**IO 제한 초과**

I/O 작업 / 초 (IOPS)의 hello 볼륨 hello 디스크에 대 한 I/O hello 제한을 초과 하기 때문에 I/O 요청은 제한 된 일관 되 게 하는 경우 Vm은 일시적으로 종료 될 수 있습니다. (표준 디스크 저장소는 제한 된 too500 IOPS입니다.) toomitigate이이 문제를 디스크 스트라이프를 사용 하거나 hello 작업 부하에 따라 hello 게스트 VM hello 저장소 공간을 구성 합니다. 자세한 내용은 [Storage 성능이 최적화되도록 Azure VM 구성](http://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx)을 참조하세요.

더 높은 IOPS 제한은 too80, 000 IOPS Azure 프리미엄 저장소를 통해 사용할 수입니다. 자세한 내용은 [고성능 Premium Storage](../articles/storage/common/storage-premium-storage.md)를 참조하세요.

### <a name="other-incidents"></a>다른 인시던트
드문 경우이지만, 확산된 문제가 Azure 데이터 센터의 여러 서버에 영향을 줄 수 있습니다. 이 문제가 발생 한 경우 hello Azure 팀 보내는 전자 메일 알림을 영향을 받는 toohello 구독 Hello를 확인할 수 있습니다 [Azure 서비스 상태 대시보드](https://azure.microsoft.com/status/) Azure 포털의 지속적인 작동 중단 및 사고 지난 hello 상태에 대 한 hello 및 합니다.
