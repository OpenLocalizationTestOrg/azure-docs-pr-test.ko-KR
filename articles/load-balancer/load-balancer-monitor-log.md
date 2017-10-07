---
title: "aaaMonitor 작업, 이벤트 및 부하 분산 장치에 대 한 카운터 | Microsoft Docs"
description: "Tooenable 이벤트, 경고 하 고 Azure 부하 분산 장치에 대 한 상태 로깅 상태를 검색 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a>Azure 부하 분산 장치에 대한 로그 분석

Azure toomanage에 서로 다른 유형의 로그를 사용할 수 있으며 부하 분산 장치 문제 해결. 일부이 로그 hello 포털을 통해 액세스할 수 있습니다. Azure Blob Storage에서 모든 로그를 추출하고 다양한 도구(예: Excel 및 PowerBI)에서 볼 수 있습니다. Hello 다른 유형의 로그 hello 목록 아래에서 자세히 알아볼 수 있습니다.

* **감사 로그:** 사용할 수 있습니다 [Azure 감사 로그](../monitoring-and-diagnostics/insights-debugging-with-events.md) (이전의 작업 로그) tooview 제출 된 tooyour Azure 구독 및 해당 상태는 모든 작업. 감사 로그는 기본적으로 설정 되어 있고 hello Azure 포털에서에서 볼 수 있습니다.
* **경고 이벤트 로그:** 이 로그 tooview 경고 rasied hello 부하 분산 장치에서 사용할 수 있습니다. hello 부하 분산 장치에 대 한 hello 상태는 5 분 마다 수집 됩니다. 이 로그는 부하 분산 장치 경고 이벤트가 발생하는 경우에만 기록됩니다.
* **상태 프로브 로그:** hello 상태 프로브 오류 때문에 hello 부하 분산 장치에서 요청을 받지 않는 경우 백 엔드 풀 인스턴스 수와 같은 프로그램 상태 프로브 검색 한이 로그 tooview 문제를 사용할 수 있습니다. 이 로그 toowhen 쓰여집니다 hello 상태 프로브 변경 합니다.

> [!IMPORTANT]
> 로그 분석은 현재 인터넷 연결 부하 분산 장치에 대해서만 작동합니다. 로그는 hello 리소스 관리자 배포 모델에서 배포 된 리소스 수만 있습니다. Hello 클래식 배포 모델의 리소스에 대 한 로그를 사용할 수 없습니다. Hello 배포 모델에 대 한 자세한 내용은 참조 [이해 리소스 관리자 배포 및 클래식 배포](../azure-resource-manager/resource-manager-deployment-model.md)합니다.

## <a name="enable-logging"></a>로깅 사용

감사 로깅은 모든 Resource Manager 리소스에 대해 사용하도록 설정됩니다. Tooenable 이벤트 및 이러한 로그를 통해 사용할 수 있는 hello 데이터 수집 상태 프로브 로깅 toostart 필요. 다음 단계 tooenable 로깅 hello를 사용 합니다.

로그인 toohello [Azure 포털](http://portal.azure.com)합니다. 부하 분산 장치가 아직 없으면, 계속하기 전에 [부하 분산 장치를 만듭니다](load-balancer-get-started-internet-arm-ps.md) .

1. Hello 포털에서 클릭 **찾아보기**합니다.
2. **부하 분산 장치**를 선택합니다.

    ![포털 - 부하 분산 장치](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. 기존 부하 분산 장치 >> **모든 설정**을 선택합니다.
4. Hello 오른쪽에 hello 이름 hello 부하 분산 장치 아래에 hello 대화 상자를 스크롤하여 너무**모니터링**, 클릭 **진단**합니다.

    ![포털 - 부하 분산 장치-설정](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. Hello에 **진단** 창 아래에서 **상태**선택, **에**합니다.
6. **저장소 계정**을 클릭합니다.
7. **로그** 아래에서 기존 저장소 계정을 선택하거나 새 저장소 계정을 만듭니다. 사용 하 여 hello 슬라이더 toodetermine 기간 (일) 동안의 이벤트 데이터는 hello 이벤트 로그에 저장 됩니다. 
8. **Save**를 클릭합니다.

    ![포털 - 진단 로그](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> 감사 로그에는 별도의 저장소 계정이 필요하지 않습니다. 사용 하 여 hello 이벤트 및 상태에 대 한 저장소의 프로브 로깅 요금을 부과할 서비스입니다.

## <a name="audit-log"></a>감사 로그

hello 감사 로그는 기본적으로 생성 됩니다. hello 로그는 90 일 동안 Azure의 이벤트 로그 저장소에 유지 됩니다. 에 대 한 자세한이 로그 hello 읽어 [ग द ृ 및 감사 로그](../monitoring-and-diagnostics/insights-debugging-with-events.md) 문서.

## <a name="alert-event-log"></a>경고 이벤트 로그

이 로그는 부하 분산 장치별로 설정한 경우에만 생성됩니다. hello 이벤트는 JSON 형식에 기록 하 고 hello 로깅을 사용 하는 경우 지정한 hello 저장소 계정에 저장 됩니다. hello 다음은 이벤트의 예입니다.

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

hello JSON 출력 표시 hello *eventname* hello 부하 분산 장치에 대 한 hello 이유를 설명 하는 속성 경고를 생성 합니다. 이 경우 생성 된 hello 경고 tooTCP 포트 소모 원본 IP NAT 제한에 의해 발생 한 (SNAT) 때문 이었습니다.

## <a name="health-probe-log"></a>상태 프로브 로그

이 로그는 위에서 설명한 대로 부하 분산 장치별로 설정한 경우에만 생성됩니다. hello 데이터 hello 로깅을 사용 하는 경우 지정한 hello 저장소 계정에 저장 됩니다. ' Insights 로그 loadbalancerprobehealthstatus' 라는 컨테이너 만들어지고 hello 같은 데이터가 기록 됩니다.

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

hello JSON 출력 hello 속성 필드 hello 기본에 대 한 정보 hello 프로브 상태에에서 표시 됩니다. hello *dipDownCount* 속성이 hello 백 엔드 toofailed 프로브 응답 인해 네트워크 트래픽을 수신 하지는 hello 총 인스턴스 수가 표시 됩니다.

## <a name="view-and-analyze-hello-audit-log"></a>보기 및 hello 감사 로그를 분석 합니다.

보고 하 고 hello 메서드를 다음 중 하나를 사용 하 여 감사 로그 데이터를 분석할 수 있습니다.

* **Azure 도구:** hello Azure preview 포털 또는 Azure PowerShell을 hello Azure 명령줄 인터페이스 (CLI) hello Azure REST API를 통해 hello 감사 로그에서 정보를 검색 합니다. 각 방법에 대 한 단계별 지침 hello에 자세히 설명 되어 [리소스 관리자와 작업을 감사](../azure-resource-manager/resource-group-audit.md) 문서.
* **Power BI:** [Power BI](https://powerbi.microsoft.com/pricing) 계정이 아직 없는 경우 무료로 사용해볼 수 있습니다. Hello를 사용 하 여 [Power BI 용 Azure Audit Logs 콘텐츠 팩](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), 미리 구성 된 대시보드를 사용 하 여 데이터를 분석할 수 있습니다 또는 요구 사항를 뷰 toosuit에 사용자 지정 합니다.

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a>보기 및 상태 프로브 hello와 이벤트 로그를 분석 합니다.

Tooconnect tooyour 저장소가 필요한 계정 및 이벤트 및 상태 프로브 로그에 대 한 hello JSON 로그 항목을 검색 합니다. Hello JSON 파일을 다운로드 한 후 Excel, PowerBI, 또는 기타 데이터 시각화 도구 뷰와 tooCSV 변환할 수 있습니다.

> [!TIP]
> Visual Studio 및 C#의 변수 및 상수에 대 한 값 변경의 기본 개념에 잘 알고 있다면 hello를 사용할 수 있습니다 [변환기 도구 로그](https://github.com/Azure-Samples/networking-dotnet-log-converter) GitHub에서 사용할 수 있습니다.

## <a name="additional-resources"></a>추가 리소스

* [Power BI를 사용하여 Azure 감사 로그 시각화](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) 블로그 게시물.
* [Power BI 등에서 Azure 감사 로그 보기 및 분석](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) 블로그 게시물.

## <a name="next-steps"></a>다음 단계

[부하 분산 장치 프로브 이해](load-balancer-custom-probe-overview.md)
