---
title: "Microsoft Azure에서 메트릭 aaaOverview | Microsoft Docs"
description: "Microsoft Azure의 메트릭 개요 및 사용"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 405ec51c-0946-4ec9-b535-60f65c4a5bd1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: johnkem
ms.openlocfilehash: 2b97f51e0554dae95a929241ae1f0e25e5c215ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Microsoft Azure의 메트릭 개요
이 문서에서는 Microsoft azure에서 이점 이란 메트릭 설명 방법과 toostart 사용 합니다.  

## <a name="what-are-metrics"></a>메트릭이 무엇인가요?
Azure 모니터 hello 성능 및 Azure에서 작업의 상태에 대 한 tooconsume 원격 분석 toogain 가시성이 있습니다. Azure 원격 분석 데이터의 가장 중요 한 형식은 hello에는 대부분의 Azure 리소스에서 내보내는 hello 메트릭 (성능 카운터)입니다. 여러 가지 방법으로 tooconfigure 제공 하 고 모니터링 및 문제 해결에 대 한 이러한 메트릭을 사용 하는 azure 모니터 합니다.

## <a name="what-can-you-do-with-metrics"></a>메트릭으로 무엇을 할 수 있나요?
메트릭 원격 분석의 중요 한 소스로 및 toodo hello 다음 작업을 사용 하면:

* **Hello 성능을 추적** 포털 차트에서 해당 메트릭이 그래프에 표시 및 해당 차트 tooa 대시보드에 고정 하 여 리소스 (예: VM, 웹 사이트 또는 논리 앱).
* **문제의 알림** 된 메트릭이 특정 임계값을 초과할 때 영향을 미치는 리소스의 성능을 hello 하 합니다.
* 메트릭이 특정 임계값을 초과할 때 리소스 자동 크기 조정 또는 runbook 실행 등과 같은 **자동화된 작업을 구성합니다**.
* 리소스의 성능 또는 사용 추세에 대한 **고급 분석**이나 보고를 수행합니다.
* **보관** 리소스의 성능 또는 상태 기록을 hello **규정 준수 또는 감사에 대 한** 목적으로 합니다.

## <a name="what-are-hello-characteristics-of-metrics"></a>메트릭 hello 특성은 무엇입니까?
메트릭 hello 특성 뒤에

* 모든 메트릭은 **1분 빈도**입니다. 메트릭 값을 1 분 마다에서 받게 리소스를 거의 hello 상태와 리소스의 상태에 대 한 실시간 가시성을 제공 합니다.
* 메트릭은 **즉시 사용할 수 있습니다**. Tooopt에 필요 하지 않거나 추가 진단을 설정 합니다.
* 각 메트릭에 대해 **30일 동안의 기록** 에 액세스할 수 있습니다. Hello 최근 및 월별 추세 hello 성능이 나 리소스의 상태를 신속 하 게 볼 수 있습니다.

또한 다음을 수행할 수 있습니다.

* 메트릭을 구성 **걸리거나 알림을 전송 하는 규칙 작업을 자동화 하는 경고** hello 메트릭을 설정 된 hello 임계값을 교차 하는 경우. 자동 크기 조정 tooscale 리소스 toomeet 들어오는 요청을 사용 하거나 웹 사이트 또는 컴퓨팅 리소스를 로드 하는 특별 한 자동화 된 작업이 됩니다. 자동 크기 조정 설정 규칙 tooscale 또는 축소 임계값을 교차 하는 메트릭을에 따라 구성할 수 있습니다.

* **경로** 모든 메트릭 Application Insights 또는 로그 분석 (OMS) tooenable 즉시 분석, 검색 및 사용자 지정 리소스의 메트릭 데이터에 대해 경고 합니다. 메트릭 tooan 이벤트 허브를 스트리밍할 수도, 수 있게 해 주는 toothen 라우팅하 tooAzure Stream Analytics 또는 거의 실시간으로 분석을 위해 toocustom 앱입니다. 진단 설정을 사용하여 Event Hub 스트리밍을 설정합니다.

* **메트릭 toostorage 보관** 더 긴 보존에 대 한 오프 라인 보고에 사용 합니다. 리소스에 대 한 진단 설정을 구성할 때 프로그램 메트릭 tooAzure Blob 저장소를 라우팅할 수 있습니다.

* 에 액세스를 쉽게 검색 하 고 **모든 메트릭을 표시** hello 리소스를 선택 하 고 차트에 메트릭을 hello 그릴 경우 Azure 포털을 통해.

* **사용할** hello 메트릭을 통해 hello 새로운 Azure 모니터 REST Api입니다.

* **쿼리** 메트릭을 사용 하 여 hello PowerShell cmdlet 또는 플랫폼 간 REST API를 환영 합니다.

  ![Azure Monitor의 메트릭 라우팅](./media/monitoring-overview-metrics/Metrics_Overview_v4.png)

## <a name="access-metrics-via-hello-portal"></a>Hello 포털을 통해 메트릭 액세스
다음은 어떻게 toocreate 메트릭 차트를 사용 하 여 hello Azure 포털의 빠른 연습입니다.

### <a name="tooview-metrics-after-creating-a-resource"></a>리소스를 만든 후 tooview 메트릭
1. Azure 포털 hello를 엽니다.
2. Azure App Service 웹 사이트를 만듭니다.
3. 웹 사이트를 만든 후 이동 toohello **개요** hello 웹 사이트의 블레이드입니다.
4. **모니터링** 타일로 새 메트릭을 볼 수 있습니다. 그런 다음 hello 타일을 편집 하 고 개의 추가 메트릭 선택 수 있습니다.

   ![Azure Monitor의 리소스에 대한 메트릭](./media/monitoring-overview-metrics/MetricsOverview1.png)

### <a name="tooaccess-all-metrics-in-a-single-place"></a>tooaccess을 한 곳에서 모든 메트릭
1. Azure 포털 hello를 엽니다.
2. 새 toohello 이동 **모니터** 탭을 클릭 한 다음 선택한 hello **메트릭** 아래에 있는 옵션입니다.
3. 구독, 리소스 그룹 및 hello 리소스의 hello 이름 hello 드롭 다운 목록에서 선택 합니다.
4. 보기 hello 사용 가능한 메트릭 목록입니다. 관심 있는 및 그리는 것 hello 메트릭을 선택 합니다.
5. Hello pin에 hello 오른쪽 위 모퉁이 클릭 하 여 toohello 대시보드 것 고정할 수 있습니다.

   ![Azure Monitor에서 모든 메트릭을 한 곳에서 액세스](./media/monitoring-overview-metrics/MetricsOverview2.png)

> [!NOTE]
> 추가적인 진단 설정 없이 VM(Azure Resource Manager 기반) 및 가상 컴퓨터 확장 집합에서 호스트 설정 메트릭에 액세스할 수 있습니다. 이러한 호스트 수준 메트릭은 Windows 및 Linux 인스턴스에서 사용할 수 있습니다. 이러한 메트릭은 toobe hello 또는 가상 컴퓨터 크기 집합 Vm에 Azure 진단에서 설정한 액세스 toowhen 있는 게스트 운영 체제 수준 메트릭와 혼동된 되지 않습니다. 진단 구성에 대 한 더 toolearn 참조 [란 Microsoft Azure 진단](../azure-diagnostics.md)합니다.
>
>

## <a name="access-metrics-via-hello-rest-api"></a>Hello REST API를 통해 메트릭 액세스
Azure 메트릭 hello Azure 모니터 Api를 통해 액세스할 수 있습니다. 메트릭 검색 및 액세스에 사용할 수 있는 2가지 API가 있습니다.

* 사용 하 여 hello [Azure 모니터 메트릭의 정의 REST API](https://msdn.microsoft.com/library/mt743621.aspx) tooaccess hello 서비스에 사용할 수 있는 메트릭 목록입니다.
* 사용 하 여 hello [Azure 모니터 메트릭 REST API](https://msdn.microsoft.com/library/mt743622.aspx) tooaccess hello 실제 메트릭 데이터입니다.

> [!NOTE]
> 이 문서에서는 hello 통해 hello 메트릭 [메트릭에 대 한 새로운 API](https://msdn.microsoft.com/library/dn931930.aspx) Azure 리소스에 대 한 합니다. hello 새 메트릭 정의 API에 대 한 hello API 버전은 2016-03-01 및 API 메트릭 hello 버전은 2016-09-01입니다. hello 레거시 메트릭 정 및 메트릭을 hello API 버전 2014-04-01로 액세스할 수 있습니다.
>
>

Hello Azure 모니터 REST Api를 사용 하 여 보다 자세한 연습을 참조 하십시오. [Azure 모니터 REST API 연습](monitoring-rest-api-walkthrough.md)합니다.

## <a name="export-metrics"></a>메트릭 내보내기
Toohello 이동할 수 있습니다 **진단 설정을** hello 아래 블레이드 **모니터** 메트릭에 대 한 탭 및 보기 hello 내보내기 옵션입니다. 이 문서의 toobe 라우팅된 tooBlob 저장소나 tooAzure 이벤트 허브 tooOMS 언급 된 사용 사례에 대 한 메트릭 (및 진단 로그)를 이전에 선택할 수 있습니다.

 ![Azure Monitor에서 메트릭에 대한 내보내기 옵션](./media/monitoring-overview-metrics/MetricsOverview3.png)

Resource Manager 템플릿, [PowerShell](insights-powershell-samples.md), [Azure CLI](insights-cli-samples.md) 또는 [REST APIs](https://msdn.microsoft.com/library/dn931943.aspx)를 통해 이 항목을 구성할 수 있습니다.

## <a name="take-action-on-metrics"></a>메트릭에 대한 작업
tooreceive 알림이나 메트릭 데이터에 대해 자동화 된 take 작업 경고 규칙 또는 자동 크기 조정 설정을 구성할 수 있습니다.

### <a name="configure-alert-rules"></a>경고 규칙 구성
메트릭에 대해 경고 규칙을 구성할 수 있습니다. 이러한 경고 규칙으로 메트릭이 특정 임계값을 초과했는지를 확인할 수 있습니다. 다음 전자 메일을 통해 알려 하거나 모든 사용자 지정 스크립트 사용된 toorun 일 수 있는 webhook 발생 수입니다. 또한 hello webhook tooconfigure 타사 제품 통합을 사용할 수 있습니다.

 ![Azure Monitor의 메트릭 및 경고 규칙](./media/monitoring-overview-metrics/MetricsOverview4.png)

### <a name="autoscale-your-azure-resources"></a>Azure 리소스에서 자동 크기 조정
일부 Azure 리소스의 크기 조정을 걸러 내 거 나에서 여러 인스턴스 toohandle 작업 hello를 지원 합니다. 자동 크기 조정 tooApp (웹 응용 프로그램) 서비스, 가상 컴퓨터 크기 집합 및 클래식 Azure 클라우드 서비스에 적용합니다. 작업에 영향을 주는 특정 메트릭을 지정 하는 임계값을 초과할 때 자동 크기 조정 규칙 tooscale 걸러 내 거 나에서 구성할 수 있습니다. 자세한 내용은 [자동 크기 조정 개요](monitoring-overview-autoscale.md)를 참조하세요.

 ![Azure Monitor의 메트릭 및 자동 크기 조정](./media/monitoring-overview-metrics/MetricsOverview5.png)

## <a name="learn-about-supported-services-and-metrics"></a>지원되는 서비스 및 메트릭에 대해 알아보기
Azure Monitor는 새로운 메트릭 인프라입니다. Azure 포털 및 hello 새 버전의 hello Azure 모니터 API hello에서 Azure 서비스를 수행 하는 hello를 지원 합니다.

* VM(Azure Resource Manager 기반)
* 가상 컴퓨터 확장 집합
* Batch
* Event Hubs 네임스페이스
* 서비스 버스 네임스페이스(프리미엄 SKU에만 해당)
* SQL Database(버전 12)
* 탄력적인 SQL 풀
* 웹 사이트
* 웹 서버 팜
* Logic Apps
* IoT Hub
* Redis 캐시
* 네트워킹: 응용 프로그램 게이트웨이
* 검색

모든 지원 되는 hello 서비스와 해당 메트릭을에서 자세한 목록을 볼 수 있습니다 [Azure 모니터 메트릭-리소스 유형 마다 지원 되는 메트릭](monitoring-supported-metrics.md)합니다.

## <a name="next-steps"></a>다음 단계
이 문서 전체에서 toohello 링크를 참조 하십시오. 또한 다음을 학습할 수 있습니다.  

* [자동 크기 조정에 대한 공통 메트릭](insights-autoscale-common-metrics.md)
* [어떻게 toocreate 경고 규칙](insights-alerts-portal.md)
* [Azure Storage에서 Log Analytics를 사용하여 로그 분석](../log-analytics/log-analytics-azure-storage.md)
