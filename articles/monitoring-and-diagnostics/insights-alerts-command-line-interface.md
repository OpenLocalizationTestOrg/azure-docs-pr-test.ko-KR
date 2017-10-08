---
title: "Azure 서비스-플랫폼 간 CLI에 대 한 경고 aaaCreate | Microsoft Docs"
description: "트리거 전자 메일 알림, 지정한 hello 조건에 해당할 때 자동화 또는 웹 사이트 Url (webhook)를 호출 합니다."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a>Azure 서비스에 대한 Azure Monitor에서 메트릭 경고 만들기 - 플랫폼 간 CLI
> [!div class="op_single_selector"]
> * [포털](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>개요
이 문서를 사용 하 여 Azure 메트릭 경고를 tooset 플랫폼 간 명령줄 인터페이스 (CLI) hello 하는 방법을 보여 줍니다.

> [!NOTE]
> Azure 모니터는 2016 년 9 월 25 일 때까지 "Azure Insights" 라고 불렀습니다 기능에 대 한 새 이름을 hello는입니다. 그러나 hello 네임 스페이스 및 아래의 hello 명령 insights"hello" 여전히 포함 합니다.
>
>

Azure 서비스 또는 Azure 서비스의 이벤트에 대한 모니터링 메트릭을 기반으로 경고를 받을 수 있습니다.

* **메트릭 값** -hello 트리거를 지정 된 메트릭 hello 값 두 방향에서 모두 할당 하는 임계값을 초과할 때 경고 합니다. 즉, 트리거합니다 둘 다 때 hello 조건이 충족 먼저 되 고 다음 나중에 조건 하는 더 이상 충족 합니다.    
* **활동 로그 이벤트** - *모든* 이벤트에 대해 또는 특정 이벤트가 발생했을 때만 경고를 트리거할 수 있습니다 활동 로그 경고에 대 한 자세한 toolearn [여기를 클릭](monitoring-activity-log-alerts.md)

메트릭 경고 toodo hello 다음 표시할 때 구성할 수 있습니다.

* 보낼 전자 메일 알림 toohello 서비스 관리자 및 공동 관리자
* 사용자가 지정한 tooadditional 메일 전자 메일을 보냅니다.
* webhook 호출
* (만 hello이 이번에는 Azure 포털)에서 Azure runbook의 실행 시작

다음을 통해 메트릭 경고 규칙에 대한 정보를 구성하고 가져올 수 있습니다.

* [Azure 포털](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [명령줄 인터페이스(CLI)](insights-alerts-command-line-interface.md)
* [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931945.aspx)

명령을 입력 하 여 명령에 대 한 도움말을 항상 받을 수 있습니다 및 배치-hello 끝에 있는 도움말입니다. 예:

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a>Hello CLI를 사용 하 여 경고 규칙 만들기
1. Hello 필수 구성 요소 및 로그인 tooAzure 수행 합니다. [Azure Monitor CLI 샘플](insights-cli-samples.md)을 참조하세요. 즉, hello CLI를 설치 하 고이 명령을 실행 합니다. 로그인 하기를 사용 하 고 준비 toorun Azure 모니터 명령을 어떤 구독이 표시 합니다.

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. 리소스 그룹에 대 한 toolist 기존 규칙 양식 다음 hello를 사용 하 여 **경고 규칙 목록 azure insights** *[옵션] &lt;리소스 그룹&gt;*

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. 규칙을 toocreate toohave 몇 가지 중요 한 정보가 필요 정보의 먼저 합니다.
  * hello **리소스 ID** hello 리소스에 대 한 원하는 tooset에 대 한 경고
  * hello **메트릭 정의** 해당 리소스에 대해 사용할 수 있는

     한 가지 방법은 tooget hello 리소스 ID는 toouse hello Azure 포털입니다. Hello 리소스를 이미 만든 경우 hello 포털에서 선택 합니다. 다음 hello 다음 블레이드를 선택 *속성* hello에서 *설정을* 섹션. hello *리소스 ID* hello 다음 블레이드에서 필드입니다. 또 다른 방법은 toouse hello [Azure 리소스 탐색기](https://resources.azure.com/)합니다.

     웹앱에 대한 예제 리소스 ID

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     tooget hello 사용 가능한 메트릭 및 hello 이전 리소스 예제에서는 다음 CLI 명령을 사용 하 여 hello에 대 한 이러한 메트릭에 대 한 단위 목록:  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     *PT1M* hello 세분성 hello 사용할 수 있는 측정 (1 분 간격으로)가 있습니다. 다른 세분성을 사용할 때는 다른 메트릭 옵션이 있습니다.
4. toocreate 메트릭을 기반 경고 규칙 hello 양식 뒤의 명령을 사용 합니다.

    **azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*

    경고를 설정 하는 예제 웹 사이트 리소스에 따라 번호입니다. hello 경고 트리거 일관 되 게 5 분에서 다시 5 분 동안 트래픽이 받는 경우에 대 한 모든 트래픽은 받을 때마다.

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. toocreate webhook 또는 송신 메일 메트릭 경고를 발생 시킨 경우에 먼저 hello 전자 메일 및/또는 webhook 만듭니다. Hello 규칙을 즉시 만들 나중에 있습니다. 연결할 수 없습니다 webhook 또는 포함 된 전자 메일 이미 hello CLI를 사용 하 여 규칙을 생성 합니다.

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. 개별 규칙을 살펴서 경고가 제대로 만들어졌는지 확인할 수 있습니다.

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. toodelete 규칙 hello 폼의 명령을 사용 합니다.

    **insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;

    이러한 명령은이 문서에서 이전에 만든 hello 규칙을 삭제 합니다.

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a>다음 단계
* [Azure 모니터링의 개요를 얻게](monitoring-overview.md) hello 형식의 정보를 수집 하 고 모니터링할 수 있습니다.
* [경고에서의 webhook 구성](insights-webhooks-alerts.md)에 대해 자세히 알아봅니다.
* [활동 로그 이벤트에 대한 경고 구성](monitoring-activity-log-alerts.md)에 대해 자세히 알아봅니다.
* [Azure Automation Runbook](../automation/automation-starting-a-runbook.md)에 대해 자세히 알아봅니다.
* 가져오기는 [진단 로그를 수집 하는 작업을 간략하게](monitoring-overview-of-diagnostic-logs.md) toocollect 고주파 메트릭 서비스에서 자세히 설명 합니다.
* 가져오기는 [메트릭 컬렉션의 개요](insights-how-to-customize-monitoring.md) toomake 서비스를 사용 가능 하 고 응답 합니다.
