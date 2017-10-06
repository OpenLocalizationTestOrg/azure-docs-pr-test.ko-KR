---
title: "Azure 검색의 다중 테 넌 트 aaaModeling | Microsoft Docs"
description: "Azure 검색을 사용할 때의 다중 테넌트 SaaS 응용 프로그램에 대한 일반적인 디자인 패턴에 대해 알아봅니다."
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 72e9696a-553b-47dc-9e05-a82db0ebf094
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/26/2016
ms.author: ashmaka
ms.openlocfilehash: dd46cda772d32566b9aaa18d407f12fdf178bd43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-multitenant-saas-applications-and-azure-search"></a>다중 테넌트 SaaS 응용 프로그램 및 Azure 검색에 대한 디자인 패턴
Hello를 제공 하는 다중 테 넌 트 응용 프로그램은 다른 테 넌 트의 hello 데이터를 공유 하거나 볼 수 있는 테 넌 트가 동일한 서비스와 기능 tooany 수 있습니다. 이 문서에서는 Azure 검색을 사용하여 작성된 다중 테넌트 응용 프로그램에 대한 테넌트 격리 전략에 대해 설명합니다.

## <a name="azure-search-concepts"></a>Azure 검색 개념
검색-as a service 솔루션으로 Azure 검색 개발자 tooadd 풍부한 검색 모든 인프라를 관리 하거나 검색 전문가가 되 고 하지 않고 tooapplications 발생할 수 있습니다. 데이터는 toohello 서비스를 업로드 하 고 다음 hello 클라우드에 저장 합니다. 간단한 요청 toohello Azure 검색 API를 사용 하 여 hello 데이터 다음 수정 및 검색할 수 있습니다. hello 서비스의 개요를 확인할 수 있습니다 [이 여기서](http://aka.ms/whatisazsearch)합니다. 디자인 패턴을 설명 하기 전에 중요 한 toounderstand 몇 가지 개념에 대해 Azure 검색 합니다.

### <a name="search-services-indexes-fields-and-documents"></a>검색 서비스, 인덱스, 필드 및 문서
Tooa 구독 한 Azure 검색을 사용할 경우 *검색 서비스*합니다. 에 저장 된 데이터를 업로드 tooAzure 검색으로는 *인덱스* hello 검색 서비스 내에서. 하나의 서비스 내에 많은 수의 인덱스가 있을 수 있습니다. 데이터베이스의 toouse hello 같은 익숙한 개념을 hello 검색 서비스 수 비유할 tooa 데이터베이스 hello 인덱스 서비스 내에서 데이터베이스 내에서 tootables 비유할 수 있습니다.

검색 서비스 내의 각 인덱스는 많은 수의 사용자 지정 가능 *필드*로 정의되는 고유 스키마를 갖습니다. 데이터가 개별 hello 형태로 tooan Azure 검색 인덱스 추가 *문서*합니다. 각 문서 업로드 tooa 특정 인덱스 및 해당 인덱스의 스키마에 포함 되어야 합니다. Azure 검색을 사용 하 여 데이터를 검색할 때는 hello 전체 텍스트 검색 쿼리는 특정 인덱스에 대해 실행 됩니다.  toocompare 데이터베이스의 이러한 개념 toothose 필드를 테이블에 비유할 toocolumns 수 및 문서에 비유할 toorows 일 수 있습니다.

### <a name="scalability"></a>확장성
모든 Azure 검색 서비스에 표준 hello [가격 책정 계층](https://azure.microsoft.com/pricing/details/search/) 2 차원에서 크기를 조정할 수: 저장소 및 가용성입니다.

* *파티션* 검색 서비스의 tooincrease hello 저장소를 추가할 수 있습니다.
* *복제본* tooa 서비스 tooincrease hello 처리량 검색 서비스가 처리할 수 있는 요청을 추가할 수 있습니다.

추가 및 제거 파티션과 복제본에는 데이터 캡슐화 된 트래픽과 hello 응용 프로그램 수요 hello 양의 hello 검색 서비스 toogrow의 hello 용량을 수 있습니다. 순서로 검색 서비스 tooachieve에 대 한 읽기 [SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/), 두 개의 복제본 필요 합니다. 요청 서비스 tooachieve에 대 한 읽기 / 쓰기 [SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/), 세 개의 복제본 필요 합니다.

### <a name="service-and-index-limits-in-azure-search"></a>Azure 검색의 서비스 및 인덱스 제한 사항
다른 몇 가지 [가격대](https://azure.microsoft.com/pricing/details/search/) Azure 검색에서는 각 hello 계층에 다른 [제한 및 할당량](search-limits-quotas-capacity.md)합니다. 이러한 제한 중 일부는 hello 서비스 수준에, 일부는 hello 인덱스 수준에서 고 hello 파티션 수준입니다.

|  | Basic | Standard1 | Standard2 | Standard3 | Standard3 HD |
| --- | --- | --- | --- | --- | --- |
| 서비스당 최대 복제본 |3 |12 |12 |12 |12 |
| 서비스당 최대 파티션 |1 |12 |12 |12 |1 |
| 서비스당 최대 검색 단위(복제본*파티션) |3 |36 |36 |36 |36(파티션 최대 3개) |
| 서비스당 최대 문서 |1백만 |1억 8천만 |7억 2천만 |14억 |6억 |
| 서비스당 최대 저장소 |2 GB |300GB |1.2TB |2.4TB |600GB |
| 파티션당 최대 문서 |1백만 |1천 5백만 |6천만 |1억 2천만 |2억 |
| 파티션당 최대 저장소 |2 GB |25GB |100GB |200GB |200GB |
| 서비스당 최대 인덱스 |5 |50 |200 |200 |3000(인덱서/파티션 최대 1000) |

#### <a name="s3-high-density"></a>S3 고밀도
Azure 검색의 S3 가격 책정 계층은 다음과 같이 다중 테 넌 트 시나리오용으로 특별히 설계 된 hello 높은 밀도 (HD) 모드에 대 한 옵션입니다. 대부분의 경우에서 필요한 toosupport 단순성 및 비용 효율성의 단일 서비스 tooachieve hello 이점에서 테 넌 트를 더 작은 많은 것합니다.

S3 HD hello 많은 작은 인덱스 toobe 단일 검색 서비스의 hello 관리에서 사용 하 여 인덱스 파티션 기능 toohost hello에 대 한 단일 서비스에서 더 많은 인덱스 아웃 hello 기능 tooscale 거래 하 여 압축을 허용 합니다.

구체적으로 S3 서비스 too1.4 십억 문서를 함께 호스팅할 수 있었던 인덱스 1 자에서 200 사이 있을 수 있습니다. S3 HD hello에 다른 손을 사용 하면 개별 인덱스 tooonly too1 백만 문서 위로 이동 하지만 파티션당 200 백만 총 문서 수와 함께 서비스 당 too3000) (위쪽 파티션당 too1000 인덱스를 처리할 수 있습니다 (too600를 서비스 당 백만).

## <a name="considerations-for-multitenant-applications"></a>다중 테넌트 응용 프로그램에 대한 고려 사항
다중 테 넌 트 응용 프로그램 효과적으로 배포 해야 hello 테 넌 트 간에 리소스 일정 수준의 hello 간의 개인 정보 보호를 유지 하면서 다양 한 테 넌 트가 있습니다. 이러한 응용 프로그램에 대 한 hello 아키텍처를 설계할 때 몇 가지 고려해 야 할 사항이 있습니다.

* *테 넌 트 격리:* 응용 프로그램 개발자는 테 넌 트가 없는 권한이 없음 했거나 다른 테 넌 트의 데이터에 액세스 toohello 원치 않는 tootake 적절 한 조치 tooensure 개발 해야 합니다. 데이터 프라이버시의 hello 관점 외 테 넌 트 격리 전략 시끄러운 이웃에서 보호 및 공유 리소스를 효과적으로 관리를 해야합니다.
* *클라우드 리소스 비용:* 다른 응용 프로그램과 마찬가지로, 소프트웨어 솔루션은 다중 테넌트 응용 프로그램의 구성 요소로서 비용 경쟁력을 유지해야 합니다.
* *작업의 용이성:* 다중 테 넌 트 아키텍처를 개발할 때 hello hello 응용 프로그램의 작업에 미치는 영향 및 복잡도 매우 중요 합니다. Azure Search는 [99.9% SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/)를 보장합니다.
* *전역 공간:* tooeffectively serve 테 넌 트 hello 전 세계에 분산 되어 있는 다중 테 넌 트 응용 프로그램 필요 합니다.
* *확장성:* 응용 프로그램 개발자 들이 충분히 낮은 수준의 응용 프로그램 복잡성을 유지 하 고 테 넌 트 수를 사용 하 여 hello 응용 프로그램 tooscale 디자인 간에 조정 방법을 tooconsider 필요 하며 테 넌 트의 데이터 크기의 hello 및 작업입니다.

Azure 검색에서는 사용 되는 tooisolate 테 넌 트의 데이터 및 작업 수 있는 몇 가지 경계를 제공 합니다.

## <a name="modeling-multitenancy-with-azure-search"></a>Azure 검색을 사용한 다중 테넌트 모델링
다중 테 넌 트 시나리오의 경우 hello 서비스, 인덱스, 또는 둘 다에서 해당 테 넌 트를 분할 하 hello 응용 프로그램 개발자 하나 이상의 검색 서비스를 사용 합니다. Azure 검색에서는 다중 테넌트 시나리오를 모델링할 때 몇 가지 일반적인 패턴을 따릅니다.

1. *테넌트당 인덱스:* 각 테넌트는 다른 테넌트와 공유되는 검색 서비스 내의 자체 인덱스를 갖습니다.
2. *테넌트당 서비스:* 각 테넌트는 자체 전용 Azure Search 서비스를 갖습니다. 이 검색 서비스는 가장 높은 수준의 데이터 및 워크로드 분리를 제공합니다.
3. *두 가지 조합:* 좀 더 작은 테넌트에는 공유 서비스 내에서 개별 인덱스가 할당되지만, 좀 더 큰 활성 테넌트에는 전용 서비스가 할당됩니다.

## <a name="1-index-per-tenant"></a>1. 테넌트당 인덱스
![Hello 인덱스 당-테 넌 트 모델을 묘사](./media/search-modeling-multitenant-saas-applications/azure-search-index-per-tenant.png)

테넌트당 인덱스 모델에서 여러 테넌트가 단일 Azure 검색 서비스에 포함되며, 각 테넌트는 고유 인덱스를 갖습니다.

모든 검색 요청 및 문서 작업은 Azure 검색의 인덱스 수준에서 실행되므로 테넌트의 데이터 격리가 구현됩니다. Hello 응용 프로그램 계층 toodirect 다양 한 테 넌 트의 트래픽 toohello 적절 한 인덱스를 모든 테 넌 트 간에 hello 서비스 수준에서 리소스를 관리 하면서 hello hello 요구 인식이 있습니다.

Hello 테 넌 인덱스 당 모델의 주요 특성은 hello 응용 프로그램의 테 넌 트 간에 검색 서비스의 hello 응용 프로그램 개발자 toooversubscribe hello 용량에 대 한 hello 기능입니다. 에 배포할 수는 작업 부하의 불균등 한 배포, 테 넌 트 수의 hello 최적 조합을 hello 테 넌 트가 있는 경우 검색 서비스의 인덱스 tooaccommodate 매우 진행 중, 리소스 사용량이 테 넌 트의 숫자의 긴 꼬리를 동시에 처리 하는 동안 덜 활성화 테 넌 트입니다. hello 대신 hello 없어서 hello 모델 toohandle 중요시 각 테 넌 트 동시에 매우 활성화 됩니다.

hello 테 넌 인덱스 당 모델에서는 전체 Azure 검색 서비스 선불 구입 되는 가변 비용 모델에 대 한 hello 기초를 제공 테 넌 트와 이후에 채워집니다. 따라서 사용 되지 않는 용량 toobe 평가판 및 무료 계정에 대 한 지정 된 수 있습니다.

전역 사용 공간 응용 프로그램에 대 한 hello 테 넌 인덱스 당 모델 hello 가장 효율적인 아닐 수 있습니다. 응용 프로그램의 테 넌 트 hello 전 세계에 분산 하는 경우 별도 서비스에서 각각의 비용을 복제할 수 있습니다는 각 지역에 대해 할 수 있습니다.

Azure 검색의 hello 개별 인덱스와 인덱스 toogrow의 총 hello hello 눈금에 대 한 있습니다. 적절 한 가격 경우 파티션 및 복제본 추가할 수 있습니다 때 hello 서비스 내에서 개별 인덱스 toohello 전체 검색 서비스 저장소 또는 트래픽 측면에서 너무 커져 계층 선택 됩니다.

단일 서비스에 대 한 인덱스의 총 hello 너무 커지면, 다른 서비스를 프로 비전 toobe tooaccommodate hello 새 테 넌 트에 있습니다. Hello 인덱스에서 hello 데이터에 다른 인덱스 한 개 toohello에서 수동으로 복사한 toobe 인덱스 새로운 서비스를 추가할 때 검색 서비스 간에 이동 toobe 있으면 Azure 검색에서 이동 하는 인덱스 toobe에 대 한 허용 하지 않으므로 합니다.

## <a name="2-service-per-tenant"></a>2. 테넌트당 서비스
![Hello 테 넌 당 서비스 모델을 묘사](./media/search-modeling-multitenant-saas-applications/azure-search-service-per-tenant.png)

테넌트당 서비스 아키텍처에서 각 테넌트에는 자체 검색 서비스가 있습니다.

이 모델에서는 hello 응용 프로그램에는 hello 최대 해당 테 넌 트에 대 한 격리 수준을 얻을 수 있습니다. 각 서비스에는 별도의 API 키 외에도, 검색 요청을 처리하기 위한 전용 저장소 및 처리량을 갖습니다.

각 테 넌 트에는 큰 사용 공간이 위치나 hello 워크 로드가 테 넌 트 tootenant에서 거의 가변성 응용 프로그램의 경우 hello 서비스 당 테 넌 model은 효과적 리소스 다양 한 테 넌 트의 워크 로드 간에 공유 되지 않습니다.

또한 테 넌 트 모델에 대해 서비스는 예측 가능 하 고 고정 비용 모델의 hello 혜택을 제공 합니다. 그러나 테 넌 트 toofill 있을 때까지 전체 검색 서비스에 없는 선행 투자는, hello 비용 당-테 넌 트 보다 크면 인덱스 당-테 넌 트 모델입니다.

hello 서비스 당 테 넌 모델은 전역 사용 공간 응용 프로그램에 사용 하면 효율적인 옵션입니다. 지리적으로 분산 테 넌 트와 것은 쉽게 toohave 각 테 넌 트의 서비스 hello 적절 한 영역입니다.

이 패턴의 크기를 조정 hello 과제 개별 테 넌 트가 해당 서비스 보다 커지는 경우 발생 합니다. Azure 검색은 모든 데이터는 수동으로 복사 toobe tooa 새 서비스를 갖도록의 가격 책정 검색 서비스의 계층 업그레이드 hello를 현재 지원 하지 않습니다.

## <a name="3-mixing-both-models"></a>3. 두 모델 조합
다중 테넌트를 모델링하기 위한 또 다른 패턴은 테넌트당 인덱스 및 테넌트당 서비스 전략을 조합하는 것입니다.

Hello 두 패턴을 혼합 하 여 hello 덜 활성, 더 작은 테 넌 트의 긴 꼬리 공유 서비스에서 인덱스를 차지할 수 하는 동안 응용 프로그램의 가장 큰 테 넌 트 전용된 서비스를 사용할 수 있습니다. 이 모델 hello 가장 큰 테 넌 트 일관 되 게 고성능 hello 서비스에서 동시에 모든 시끄러운 이웃에서 더 작은 테 넌 트 hello tooprotect 수 있는지 확인 합니다.

그러나 이 전략을 구현하려면 공유 서비스의 인덱스 대비, 전용 서비스를 요구하는 테넌트를 예측해야 합니다. 응용 프로그램 복잡성 hello 필요 toomanage 모두 이러한 다중 테 넌 트 모델에 따라 카운터가 증가 합니다.

## <a name="achieving-even-finer-granularity"></a>훨씬 더 미세한 세밀성 달성
디자인 패턴 toomodel Azure 검색의 다중 테 넌 트 시나리오가 위의 hello 각 테 넌 트 응용 프로그램의 전체 인스턴스에 인 동일한 범위를 가정 합니다. 그러나 응용 프로그램은 경우에 따라 좀 더 작은 여러 범위를 처리할 수 있습니다.

서비스 당-테 넌 트 및 테 넌 인덱스 당 모델 그리 크지 범위를 없는 경우 가능한 toomodel 인덱스 tooachieve는 훨씬 더 세밀 수준의 세분성입니다.

다른 클라이언트 끝점에 대 한 단일 인덱스로 동작이 toohave, 필드 가능한 각 클라이언트에 대 한 특정 값을 지정 하는 추가 된 tooan 인덱스 수 있습니다. Hello 클라이언트 응용 프로그램에서 hello 코드 hello Azure 검색을 사용 하 여 해당 필드에 대 한 적절 한 값을 지정 하 고, 클라이언트가 Azure 검색 tooquery를 호출 하거나 인덱스를 수정 될 때마다 [필터](https://msdn.microsoft.com/library/azure/dn798921.aspx) 쿼리 시 기능입니다.

이 메서드는 별도 사용자 계정, 별도 사용 권한 수준 및 완전히 별도 응용 프로그램의 기능을 사용 하는 tooachieve 될 수 있습니다.

> [!NOTE]
> Hello 방식을 사용 하 여 위에서 설명한 tooconfigure 단일 인덱스 tooserve 검색 결과 관련성 hello 여러 테 넌 트에 영향을 줍니다. 검색 관련성 점수는 모든 테 넌 트의 데이터는 hello 관련성 점수 용어 빈도 같은 기본 통계에 포함 되므로 테 넌 트 수준 범위 인덱스 수준 범위에서 계산 됩니다.
> 
> 

## <a name="next-steps"></a>다음 단계
Azure 검색은 많은 응용 프로그램에 대 한 눈에 띄는 선택 [hello 서비스의 강력한 기능에 대 한 자세한 내용을 읽어보십시오](http://aka.ms/whatisazsearch)합니다. 때 평가 hello 다양 한 다중 테 넌 트 응용 프로그램 패턴을 디자인, hello는 것이 좋습니다 [다양 한 가격 책정 계층](https://azure.microsoft.com/pricing/details/search/) 및 각각 hello [제한 서비스](search-limits-quotas-capacity.md) toobest Azure 검색 toofit 조정 응용 프로그램 작업 및 모든 규모의 아키텍처입니다.

Azure 검색 및 다중 테 넌 트 시나리오에 대 한 질문을 전송할 수 tooazuresearch_contact@microsoft.com합니다.

