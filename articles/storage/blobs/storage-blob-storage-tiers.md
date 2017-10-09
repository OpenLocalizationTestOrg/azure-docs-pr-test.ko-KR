---
title: "aaaAzure 핫, 됐습니다, 및 보관 저장소 blob에 대 한 | Microsoft Docs"
description: "Azure Blob Storage 계정에 대한 핫, 쿨 및 보관 저장소입니다."
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: eb33ed4f-1b17-4fd6-82e2-8d5372800eef
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/05/2017
ms.author: mihauss
ms.openlocfilehash: 42fb699bf16147ba8a4d9f75a62debadea5af65e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-blob-storage-hot-cool-and-archive-preview-storage-tiers"></a>Azure Blob Storage: 핫, 쿨 및 보관(미리 보기) 저장소 계층

## <a name="overview"></a>개요

Azure Storage는 Blob 개체 저장소에 세 가지 저장소 계층을 제공하므로 사용하는 방식에 따라 가장 비용 효율적으로 데이터를 저장할 수 있습니다. Azure hello **핫 저장소 계층** 자주 액세스 되는 데이터를 저장 하기 위해 최적화 됩니다. Azure hello **쿨 저장소 계층** 자주 액세스 되 고 적어도 한 달 저장 된 데이터를 저장 하기 위해 최적화 됩니다. hello [보관 저장소 계층 (미리 보기)](https://azure.microsoft.com/blog/announcing-the-public-preview-of-azure-archive-blob-storage-and-blob-level-tiering) 거의 액세스 되 고 6 개월 이상 시간의 hello 순서 대로) (on 유연한 대기 시간 요구 사항에 대해 저장 된 데이터를 저장 하기 위해 최적화 됩니다. hello *보관* 저장소 계층 hello 전체 저장소 계정이 아니라 hello blob 수준에 사용할 수만 있습니다. Hello 쿨 저장소 계층의 데이터를 약간 낮아집니다 가용성을 허용할 수 있지만 여전히 내구성이 수준과 핫 데이터와 비슷한 액세스 시간 및 처리량 특징이 필요 합니다. 쿨 데이터 및 보관 데이터의 경우 저장소 비용을 크게 낮추기 위해 가용성 SLA는 약간 낮고 액세스 비용은 다소 높아도 됩니다.

오늘날 hello 클라우드에 저장 된 데이터는 지 수 속도로 커지고 있습니다. 확장 저장소 요구 사항에 대 한 비용이 toomanage에 유용한 tooorganize 데이터 액세스의 빈도 같은 특성을 기반으로 하 고 보존 기간을 계획 합니다. Hello 클라우드에 저장 된 데이터를 생성, 처리 및 방법을 수명 주기 동안 액세스 측면에서 다를 수 있습니다. 일부 데이터는 수명 기간 전반에 걸쳐 활발하게 액세스되고 수정됩니다. 일부 데이터는 hello 데이터 연령으로 현저 하 게 삭제 액세스 권한이 있는, 수명 중에 일찍 자주 액세스 됩니다. 일부 데이터 hello 클라우드에서 유휴 상태를 유지 하 고 경우에, 어느 단 한 번 액세스 하는 경우 저장 합니다.

이러한 각각의 데이터 액세스 시나리오에서는 특정 액세스 패턴에 맞게 최적화되어 차별화된 저장소 계층이 유익합니다. Azure Blob Storage는 핫, 쿨 및 보관 저장소 계층에서 별도의 가격 책정 모델을 통한 차별화된 저장소 계층에 대한 이러한 수요를 해결합니다.

## <a name="blob-storage-accounts"></a>Blob 저장소 계정

**Blob 저장소 계정**은 Azure Storage에서 Blob(개체)과 같은 구조화되지 않은 데이터를 저장하기 위한 특수 저장소 계정입니다. Blob 저장소 계정이 있는 핫 사이 이제 선택할 수 있으며 쿨 저장소 계층 계정 수준 또는 핫, 냉각용, 및 액세스 패턴을 기반으로 hello blob 수준에서 계층을 보관 합니다. Hello 가장 낮은 저장소 비용이, 핫 hello 최저 액세스 비용에 더 자주 액세스 핫 데이터를 저장할 것 보다 비용이 낮은 저장소에서 자주 액세스 쿨 데이터를 적게 거의 액세스 콜드 데이터를 저장 합니다. Blob 저장소 계정이 유사한 tooyour 기존 범용 저장소 계정 및 모든 hello 훌륭한 내구성, 가용성, 확장성 및 성능 기능을 사용 하면 오늘날에 블록 blob에 대 한 API 일관성 100%를 포함 하 여 공유 및 추가 blob입니다.

> [!NOTE]
> Blob 저장소 계정은 블록 및 추가 Blob만 지원하고 페이지 Blob은 지원하지 않습니다.

Blob 저장소 계정 노출 hello **액세스 계층** toospecify hello 저장소 계층으로 수 있는 특성 **핫** 또는 **쿨** hello에 저장 된 hello 데이터에 따라 계정입니다. 데이터의 hello 사용 패턴에서 변경 있으면 언제 든 지 이러한 저장소 계층 간에 전환할 수 있습니다. hello 보관 계층 (미리 보기) hello blob 수준에만 적용할 수 있습니다.

> [!NOTE]
> 변경 hello 저장소 계층 추가 요금이 발생할 수 있습니다. Hello 참조 [가격 및 청구](#pricing-and-billing) 자세한 내용은 섹션.

### <a name="hot-access-tier"></a>핫 액세스 계층

Hello 핫 저장소 계층에 대 한 예제 사용 시나리오는 다음과 같습니다.

* 현재 사용 중인 또는 예상된 toobe (에서 읽기 및 쓰기) 자주 액세스 하는 데이터입니다.
* 처리 및 최종 마이그레이션 toohello 쿨 저장소 계층에 대 한 준비 된 데이터입니다.

### <a name="cool-access-tier"></a>쿨 액세스 계층

Hello 쿨 저장소 계층에 대 한 예제 사용 시나리오는 다음과 같습니다.

* 단기 백업 및 재해 복구 데이터 집합
* 오래 된 미디어 콘텐츠 자주 더 이상 볼 아니라은 액세스 하는 때에 즉시 사용할 수 있는 예상된 toobe 수 있습니다.
* 나중에 처리에 대 한 더 많은 데이터를 수집 하는 비용 효과적으로 저장 toobe 해야 하는 큰 데이터 집합. (*예:* 과학적 데이터의 장기 저장, 제조 설비의 원시 원격 분석 데이터)

### <a name="archive-access-tier-preview"></a>보관 액세스 계층(미리 보기)

[보관 저장소](https://azure.microsoft.com/blog/announcing-the-public-preview-of-azure-archive-blob-storage-and-blob-level-tiering) hello 가장 낮은 저장소 비용 및 높은 데이터 검색에 비해 비용이 toohot와 쿨 저장 합니다.

Blob이 보관 저장소에 있지만 읽거나, 복사하거나, 덮어쓰거나, 수정할 수 없습니다. 또는 보관 저장소에서 Blob의 스냅숏을 만들 수도 없습니다. 그러나 기존 작업 toodelete를 사용 하 여, 목록, blob 속성/메타 데이터 가져오기 수도 있습니다 blob의 hello 계층을 변경 합니다. 보관 저장소에서 tooread 데이터를 먼저 hello blob toohot 또는 쿨 hello 계층을 변경 해야 합니다. 이 프로세스는 리하이드레이션 라고 하 고 50GB 보다 작은 blob에 대 한 시간 toocomplete too15 정도 걸릴 수 있습니다. Hello blob 처리량 한도 보다 큰 blob에 대 한 필요한 추가 시간에 따라 다릅니다.

리하이드레이션을 하는 동안 hello 계층 변경 된 경우 hello "상태를 보관" blob 속성 tooconfirm를 확인할 수 있습니다. hello 상태 "리하이드레이션-보류 중인-에-높음" 또는 "리하이드레이션-보류 중인-에-쿨" hello 대상 계층에 따라 읽습니다. Blob 속성 완료, "상태를 보관" blob 속성이 제거 되 면 hello 및 "액세스 계층" hello 시 hello 핫 또는 쿨 계층을 반영 합니다.  

Hello 보관 저장소 계층에 대 한 예제 사용 시나리오는 다음과 같습니다.

* 장기 백업, 보관 및 재해 복구 데이터 집합
* 사용 가능한 최종 형태로 처리된 후에도 보존할 필요가 있는 원래(원시) 데이터. (*예:* 다른 형식으로 코드 변환한 원시 미디어 파일)
* 규정 준수 및 아카이브 데이터에 필요한 toobe 오랜 시간 동안 저장 하 고 액세스 거의 적이 됩니다. (*예:* 보안 카메라 영상, 의료 기관의 오래된 X레이/MRI, 금융 기관의 고객 통화에 대한 오디오 녹음 및 내용 자료)

### <a name="recommendations"></a>권장 사항

저장소 계정에 대한 자세한 내용은 [Azure 저장소 계정 정보](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) 를 참조하세요.

만 필요한 응용 프로그램을 차단 하거나 blob 저장소를 추가, Blob 저장소 계정을 사용 하는 것이 좋습니다, 그리고 tootake 활용 hello 계층화 된 저장소의 가격 책정 모델을 구분 합니다. 그러나 이렇게 하지 못할 수도 있습니다 특정 상황에서 있는 방식으로 toogo hello 범용 저장소 계정은 것을 사용 하 여 같은 이해:

* 파일 및 필요에 blob에 저장 된 hello 동일한 저장소 계정 또는 toouse 테이블, 큐를 필요. 있다는 없는 기술적 장점 toostoring hello 공유 키를 동일한 hello 것 이외의 동일한 계정에서 이러한 note 합니다.

* 여전히 toouse hello 클래식 배포 모델을 필요합니다. Blob 저장소 계정이 에게만 hello Azure 리소스 관리자 배포 모델을 통해 제공 됩니다.

* 페이지 blob toouse 필요합니다. Blob 저장소 계정은 페이지 Blob을 지원하지 않습니다. 일반적으로 페이지 Blob가 특별히 필요한 상황이 아니라면 블록 Blob를 사용하는 것이 좋습니다.

* 버전의 hello 사용 하 여 [저장소 서비스 REST API](https://msdn.microsoft.com/library/azure/dd894041.aspx) 이전 2014-02-14 버전 또는 버전으로 클라이언트 라이브러리 4.x 보다 낮게 및 응용 프로그램을 업그레이드할 수 없습니다.

> [!NOTE]
> Blob 저장소 계정은 현재 모든 Azure 지역에서 지원됩니다.
 

## <a name="blob-level-tiering-feature-preview"></a>Blob 수준 계층 기능(미리 보기)

Blob 수준 계층화 지금 사용 하면 한 번의 호출 작업을 사용 하 여 hello 개체 수준에서 데이터의 toochange hello 계층 [Blob 계층 설정](/rest/api/storageservices/set-blob-tier)합니다. 계정 간에 toomove 데이터 필요 없이 사용 패턴이 변경으로 hello 핫, 쿨, 간에 blob의 hello 액세스 계층 또는 보관 계층 쉽게 변경할 수 있습니다. 모든 계층 변경 내용은 Blob가 보관에서 리하이드레이션하는 경우를 제외하고 즉시 적용됩니다. 계층 내에서 공존할 수 있는 모든 세 가지 저장소에서 blob hello 동일한 계정입니다. 명시적으로 할당 된 계층에 없는 모든 blob는 hello 계층 hello 계정 액세스 계층 설정에서 상속 합니다.

toouse 미리 보기에서 이러한 기능에 hello hello 지침에 따라 [Azure 보관 및 Blob 수준 계층화 블로그 알림을](https://azure.microsoft.com/blog/announcing-the-public-preview-of-azure-archive-blob-storage-and-blob-level-tiering)합니다.

hello에 따라 blob 수준 계층 구성에 대 한 미리 보기 기간 동안 적용 되는 몇 가지 제한 사항이 나와 있습니다.

* 미리 보기 등록 지원 보관 저장소가 성공한 후에 미국 동부 2에서 만든 새 Blob 저장소 계정입니다.

* 미리 보기 등록 지원 Blob 수준 계층이 성공한 후에 공용 지역에서 만든 새 Blob 저장소 계정입니다.

* Blob 수준 계층 및 보관 저장소는 [LRS](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#locally-redundant-storage) 저장소에서만 지원됩니다. [GRS](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#geo-redundant-storage) 및 [RA-GRS](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#read-access-geo-redundant-storage) hello 나중에 지원 됩니다.

* 스냅숏이 있는 blob의 hello 계층을 변경할 수 없습니다.

* 보관 저장소에서 Blob을 복사하거나 스냅숏을 만들지 않을 수 있습니다.

## <a name="comparison-of-hello-storage-tiers"></a>Hello 저장소 계층의 비교

다음 표에서 hello hello 핫 및 쿨 저장소 계층의 비교를 보여 줍니다. hello 보관 blob 수준 계층 이므로 미리 보기에서는 것에 대 한 Sla 없습니다.

| | **핫 저장소 계층** | **쿨 저장소 계층** |
| ---- | ----- | ----- |
| **가용성** | 99.9% | 99% |
| **가용성** <br> **(RA-GRS 읽기)**| 99.99% | 99.9% |
| **사용 요금** | 저장소 비용 더 높음, 액세스 및 트랜잭션 비용 더 낮음 | 저장소 비용 더 낮음, 액세스 및 트랜잭션 비용 더 높음 |
| **최소 개체 크기** | 해당 없음 | 해당 없음 |
| **최소 저장 기간** | 해당 없음 | 해당 없음 |
| **대기 시간** <br> **(Toofirst 바이트 시간)** | 밀리초 | 밀리초 |
| **확장성 및 성능 대상** | 범용 저장소 계정과 동일 | 범용 저장소 계정과 동일 |

> [!NOTE]
> Blob 저장소 계정을 지원 hello 일반적인 용도의 스토리지 계정으로 동일한 성능 및 확장성 목표입니다. 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) (영문)를 참조하십시오.


## <a name="pricing-and-billing"></a>가격 책정 및 대금 청구
Blob 저장소 계정 hello 저장소 계층에 따라 blob 저장소에 대 한 가격 모델을 사용 합니다. Blob 저장소 계정, 사용 하 여 hello 청구 고려 사항에 따라 적용 됩니다.

* **저장소 비용**: 또한 toohello 저장 된 데이터, 데이터를 저장할 경우의 hello 비용에 따라 다릅니다 hello 저장소 계층입니다. hello 1gb 당 비용이 hello 핫 저장소 계층에 대 한 보다 hello 쿨 저장소 계층에 대 한 더 합니다.

* **데이터 액세스 비용**: hello 쿨 저장소 계층에 있는 데이터에 대 한 읽기 및 쓰기 1gb 당 데이터 액세스 요금이 청구 됩니다.

* **트랜잭션 비용**: 두 계층에 모두 트랜잭션당 요금이 있습니다. 그러나 hello 쿨 저장소 계층에 대 한 hello 트랜잭션 별로 비용 hello 핫 저장소 계층의 경우 보다 더 높습니다.

* **지리적 복제 데이터 전송 비용**:만 tooaccounts 지역에서 복제 구성, GRS 및 RA-GRS를 포함 하 여 적용 됩니다. 지역 복제 데이터 전송에는 기가바이트당 요금이 발생합니다.

* **아웃바운드 데이터 전송 비용**: 아웃바운드 데이터 전송(Azure 지역 밖으로 전송된 데이터)에서는 기가바이트당 요금을 기준으로 대역폭 사용 요금이 발생하며 범용 저장소 계정과 같습니다.

* **변경 hello 저장소 계층**: 충전 같은 tooreading 각 전환에 대 한 hello 저장소 계정에 있는 모든 hello 데이터 발생 쿨 toohot에서 hello 저장소 계층을 변경 합니다. Hello 핫 toocool에서 hello 저장소 계층을 변경 합니다. 그러나 비용의 무료입니다.

> [!NOTE]
> Blob 저장소 계정에 대 한 가격 책정 hello 대 한 자세한 내용은 참조 하십시오. [Azure 저장소 가격](https://azure.microsoft.com/pricing/details/storage/) 페이지. Hello 아웃 바운드 데이터 전송 요금이 대 한 자세한 내용은 참조 하십시오. [데이터 전송 가격 정보](https://azure.microsoft.com/pricing/details/data-transfers/) 페이지.

## <a name="quickstart"></a>빠른 시작

이 섹션에서는 다음 시나리오 hello Azure 포털을 사용 하 여 hello 보여 줍니다.

* 어떻게 toocreate Blob 저장소 계정입니다.
* 어떻게 toomanage Blob 저장소 계정입니다.

이 설정은 적용 toohello 전체 저장소 계정 때문에 예제를 따르는 hello에 hello 액세스 계층 tooarchive를 설정할 수 없습니다. 보관은 특정 Blob에만 설정할 수 있습니다.

### <a name="create-a-blob-storage-account-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 Blob 저장소 계정 만들기

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.

2. Hello 허브 메뉴에서 선택 **새로** > **데이터 + 저장소** > **저장소 계정**합니다.

3. 저장소 계정의 이름을 입력합니다.
   
    이 이름은 전역적으로 고유 해야 합니다. hello URL의 일부 tooaccess hello 개체 hello 저장소 계정에서 사용 되는 사용 됩니다.  

4. 선택 **리소스 관리자** hello 배포 모델입니다.
   
    계층화 된 저장소만 사용 하 여 리소스 관리자 저장소 계정. 이 hello 새 리소스에 대 한 배포 모델을 권장 합니다. 자세한 내용은 체크 아웃 hello [Azure 리소스 관리자 개요](../../azure-resource-manager/resource-group-overview.md)합니다.  

5. Hello 계정 종류 드롭다운 목록에서 선택 **Blob 저장소**합니다.
   
    이 hello 유형의 저장소 계정 선택 하는 위치입니다. 계층화 된 저장소를 범용 저장소;에서 사용할 수 없습니다. hello Blob 저장소 유형 계정에서에서 제공 됩니다.     
   
    이 옵션을 선택 하는 경우 hello 성능 계층 설정 되어 있는지 tooStandard note 합니다. 계층화 된 저장소 hello 프리미엄 성능 계층으로 사용할 수 없는 경우

6. Hello 저장소 계정에 대 한 hello 복제 옵션을 선택: **LRS**, **GRS**, 또는 **RA-GRS**합니다. hello 기본값은 **RA-GRS**합니다.
   
    LRS; 로컬 중복 저장소 = GRS = 지역 중복 저장소 (2 지역); RA-GRS는 읽기 액세스 지리적 중복 저장소 (읽기 2 영역에 액세스 toohello 초)입니다.
   
    Azure 저장소 복제 옵션에 대한 자세한 내용은 아래의 [Azure 저장소 복제](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)를 확인하세요.

7. 필요에 따라 선택 hello 오른쪽 저장소 계층: 집합 hello **액세스 계층** tooeither **쿨** 또는 **핫**합니다. hello 기본값은 **핫**합니다. 

8. Hello 구독 하려는 toocreate hello 새 저장소 계정을 선택 합니다.

9. 새 리소스 그룹을 지정하거나 기존 리소스 그룹을 선택합니다. 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)를 참조하세요.

10. 저장소 계정에 대 한 hello 지역을 선택 합니다.

11. 클릭 **만들기** toocreate hello 저장소 계정입니다.

### <a name="change-hello-storage-tier-of-a-blob-storage-account-using-hello-azure-portal"></a>Hello 저장소 계층의 hello Azure 포털을 사용 하 여 Blob 저장소 계정 변경

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.

2. toonavigate tooyour 저장소 계정에 모든 리소스를 선택한 다음 저장소 계정을 선택 합니다.

3. Hello 설정 블레이드에서 클릭 **구성** hello 계정 구성을 tooview 및/또는 변경 합니다.

4. 필요에 따라 선택 hello 오른쪽 저장소 계층: 집합 hello **액세스 계층** tooeither **쿨** 또는 **핫**...

5. 저장 hello hello 블레이드 위쪽에 클릭 합니다.

> [!NOTE]
> 변경 hello 저장소 계층 추가 요금이 발생할 수 있습니다. Hello 참조 [가격 및 요금 청구](#pricing-and-billing) 자세한 내용은 섹션.


## <a name="evaluating-and-migrating-tooblob-storage-accounts"></a>평가 및 tooBlob 저장소 계정 마이그레이션
hello이 섹션의 목적은 toohelp 사용자 toomake 매끄러운 전환 toousing Blob 저장소 계정입니다. 두 가지 사용자 시나리오가 있습니다.

* 범용 저장소 계정이 기존와 때 tooevaluate 변경 tooa Blob 저장소 계정 hello 오른쪽 저장소 계층을 사용 합니다.
* Blob 저장소 계정 toouse 결정 또는 이미 하나 있고 tooevaluate hello 상시 또는 쿨 저장소 계층을 사용 해야 하는지를 합니다.

두 경우 모두 hello 우선입니다 tooestimate hello 비용을 저장 하 고 Blob 저장소 계정에 저장 된 데이터에 액세스 하는 고 현재 비용을 비교 하는 합니다.

## <a name="evaluating-blob-storage-account-tiers"></a>Blob 저장소 계정 계층 평가

Blob 저장소 계정에 저장 된 데이터 저장 및 액세스의 순서 tooestimate hello 비용, tooevaluate 기존 사용 패턴 또는 예상된 사용량 패턴을 계산 합니다. 일반적으로 tooknow를 보겠습니다.

* 저장소 사용량 – 데이터 저장 규모 및 월 기준 변화

* 저장소 액세스 패턴-읽기 가능 및 서 면된 toohello 계정 (새 데이터를 포함 하 여) 데이터의 양이 되 고 있습니까? 데이터 액세스에 사용되는 트랜잭션 양 및 트랜잭션 유형

## <a name="monitoring-existing-storage-accounts"></a>기존 저장소 계정 모니터링

기존 저장소 계정 및 이러한 데이터를 수집할 toomonitor, 로깅을 수행 하 고 저장소 계정에 대 한 메트릭 데이터를 제공 하는 Azure Storage Analytics의 사용을 만들 수 있습니다. Storage Analytics는 요청 toohello로 범용 저장소 계정은 Blob 저장소 계정에 대 한 Blob 저장소 서비스에 대 한 집계 된 트랜잭션 통계 및 용량 데이터가 포함 된 메트릭을 저장할 수 있습니다. 이 데이터는 hello에 잘 알려진 테이블에 저장 된 동일한 저장소 계정입니다.

자세한 내용은 [저장소 분석 메트릭 정보](https://msdn.microsoft.com/library/azure/hh343258.aspx) 및 [저장소 분석 메트릭 테이블 스키마](https://msdn.microsoft.com/library/azure/hh343264.aspx)를 참조하세요.

> [!NOTE]
> Blob 저장소 계정을 저장 하 고 해당 계정에 대 한 hello 메트릭 데이터 액세스에 대해서만 hello 테이블 서비스 끝점을 노출 합니다.

hello Blob 저장소 서비스에 대 한 hello 저장소 소비의 toomonitor tooenable hello 용량 메트릭에 필요합니다.
이 옵션을 사용 용량 데이터는 저장소 계정의 Blob 서비스에 대해 매일 기록 되며이 고 toohello 작성 된 테이블 항목으로 기록 *$MetricsCapacityBlob* hello 내에서 동일한 테이블 저장소 계정입니다.

toomonitor hello 데이터 액세스 패턴에 대 한 hello Blob 저장소 서비스 API 수준에서 tooenable hello 시간 트랜잭션 메트릭 사용 해야 합니다. 이 옵션을 사용으로 API 당 트랜잭션은 매시간 집계 이며 toohello 작성 된 테이블 항목으로 기록 *$MetricsHourPrimaryTransactionsBlob* hello 내에서 동일한 테이블 저장소 계정입니다. hello *$MetricsHourSecondaryTransactionsBlob* RA-GRS 저장소 계정을 사용 하는 경우 테이블 레코드 hello 트랜잭션을 toohello 보조 끝점입니다.

> [!NOTE]
> 페이지 Blob과 블록 및 추가 Blob 데이터와 함께 가상 컴퓨터 디스크를 저장한 범용 저장소 계정이 있는 경우 이 예측 프로세스는 적용되지 않습니다. 용량을 구분할 수 있는 방법이 있고 트랜잭션 메트릭 형식을 기반으로 hello에 대 한 blob만 차단 하 고 추가 될 수 있는 blob 마이그레이션할 tooa Blob 저장소 계정 때문입니다.

데이터 소비 액세스 패턴에 대해 적절 한 근사치 tooget 일반 사용을 대표 하는 hello 메트릭에 대 한 보존 기간을 선택 하 고 추정 좋습니다. 한 가지 방법은 tooretain hello 메트릭 데이터 7 일 및 수집 hello 데이터에 대 한 hello 달의 마지막 hello에 대 한 분석을 위해 매주입니다. 또 다른 옵션 tooretain hello 메트릭 데이터 hello에 대 한 지난 30 일의 수집 및 hello hello 30 일의 기간이 끝나기 전에 hello 데이터를 분석 합니다.

메트릭 데이터 사용, 수집 및 보기는 [Azure Storage 메트릭 사용 및 메트릭 데이터 보기](../common/storage-enable-and-view-metrics.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)를 참조하세요.

> [!NOTE]
> 분석 데이터 저장, 액세스 및 다운로드는 일반 사용자 데이터와 마찬가지로 청구됩니다.

### <a name="utilizing-usage-metrics-tooestimate-costs"></a>사용 메트릭 tooestimate 비용을 사용 하 여

### <a name="storage-costs"></a>저장소 비용

hello 용량 메트릭 테이블의 최신 항목 hello *$MetricsCapacityBlob* hello 행 키를 가진 *'데이터'* 표시 hello 사용자 데이터에 사용 된 저장소 용량입니다. hello 용량 메트릭 테이블의 최신 항목 hello *$MetricsCapacityBlob* hello 행 키를 가진 *'분석'* 표시 hello hello 분석 로그에서 사용 하는 저장소 용량입니다.

이 총 용량 (사용) 하는 경우 두 사용자 데이터 및 분석 로그에서 사용 될 수 있습니다 사용할 tooestimate hello 비용 hello 저장소 계정에서 데이터를 저장 합니다. hello 동일한 메서드 블록에 대 한 저장소 비용을 예상 하는 데 사용할 수도 있습니다 및 범용 저장소 계정에서 blob을 추가 합니다.

### <a name="transaction-costs"></a>트랜잭션 비용

hello 총 *'TotalBillableRequests'*, 메트릭 테이블 hello 트랜잭션에서 API에 대 한 모든 항목에 걸쳐 hello 해당 특정 API에 대 한 트랜잭션 총 수를 나타냅니다. *예를 들어*의 총 hello *'GetBlob'* 트랜잭션을 지정 된 기간 동안에서 hello 행 키를 가진 모든 항목에 대 한 총 청구 가능 요청의 hello 총합으로 계산할 수 *' 사용자; GetBlob'*합니다.

Blob 저장소 계정에 대 한 순서 tooestimate 트랜잭션 비용을 다르게 가격이 책정 됩니다 이후 toobreak 3 개의 그룹으로 hello 트랜잭션 아래로 필요 합니다.

* *'PutBlob'*, *'PutBlock'*, *'PutBlockList'*, *'AppendBlock'*, *'ListBlobs'*, *'ListContainers'*, *'CreateContainer'*, *'SnapshotBlob'* 및 *'CopyBlob'*과 같은 쓰기 트랜잭션
* *'DeleteBlob'* 및 *'DeleteContainer'*와 같은 삭제 트랜잭션
* 모든 다른 트랜잭션.

범용 저장소 계정에 대 한 순서 tooestimate 트랜잭션 비용을 tooaggregate hello 작업/API에 관계 없이 모든 트랜잭션을 필요 합니다.

### <a name="data-access-and-geo-replication-data-transfer-costs"></a>데이터 액세스 및 지역에서 복제 데이터 전송 비용

저장소 분석을 제공 하지 않는 hello 양의 데이터를 읽고 tooa 저장소 계정 작성, 그 수 대략적으로 계산할 수 hello 트랜잭션 메트릭 테이블을 살펴보면 합니다. hello 총 *'TotalIngress'* hello 트랜잭션 메트릭에서 API에 대 한 모든 항목에 걸쳐 테이블 해당 특정 API에 대 한 hello 바이트에서 수신 데이터의 총 크기를 나타냅니다. 마찬가지로 hello 총 *'TotalEgress'* hello 총 양을 바이트 단위로 송신 데이터를 나타냅니다.

순서 tooestimate hello 데이터 액세스 비용에 Blob 저장소 계정에 대 한 두 그룹으로 hello 트랜잭션 아래로 toobreak을 해야합니다. 

* hello 총 확인 하 여 hello hello 저장소 계정에서 검색 된 데이터 양을 예상할 수 있는 *'TotalEgress'* 주로 hello에 대 한 *'GetBlob'* 및 *'CopyBlob'* 작업입니다.

* hello 총 확인 하 여 hello toohello 저장소 계정 작성 된 데이터 양을 예상할 수 있는 *'TotalIngress'* 주로 hello에 대 한 *'PutBlob'*, *'PutBlock'*, *'CopyBlob'* 및 *'AppendBlock'* 작업 합니다.

Blob 저장소 계정은 GRS 또는 RA-GRS 저장소 계정을 사용 하는 경우 기록 된 데이터 양을 hello에 대 한 hello 예상 값을 사용 하 여 계산에 대 한 지리적 복제 데이터 전송의 hello 비용입니다.

> [!NOTE]
> Hello 상시 또는 쿨 저장소 계층을 사용 하기 위한 hello 비용을 계산 하는 방법에 대 한 더 자세한 예제를 살펴보세요 hello 제목의 FAQ *'핫 및 쿨 액세스 계층은 무엇 이며 어느 한 toouse를 어떻게 확인 해야?'* hello에 [Azure 저장소 가격 페이지](https://azure.microsoft.com/pricing/details/storage/)합니다.
 
## <a name="migrating-existing-data"></a>기존 데이터 마이그레이션

Blob 저장소 계정은 저장 전용 블록 및 추가 Blob에 맞게 특별히 설정됩니다. Blob와 함께 toostore 테이블, 큐, 파일, 디스크를 사용 하면, 기존의 일반적인 용도의 스토리지 계정에는 변환 된 tooBlob 저장소 계정 수 없습니다. toouse hello 저장소 계층, toocreate 새 Blob 저장소 계정이 필요 하 고 hello 새로 만든 계정으로 기존 데이터를 마이그레이션합니다.

온-프레미스 저장 장치, 타사 클라우드 저장소 공급자 또는 Azure에서 기존 범용 저장소 계정에서 Blob 저장소 계정에 같은 메서드 toomigrate 기존 데이터가 hello를 사용할 수 있습니다.

### <a name="azcopy"></a>AzCopy

AzCopy는 고성능 데이터 tooand의 Azure 저장소에서 복사를 위해 설계 된 Windows 명령줄 유틸리티입니다. Blob 저장소 계정에 온-프레미스 저장소 장치의 기존 범용 저장소 계정에서 Blob 저장소 계정에 AzCopy toocopy 데이터 또는 tooupload 데이터를 사용할 수 있습니다.

자세한 내용은 참조 하십시오. [hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)합니다.

### <a name="data-movement-library"></a>데이터 이동 라이브러리

.NET 용 azure 저장소 데이터 이동을 라이브러리 hello 핵심 데이터 이동 프레임 워크 AzCopy를 구동 하는 기반으로 합니다. hello 라이브러리 높은 성능, 신뢰할 수 있는, 용인지 하 고 데이터를 손쉽게 작업 비슷한 tooAzCopy를 전송 합니다. 이렇게 하면 제공한 AzCopy 응용 프로그램에서 고유 하 게 실행 및 외부 인스턴스의 AzCopy 모니터링 toodeal 필요 없이 hello 기능 제품의 모든 혜택 tootake 있습니다.

자세한 내용은 [.NET용 Azure 저장소 데이터 이동 라이브러리](https://github.com/Azure/azure-storage-net-data-movement)

### <a name="rest-api-or-client-library"></a>REST API 또는 클라이언트 라이브러리

Hello Azure 저장소 서비스 REST API 또는 hello Azure 클라이언트 라이브러리 중 하나를 사용 하 여 Blob 저장소 계정에 사용자 지정 응용 프로그램 toomigrate 데이터를 만들 수 있습니다. Azure 저장소는 NET, Java, C++, Node.JS, PHP, Ruby, Python 등, 여러 언어와 플랫폼을 위한 다양한 클라이언트 라이브러리를 제공합니다. hello 클라이언트 라이브러리에 다시 시도 논리, 로깅 및 병렬 업로드 같은 고급 기능을 제공합니다. Hello HTTP/HTTPS 요청 하는 모든 언어에서 호출 될 수 있는 REST API에 대해 직접 개발할 수 있습니다.

자세한 내용은 [Azure Blob 저장소 시작](storage-dotnet-how-to-use-blobs.md)을 참조하세요.

> [!NOTE]
> 클라이언트 쪽 암호화를 사용 하 여 암호화 하는 blob hello blob과 함께 저장 된 암호화 관련 메타 데이터를 저장 합니다. 것이 매우 중요 하는 hello blob 메타 데이터 및 특히 hello 암호화 관련 메타 데이터, 유지 되는 복사 메커니즘 확인 해야 합니다. 이 메타 데이터 없이 hello blob를 복사 하는 경우 hello blob 콘텐츠를 검색할 수 없습니다 다시 합니다. 암호화 관련 메타데이터에 대한 자세한 내용은 [Azure Storage 클라이언트 쪽 암호화](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)를 참조하세요.
 
## <a name="faq"></a>FAQ

1. **기존 저장소 계정을 계속 사용할 수 있나요?**
   
    예, 기존 저장소 계정은 계속 사용할 수 있으며 가격 책정이나 기능은 바뀌지 않습니다.  hello 기능 toochoose 저장소 계층 없고 hello 나중에 계층화 기능이 제공 되지 않습니다.

2. **Blob 저장소 계정을 왜 사용해야 하며 언제 사용을 시작해야 하나요?**
   
    Blob 저장소 계정은 blob 저장용으로 특별히 고 toointroduce 새로운 blob 중심 기능이 수입니다. 를 기대 하 고 있는 Blob 저장소 계정이 hello 계층적 저장소 같은 향후 기능으로 blob을 저장 하 고 계층으로 구성 하는 방법을 권장 합니다.이 계정 유형 기반의 도입 될 것입니다. 그러나 중인지 tooyou toomigrate 비즈니스 요구 사항에 따라 선택 하는 경우.

3. **기존 저장소 계정 tooa Blob 저장소 계정 내 변환할 수 있습니까?**
   
    아니요. Blob Storage 계정은 다른 종류의 저장소 계정이며, 새로 계정을 만들고 이전에 설명한 대로 데이터를 마이그레이션해야 합니다.

4. **Hello에 두 저장소 계층에서 개체를 저장할 수 동일한 계정?**
   
    hello *' 액세스 계층 '* 특성 계정 수준에서 설정 하는 hello 저장소 계층의 hello 값을 표시 하 고 tooall 개체 해당 계정에 적용 됩니다. 그러나 hello blob 수준 계층화 (미리 보기) 기능을 사용 하면 있습니다 tooset hello 액세스 계층 특정 blob에 대 한 고 hello hello 계정의 액세스 계층 설정을 덮어씁니다. 

5. **Blob 저장소 계정 내의 hello 저장소 계층을 변경할 수 있나요?**
   
    예. Hello 설정 하 여 hello 저장소 계층을 변경할 수 있습니다 *' 액세스 계층 '* hello 저장소 계정에는 특성입니다. 변경 hello 저장소 계층은 hello 계정에 저장 된 tooall 개체에 적용 됩니다. 핫 toocool에서 hello 저장소 계층을 변경 발생 시 키 지 않는 쿨 toohot에서 변경 하는 동안 모든 요금을 유발 하지 않으므로 hello 계정에서 모든 hello 데이터를 읽기 위한 비용 GB 당 합니다.

6. **Blob 저장소 계정 내의 hello 저장소 계층을 변경할 수는 얼마나 자주**
   
    얼마나 자주 hello 저장소 계층을 변경할 수 있습니다에 대 한 제한이 적용 안 함, 하는 동안 주의 쿨 toohot에서 hello 저장소 계층을 변경 상당한 비용이 초래할 수 있습니다. 자주 hello 저장소 계층을 변경 하는 것은 좋지 않습니다.

7. **Hello hello 핫 저장소 계층에서 보다 hello 쿨 저장소 계층의 hello blob 다르게 동작 할까요?**
   
    Hello 핫 저장소 계층에는 blob은 hello 범용 저장소 계정에 blob으로 동일한 대기 시간입니다. Hello 쿨 저장소 계층에는 blob 범용 저장소 계정에서 blob으로 유사한 대기 시간 (밀리초)을 은합니다.
   
    Hello 쿨 저장소 계층의 blob 약간 낮아집니다 가용성 서비스 (SLA) 비해 수준이 hello 핫 저장소 계층에 저장 된 hello blob입니다. 자세한 내용은 [저장소용 SLA](https://azure.microsoft.com/support/legal/sla/storage)를 참조하세요.

8. **페이지 Blob과 가상 컴퓨터 디스크를 Blob 저장소 계정에 저장할 수 있나요?**
   
    Blob 저장소 계정은 블록 및 추가 Blob만 지원하고 페이지 Blob은 지원하지 않습니다. Azure 가상 컴퓨터 디스크 페이지 blob에서 지원 됩니다 하 및 결과적으로 Blob 저장소 계정이 가상 컴퓨터 디스크를 사용 하는 toostore 커야 합니다. 그러나 Blob 저장소 계정에 블록 blob으로 hello 가상 컴퓨터 디스크의 가능한 toostore 백업 됩니다.

9. **해야 toochange 내 기존 응용 프로그램 toouse Blob 저장소 계정은?**
   
    Blob 저장소 계정은 블록 및 추가 Blob에 대한 범용 저장소 계정과 API가 100% 동일합니다. Hello 2014-02-14 버전의 hello 사용 하는 응용 프로그램은 블록 blob을 통해 또는 추가 blob 있고 [저장소 서비스 REST API](https://msdn.microsoft.com/library/azure/dd894041.aspx) 큰 응용 프로그램이 작동 해야 합니다. 이전 버전의 hello 프로토콜을 사용 하는 경우 업데이트 해야 합니다 응용 프로그램 toouse hello 새 버전 따라서 toowork로 원활 하 게 두 가지 유형의 저장소 계정을 합니다. 일반적으로 항상 권장 사용 하면 저장소 계정 유형에 관계 없이 hello 최신 버전을 사용 합니다.

10. **사용자 환경이 변경되나요?**
    
    Blob 저장소 계정이 블록을 저장 하기 위한 매우 유사한 tooa 범용 저장소 계정 추가 blob 및 모든 hello 내구성이 및 가용성, 확장성, 성능 및 보안을 포함 하 여 Azure 저장소의 주요 기능을 지원 합니다. Hello 기능 및 제한 사항 특정 tooBlob 저장소 계정 및 모든 항목 위에 명시 된 해당 저장소 계층 이외의 다른 남아 hello 동일 합니다.

## <a name="next-steps"></a>다음 단계

### <a name="evaluate-blob-storage-accounts"></a>Blob 저장소 계정 평가

[지역별 Blob 저장소 계정의 가용성 확인](https://azure.microsoft.com/regions/#services)

[Azure 저장소 메트릭을 활성화하여 현재 저장소 계정의 사용 현황 평가](../common/storage-enable-and-view-metrics.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[지역별 Blob 저장소 가격 확인](https://azure.microsoft.com/pricing/details/storage/)

[데이터 전송 가격 확인](https://azure.microsoft.com/pricing/details/data-transfers/)

### <a name="start-using-blob-storage-accounts"></a>Blob 저장소 계정 사용 시작

[Azure Blob 저장소 시작](storage-dotnet-how-to-use-blobs.md)

[Azure 저장소에서 데이터 tooand 이동](../common/storage-moving-data.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송 합니다.](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[저장소 계정 찾아보기 및 탐색](http://storageexplorer.com/)