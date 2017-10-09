# <a name="regions-and-availability-for-virtual-machines-in-azure"></a>Azure에서 가상 컴퓨터의 지역 및 가용성
Azure는 hello 전 세계 여러 데이터 센터에서 작동합니다. 이러한 데이터 센터 위치 선택에 유연성을 제공, toogeographic 영역에 그룹화 되어 toobuild 응용 프로그램입니다. 이것은 중요 한 toounderstand 어떻게 옵션 toomaximize 성능, 가용성 및 중복성 함께 가상 컴퓨터 (Vm) Azure에서 작동 하는 위치입니다. 이 문서에서는 hello 가용성에 대 한 개요 및 Azure의 중복 기능을 사용 합니다.

## <a name="what-are-azure-regions"></a>Azure 지역이란?
'미국 서부', '북유럽' 또는 '동남 아시아'와 같이 정의된 지역에 Azure 리소스를 만듭니다. Hello를 검토할 수 있습니다 [지역 및 해당 위치의 목록](https://azure.microsoft.com/regions/)합니다. 각 지역의 여러 데이터 센터 tooprovide 중복성 및 가용성을 위해 존재합니다. 이 방법을 사용 하면 유연성 법률, 규정 준수, 응용 프로그램 toocreate Vm 가장 가까운 tooyour 사용자 및 toomeet를 디자인 하거나 세금 때.

## <a name="special-azure-regions"></a>특수 Azure 지역
Azure에 몇 가지 특별 한 지역 규정 준수 또는 법적 목적으로 응용 프로그램을 빌드할 때 toouse를 지정할 수 있습니다. 이 특수 지역에는 다음이 포함됩니다.

* **미국 버지니아 주 정부** 및 **미국 아이오와 주 정부**
  * 미국 정부 기관 및 파트너를 위한 물리적 및 논리적 네트워크로 격리된 Azure 인스턴스로, 선별된 미국인이 운영합니다. [FedRAMP](https://www.microsoft.com/en-us/TrustCenter/Compliance/FedRAMP) 및 [DISA](https://www.microsoft.com/en-us/TrustCenter/Compliance/DISA)와 같은 추가 규정 준수 인증서를 포함합니다. [Azure Government](https://azure.microsoft.com/features/gov/)에 대해 자세히 알아보세요.
* **중국 동부** 및 **중국 북부**
  * 이러한 영역은 Microsoft와 그에 따라 Microsoft는 직접 유지 관리 하지 hello 데이터 센터 21Vianet 사이의 고유한 파트너 관계를 통해 사용할 수 있습니다. [중국의 Microsoft Azure](http://www.windowsazure.cn/)에 대해 자세히 알아보세요.
* **독일 중부** 및 **독일 북동부**
  * 이러한 영역은 T-시스템의 제어 역할을 hello 독일어 데이터 트러스티 독일 통신 국 회사에서 고객 데이터 독일에 유지 하는 그에 따라 데이터 트러스티 모델을 통해 사용할 수 있습니다.

## <a name="region-pairs"></a>지역 쌍
각 Azure 영역의 다른 영역 hello 내와 쌍을 이루는 동일한 지리적 위치 (미국, 유럽, 아시아 등). Hello 자연 재해, 민사 동요, 정전 또는 한 번에 두 지역에 영향을 주는 실제 네트워크 작동 중단 될 가능성을 축소 해야 하는 지리 분산 시킬 수 있으므로 hello 복제 VM 저장소 등의 리소스에 대 한이 방법을 사용 합니다. 지역 쌍에 대한 추가적인 이점은 다음과 같습니다.

* 더 다양 한 Azure 중단의 hello 이벤트에서 한 영역 우선 순위가 지정 되어 모든 쌍 부족 toohelp 줄일 응용 프로그램에 대 한 hello 시간 toorestore 합니다. 
* 계획 된 Azure 업데이트 toopaired 영역 하나에서 시간 toominimize 가동 중지 시간 및 응용 프로그램 중단의 위험이 롤백됩니다.
* 데이터 계속 hello 내 tooreside 세금 및 법 적용 jurisdiction 용도 쌍 (제외 브라질 남쪽)으로 동일한 지리적 위치입니다.

지역 쌍 예제는 다음과 같습니다.

| 보조 | 주 |
|:--- |:--- |
| 미국 서부 |미국 동부 |
| 북유럽 |서유럽 |
| 동남아시아 |동아시아 |

Hello 전체를 볼 수 있습니다 [국가 목록이 여기 쌍](../articles/best-practices-availability-paired-regions.md#what-are-paired-regions)합니다.

## <a name="feature-availability"></a>기능 가용성
일부 서비스 또는 VM 기능(예: 특정 VM 크기 또는 저장소 형식)은 특정 지역에서만 사용할 수 있습니다. 필요 하지 않은 있습니다 tooselect 특정 지역와 같은 일부 글로벌 Azure 서비스는 또한 [Azure Active Directory](../articles/active-directory/active-directory-whatis.md), [트래픽 관리자](../articles/traffic-manager/traffic-manager-overview.md), 또는 [Azure DNS](../articles/dns/dns-overview.md)합니다. tooassist 하면 응용 프로그램 환경을 디자인할 hello를 확인할 수 있습니다 [각 지역에 걸쳐 Azure 서비스의 가용성](https://azure.microsoft.com/regions/#services)합니다. 

## <a name="storage-availability"></a>저장소 가용성
Hello 사용 가능한 저장소 복제 옵션을 고려 하는 경우 Azure 지역 및 지리적 이해 하는 것이 중요 합니다. Hello 저장 유형에 따라 서로 다른 복제 선택 사항이 있습니다.

**Azure Managed Disks**
* LRS(로컬 중복 저장소)
  * 세 번 저장소 계정을 만든 hello 영역 내에 데이터를 복제 합니다.

**저장소 계정 기반 디스크**
* LRS(로컬 중복 저장소)
  * 세 번 저장소 계정을 만든 hello 영역 내에 데이터를 복제 합니다.
* ZRS(영역 중복 저장소)
  * 단일 지역 내 또는 두 영역 간 두 toothree 시설에 걸쳐 데이터를 3 번 복제 합니다.
* GRS(지역 중복 저장소)
  * 사용자 데이터 tooa 보조 지역에 수백 마일 떨어진 hello 기본 지역에 복제 합니다.
* RA-GRS(읽기 액세스 지역 중복 저장소)
  * GRS를와 마찬가지로 tooa 보조, 데이터 영역을 복제 하 하지만 그 후 toohello 데이터 hello 보조 위치에 읽기 전용 액세스를 제공 합니다.

hello 다음 표에서 hello 저장소 복제 유형 간의 hello 차이점을 간략히 요약 합니다.

| 복제 전략 | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| 데이터가 여러 시설에 걸쳐 복제됩니다. |아니요 |예 |예 |예 |
| Hello 기본 위치와 hello 보조 위치에서 데이터를 읽을 수 있습니다. |아니요 |아니요 |아니요 |예 |
| 별도 노드에서 유지 관리되는 데이터 복사본 수입니다. |3 |3 |6 |6 |

[여기에서 Azure Storage 복제 옵션](../articles/storage/common/storage-redundancy.md)에 대해 자세히 알아볼 수 있습니다. 관리 디스크에 대한 자세한 내용은 [Azure Managed Disks 개요](../articles/virtual-machines/windows/managed-disks-overview.md)를 참조하세요.

### <a name="storage-costs"></a>저장소 비용
Hello 저장소 유형 및 선택 하는 가용성에 따라 가격이 달라 집니다.

**Azure Managed Disks**
* 프리미엄 Managed Disks는 SSD(반도체 드라이브)로 지원되며, 표준 Managed Disks는 일반 회전 디스크로 지원됩니다. Premium 및 관리 하는 표준 디스크를 모두 hello 디스크에 대 한 사용자를 프로 비전 하는 hello 용량에 따라 요금이 청구 됩니다.

**관리되지 않는 디스크**
* 프리미엄 저장소는 Solid-State Ssd ()에서 지원 되며 및 hello 디스크의 hello 용량에 따라 요금이 부과 됩니다.
* 표준 저장소 hello 사용 중인 용량에 따라 요금이 청구 및 필요한 저장소 가용성 일반 회전 디스크에 의해 지원 됩니다.
  * RA-GRS 해당 데이터 tooanother Azure 지역 복제의 hello 대역폭에 대 한 추가 지리적 복제 데이터 전송 요금이 있습니다.

참조 [Azure 저장소 가격](https://azure.microsoft.com/pricing/details/storage/) 가격 hello 다른 저장소 형식 및 사용 가능 옵션에 대 한 정보입니다.

## <a name="availability-sets"></a>가용성 집합
가용성 집합은 Azure toounderstand 허용 하는 Vm의 논리적 그룹 응용 프로그램 빌드 tooprovide 중복성 및 가용성이 대 한 방법입니다. 항상 사용 가능한 응용 프로그램 및 toomeet hello에 대 한 가용성 집합 tooprovide 프로그램 내에서 둘 이상의 Vm 만들어졌는지 하는 것이 좋습니다 [99.95% Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)합니다. 단일 VM 사용 하 여 [Azure 프리미엄 저장소](../articles/storage/common/storage-premium-storage.md), hello 계획 되지 않은 유지 관리 이벤트에 대 한 Azure SLA를 적용 합니다. 

하드웨어 오류 로부터 보호 하 고 toosafely 수 업데이트를 허용 하는 두 개의 추가 그룹화는 가용성 집합은 구성 적용-오류 도메인 (Fd) 및 도메인 (Ud)를 업데이트 합니다.

![개념도 hello 업데이트 도메인과 오류 도메인 구성](./media/virtual-machines-common-regions-and-availability/ud-fd-configuration.png)

에 대 한 자세한 내용은 방법 toomanage hello의 가용성을 [Linux Vm](../articles/virtual-machines/linux/manage-availability.md) 또는 [Windows Vm](../articles/virtual-machines/windows/manage-availability.md)합니다.

### <a name="fault-domains"></a>장애 도메인
장애 도메인은 동일한 전원을 공유 하는 기본 하드웨어의 논리적 그룹 및 네트워크 스위치는 온-프레미스 데이터 센터 내에서 유사한 tooa 랙 합니다. 가용성 집합 내에서 Vm을 만들 때 hello Azure 플랫폼 장애 도메인 이러한 Vm에 자동으로 분산 합니다. 이 방법은 발생할 수 있는 물리적 하드웨어 오류, 네트워크 중단 또는 전원 중단의 hello 영향을 제한합니다.

### <a name="update-domains"></a>업데이트 도메인
업데이트 도메인 유지 관리 될 수 있습니다 또는 hello에서 다시 부팅 해야 하는 기본 하드웨어의 논리적 그룹은 같은 시간입니다. 가용성 집합 내에서 Vm을 만들 때 hello Azure 플랫폼 자동으로 분산 Vm이 도메인을 업데이트 합니다. 이 방법을 사용 하면 응용 프로그램의 인스턴스를 하나 이상 해당 항상 hello Azure 플랫폼에서 정기적으로 유지 관리 실행 되는 상태로 유지 됩니다. 한 번에 하나의 업데이트 도메인을 다시 부팅 되 고 계속할 수 없습니다 순차적으로 계획 된 유지 관리 하는 동안 업데이트 도메인의 hello 순서를 다시 부팅 합니다.

### <a name="managed-disk-fault-domains"></a>관리 디스크 장애 도메인
[Azure Managed Disks](../articles/virtual-machines/windows/faq-for-disks.md)를 사용하는 VM의 경우, 관리 가용성 집합을 사용할 때 VM은 관리 디스크 장애 도메인에 맞춰집니다. 이 정렬 되도록 연결 된 tooa VM hello 내에 있는 관리 되는 디스크를 hello 모두 같은 관리 되는 디스크 오류 도메인입니다. 관리 디스크의 VM만 관리 가용성 집합에서 만들어질 수 있습니다. 관리 되는 디스크 오류 도메인 hello 수 / 지역당 2 또는 3 개의 관리 되는 디스크 오류 도메인-지역에 따라 달라 집니다.

![Managed Disk FD](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> 지역-관리 되는 가용성 집합에 대 한 장애 도메인 수 hello 다릅니다 2 또는 3 / 지역당 중 하나입니다. 다음 테이블 / 지역당 hello 수를 표시 하는 hello

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

## <a name="next-steps"></a>다음 단계
이제 시작할 수 있습니다 toouse 이러한 가용성 및 중복 기능 toobuild Azure 환경입니다. 모범 사례 정보는 [Azure 가용성 모범 사례](../articles/best-practices-availability-checklist.md)를 참조하세요.

