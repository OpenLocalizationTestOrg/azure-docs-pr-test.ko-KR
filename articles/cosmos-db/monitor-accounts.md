---
title: "Azure Cosmos DB 요청 및 저장소 모니터링 | Microsoft Docs"
description: "성능 메트릭(예: 요청 및 서버 오류) 및 사용 메트릭(예: 저장소 사용)에 대해 Azure Cosmos DB 계정을 모니터링하는 방법을 알아봅니다."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 4c6a2e6f-6e78-48e3-8dc6-f4498b235a9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: mimig
ms.openlocfilehash: 0ca652d31d6c50124f87916b4486d8279075f106
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-azure-cosmos-db-requests-usage-and-storage"></a>Azure Cosmos DB 요청, 사용 및 저장소 모니터링
[Azure Portal](https://portal.azure.com/)에서 Azure Cosmos DB 계정을 모니터링할 수 있습니다. 각 Azure Cosmos DB 계정에 대해 성능 메트릭(예: 요청 및 서버 오류) 및 사용 메트릭(예: 저장소 사용)을 사용할 수 있습니다.

계정 블레이드, 새 메트릭 블레이드 또는 Azure Monitor에서 메트릭을 검토할 수 있습니다.

## <a name="view-performance-metrics-on-the-metrics-blade"></a>메트릭 블레이드에서 성능 메트릭 보기
1. [Azure Portal](https://portal.azure.com/)에서 **서비스 더 보기**를 클릭하고, **데이터베이스**로 스크롤한 다음 **Azure Cosmos DB**를 클릭하고 성능 메트릭을 보려는 Azure Cosmos DB 계정의 이름을 클릭합니다.
2. 리소스 메뉴의 **모니터링** 아레에서 **메트릭**을 클릭합니다.

메트릭 블레이드가 열리고 검토할 컬렉션을 선택할 수 있습니다. 가용성, 요청, 처리량 및 저장소 메트릭을 검토하고 Azure Cosmos DB SLA와 비교할 수 있습니다.

## <a name="view-performance-metrics-by-using-azure-monitoring"></a>Azure 모니터링을 사용하여 성능 메트릭 보기
1. [Azure Portal](https://portal.azure.com/)에서 표시줄에 있는 **모니터**를 클릭합니다.
2. 리소스 메뉴에서 **메트릭**을 클릭합니다.
3. **모니터 - 메트릭** 창의 **리소스 그룹** 드롭다운 메뉴에서 모니터링할 Azure Cosmos DB 계정과 연결된 리소스 그룹을 선택합니다. 
4. **리소스** 드롭 다운 메뉴에서 모니터링할 데이터베이스 계정을 선택합니다.
5. **사용 가능한 메트릭** 목록에서 표시할 메트릭을 선택합니다. 다중 선택을 하려면 CTRL 단추를 사용합니다. 

    **그림** 창에서 메트릭이 표시됩니다. 

## <a name="view-performance-metrics-on-the-account-blade"></a>계정 블레이드에서 성능 메트릭 보기
1. [Azure Portal](https://portal.azure.com/)에서 **서비스 더 보기**를 클릭하고, **데이터베이스**로 스크롤한 다음 **Azure Cosmos DB**를 클릭하고 성능 메트릭을 보려는 Azure Cosmos DB 계정의 이름을 클릭합니다.
2. **모니터링** 렌즈에는 기본적으로 다음 타일이 표시됩니다.
   
   * 오늘의 총 요청 수
   * 사용된 저장소.
   
   데이터베이스에 데이터가 있는데 테이블에 **데이터를 사용할 수 없음** 이 표시되면 [문제 해결](#troubleshooting) 섹션을 참조하세요.
   
   ![요청 및 저장소 사용량이 표시된 모니터링 렌즈의 스크린샷](./media/monitor-accounts/documentdb-total-requests-and-usage.png)
3. **요청** 또는 **사용 할당량** 타일을 클릭하면 자세한 **메트릭** 블레이드가 열립니다.
4. **메트릭** 블레이드는 선택한 메트릭에 대한 세부 정보를 보여 줍니다.  블레이드 맨 위에는 시간별 요청 그래프가 표시되고 아래에는 정제 및 총 요청의 집계 값을 표시하는 테이블이 있습니다.  또한 메트릭 블레이드는 현재 메트릭 블레이드에 표시되는 메트릭으로 정의 및 필터링된 경고 목록을 보여 줍니다. 이런 방법으로, 경고가 많은 경우 여기에 표시되는 관련성 높은 경고만 볼 수 있습니다.   
   
   ![정제된 요청을 포함하는 메트릭 블레이드의 스크린샷](./media/monitor-accounts/documentdb-metric-blade.png)

## <a name="customize-performance-metric-views-in-the-portal"></a>포털에서 성능 메트릭 뷰 사용자 지정
1. 특정 차트에서 표시되는 메트릭을 사용자 지정하려면 차트를 클릭하여 **메트릭** 블레이드에서 열고 **차트 편집**을 클릭합니다.  
   ![차트 편집이 강조된 메트릭 블레이드 컨트롤의 스크린샷](./media/monitor-accounts/madocdb3.png)
2. **차트 편집** 블레이드는 차트에 표시되는 메트릭과 메트릭의 시간 범위를 수정하는 옵션이 있습니다.  
   ![차트 편집 블레이드의 스크린샷](./media/monitor-accounts/madocdb4.png)
3. 이 부분에 표시되는 메트릭을 변경하려는 경우 사용 가능한 성능 메트릭을 선택/선택 취소한 다음 블레이드의 아래쪽에 있는 **확인** 을 클릭하면 됩니다.  
4. 시간 범위를 변경하려면 다른 범위(예: **사용자 지정**)를 선택한 다음 블레이드의 아래쪽에 있는 **확인**을 클릭합니다.  
   
   ![사용자 지정 시간 범위를 입력하는 방법을 보여 주는 차트 편집 블레이드 시간 범위 파트의 스크린샷](./media/monitor-accounts/madocdb5.png)

## <a name="create-side-by-side-charts-in-the-portal"></a>포털에서 병렬 차트 만들기
Azure 포털에서 병렬 메트릭 차트를 만들 수 있습니다.  

1. 먼저 복사할 차트를 마우스 오른쪽 단추로 클릭하고 **사용자 지정**을 선택합니다.
   
   ![사용자 지정 옵션이 강조 표시된 총 요청 차트의 스크린샷](./media/monitor-accounts/madocdb6.png)
2. 메뉴에서 **복제**를 클릭하여 파트를 복사한 후 **사용자 지정 완료**를 클릭합니다.
   
   ![복제 및 사용자 지정 완료 옵션이 강조 표시된 총 요청 차트의 스크린샷](./media/monitor-accounts/madocdb7.png)  

이제 파트에 표시되는 메트릭 및 시간 범위를 사용자 지정하면서 이 파트를 다른 메트릭 파트로 처리할 수 있습니다.  이렇게 하면 두 가지 다른 메트릭 차트를 동시에 병렬로 볼 수 있습니다.  
    ![총 요청 차트 및 지난 1시간의 새로운 총 요청 차트의 스크린샷](./media/monitor-accounts/madocdb8.png)  

## <a name="set-up-alerts-in-the-portal"></a>포털에서 경고 설정
1. [Azure Portal](https://portal.azure.com/)에서 **서비스 더 보기**, **Azure Cosmos DB**를 차례로 클릭하고 성능 메트릭 경고를 설정할 Azure Cosmos DB 계정의 이름을 클릭합니다.
2. 리소스 메뉴에서 **경고 규칙** 을 클릭하여 경고 규칙 블레이드를 엽니다.  
   ![경고 규칙 부분이 선택된 스크린샷](./media/monitor-accounts/madocdb10.5.png)
3. **경고 규칙** 블레이드에서 **경고 추가**를 클릭합니다.  
   ![경고 추가 단추가 강조 표시된 경고 규칙 블레이드의 스크린샷](./media/monitor-accounts/madocdb11.png)
4. **경고 규칙 추가** 블레이드에서 다음을 지정합니다.
   
   * 설정 중인 경고 규칙의 이름
   * 새 경고 규칙에 대한 설명
   * 경고 규칙에 대한 메트릭
   * 경고가 활성화되는 시기를 결정하는 조건, 임계값 및 기간. 예를 들어 서버 오류가 지난 15분 동안 5개보다 많습니다.
   * 경고가 발생할 때 서비스 관리자 및 공동 관리자에게 메일을 보낼지 여부
   * 경고 알림에 대한 추가 메일 주소  
     ![경고 규칙 추가 블레이드의 스크린샷](./media/monitor-accounts/madocdb12.png)

## <a name="monitor-azure-cosmos-db-programatically"></a>프로그래밍 방식으로 Azure Cosmos DB 모니터링
포털에서 제공되는 계정 수준 메트릭(예: 계정 저장소 사용 및 총 요청)은 DocumentDB API를 통해 사용할 수 없습니다. 그러나 DocumentDB API를 사용하여 컬렉션 수준에서 사용 데이터를 조회할 수 있습니다. 컬렉션 수준 데이터를 검색하려면 다음을 수행합니다.

* REST API를 사용하려면 [컬렉션에 대해 GET을 수행](https://msdn.microsoft.com/library/mt489073.aspx)합니다. 컬렉션에 대한 할당량 및 사용량 정보는 응답의 x-ms-resource-quota 및 x-ms-resource-usage 헤더에서 반환됩니다.
* .NET SDK를 사용하려면 [DocumentClient.ReadDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.readdocumentcollectionasync.aspx) 메서드를 사용합니다. 이 메서드는 **CollectionSizeUsage**, **DatabaseUsage**, **DocumentUsage** 등의 여러 사용량 속성이 포함된 [ResourceResponse](https://msdn.microsoft.com/library/dn799209.aspx)를 반환합니다.

추가 메트릭에 액세스하려면 [Azure Monitor SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights)를 사용하세요. 가용 메트릭 정의는 다음을 호출하면 검색할 수 있습니다.

    https://management.azure.com/subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metricDefinitions?api-version=2015-04-08

개별 메트릭을 검색하는 쿼리는 다음 형식을 사용합니다.

    https://management.azure.com/subscriptions/{SubecriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metrics?api-version=2015-04-08&$filter=%28name.value%20eq%20%27Total%20Requests%27%29%20and%20timeGrain%20eq%20duration%27PT5M%27%20and%20startTime%20eq%202016-06-03T03%3A26%3A00.0000000Z%20and%20endTime%20eq%202016-06-10T03%3A26%3A00.0000000Z

자세한 내용은 [Azure Monitor REST API를 통해 리소스 메트릭 검색](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/02/23/retrieving-resource-metrics-via-the-azure-insights-api/)을 참조하세요. "Azure Inights"가 "Azure Monitor"로 이름이 변경되었습니다.  이 블로그 항목에서는 이전 이름을 참조합니다.

## <a name="troubleshooting"></a>문제 해결
최근에 데이터를 요청했거나 데이터베이스에 데이터를 추가했는데 모니터링 타일에 **데이터를 사용할 수 없음** 메시지가 표시되면 최근 사용 현황을 반영하도록 이 타일을 편집할 수 있습니다.

### <a name="edit-a-tile-to-refresh-current-data"></a>현재 데이터를 새로 고치도록 타일 편집
1. 특정 부분에 표시되는 메트릭을 사용자 지정하려면 차트를 클릭하여 **메트릭** 블레이드를 열고 **차트 편집**을 클릭합니다.  
   ![차트 편집이 강조된 메트릭 블레이드 컨트롤의 스크린샷](./media/monitor-accounts/madocdb3.png)
2. **차트 편집** 블레이드의 **시간 범위** 섹션에서 **지난 시간**, **확인**을 차례로 클릭합니다.  
   ![지난 시간이 선택된 차트 편집 블레이드의 스크린샷](./media/monitor-accounts/documentdb-no-available-data-past-hour.png)
3. 그러면 타일이 새로 고쳐져 최신 데이터 및 사용 현황이 표시됩니다.  
   ![업데이트된 총 요청 지난 시간 타일의 스크린샷](./media/monitor-accounts/documentdb-no-available-data-fixed.png)

## <a name="next-steps"></a>다음 단계
Azure Cosmos DB 용량 계획에 대한 자세한 내용은 [Azure Cosmos DB Capacity Planner 계산기](https://www.documentdb.com/capacityplanner)를 참조하세요.

