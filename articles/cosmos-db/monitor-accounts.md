---
title: "Azure Cosmos DB aaaMonitor 요청 및 저장소 | Microsoft Docs"
description: "어떻게 toomonitor Azure Cosmos DB는 요청 및 서버 오류와 같은 성능 메트릭 및 사용 메트릭을 저장소 소비 등을 계정에 대해 알아봅니다."
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
ms.openlocfilehash: aea029d10717236a573a080dab9d06d87f97f318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-cosmos-db-requests-usage-and-storage"></a>Azure Cosmos DB 요청, 사용 및 저장소 모니터링
Hello에서 Azure Cosmos DB 계정을 모니터링할 수 있습니다 [Azure 포털](https://portal.azure.com/)합니다. 각 Azure Cosmos DB 계정에 대해 성능 메트릭(예: 요청 및 서버 오류) 및 사용 메트릭(예: 저장소 사용)을 사용할 수 있습니다.

Azure 모니터 또는 새 메트릭 블레이드 hello hello 계정 블레이드에서 메트릭은 검토할 수 있습니다.

## <a name="view-performance-metrics-on-hello-metrics-blade"></a>Hello 메트릭 블레이드를 성능 메트릭 보기
1. Hello에 [Azure 포털](https://portal.azure.com/), 클릭 **더 서비스**, 너무 스크롤하여**데이터베이스**, 클릭 **Azure Cosmos DB**, 다음의 hello hello 이름을 클릭 하 고 Azure Cosmos DB 계정 tooview 성능 메트릭을 방식입니다.
2. Hello 리소스 메뉴에서 아래 **모니터링**, 클릭 **메트릭**합니다.

hello 메트릭 블레이드 열리고 hello 컬렉션 tooreview를 선택할 수 있습니다. 가용성, 요청, 처리량 및 저장소 메트릭을 검토 수 있으며 toohello Azure Cosmos DB Sla 비교할 수 있습니다.

## <a name="view-performance-metrics-by-using-azure-monitoring"></a>Azure 모니터링을 사용하여 성능 메트릭 보기
1. Hello에 [Azure 포털](https://portal.azure.com/), 클릭 **모니터** Jumpbar hello에 있습니다.
2. Hello 리소스 메뉴에서 클릭 **메트릭**합니다.
3. Hello에 **모니터-메트릭** 창의 hello **사용할 수 있는 리소스 그룹** 드롭 다운 메뉴에서 싶다는 의사를 toomonitor hello Azure Cosmos DB 계정과 연결 된 선택 hello 리소스 그룹입니다. 
4. Hello에 **리소스** 드롭 다운 메뉴에서 선택 hello 데이터베이스 계정 toomonitor 합니다.
5. Hello 목록에 **사용 가능한 메트릭**, hello 메트릭 toodisplay를 선택 합니다. Hello CTRL 단추 toomulti select를 사용 합니다. 

    하면 메트릭이 hello에서에 표시 됩니다 **그릴** 창. 

## <a name="view-performance-metrics-on-hello-account-blade"></a>Hello 계정 블레이드에서 성능 메트릭 보기
1. Hello에 [Azure 포털](https://portal.azure.com/), 클릭 **더 서비스**, 너무 스크롤하여**데이터베이스**, 클릭 **Azure Cosmos DB**, 다음의 hello hello 이름을 클릭 하 고 Azure Cosmos DB 계정 tooview 성능 메트릭을 방식입니다.
2. hello **모니터링** 렌즈 hello 기본적으로 타일을 따라 표시 됩니다.
   
   * 현재 날짜 hello에 대 한 총 요청 수입니다.
   * 사용된 저장소.
   
   테이블에 표시 되는 경우 **사용 가능한 데이터가 없습니다** hello 참조, 데이터베이스의 데이터가 있다고 생각 되 고 [문제 해결](#troubleshooting) 섹션.
   
   ![Hello 모니터링 렌즈 hello 요청 및 hello 저장소 사용을 보여 주는 스크린 샷](./media/monitor-accounts/documentdb-total-requests-and-usage.png)
3. Hello 클릭 하면 **요청** 또는 **사용 할당량** 타일 열립니다는 자세한 **메트릭을** 블레이드입니다.
4. hello **메트릭을** 블레이드는 선택한 hello 메트릭에 대 한 자세한 정보 표시 합니다.  Hello hello 블레이드 맨은 요청에 대 한 그래프 시간별, 축은 차트에 포함 되며 그 아래 정체 된 및 총 요청에 대 한 집계 값을 보여 주는 표입니다.  hello 메트릭 블레이드도 hello 목록으로 표시 된 현재 메트릭 블레이드 hello에 표시 되는 정의 되 고 필터링 된 toohello 메트릭을 하는 경고 (이러한 방식으로 있는 다양 한 경고를 볼 수 있습니다만 여기에 제공 된 관련 항목이 hello).   
   
   ![요청을 제한 하는 포함 하는 hello 메트릭 블레이드의 스크린샷](./media/monitor-accounts/documentdb-metric-blade.png)

## <a name="customize-performance-metric-views-in-hello-portal"></a>Hello 포털의 성능 메트릭 보기를 사용자 지정
1. 특정 차트에 표시 하는 toocustomize hello 메트릭을 클릭 hello 차트 tooopen hello에서 **메트릭을** 블레이드에서 하 고 클릭 한 다음 **차트 편집**합니다.  
   ![Hello 메트릭 블레이드 컨트롤을 강조 표시 된 차트 편집 스크린 샷](./media/monitor-accounts/madocdb3.png)
2. Hello에 **차트 편집** 블레이드를 가지는 시간 범위를 비롯 하 여 hello 차트에 표시 하는 옵션 toomodify hello 메트릭이 있습니다.  
   ![Hello 차트 편집 블레이드의 스크린 샷](./media/monitor-accounts/madocdb4.png)
3. hello 부분에 표시 되는 toochange hello 메트릭 선택 하기만 하면 또는 hello 사용 가능한 성능 메트릭 지우고 클릭 **확인** hello hello 블레이드 맨 아래에 있습니다.  
4. toochange hello 시간 범위를 다른 범위를 선택 합니다. (예를 들어 **사용자 지정**)를 클릭 하 고 **확인** hello hello 블레이드 맨 아래에 있습니다.  
   
   ![스크린 샷 부분의 hello 시간 범위 hello 차트 편집 블레이드 보여 주는 방법을 tooenter 사용자가 지정한 시간 범위](./media/monitor-accounts/madocdb5.png)

## <a name="create-side-by-side-charts-in-hello-portal"></a>Hello 포털에서 side-by-side-차트 만들기
Azure 포털 hello toocreate side-by-side-메트릭 차트 수 있습니다.  

1. 첫째, toocopy 한 선택 hello 차트에서 마우스 오른쪽 단추로 클릭 **사용자 지정**합니다.
   
   ![강조 표시 하는 hello 사용자 지정 옵션을 포함 하는 hello 총 요청 수 차트 스크린 샷](./media/monitor-accounts/madocdb6.png)
2. 클릭 **복제** 메뉴 toocopy hello 파트 hello 되 고 클릭 **사용자 지정 작업은 수행**합니다.
   
   ![스크린 샷 hello 복제본이 있는 hello 총 요청 수 차트의 대상과 강조 표시 하는 사용자 지정 옵션](./media/monitor-accounts/madocdb7.png)  

있습니다 취급할 수 있습니다 이제이 부분 어떠한 메트릭 부분으로 hello 파트에 표시 된 hello 메트릭 및 시간 범위를 사용자 지정 합니다.  이 작업을 수행 하 여 두 가지 다른 메트릭으로 차트-함께 hello에서 볼 수 있습니다 동시 합니다.  
    ![스크린 샷 hello 총 요청 수 차트 및 hello 지난 시간 차트 새 총 요청 수](./media/monitor-accounts/madocdb8.png)  

## <a name="set-up-alerts-in-hello-portal"></a>Hello 포털의 경고 설정
1. Hello에 [Azure 포털](https://portal.azure.com/), 클릭 **더 서비스**, 클릭 **Azure Cosmos DB**, 하려는 toosetup hello Azure Cosmos DB 계정의 hello 이름을 클릭 하 고 성능 메트릭 알림을 제공 합니다.
2. Hello 리소스 메뉴에서 클릭 **경고 규칙** tooopen hello 경고 규칙 블레이드입니다.  
   ![선택 부분 스크린 샷 hello 경고 규칙](./media/monitor-accounts/madocdb10.5.png)
3. Hello에 **규칙 경고** 블레이드에서 클릭 **추가 경고**합니다.  
   ![Hello 경고 추가 단추가 강조 표시 된 hello 경고 규칙 블레이드의 스크린샷](./media/monitor-accounts/madocdb11.png)
4. Hello에 **경고 규칙 추가** 블레이드를 지정 합니다.
   
   * 설정 하는 hello 경고 규칙의 hello 이름입니다.
   * Hello 새 경고 규칙에 대 한 설명
   * hello 경고 규칙에 대 한 hello 메트릭입니다.
   * hello 조건, 임계값 및 기간 hello 경고가 활성화 되는 시기를 결정 하는 합니다. 예를 들어 서버 오류 횟수를 5 이상 지난 15 분 동안 hello를 통해.
   * 서비스 관리자를 hello 여부 및 coadministrators hello 경고가 발생할 때 전자 메일로 전송 합니다.
   * 경고 알림에 대한 추가 메일 주소  
     ![경고 규칙 블레이드 추가 hello 스크린 샷](./media/monitor-accounts/madocdb12.png)

## <a name="monitor-azure-cosmos-db-programatically"></a>프로그래밍 방식으로 Azure Cosmos DB 모니터링
계정 수준 메트릭이 저장소 계정 사용 같이 hello 포털에서 사용할 수 있는 hello 및 hello DocumentDB Api를 통해 사용할 수 없는 총 요청 합니다. 그러나 hello DocumentDB Api를 사용 하 여 hello 컬렉션 수준에서 사용 현황 데이터를 검색할 수 있습니다. tooretrieve 컬렉션 수준 데이터에 따라 hello지 않습니다.

* REST API toouse hello [hello 컬렉션에 대해 GET을 수행](https://msdn.microsoft.com/library/mt489073.aspx)합니다. hello 컬렉션에 대 한 hello 할당량 및 사용 정보는 hello x ms-리소스 할당량 및 x ms-리소스 사용 헤더 hello에 대 한 응답에 반환 됩니다.
* toouse hello.NET SDK를 사용 하 여 hello [DocumentClient.ReadDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.readdocumentcollectionasync.aspx) 반환 하는 [ResourceResponse](https://msdn.microsoft.com/library/dn799209.aspx) 같은 다양 한 사용 속성을 포함 하  **CollectionSizeUsage**, **DatabaseUsage**, **DocumentUsage**, 등입니다.

tooaccess 추가 메트릭을 사용 하 여 hello [Azure 모니터 SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights)합니다. 가용 메트릭 정의는 다음을 호출하면 검색할 수 있습니다.

    https://management.azure.com/subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metricDefinitions?api-version=2015-04-08

쿼리 tooretrieve 개별 메트릭 사용 하 여 hello 형식에 따라:

    https://management.azure.com/subscriptions/{SubecriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metrics?api-version=2015-04-08&$filter=%28name.value%20eq%20%27Total%20Requests%27%29%20and%20timeGrain%20eq%20duration%27PT5M%27%20and%20startTime%20eq%202016-06-03T03%3A26%3A00.0000000Z%20and%20endTime%20eq%202016-06-10T03%3A26%3A00.0000000Z

자세한 내용은 참조 [hello Azure 모니터 REST API를 통해 리소스 메트릭 검색](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/02/23/retrieving-resource-metrics-via-the-azure-insights-api/)합니다. "Azure Inights"가 "Azure Monitor"로 이름이 변경되었습니다.  이 블로그 항목 toohello 이전 이름을 참조합니다.

## <a name="troubleshooting"></a>문제 해결
디스플레이 hello 타일을 모니터링 하는 경우 **사용 가능한 데이터가 없습니다** 수 최근에 요청을 수행 하거나 데이터 toohello 데이터베이스를 추가, hello 타일 tooreflect hello 최근 사용을 편집할 수 있습니다.

### <a name="edit-a-tile-toorefresh-current-data"></a>타일 toorefresh 현재 데이터 편집
1. 특정 부분에 표시 하는 toocustomize hello 메트릭을 클릭 hello 차트 tooopen hello **메트릭을** 블레이드에서 하 고 클릭 한 다음 **차트 편집**합니다.  
   ![Hello 메트릭 블레이드 컨트롤을 강조 표시 된 차트 편집 스크린 샷](./media/monitor-accounts/madocdb3.png)
2. Hello에 **차트 편집** 블레이드 hello **시간 범위** 섹션에서 클릭 **지난 시간**, 클릭 하 고 **확인**합니다.  
   ![지난 시간 선택 hello 차트 편집 블레이드의 스크린 샷](./media/monitor-accounts/documentdb-no-available-data-past-hour.png)
3. 그러면 타일이 새로 고쳐져 최신 데이터 및 사용 현황이 표시됩니다.  
   ![스크린 샷 hello 업데이트의 총 시간 타일 지난 요청](./media/monitor-accounts/documentdb-no-available-data-fixed.png)

## <a name="next-steps"></a>다음 단계
Azure Cosmos DB 용량 계획에 대해 자세히 toolearn 참조 hello [Azure Cosmos DB 용량 플래너 계산기](https://www.documentdb.com/capacityplanner)합니다.

