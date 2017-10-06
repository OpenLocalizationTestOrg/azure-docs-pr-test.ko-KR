---
title: "Azure 저장소에 복제 aaaData | Microsoft Docs"
description: "Microsoft Azure Storage 계정의 데이터는 내구성 및 고가용성을 위해 복제됩니다. 복제 옵션은 (LRS) 로컬 중복 저장소(LRS), 영역 중복 저장소 (ZRS), 지역 중복 저장소 (GRS) 및 읽기 액세스 지역 중복 저장소 (RA-GRS)에 포함 됩니다."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 86bdb6d4-da59-4337-8375-2527b6bdf73f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: ce48d1992fec7bd5ed32feb96b86bef88ca759df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-replication"></a>Azure 저장소 복제

저장소 계정은 항상 Microsoft Azure의 hello 데이터 tooensure 내 구성과 고가용성을 복제 합니다. 내 데이터를 동일한 데이터 센터 또는 tooa 보조 데이터 센터를 선택 하면 복제 옵션에 따라 hello 복제 복사 합니다. 복제는에서는 데이터를 보호 하 고 일시적인 하드웨어 오류의 hello 이벤트에서 응용 프로그램 실행 시간 프로그램을 유지 합니다. 데이터가 복제 된 tooa 보조 데이터 센터 경우 hello 기본 위치에서 치명적인 오류 로부터 보호 됩니다.

복제를 사용 하면 저장소 계정의 hello 맞는지 [서비스 수준 계약 (SLA) 저장소에 대 한](https://azure.microsoft.com/support/legal/sla/storage/) hello 얼굴 오류의 경우에 합니다. 지 속성 및 가용성에 대 한 Azure 저장소에 대 한 정보에 대 한 hello SLA 보장을 참조 하십시오.

저장소 계정을 만들 때 hello 다음 복제 옵션 중 하나를 선택할 수 있습니다.

* [LRS(로컬 중복 저장소)](#locally-redundant-storage)
* [ZRS(영역 중복 저장소)](#zone-redundant-storage)
* [GRS(지역 중복 저장소)](#geo-redundant-storage)
* [RA-GRS(읽기 액세스 지역 중복 저장소)](#read-access-geo-redundant-storage)

읽기 액세스 지역 중복 저장소 (RA-GRS)는 저장소 계정을 만들 때 hello 기본 옵션을입니다.

다음 표에서 hello 후속 섹션에서는 각 유형의 복제에서 자세히 다루고 LRS, ZRS, GRS 및 RA-GRS 간의 hello 차이점의 간략 한 개요를 제공 합니다.

| 복제 전략 | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| 데이터가 여러 데이터 센터에 걸쳐 복제됩니다. |아니요 |예 |예 |예 |
| 데이터는 보조 위치는 물론 hello 기본 위치에서 읽을 수 있습니다. |아니요 |아니요 |아니요 |예 |
| 별도 노드에서 유지 관리되는 데이터 복사본 수입니다. |3 |3 |6 |6 |

참조 [Azure 저장소 가격](https://azure.microsoft.com/pricing/details/storage/) 가격 hello 다른 중복 옵션에 대 한 정보입니다.

> [!NOTE]
> 프리미엄 저장소는 LRS(로컬 중복 저장소)만 지원합니다. 프리미엄 저장소에 대한 자세한 내용은 [프리미엄 저장소: Azure 가상 컴퓨터에 대한 고성능 저장소](../storage-premium-storage.md)를 참조하세요.
>

## <a name="locally-redundant-storage"></a>로컬 중복 저장소
로컬 중복 저장소 (LRS) 세 번 hello 지역의 저장소 계정을 만든 데이터 센터에 호스트 된 저장소 배율 단위 내에서 데이터를 복제 합니다. 경과 했는데도 문제가 있다면 서 면된 tooall 세 개의 복제본에 한 번만 쓰기 요청을 성공적으로 반환 합니다. 이러한 3개의 복제본은 하나의 저장소 배율 단위 내에서 각기 별도 오류 도메인 및 업그레이드 도메인에 상주합니다.

저장소 배율 단위는 저장소 노드의 랙 컬렉션입니다. 오류 도메인 (FD)은 물리적 장애 단위를 나타내고 toohello 속하는 노드로 간주 될 수 있는 노드 그룹 동일한 물리적 랙에 합니다. 업그레이드 도메인 (UD)은 서비스 업그레이드 (롤아웃)를 사용 하는 hello 프로세스 중에 함께 업그레이드 된 노드 그룹입니다. 세 개의 복제본 hello 분산 되어 Ud와 Fd에 하나의 저장소 배율 단위 tooensure 롤아웃 중 노드를 업그레이드 하는 경우 또는 하드웨어 오류가 단일 랙에 영향 하는 경우에 데이터를 사용할 수 있습니다.

LRS는 hello 저렴 한 비용 옵션은 있으며 최소 내구성 비교 tooother 옵션이 있습니다. 데이터 센터 수준의 재해 (화재, 폭주 등)의 hello 이벤트에서 모두 세 개의 복제본 손실 되거나 복구 불능 상태일 수 있습니다. 이 위험 toomitigate, 지역 중복 저장소 (GRS) 대부분의 응용 프로그램에 권장 됩니다.

로컬 중복 저장소는 특정 시나리오에서 적합할 수 있습니다.

* Azure Storage 복제 옵션 중 가장 높은 최대 대역폭을 제공합니다.
* 응용 프로그램이 쉽게 재구성될 수 있는 데이터를 저장하는 경우 LRS를 선택할 수 있습니다.
* 일부 응용 프로그램은 toodata 거 버 넌 스 요구 사항 인해 국가 내 에서만 제한 tooreplicating 데이터입니다. 쌍을 이루는 지역은 다른 국가일 수 있습니다. 쌍을 이루는 지역에 대한 자세한 내용은 [Azure 지역](https://azure.microsoft.com/regions/)을 참조하세요.

## <a name="zone-redundant-storage"></a>영역 중복 저장소
영역 중복 저장소 (ZRS)에 더하기 toostoring 세 복제본 비슷한 tooLRS, 따라서 LRS 보다 높은 지 속성 제공 하는 하나 또는 두 개의 영역 내에서 데이터 센터 간에 데이터를 비동기적으로 복제 합니다. ZRS에 저장 된 데이터 hello 기본 데이터 센터를 사용할 수 없거나 복구할 수 없는 경우에 지속 됩니다.
고객에 게 toouse ZRS 계획을 알고 있어야 하는:

* ZRS는 범용 저장소 계정의 블록 Blob에 대해서만 사용할 수 있으며, 저장소 서비스 버전 2014-02-14 이상에서만 지원됩니다.
* 비동기 복제는 로컬 재해의 hello 이벤트에서 지연을 포함 하므로 가능한 아직 되지 않은 변경 내용이 복제 toohello 보조가 기본 hello에서 hello 데이터를 복구할 수 없는 경우 손실 됩니다.
* Microsoft 장애 조치 toohello 보조를 시작할 때까지 hello 복제본을 사용할 수 없습니다.
* ZRS 계정 나중 tooLRS 또는 GRS 변환할 수 없습니다. 마찬가지로, 기존 LRS 또는 GRS 계정 수 없습니다 tooa ZRS 계정 변환 합니다.
* ZRS 계정에는 메트릭 또는 로깅 기능이 없습니다.

## <a name="geo-redundant-storage"></a>지역 중복 저장소
지역 중복 저장소 (GRS) 수백 마일 떨어진 hello 기본 지역 데이터 tooa 보조 지역에 복제 합니다. GRS를 활성화 한 저장소 계정의 데이터가 전체 지역 가동 중단 또는 재해는 hello에 기본 지역을 복구할 수의 hello 경우에도 지속 됩니다.

GRS 활성화 한 저장소 계정의 대 한 업데이트가 처음 커밋된 toohello 기본 지역에 3 번 복제입니다. Hello 업데이트가 비동기적으로 복제 한 다음 toohello 보조 지역, 여기서 것도 3 번 복제 됩니다.

Grs를 사용할 경우 두 hello 기본 및 보조 영역 별도 오류 도메인에 걸쳐 복제본을 관리 하 고 업그레이드 도메인 LRS를 사용 하 여 설명 저장소 배율 단위 내에서.

고려 사항:

* 비동기 복제에는 아직 복제 되지 않은 변경 하는 수는 지역적 재해의 hello 이벤트에서의 지연이 수반 되므로 이후 보조 지역의 toohello가 hello 기본 지역에서 hello 데이터를 복구할 수 없는 경우 손실 됩니다.
* Microsoft 장애 조치 toohello 보조 영역을 시작 하지 않는 한 hello 복제본을 사용할 수 없습니다. Microsoft에서는 장애 조치 toohello 보조 지역을 시작 하는 경우 hello 장애 조치 완료 된 후 toothat 데이터 읽기 및 쓰기 권한을 갖습니다. 자세한 내용은 [재해 복구 지침](../storage-disaster-recovery-guidance.md)을 참조하세요. 
* 응용 프로그램 tooread hello 보조 지역에서 원하는 hello 사용자 RA-GRS를 사용 해야 합니다.

저장소 계정을 만들 때 hello hello 계정에 대 한 기본 지역을 선택 합니다. hello 보조 지역 hello 기본 지역에 따라 확인 하 고 변경할 수 없습니다. 다음 표에서 hello hello 기본 및 보조 지역 쌍을 보여 줍니다.

| 보조 | 주 |
| --- | --- |
| 미국 중북부 |미국 중남부 |
| 미국 중남부 |미국 중북부 |
| 미국 동부 |미국 서부 |
| 미국 서부 |미국 동부 |
| 미국 동부 2 |미국 중부 |
| 미국 중부 |미국 동부 2 |
| 북유럽 |서유럽 |
| 서유럽 |북유럽 |
| 동남아시아 |동아시아 |
| 동아시아 |동남아시아 |
| 중국 동부 |중국 북부 |
| 중국 북부 |중국 동부 |
| 일본 동부 |일본 서부 |
| 일본 서부 |일본 동부 |
| 브라질 남부 |미국 중남부 |
| 오스트레일리아 동부 |오스트레일리아 남동부 |
| 오스트레일리아 남동부 |오스트레일리아 동부 |
| 인도 남부 |인도 중부 |
| 인도 중부 |인도 남부 |
| 인도 서부 |인도 남부 |
| 미국 정부 아이오와 |미국 정부 버지니아 |
| 미국 정부 버지니아 |미국 정부 텍사스 |
| 미국 정부 텍사스 |미국 정부 애리조나 |
| 미국 정부 애리조나 |미국 정부 텍사스 |
| 캐나다 중부 |캐나다 동부 |
| 캐나다 동부 |캐나다 중부 |
| 영국 서부 |영국 남부 |
| 영국 남부 |영국 서부 |
| 독일 중부 |독일 북동부 |
| 독일 북동부 |독일 중부 |
| 미국 서부 2 |미국 중서부 |
| 미국 중서부 |미국 서부 2 |

Azure에서 지원되는 지역에 대한 최신 정보는 [Azure 지역](https://azure.microsoft.com/regions/)을 참조하세요.

>[!NOTE]  
> 미국 버지니아 주 정부 보조 지역은 미국 텍사스 주 정부입니다. 이전에는 미국 버지니아 주 정부가 보조 지역으로 미국 아이오와 주 정부를 활용했습니다. 보조 지역 되는 미국 정부 기관용 이유로 사용 하는 저장소 계정에 연결한 경우 영역 tooUS 정부 기관용 텍사스 마이그레이션. 
> 
> 

## <a name="read-access-geo-redundant-storage"></a>읽기 액세스 지역 중복 저장소
읽기 액세스 지역 중복 저장소 (RA-GRS)는 두 영역 간 toohello 복제 GRS에서 제공 하는 또한 toohello 데이터 hello 보조 위치에 읽기 전용 액세스를 제공 하 여 저장소 계정의 가용성을 최대화 합니다.

Tooyour 데이터 hello 보조 지역에 읽기 전용 액세스를 사용 하도록 설정 하면 데이터가 저장소 계정에 대 한 추가 toohello 기본 끝점에서 보조 끝점에서 사용할 수 있는 됩니다. hello 보조 끝점은 유사한 toohello 기본 끝점 하지만 hello 접미사 추가 `–secondary` toohello 계정 이름입니다. 예를 들어 기본 끝점에 대 한 hello Blob 서비스는 `myaccount.blob.core.windows.net`, 보조 끝점은 `myaccount-secondary.blob.core.windows.net`합니다. 기본 및 보조 끝점 hello 둘 다에 대 한 저장소 계정에 대 한 선택 키 hello 동일한 hello 됩니다.

고려 사항:

* 응용 프로그램 toomanage RA-GRS를 사용 하는 경우 상호 작용 하는 끝점을에 있습니다.
* 비동기 복제에는 아직 복제 되지 않은 변경 하는 수는 지역적 재해의 hello 이벤트에서의 지연이 수반 되므로 이후 보조 지역의 toohello가 hello 기본 지역에서 hello 데이터를 복구할 수 없는 경우 손실 됩니다.
* Microsoft 장애 조치 toohello 보조 영역을 시작 하는 경우 hello 장애 조치 완료 된 후 toothat 데이터 읽기 및 쓰기 권한을 갖습니다. 자세한 내용은 [재해 복구 지침](../storage-disaster-recovery-guidance.md)을 참조하세요. 
* RA-GRS는 높은 가용성을 위해 제공됩니다. 확장성 지침 hello를 검토 하십시오 [성능 검사 목록](../storage-performance-checklist.md)합니다.

## <a name="frequently-asked-questions"></a>질문과 대답

<a id="howtochange"></a>
#### <a name="1-how-can-i-change-hello-geo-replication-type-of-my-storage-account"></a>1. 내 저장소 계정의 hello 지리적 복제 유형을 변경 하려면 어떻게 해야 합니까?

   LRS, GRS, 간의 저장소 계정의 hello 지리적 복제 유형을 변경할 수 있습니다 및 RA-GRS를 사용 하 여 hello [Azure 포털](https://portal.azure.com/), [Azure Powershell](storage-powershell-guide-full.md) 또는 프로그래밍 방식으로 여러 저장소 클라이언트인 중 하나를 사용 하 여 라이브러리입니다. ZRS 계정은 LRS 또는 GRS로 변환할 수 없습니다. 마찬가지로, 기존 LRS 또는 GRS 계정 수 없습니다 tooa ZRS 계정 변환 합니다.

<a id="changedowntime"></a>
#### <a name="2-will-there-be-any-down-time-if-i-change-hello-replication-type-of-my-storage-account"></a>2. 모든 중단 시간 경우 있을 내 저장소 계정의 hello 복제 유형을 변경 하려면?

   아니요, 중단 시간이 발생하지 않습니다.

<a id="changecost"></a>
#### <a name="3-will-there-be-any-additional-cost-if-i-change-hello-replication-type-of-my-storage-account"></a>3. 저장소 계정 내의 hello 복제 유형을 변경 하는 경우 추가 비용이 있이 됩니다?

   예. LRS tooGRS (RA-GRS)에서 저장소 계정에 대 한 변경 하면 기본 위치 toohello 보조 위치에서 기존 데이터를 복사 하는 관련 된 수신에 대 한 추가 요금이 발생 시 키 지 것입니다. Hello 초기 데이터가 복사 되 면 더 이상 추가 송신 비용이 부과가 않습니다 지역 hello 기본 toosecondary 위치에서 hello 데이터를 복제 합니다. hello에서 대역폭 요금에 대 한 hello 세부 정보를 확인할 수 있습니다 [Azure 저장소 가격 페이지](https://azure.microsoft.com/pricing/details/storage/blobs/)합니다. GRS tooLRS에서 변경 하는 경우 추가 비용 없이 없지만 데이터 hello 보조 위치에서 삭제 됩니다.

<a id="ragrsbenefits"></a>
#### <a name="4-how-can-ra-grs-help-me"></a>4. RA-GRS가 어떻게 도움이 되나요?
   
   GRS 저장소 기본 tooa 보조 지역에 수백 마일 떨어진 hello 기본 지역에서 데이터의 복제를 제공 합니다. 이러한 경우에는 데이터가 전체 지역 가동 중단 또는 재해는 hello에 기본 지역을 복구할 수의 hello 경우에도 지속 됩니다. RA-GRS 저장소가 함께 hello 보조 위치에서 hello 기능 tooread hello 데이터를 추가 합니다. 방법에 대 한 몇 가지 아이디어에 대 한 tooleverage 하는이 기능은 너무를 참조 하십시오[항상 사용 가능한 응용 프로그램 설계 RA-GRS 저장소를 사용 하 여](../storage-designing-ha-apps-with-ragrs.md)합니다. 

<a id="lastsynctime"></a>
#### <a name="5-is-there-a-way-for-me-toofigure-out-how-long-it-takes-tooreplicate-my-data-from-hello-primary-toohello-secondary-region"></a>5. 방법이 있습니까 위해 걸리는 시간 tooreplicate 내 데이터 hello 기본 toohello 보조 지역에서 아웃 toofigure?
   
   RA-GRS 저장소를 사용 하는 경우에 hello 저장소 계정의 마지막 동기화 시간을 확인할 수 있습니다. 마지막 동기화 시간은 GMT 날짜/시간 값입니다. 모든 주 쓰기 hello 마지막 동기화 시간 전에 기록 되었습니다 toohello 보조 위치는 사용할 수 있는 toobe hello 보조 위치에서 읽을 것을 의미 있는 합니다. 마지막 동기화 시간 수 또는 사용 하지 못할 읽기에 아직 hello 후 기본이 씁니다. Hello를 사용 하 여이 값을 쿼리할 수 [Azure 포털](https://portal.azure.com/), [Azure PowerShell](storage-powershell-guide-full.md), 또는 REST API 또는 hello 저장소 클라이언트 라이브러리 중 하나를 환영 프로그래밍 방식으로 사용 합니다. 

<a id="outage"></a>
#### <a name="6-how-can-i-switch-toohello-secondary-region-if-there-is-an-outage-in-hello-primary-region"></a>6. Hello 기본 지역에서 중단 될 경우 toohello 보조 지역을 전환 하려면 어떻게 합니까?
   
   Toohello 문서를 참조 하십시오 [Azure 저장소 중단이 발생할 경우 어떤 toodo](../storage-disaster-recovery-guidance.md) 내용을 확인 합니다.

<a id="rpo-rto"></a>
#### <a name="7-what-is-hello-rpo-and-rto-with-grs"></a>7. RPO 및 RTO grs hello는 무엇입니까?
   
   복구 지점 목표 (RPO): GRS 및 RA-GRS hello 저장소 서비스 비동기적으로 hello 기본 toohello 보조 위치에서 지리적 복제 hello 데이터입니다. 주요 지역적 재해가 장애 조치에 toobe 수행 하는 경우 지리적으로 복제 되지 않은 최근 델타 변경 내용을 손실 될 수 있습니다. 잠재적 데이터 손실을 분 hello 수는 참조 된 tooas hello RPO (즉, hello 지점 toowhich 데이터의 복구할 수)입니다. 현재 지역에서 복제를 수행하는 데 소요되는 시간에 대한 SLA는 없지만 일반적으로 RPO는 15분 미만입니다.

   복구 시간 목표 (RTO): toodo hello 장애 조치는 및 돌아갈 hello 저장소 계정이 온라인 toodo 장애 조치가 있는 경우 시간을 측정 한 것입니다. hello 시간 toodo hello 장애 조치 hello 다음이 포함 됩니다.
    * hello 시간이 tooinvestigate는 hello 기본 위치의 hello 데이터를 복구할 수 있습니다 toodo 장애 조치 해야 하는 경우 또는 결정 합니다.
    * Hello 주 DNS 항목 toopoint toohello 보조 위치를 변경 하 여 장애 조치 hello 계정입니다.

   म 하므로 잠시만 기다려 hello 장애 조치를 수행 하 고 hello 기본 위치에서 hello 데이터 복구에 집중 합니다 hello 데이터 복구 기회가 이면 데이터를 매우 심각 하 게 유지 hello 책임을 져야 합니다. Hello 이후, tooprovide API tooallow 계획 계정 수준에서 장애 조치 tootrigger 하는 다음 사용 하면 toocontrol hello RTO를 직접 있지만 아직 사용할 수 없으면입니다.
   
## <a name="next-steps"></a>다음 단계
* [RA-GRS 저장소를 사용하여 항상 사용 가능한 응용 프로그램 설계](../storage-designing-ha-apps-with-ragrs.md)
* [Azure Storage 가격 책정](https://azure.microsoft.com/pricing/details/storage/)
* [Azure 저장소 계정 정보](../storage-create-storage-account.md)
* [Azure Storage 확장성 및 성능 목표](storage-scalability-targets.md)
* [Microsoft Azure Storage 중복 옵션 및 읽기 액세스 지역 중복 저장소 ](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx)
* [SOSP 문서 - Azure Storage: 일관성과 가용성이 뛰어난 클라우드 저장소 서비스](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

