---
title: "Azure CDN에 대 한 aaaLog 분석 | Microsoft Docs"
description: "고객은 Azure CDN에 대한 Log Analytics를 사용하도록 설정할 수 있습니다."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a>Azure CDN에 대한 진단 로그

응용 프로그램에 대해 CDN을 활성화 한 다음 됩니다 가능성이 toomonitor hello CDN 사용, 배달의 hello 상태를 확인을 잠재적인 문제를 해결 합니다. Azure CDN에서는 [CDN 핵심 분석](cdn-analyze-usage-patterns.md) 및 [진단 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)에 이러한 기능을 제공합니다.

## <a name="cdn-core-analytics"></a>CDN 핵심 분석
Verizon 표준 또는 프리미엄 프로필과 현재 Azure CDN 사용자로 이미 있는 수 tooview 코어 분석 hello 보조 포털 hello hello Azure 포털에서에서 "관리" 옵션을 통해 액세스할 수 있습니다. 

## <a name="azure-diagnostic-logs"></a>Azure 진단 로그

이 새로운 기능의 Azure를 통해 이제 핵심 분석을 보고 다음을 포함한 하나 이상의 대상에 저장할 수 있습니다.

 - Azure Storage 계정
 - Azure Event Hubs
 - [OMS Log Analytics 리포지토리](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 이 기능은 tooVerizon (Standard 및 Premium) 및 (표준) Akamai CDN 프로필에 속한 모든 CDN 끝점에 사용할 수 있습니다.

진단 로그를 사용 하면 프로그램 CDN 끝점 tooa의 다양 한 원본에서 기본 사용 현황 메트릭 tooexport 사용자 지정 된 방식으로 사용할 수 있도록 합니다. 수행할 수는 예를 들어 다음 데이터 내보내기의 유형을 hello:

- 데이터 tooblob 저장소 내보내기, tooCSV, 내보내기 및 그래프를 생성 합니다. excel에서 합니다.
- Tooevent 허브 데이터를 내보내고 다른 azure 서비스의 데이터로 상관 관계를 지정 합니다.
- OMS 작업 영역에서 데이터 toolog 보기 및 분석 데이터 내보내기

hello 다음 그림은 데이터에 대 한 일반적인 CDN 코어 분석 뷰.

![포털 - 진단 로그](./media/cdn-diagnostics-log/01_OMS-workspace.png)

*그림 1 - CDN 핵심 분석 뷰*

연습을 수행 하는 hello hello 스키마의 hello 코어 분석 데이터를 hello 기능을 사용 하 고 toovarious 대상에 게 배달 하 고, 이러한 대상에서 사용에 관련 된 단계를 거칩니다.

## <a name="enable-logging-with-azure-portal"></a>Azure Portal에서 로깅을 사용하도록 설정

> [!NOTE]
> hello 진단 로그는 되어 **오프** 기본적으로 합니다. 

CDN 코어 분석을 tooenable 로깅 아래 hello 단계를 수행 합니다.

Toohello 로그인 [Azure 포털](http://portal.azure.com)합니다. 워크플로에 대해 아직 CDN을 사용하도록 설정하지 않은 경우 계속하기 전에 [Azure CDN을 사용](cdn-create-new-endpoint.md)하도록 설정합니다.

1. Hello 포털에서 이동 너무**CDN 프로필**합니다.
2. CDN 프로필을 선택 하 고 원하는 tooenable hello CDN 끝점을 선택 **진단 로그**합니다.

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. 너무 이동**진단 로그** 아래 블레이드 **모니터링** 섹션에서 다음도 hello 상태 변경**에**합니다.

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a>Azure Storage에서 로깅을 사용하도록 설정
    
toouse Azure 저장소 toostore hello 로그 선택 **tooa 저장소 계정 보관**, 보존 (일)를 선택 하 고 클릭 **CoreAnalytics** 아래 **로그**합니다.

![포털 - 진단 로그](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

*그림 2 - Azure Storage로 로깅*

### <a name="logging-with-oms-log-analytics"></a>OMS Log Analytics로 로깅

toouse OMS 로그 분석 toostore hello 로그는 다음이 단계를 따르십시오.

1. Hello에서 **진단 로그** 아래 블레이드 **모니터링**선택, **tooLog 분석 보내기** 에서 

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. 구성을 클릭 하 여 hello 로그 분석 로깅을 구성 합니다. 이렇게 하면 tooa 대화 이전 작업 영역을 선택 하거나 새로 만들 수 있습니다.

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. **새 작업 영역 만들기**를 클릭합니다.

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/07_Create-new.png)

4. 그런 다음 새 작업 영역 이름, 기존 구독, 리소스 그룹(새로운 또는 기존), 위치 및 가격 책정 계층을 선택해야 합니다. 이 구성 tooyour 대시보드에 고정 hello 선택할을 수 있습니다. 확인 toocomplete hello 구성을 클릭 합니다.

    그러면 OMS 작업 영역 및 리소스 그룹 이름과 함께 작업 영역이 표시됩니다. 이름은 고유해야 하며 문자, 숫자 및 하이픈만 사용할 수 있습니다. 공백 및 밑줄은 허용되지 않습니다. 

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. 다음 작업 영역을 만든 및 구성 화면 로깅 tooyour 반환될지 말하는 짧은 메시지를 가져옵니다. 로그 분석 작업 영역의 hello 이름을 확인할 수 있습니다.

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    Hello 로그 분석 구성을 설정한 되 면 CDN 로깅에 대 한 hello CoreAnalytics 상자도 확인 해야 합니다.

6. 원하는 대로 tooyour 내용이 없으면 클릭 hello **저장** hello hello 구성 대화 상자 위쪽에 단추입니다.

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/10_Save-me.png)

    hello **저장** 단추는 더 이상 활성 및 해당 hello/끄기 단추는 이제 ON, 하지만 자주색 아닌 파란색입니다.

7. 새 OMS 작업 영역 toosee을 원하는 경우 이동 tooyour Azure 포털의 대시보드를 hello 로그 분석 작업 영역 이름을 클릭 합니다. 작업 영역을 다음 표시 됩니다 (있는지 OMS 작업 영역 hello 왼쪽에 강조 표시 되어 있는지 확인). Hello OMS 포털 타일 toosee hello OMS 리포지토리에 작업 영역 클릭 합니다. 

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    OMS 리포지토리는 준비 toolog 데이터. 순서로 tooconsume 해당 데이터를 사용 해야 합니다는 [OMS 솔루션](#consuming-oms-log-analytics-data),이 문서의 뒷부분에 포함 합니다.

로그 데이터 지연에 대한 자세한 내용은 [여기](#log-data-delays)로 이동하세요.

## <a name="enable-logging-with-powershell"></a>PowerShell을 통해 로깅을 사용하도록 설정

다음은 방법을 통해 tooenable 및 get 진단 로그 hello Azure PowerShell Cmdlet의 예입니다.

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a>저장소 계정에서 진단 로그 사용

먼저 로그인하고 구독을 선택합니다.

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


tooEnable 진단 로그는 저장소 계정에이 명령을 사용 합니다.

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
tooEnable 진단 로그는 OMS 작업 영역에서에이 명령을 사용 합니다.

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a>Azure Storage에서 진단 로그 사용
이 섹션에서는 hello CDN 코어 분석의 hello 스키마 설명, 샘플 코드 toodownload hello tooa CSV 파일의 로그는 Azure 저장소 계정 내에서 구성 된 이러한 및 제공 하는 방법입니다.

### <a name="using-microsoft-azure-storage-explorer"></a>Microsoft Azure Storage 탐색기 사용
Hello Azure 저장소 계정에서에서 hello 코어 분석 데이터에 액세스 하기 전에 먼저 저장소 계정에 도구 tooaccess hello 내용을 해야 합니다. Hello 시장에서 사용할 수 있는 여러 도구가 있습니다, hello Microsoft Azure 저장소 탐색기는 hello 하나 것이 좋습니다. Hello 도구를 다운로드할 수 [여기](http://storageexplorer.com/)합니다. Hello 소프트웨어 다운로드 및 설치 구성 후 toouse hello 대상 toohello CDN 진단 로그로 구성 된 동일한 Azure 저장소 계정입니다.

1.  **Microsoft Azure Storage 탐색기**를 엽니다.
2.  Hello 저장소 계정 찾기
3.  Toohello 이동 **"Blob 컨테이너"** 노드 아래의이 저장소 계정 및 hello 노드 확장
4.  라는 선택 hello 컨테이너 **"insights 로그 coreanalytics"** 두 번 클릭 하 고
5.  표시 위로 hello 오른쪽 창에서 hello로 먼저 시작 수준으로 다음과 같은 결과 **"resourceId ="**합니다. 계속 hello 파일 표시 될 때까지 모든 hello 방법을 클릭 **PT1H.json**합니다. Hello 다음 hello 경로 대 한 설명에 대 한 참고를 참조 하십시오.
6.  각 blob **PT1H.json** 나타내는 특정 CDN 끝점 또는 해당 사용자 지정 도메인에 대 한 시간에 대 한 분석 로그 hello 합니다.
7.  이 JSON 파일의 hello 내용의 hello 스키마 hello 코어 분석 로그의 hello 섹션 스키마에서 설명


> [!NOTE]
> **Blob 경로 형식**
> 
> 핵심 분석 로그에는 1시간마다 생성됩니다. 1시간 동안의 모든 데이터는 수집된 후 단일 Azure Blob 내에 JSON 페이로드로 저장됩니다. hello 경로 toothis Azure Blob는 계층 구조 처럼 나타납니다. Hello 저장소 탐색기 도구 해석 하기 때문에 '/'를 디렉터리 구분 기호로 이므로 편의 위해 hello 계층을 보여 줍니다. 실제로, 전체 경로 hello hello blob 이름을 나타냅니다. 이 hello blob의 이름은 hello 명명 규칙 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

**필드 설명:**

|값|description|
|-------|---------|
|구독 ID    |Azure 구독 hello의 ID입니다. Hello Guid 형식입니다.|
|리소스 |그룹 이름 hello 리소스 그룹 toowhich hello CDN 리소스의 이름에 속해 있습니다.|
|프로필 이름 |Hello CDN 프로필의 이름|
|끝점 이름 |Hello CDN 끝점의 이름|
|Year|  예를 들어 2017 hello 연도의 4 자릿수로 표시|
|월| hello 월 수의 2 자리 표현입니다. 01=1월 ... 12=12월|
|일|   hello hello 월간 일자 2 자릿수로 표시|
|PT1H.json| Hello 분석 데이터가 저장 되는 실제 JSON 파일|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a>Hello 코어 분석 데이터 tooa CSV 파일로 내보내기

toomake 쉽게 tooaccess hello 코어 분석을 제공 하는 it tooeasily 사용된 될 수 있는 쉼표로 구분 된 플랫 파일 형식으로 hello JSON 파일을 다운로드할 수 있는 도구에 대 한 샘플 코드 차트 또는 다른 집계를 만듭니다.

Hello 도구를 사용 하는 방법을 다음과 같습니다.

1.  Hello github 링크를 방문: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )
2.  Hello 코드 다운로드
3.  Toocompile 지침에 따라 및 구성
4.  Hello 도구 실행
5.  결과 CSV 파일 간단한 플랫 계층의 hello 분석 데이터를 표시 합니다.

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a>OMS Log Analytics 리포지토리에서 진단 로그 사용
로그 분석은에 OMS Operations Management Suite ()의 가용성과 성능을 클라우드 및 온-프레미스 환경 toomaintain 프로그램을 모니터링 하는 서비스입니다. 여러 소스에서 리소스를 클라우드 및 온-프레미스 환경에서와 다른 모니터링 도구 tooprovide 분석에 의해 생성 된 데이터를 수집 합니다. 

toouse 로그 분석을 수행 해야 [로깅을 사용 하도록 설정](#enable-logging-with-azure-storage) toohello Azure OMS 로그 분석 저장소가이 문서의 앞부분에서 설명 합니다.

### <a name="using-hello-oms-repository"></a>OMS 리포지토리에 hello를 사용 하 여

 다이어그램을 다음 hello hello 입력의 hello 아키텍처 및 hello 저장소의 출력을 보여 줍니다.

![OMS Log Analytics 리포지토리](./media/cdn-diagnostics-log/12_Repo-overview.png)

*그림 3 - Log Analytics 리포지토리*

관리 솔루션을 사용 하 여 여러 가지 방법으로 hello 데이터를 표시할 수 있습니다. Hello에서 관리 솔루션을 가져올 수 있습니다 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions)합니다.

Hello를 클릭 하 여 Azure marketplace의 관리 솔루션을 설치할 수 있습니다 **지금 사용해 보세요** 각 솔루션의 hello 맨 아래에 링크 합니다.

### <a name="adding-an-oms-cdn-management-solution"></a>OMS CDN 관리 솔루션 추가

이러한 단계 tooadd 관리 솔루션을 수행 합니다.

1.   아직 그렇게 수행 하지 않은, toohello Azure 구독을 사용 하 여 Azure 포털 로그인을 tooyour 대시보드를 이동 합니다.
    ![Azure 대시보드](./media/cdn-diagnostics-log/13_Azure-dashboard.png)

2. Hello에 **새로** 아래 블레이드 **마켓플레이스**선택, **모니터링 + 관리**합니다.

    ![마켓플레이스](./media/cdn-diagnostics-log/14_Marketplace.png)

3. Hello에 **모니터링 + 관리** 블레이드에서 클릭 **스크롤하게**합니다.

    ![모두 표시](./media/cdn-diagnostics-log/15_See-all.png)

4.  Hello 검색 상자에 CDN에 대 한 검색입니다.

    ![모두 표시](./media/cdn-diagnostics-log/16_Search-for.png)

5.  **Azure CDN 핵심 분석**을 선택합니다. 

    ![모두 표시](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  클릭 한 후 **만들기**, 됩니다 toocreate 새로운 OMS 작업 영역을 요청 하거나 기존 집합을 사용 합니다. 

    ![모두 표시](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  전에 만든 hello 작업 영역을 선택 합니다. 다음 자동화 계정을 tooadd를 해야합니다.

    ![모두 표시](./media/cdn-diagnostics-log/19_Add-automation.png)

8. hello 다음 화면 표시를 작성 해야 하는 hello 자동화 계정 폼 됩니다. 

    ![모두 표시](./media/cdn-diagnostics-log/20_Automation.png)

9. 준비 tooadd는 hello 자동화 계정을 만든 후 솔루션입니다. Hello 클릭 **만들기** 단추입니다.

    ![모두 표시](./media/cdn-diagnostics-log/21_Ready.png)

10. 솔루션에 이제 tooyour 작업 영역을 추가 되었습니다. Azure 포털의 대시보드 tooyour를 돌아갑니다.

    ![모두 표시](./media/cdn-diagnostics-log/22_Dashboard.png)

    Toogo tooyour 작업 영역을 만든 hello 로그 분석 작업 영역을 클릭 합니다. 

11. Hello 클릭 **OMS 포털** toosee hello OMS 포털에서 새 솔루션 타일입니다.

    ![모두 표시](./media/cdn-diagnostics-log/23_workspace.png)

12. OMS 포털은 이제 다음 화면 hello 같습니다.

    ![모두 표시](./media/cdn-diagnostics-log/24_OMS-solution.png)

    중 하나를 클릭 hello 타일 toosee 여러 뷰 데이터에 있습니다.

    ![모두 표시](./media/cdn-diagnostics-log/25_Interior-view.png)

    왼쪽 스크롤할 수 또는 오른쪽 toosee 추가로 hello 데이터로 개별 보기를 나타내는 배열입니다. 

    Hello 타일 중 하나를 클릭 하 여 데이터에 대 한 자세한 내용은 제공 합니다.

     ![모두 표시](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a>제품 및 가격 책정 계층

[여기](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)에서 OMS 관리 솔루션에 대한 제품 및 가격 책정 계층을 볼 수 있습니다.

### <a name="customizing-views"></a>뷰 사용자 지정

Hello 보기 hello를 사용 하 여 데이터를 사용자 지정할 수 **뷰 디자이너**합니다. Tooyour OMS 작업 영역을 이동 하 고 hello를 클릭 하 여 설계를 시작 **뷰 디자이너** 바둑판식으로 배열입니다.

![뷰 디자이너](./media/cdn-diagnostics-log/27_Designer.png)

있습니다 수 끌어서의 차트 종류 hello 왼쪽에서 놓은 tooanalyze hello 왼쪽에 원하는 hello 데이터 세부 정보를 입력 합니다.

![뷰 디자이너](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a>로그 데이터 지연

Verizon 로그 데이터 지연 | Akamai 로그 데이터 지연
--- | ---
Verizon 로그 데이터가 1 시간 지연 되 고 too2 시간 toostart 끝점 전파가 완료 된 후 표시를 수행 합니다. | Akamai 로그 데이터는 지연 24 시간 및 24 시간 넘게 만들어진 경우 나타나는 too2 시간 toostart 차지 하지 않습니다. 최근에 만든 경우 hello 로그 toostart 표시에 대 한 too25 시간이 걸릴 수 있습니다.

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a>CDN 핵심 분석에 대한 진단 로그 유형

현재 HTTP 응답 통계 및 hello CDN Pop/가장자리에서에서 본 송신 통계를 표시 하는 메트릭을 포함 하는 핵심 분석 로그만을 제공 합니다.

### <a name="core-analytics-metrics-details"></a>핵심 분석 메트릭 정보
다음 표에서 hello hello 코어 분석 로그에서 사용할 수 있는 메트릭 목록을 보여 줍니다. 모든 공급자의 모든 메트릭을 사용할 수 있는 것은 아니지만 이러한 차이는 미미합니다. 다음 표도 hello 지정된 된 메트릭이 공급자에서 사용할 수 있는지를 보여 줍니다. 때문에 해당 CDN 끝점에 트래픽을 있는 사용할 수 있는 hello 메트릭이 note 하십시오.


|메트릭                     | 설명   | Verizon  | Akamai 
|---------------------------|---------------|---|---|
| RequestCountTotal         |이 기간 동안의 요청 적중의 총 수| 예  |예   |
| RequestCountHttpStatus2xx |2xx HTTP 코드(예: 200, 202)를 생성한 모든 요청의 수              | 예  |예   |
| RequestCountHttpStatus3xx | 3xx HTTP 코드(예: 300, 302)를 생성한 모든 요청의 수              | 예  |예   |
| RequestCountHttpStatus4xx |4xx HTTP 코드(예: 400, 404)를 생성한 모든 요청의 수               | 예   |예   |
| RequestCountHttpStatus5xx | 5xx HTTP 코드(예: 500, 504)를 생성한 모든 요청의 수              | 예  |예   |
| RequestCountHttpStatusOthers |  다른 모든 HTTP 코드의 수(2xx-5xx 이외) | 예  |예   |
| RequestCountHttpStatus200 | 200 HTTP 코드 응답을 생성한 모든 요청의 수              |아니요   |예   |
| RequestCountHttpStatus206 | 206 HTTP 코드 응답을 생성한 모든 요청의 수              |아니요   |예   |
| RequestCountHttpStatus302 | 302 HTTP 코드 응답을 생성한 모든 요청의 수              |아니요   |예   |
| RequestCountHttpStatus304 |  304 HTTP 코드 응답을 생성한 모든 요청의 수             |아니요   |예   |
| RequestCountHttpStatus404 | 404 HTTP 코드 응답을 생성한 모든 요청의 수              |아니요   |예   |
| RequestCountCacheHit |캐시 적중을 발생한 모든 요청의 수. 이 hello 자산 hello POP toohello 클라이언트에서 직접 처리 된 것을 의미 합니다.               | 예  |아니요   |
| RequestCountCacheMiss | 캐시 누락을 발생한 모든 요청의 수. 즉 hello 자산 hello POP 가장 가까운 toohello 클라이언트에서 찾을 수 없습니다 하며 따라서 hello 원본에서에서 검색 되었습니다.              |예   | 아니요  |
| RequestCountCacheNoCache | 모든의 개수를 hello 가장자리에 tooa 사용자 구성 인해 캐시에 저장할 수 없습니다 tooan 자산을 요청 합니다.              |예   | 아니요  |
| RequestCountCacheUncacheable | 모든의 개수를 hello 자산의 캐시 제어 하 여 캐시에 저장할 수 없습니다 tooassets를 요청 하 고 있는지 것 캐시 되어서는 안 POP 또는 hello HTTP 클라이언트에서 표시 하는 헤더가 만료                |예   |아니요   |
| RequestCountCacheOthers | 위에 포함되지 않는 캐시 상태를 갖는 모든 요청의 수              |예   | 아니요  |
| EgressTotal | 아웃바운드 데이터 전송(GB)              |예   |예   |
| EgressHttpStatus2xx | 2xx HTTP 상태 코드를 나타내는 응답에 대한 아웃바운드 데이터 전송*(GB)            |예   |아니요   |
| EgressHttpStatus3xx | 3xx HTTP 상태 코드를 나타내는 응답에 대한 아웃바운드 데이터 전송(GB)              |예   |아니요   |
| EgressHttpStatus4xx | 4xx HTTP 상태 코드를 나타내는 응답에 대한 아웃바운드 데이터 전송(GB)               |예   | 아니요  |
| EgressHttpStatus5xx | 5xx HTTP 상태 코드를 나타내는 응답에 대한 아웃바운드 데이터 전송(GB)               |예   |  아니요 |
| EgressHttpStatusOthers | 다른 HTTP 상태 코드를 나타내는 응답에 대한 아웃바운드 데이터 전송(GB)                |예   |아니요   |
| EgressCacheHit |  아웃 바운드 데이터 전송 전송 된 응답에 대 한 hello CDN 캐시에서 직접의 hello CDN Pop/가장자리  |예   |  아니요 |
| EgressCacheMiss | 가장 근접 한 POP 서버 hello에서 발견 되 고 hello 원본 서버에서 검색 된 응답에 대 한 아웃 바운드 데이터 전송              |예   |  아니요 |
| EgressCacheNoCache | hello 가장자리에 tooa 사용자 구성 인해 캐시에 저장할 수 없는 자산에 대 한 아웃 바운드 데이터 전송 합니다.                |예   |아니요   |
| EgressCacheUncacheable | hello 자산의 캐시 제어 및/또는 Expires 헤더는 해당 캐시 되어서는 안 POP에 또는 hello HTTP 클라이언트를 나타내는 캐시에 저장할 수 없는 자산에 대 한 아웃 바운드 데이터 전송                    |예   | 아니요  |
| EgressCacheOthers |  다른 캐시 시나리오에 대한 아웃바운드 데이터 전송             |예   | 아니요  |

* 아웃 바운드 데이터 전송 참조 tootraffic CDN POP 서버 toohello 클라이언트에서 전달 합니다.


### <a name="schema-of-hello-core-analytics-logs"></a>Hello 코어 분석 로그의 스키마 

모든 로그는 JSON 형식에 저장 하 고 각 항목에 아래의 스키마 hello 다음 문자열 필드:

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

여기서 hello 'time를' hello 통계 보고 hello 시간 경계의 hello 시작 시간을 나타냅니다. CDN 공급자가 메트릭을 지원하지 않을 경우 double 또는 정수 값 대신 null 값이 사용됩니다. Null 값이 메트릭 hello 없음을 나타내고 0은 다릅니다. 이러한 메트릭 hello 끝점에서 구성 된 도메인당 하나의 집합 생깁니다 참고도 합니다.

예제 속성은 다음과 같습니다.

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a>추가 리소스

* [Azure 진단 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [Azure CDN 보조 포털을 통한 핵심 분석](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [Azure OMS Log Analytics](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [Azure Log Analytics REST API](https://docs.microsoft.com/en-us/rest/api/loganalytics)







