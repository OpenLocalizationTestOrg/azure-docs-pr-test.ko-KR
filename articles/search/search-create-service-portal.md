---
title: "aaaCreate hello 포털에서 Azure 검색 서비스 | Microsoft Docs"
description: "Hello 포털에서 Azure 검색 서비스를 프로 비전 합니다."
services: search
manager: jhubbard
author: HeidiSteen
documentationcenter: 
ms.assetid: c8c88922-69aa-4099-b817-60f7b54e62df
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: f1c7197a1467e32bd4b360b165c9059e6bb0e496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-service-in-hello-portal"></a>Hello 포털에서 Azure 검색 서비스 만들기

이 문서 어떻게 toocreate 또는 프로 비전 한 Azure 검색 서비스 hello 포털에 설명 합니다. PowerShell 지침에 대한 자세한 내용은 [PowerShell을 사용하여 Azure Search 관리](search-manage-powershell.md)를 참조하세요.

## <a name="subscribe-free-or-paid"></a>구독(무료 또는 유료)

[무료 Azure 계정을 엽니다](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) 아웃 무료 크레딧을 tootry 유료 Azure 서비스를 사용 하 고 있습니다. 크레딧을 모두 사용 된 후 hello 계정을 유지 하 고 toouse 무료 Azure 같은 서비스를 웹 사이트를 계속 합니다. 명시적으로 설정을 변경 하 고 청구 toobe 요청 하지 않는 한 신용 카드 청구 되지 됩니다.

아니면 [MSDN 구독자 혜택을 활성화합니다](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F). MSDN 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다. 

## <a name="find-azure-search"></a>Azure Search 찾기
1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Hello 왼쪽 위 모서리의에서 hello 더하기 기호 ("+")를 클릭 합니다.
3. **웹 + 모바일** > **Azure Search**를 선택합니다.

![](./media/search-create-service-portal/find-search2.png)

## <a name="name-hello-service-and-url-endpoint"></a>이름 hello 서비스와 끝점 URL

서비스 이름은 API 호출은 발급 된 hello URL 끝점의 일부입니다. Hello에 서비스 이름을 입력 **URL** 필드입니다. 

서비스 이름 요구 사항:
   * 2 ~ 60자 길이
   * 소문자, 숫자 또는 대시("-")
   * 없음 대시 ("-")으로 hello 처음 두 문자나 마지막 단일 문자
   * 연속 대시("--")를 사용할 수 없음

## <a name="select-a-subscription"></a>구독 선택
둘 이상의 구독이 있는 경우 데이터 또는 파일 저장소 서비스도 있는 구독을 선택합니다. Azure 검색 수 자동 검색 Azure 테이블 및 Blob 저장소, SQL 데이터베이스 및 Azure Cosmos DB를 통해 인덱싱을 *인덱서*, hello에 대 한 서비스에 대해서만 동일한 구독 합니다.

## <a name="select-a-resource-group"></a>리소스 그룹 선택
리소스 그룹은 함께 사용된 Azure 서비스 및 리소스의 컬렉션입니다. 예를 들어 Azure 검색 tooindex SQL 데이터베이스를 사용 하는 경우 다음 두 서비스의 일부 여야 hello 동일한 리소스 그룹입니다.

> [!TIP]
> 리소스 그룹을 삭제 하면 그 안에 hello 서비스도 삭제 됩니다. 여러 서비스를 사용 하 여, 모든 hello에 넣는 프로토타입 프로젝트에 대 한 동일한 리소스 그룹 더 쉽게 정리 hello 프로젝트 끝난 후 있습니다. 

## <a name="select-a-hosting-location"></a>호스팅 위치 선택 
Azure 서비스로 hello 전 세계 데이터 센터에서 Azure 검색을 호스팅할 수 있습니다. 지역별로 [가격이 다를 수](https://azure.microsoft.com/pricing/details/search/) 있습니다.

## <a name="select-a-pricing-tier-sku"></a>가격 책정 계층(SKU) 선택
[Azure 검색은 무료, 기본 또는 표준 등 여러 가지 가격 책정 계층에서 현재 제공됩니다](https://azure.microsoft.com/pricing/details/search/). 각 계층에는 자체 [용량 및 제한](search-limits-quotas-capacity.md)이 있습니다. 지침은 [가격 책정 계층 또는 SKU 선택](search-sku-tier.md) 을 참조하세요.

이 연습에서는 서비스에 대 한 hello 표준 계층을 했습니다.

## <a name="create-your-service"></a>서비스 만들기

에 로그인 할 때마다 toopin 쉬운 액세스를 위해 서비스 toohello 대시보드를 기억 합니다.

![](./media/search-create-service-portal/new-service2.png)

## <a name="scale-your-service"></a>서비스 확장
몇 분 toocreate (15 분 이상 hello 계층에 따라) 서비스를 걸릴 수 있습니다. 서비스 프로 비전 되 면 있습니다 크기를 조정할 수 toomeet 필요 합니다. Azure 검색 서비스에 대 한 hello 표준 계층을 선택 했기 때문에 두 가지 차원에서 서비스를 확장할 수 있습니다: 복제본과 파티션 합니다. Hello 기본 계층을 선택 했다면 있습니다, 복제본만 추가할 수 있습니다. Hello 무료 서비스를 프로 비전 하는 경우 배율 ´ ù.

***파티션*** 서비스 toostore 및 더 많은 문서를 검색 합니다.

***복제본*** 서비스 toohandle 검색 쿼리의 더 높은 부하를 허용 합니다.

> [!Important]
> 서비스는 [SLA 읽기 전용으로 2개의 복제본과 SLA 읽기/쓰기용으로 3개의 복제본](https://azure.microsoft.com/support/legal/sla/search/v1_0/)이 있어야 합니다.

1. Hello Azure 포털에서에서 tooyour 검색 서비스 블레이드로 이동 합니다.
2. Hello 왼쪽 탐색 창에서 선택 **설정** > **배율**합니다.
3. Hello slidebar tooadd 복제본 또는 파티션을 사용 합니다.

![](./media/search-create-service-portal/settings-scale.png)

> [!Note] 
> 각 계층 마다 서로 다른 [제한](search-limits-quotas-capacity.md) hello 단일 서비스에서 허용 하는 검색 단위의 총 수 (복제본 * 파티션을 총 검색 단위 =) 합니다.

## <a name="when-tooadd-a-second-service"></a>때 tooadd 두 번째 서비스

Hello를 제공 하는 계층에서 프로 비전 한 서비스를 사용 하는 대부분 고객의 [리소스의 균형을 마우스 오른쪽 단추로](search-sku-tier.md)합니다. 여러 색인, 제목 toohello 하나의 서비스 호스팅할 수 있습니다 [선택한 hello 계층의 최대 제한](search-capacity-planning.md), 된 각 인덱스를 서로 격리 합니다. Azure 검색 요청 tooone 방향이 지정 된 인덱스 수, 다른에서 실수로 또는 의도적으로 데이터를 검색할 hello 가능성이 최소화 인덱스 hello에 동일한 수 서비스입니다.

대부분의 고객이 한 서비스를 사용 하지만 서비스 중복성 운영 요구 사항을 hello 다음을 포함 하는 경우 필요한 수 있습니다.

+ 재해 복구(데이터 센터 작동 중단). Azure 검색에 즉각적인 장애 조치가 가동 중단의 hello 이벤트에서 제공 하지 않습니다. 권장 사항 및 지침에 대해서는 [서비스 관리](search-manage.md)를 참조하세요.
+ 다중 테 넌 트 모델링 조사 추가 서비스는 hello 최적의 디자인 결정 합니다. 자세한 내용은 [다중 테넌트 디자인](search-modeling-multitenant-saas-applications.md)을 참조하세요.
+ 전체적으로 배포 된 응용 프로그램에 대 한 Azure 검색의 인스턴스를 응용 프로그램의 국제 트래픽의 여러 영역 toominimize 대기 시간에 필요할 수 있습니다.

> [!NOTE]
> Azure Search에서는 인덱싱 및 쿼리 작업을 분리할 수 없습니다. 따라서 분리 된 작업에 대해 여러 서비스를 만들지 마세요. 인덱스는 항상 쿼리할 hello 서비스에는 자신이 만든 (하면 하나의 서비스에는 인덱스를 만들 없으며 tooanother 복사).
>

고가용성을 위해 두 번째 서비스가 필요하지 않습니다. 2를 사용 하거나 이상의 복제본에 동일한 서비스 hello 쿼리에 대 한 가용성을 높일 수 있습니다. 복제본 업데이트는 순차적입니다. 즉, 서비스 업데이트가 롤아웃될 때도 적어도 하나의 서비스는 작동됩니다. 가동 시간에 대한 자세한 내용은 [서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/search/v1_0/)을 참조하세요.

## <a name="next-steps"></a>다음 단계
Azure 검색 서비스에서 프로 비전 후 준비가 너무[인덱스 정의](search-what-is-an-index.md) 업로드 하 고 데이터를 검색할 수 있습니다.

hello URL을 제공 하는 코드 또는 스크립트에서 tooaccess hello 서비스 (*서비스 이름*.으로 끝나므로)와 키입니다. 관리 키는 모든 액세스 권한을 부여하고, 쿼리 키는 읽기 전용 액세스 권한을 부여합니다. 참조 [toouse Azure 검색.NET 방법](search-howto-dotnet-sdk.md) tooget 시작 합니다.

빠른 포털 기반 자습서는 [첫 번째 인덱스 빌드 및 쿼리](search-get-started-portal.md)를 참조하세요.

