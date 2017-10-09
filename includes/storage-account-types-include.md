저장소 계정에는 다음과 같은 두 종류가 있습니다.

### <a name="general-purpose-storage-accounts"></a>범용 저장소 계정
일반적인 용도의 스토리지 계정 액세스할 수 있도록 테이블, 큐, 파일, Blob 및 Azure와 같은 tooAzure 저장소 서비스는 단일 계정에서 가상 컴퓨터 디스크. 이 저장소 계정이 유형에는 다음과 같이 두 가지 성능 계층이 있습니다.

* 표준 저장소 성능 계층 toostore 테이블, 큐, 파일, Blob 및 Azure 수 있는 가상 컴퓨터 디스크.
* 현재 Azure 가상 컴퓨터 디스크만 지원하는 프리미엄 저장소 성능 계층. 프리미엄 저장소의 자세한 개요는 [프리미엄 저장소: Azure 가상 컴퓨터 작업을 위한 고성능 저장소](../articles/storage/common/storage-premium-storage.md) 를 참조하세요.

### <a name="blob-storage-accounts"></a>Blob 저장소 계정
Blob 저장소 계정은 Azure 저장소에서 Blob와 같은 구조화되지 않은 데이터(개체) 저장을 위한 특수 저장소 계정입니다. Blob 저장소 계정이 유사한 tooyour 기존 일반적인 용도의 스토리지 계정 이므로 기능을 공유 모든 hello 훌륭한 내구성, 가용성, 확장성 및 성능 100 %API 일관성 비롯 하 여 블록 blob에 대 한 현재 사용 하 고 추가 blob입니다. 블록 또는 연결 Blob 저장소만 필요한 응용 프로그램의 경우 Blob 저장소 계정을 사용하는 것이 좋습니다.

> [!NOTE]
> Blob 저장소 계정은 블록 및 추가 Blob만 지원하고 페이지 Blob은 지원하지 않습니다.
> 
> 

Blob 저장소 계정 노출 hello **액세스 계층** 특성-계정 만들기 중에 지정 하 고 필요에 따라 나중에 수정할 수 있습니다. 데이터 액세스 패턴에 따라 다음 두 가지 액세스 계층 유형을 지정할 수 있습니다.

* A **핫** 액세스 계층 hello 개체 hello 저장소 계정에 더 자주 액세스는 나타냅니다. 이렇게 하면 있습니다 toostore 데이터 액세스 비용 절감.
* A **쿨** 액세스 계층 hello 개체 hello 저장소 계정에 덜 자주 액세스는 나타냅니다. 이렇게 하면 있습니다 toostore 데이터 데이터 저장소 비용이 저렴 합니다.

데이터의 hello 사용 패턴에서 변경 있으면 언제 든 지 이러한 액세스 계층 간에 전환할 수 있습니다. 변경 hello 액세스 계층 추가 요금이 발생할 수 있습니다. 자세한 내용은 [Pricing and billing for Blob storage accounts](../articles/storage/blobs/storage-blob-storage-tiers.md#pricing-and-billing) (Blob 저장소 계정에 대한 가격 책정 및 청구)를 참조하세요.

Blob 저장소 계정에 대한 자세한 내용은 [Azure Blob 저장소: 쿨 및 핫 계층](../articles/storage/blobs/storage-blob-storage-tiers.md)을 참조하세요.

Azure 구독을 제공 하는 계획은 저장소 계정을 만들 수 있습니다, 전에 있어야 tooa 다양 한 Azure 서비스에 액세스 합니다. [무료 계정](https://azure.microsoft.com/pricing/free-trial/)으로 Azure를 시작할 수 있습니다. Toopurchase 구독 계획을 결정 하면 다양 한에서 선택할 수 있습니다 [구매 옵션](https://azure.microsoft.com/pricing/purchase-options/)합니다. [MSDN 구독자](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)는 Azure 저장소를 포함한 Azure 서비스에 사용할 수 있는 무료 월별 크레딧을 받습니다. 볼륨 가격에 대한 자세한 내용은 [Azure 저장소 가격 책정 ](https://azure.microsoft.com/pricing/details/storage/) 을 참조하세요.

toolearn toocreate 저장소 계정을 참조 하는 방법을 [저장소 계정 만들기](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account) 내용을 확인 합니다. 단일 구독으로 저장소 계정 이름이 고유한 too200를 만들 수 있습니다. 저장소 계정 제한에 대한 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](../articles/storage/common/storage-scalability-targets.md) 를 참조하세요.

