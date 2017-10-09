## <a name="understand-vm-reboots---maintenance-vs-downtime"></a>VM 다시 부팅 이해 - 유지 관리 및 가동 중지
영향을 받음 되 고 Azure에서 toovirtual 컴퓨터를 초래할 수 있는 세 가지 시나리오가 있습니다: 계획 되지 않은 하드웨어 유지 관리, 예기치 않은 작동 중단 및 계획 된 유지 관리 합니다.

* **계획 되지 않은 하드웨어 유지 관리 이벤트** toofail에 대 한 hello 하드웨어 또는 모든 플랫폼 구성 요소 관련된 tooa 물리적 컴퓨터는 Azure 플랫폼 예측 때 hello 발생 합니다. Hello 플랫폼 오류가 예측 하는 경우는 계획 되지 않은 하드웨어 유지 관리 이벤트 tooreduce hello 영향 toohello 호스팅되는 가상 컴퓨터 하드웨어에서 실행 됩니다. Azure는 hello 장애가 발생 한 하드웨어 tooa 정상적인 물리적 컴퓨터에서에서 실시간 마이그레이션 기술 toomigrate hello 가상 컴퓨터를 사용 합니다. 실시간 마이그레이션이 VM 작업을 일시 중지만 짧은 시간에 대 한 가상 컴퓨터를 hello를 유지 합니다. 메모리, 열려 있는 파일 및 네트워크 연결 유지 되지만 앞 이나 뒤 hello 이벤트 성능이 저하 될 수 있습니다. 실시간 마이그레이션을 사용할 수 없습니다의 경우에서 아래 설명 된 대로 hello VM 예기치 않은 작동 중단 발생 합니다.


* **예기치 않은 작동 중단 시간이** 거의 어떤 방식으로든에서 hello 하드웨어 또는 가상 컴퓨터를 내부 hello 실제 인프라에 오류가 발생 하는 경우 발생 합니다. 여기에는 로컬 네트워크 오류, 로컬 디스크 오류 또는 기타 랙 수준의 오류가 포함될 수도 있습니다. 이러한 오류가 감지 되 면 hello Azure 플랫폼 자동 마이그레이션합니다 (회복) 가상 컴퓨터 tooa 정상적인 물리적 컴퓨터입니다. 가상 컴퓨터 복구 프로시저는 hello, 동안 가동 중지 시간 (다시 부팅)을 발생할 및 hello 임시 드라이브의 일부의 경우 손실에서 합니다. hello 연결 OS 및 데이터 디스크 항상 유지 됩니다. 

* **유지 관리 이벤트가 예정** Azure 플랫폼 tooimprove 기본 Microsoft toohello를 통한 정기적인 업데이트는 전체 안정성, 성능 및 가상 컴퓨터에서 실행 되는 hello 플랫폼 인프라의 보안을 합니다. 이러한 업데이트는 대부분 Virtual Machines 또는 Cloud Services에 영향을 주지 않고 수행됩니다([VM 보존 유지 관리](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/preserving-maintenance) 참조). Hello Azure 플랫폼의 모든 가능한 경우에서 toouse VM 유지 유지 관리 하면, 하는 경우가 드물게 이러한 업데이트에는 가상 컴퓨터 tooapply hello 필수 업데이트 toohello 기본 인프라를 다시 부팅 해야 합니다. 이 경우 hello 적합 한 기간에 해당 Vm에 대 한 hello 유지 관리를 시작 하 여 Azure 계획 된 유지 관리 재배포 유지 관리 작업을 수행할 수 있습니다. 자세한 내용은 [Virtual Machines에 대한 계획된 유지 관리](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/planned-maintenance/)를 참조하세요.


이러한 이벤트 중 tooone 이상 인해 가동 중지 시간 tooreduce hello 영향, hello 고가용성 가상 컴퓨터에 대 한 최선의 구현 방법을 권장 합니다.

* [중복성을 위해 가용성 집합에서 여러 가상 컴퓨터 구성]
* [가용성 집합의 VM에 Managed Disks 사용]
* [예약 된 이벤트 tooproactively 응답 tooVM 이벤트에 영향을 주지 사용] (https://docs.microsoft.com/en-us/azure/virtual-machines/virtual-machines-scheduled-events)
* [각 응용 프로그램 계층을 별도의 가용성 집합으로 구성]
* [가용성 집합과 부하 분산 장치 결합]

## <a name="configure-multiple-virtual-machines-in-an-availability-set-for-redundancy"></a>중복성을 위해 가용성 집합에서 여러 가상 컴퓨터 구성
tooprovide 중복 tooyour 응용 프로그램을 가용성 집합에 두 개 이상의 가상 컴퓨터를 그룹화 할 두는 것이 좋습니다. 이 구성을 사용 하면 계획 되거나 계획 되지 않은 유지 관리 이벤트 중 하나에서 하나 이상의 가상 컴퓨터를 사용할 수 있는 충족 hello 99.95% Azure SLA 합니다. 자세한 내용은 참조 hello [가상 컴퓨터에 대 한 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)합니다.

> [!IMPORTANT]
> 가용성 집합 안에 단일 인스턴스 가상 컴퓨터를 단독으로 두지 않도록 하십시오. 이러한 구성의 VM은 SLA 보증에 맞지 않으며 단일 VM이 [Azure Premium Storage](../articles/storage/common/storage-premium-storage.md)를 사용하는 경우를 제외하고 Azure 계획된 유지 관리 이벤트 중에 가동 중지하게 됩니다. 프리미엄 저장소를 사용 하 여 단일 Vm에 대 한 Azure SLA hello 적용 됩니다.

각 가상 컴퓨터 가용성 집합에 할당 된 프로그램 **업데이트 도메인** 및 **장애 도메인** hello Azure 플랫폼을 기본으로 합니다. 지정 된 가용성 집합에 대 한 5 개의 사용자를 구성할 수 없는 업데이트 도메인은 기본적으로 할당 됩니다 (리소스 관리자 배포 수 too20 업데이트 도메인을 증가 tooprovide) 가상 컴퓨터 및 기본 물리적 하드웨어 tooindicate 그룹 hello에 다시 부팅할 수 있습니다 동시 합니다. Hello 여섯 번째 가상 컴퓨터 것과 같은 업데이트 도메인으로 첫 번째 가상 컴퓨터 hello hello 일곱 번째 hello로 두 번째 가상 컴퓨터를 hello 등과 같은 업데이트 도메인에 hello에 놓입니다 단일 가용성 집합 내에서 6 개 이상의 가상 컴퓨터를 구성한 경우 켜 집니다. 한 번에 하나의 업데이트 도메인을 다시 부팅 되 고 계속할 수 없습니다 순차적으로 계획 된 유지 관리 하는 동안 업데이트 도메인의 hello 순서를 다시 부팅 합니다. 서로 다른 업데이트 도메인에서 유지 관리 시작 하기 전에 다시 부팅 된 업데이트 도메인에서 30 분 toorecover를 제공 됩니다.

오류 도메인 hello 공통 전원 원본과 네트워크 스위치를 공유 하는 가상 컴퓨터 그룹을 정의 합니다. 기본적으로 가용성 집합 내에서 구성 된 hello 가상 컴퓨터 (클래식에 대 한 두 개의 오류 도메인) 리소스 관리자 배포에 대 한 toothree 오류 도메인을 걸쳐 분리 되어 있습니다. 가용성 집합에 가상 컴퓨터 배치를 보호 하지 응용 프로그램에서 운영 체제 또는 응용 프로그램 관련 오류가 발생 하는 동안 발생할 수 있는 물리적 하드웨어 오류, 네트워크 중단 또는 전원 중단의 hello 영향을 제한지 않습니다.

<!--Image reference-->
   ![개념도 hello 업데이트 도메인과 오류 도메인 구성](./media/virtual-machines-common-manage-availability/ud-fd-configuration.png)

## <a name="use-managed-disks-for-vms-in-an-availability-set"></a>가용성 집합에서 VM에 Managed Disks 사용
관리 되지 않는 디스크가 있는 Vm을 현재 사용 중인, 하는 경우 항상 좋습니다 [toouse 관리 하는 디스크 가용성 집합의 Vm으로 변환](../articles/virtual-machines/windows/convert-unmanaged-to-managed-disks.md)합니다.

[관리 디스크](../articles/virtual-machines/windows/managed-disks-overview.md) tooavoid 단일 실패 지점을를 서로 격리 된 가용성 집합에 있는 Vm의 hello 디스크는 충분히 확인 하 여 가용성 집합에 대 한 안정성을 제공 합니다. 다른 저장소 클러스터에 hello 디스크를 자동으로 배치 하 여 수행 합니다. 저장소 클러스터 toohardware 또는 소프트웨어 오류로 인해 실패 하면 해당 스탬프에 디스크를 사용 하 여 VM 인스턴스만 hello 실패 합니다.

![Managed Disk FD](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> 지역-관리 되는 가용성 집합에 대 한 장애 도메인 수 hello 다릅니다 2 또는 3 / 지역당 중 하나입니다. 다음 테이블 / 지역당 hello 수를 표시 하는 hello

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

Toouse Vm을 계획 하는 경우 [디스크를 관리 되지 않는](../articles/virtual-machines/windows/about-disks-and-vhds.md#types-of-disks), 아래 저장소 계정으로 Vm의 가상 하드 디스크 (Vhd) 저장 되는 위치에 대 한 모범 사례에 따라 [페이지 blob](https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs#about-page-blobs)합니다.

1. **유지 (OS 및 데이터) 관련 된 모든 디스크에 있는 VM hello에 동일한 저장소 계정**
2. **검토 hello [제한](../articles/storage/common/storage-scalability-targets.md) hello 다양 한 저장소 계정에 관리 되지 않는 디스크에** 자세한 Vhd tooa 저장소 계정을 추가 하기 전에
3. **가용성 집합의 각 VM마다 별도의 저장소 계정을 사용합니다.** Hello에 여러 Vm이 포함 된 저장소 계정을 공유 하지 않으므로 동일한 가용성 집합입니다. 사용할 수 있기 Vm에 대 한 다른 가용성 집합 tooshare 저장소 계정에서 위에 모범 사례를 수행 하는 경우

## <a name="configure-each-application-tier-into-separate-availability-sets"></a>각 응용 프로그램 계층을 별도의 가용성 집합으로 구성
가상 컴퓨터 모두 거의 동일 하 고 hello를 사용 하는 경우 동일한 용도로 응용 프로그램에 대 한 가용성 집합을 응용 프로그램의 각 계층을 구성 하는 것이 좋습니다.  배치 하는 경우 두 개의 서로 다른 계층 hello에 동일한 가용성 집합 모든 가상 컴퓨터가 hello 동일한 응용 프로그램 계층을 한 번에 다시 부팅할 수 있습니다. 각 계층에 대해 최소 두 개의 가상 컴퓨터를 가용성 집합 안에 구성하면 각 계층에서 최소한 하나의 가상 컴퓨터는 사용할 수 있습니다.

예를 들어 단일 가용성 집합에 IIS, Apache Nginx를 실행 하는 응용 프로그램의 프런트 엔드 hello에서에서 모든 hello 가상 컴퓨터를 배치할 수 있습니다. 사용 했는지 확인 프런트 엔드 가상 컴퓨터는 hello에 동일한 가용성 집합입니다. 마찬가지로 데이터 계층 가상 컴퓨터만 자체의 가용성 집합(예: 복제된 SQL Server 가상 컴퓨터 또는 MySQL 가상 컴퓨터)에 배치해야 합니다.

<!--Image reference-->
   ![응용 프로그램 계층](./media/virtual-machines-common-manage-availability/application-tiers.png)

## <a name="combine-a-load-balancer-with-availability-sets"></a>가용성 집합과 부하 분산 장치 결합
Hello 결합 [Azure 부하 분산 장치](../articles/load-balancer/load-balancer-overview.md) 가용성 집합 tooget hello 대부분 응용 프로그램 복구 합니다. hello Azure 부하 분산 장치에는 여러 가상 컴퓨터 간에 트래픽을 분산 시킵니다. 이 표준 계층 가상 컴퓨터에 대 한 hello Azure 부하 분산 장치는 포함 되어 있습니다. 일부 가상 컴퓨터 계층 hello Azure 부하 분산 장치를 포함합니다. 가상 컴퓨터 부하 분산에 대한 자세한 내용은 [가상 컴퓨터 부하 분산](../articles/virtual-machines/virtual-machines-linux-load-balance.md)을 참조하세요.

부하 분산 장치 hello 없으면 toobalance 트래픽을 여러 가상 컴퓨터에서 구성 된 계획 된 유지 관리 이벤트 hello만 트래픽 서비스 가상 컴퓨터를 일으키는 중단 tooyour 응용 프로그램 계층에 영향을 줍니다. 동일한 부하 분산 장치 및 가용성 집합 사용 트래픽 toobe 지속적으로 인스턴스를 하나 이상에서 제공 하는 hello에서 동일한 계층 hello의 여러 가상 컴퓨터를 배치 합니다.


<!-- Link references -->
[중복성을 위해 가용성 집합에서 여러 가상 컴퓨터 구성]: #configure-multiple-virtual-machines-in-an-availability-set-for-redundancy
[각 응용 프로그램 계층을 별도의 가용성 집합으로 구성]: #configure-each-application-tier-into-separate-availability-sets
[가용성 집합과 부하 분산 장치 결합]: #combine-a-load-balancer-with-availability-sets
[Avoid single instance virtual machines in availability sets]: #avoid-single-instance-virtual-machines-in-availability-sets
[가용성 집합의 VM에 Managed Disks 사용]: #use-managed-disks-for-vms-in-an-availability-set
