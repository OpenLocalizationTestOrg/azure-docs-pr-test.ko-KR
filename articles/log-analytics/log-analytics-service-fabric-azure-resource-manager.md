---
title: "로그 분석에 사용 하 여 서비스 패브릭 응용 프로그램 aaaAssess hello Azure 포털 | Microsoft Docs"
description: "Hello 서비스 패브릭 솔루션을 사용 하 여 hello Azure 포털 tooassess hello 위험 및 서비스 패브릭 응용 프로그램의 상태를 사용 하 여 로그 분석에서 마이크로 서비스, 노드 및 클러스터입니다."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a>서비스 패브릭 응용 프로그램 및 Azure 포털 hello로 마이크로 서비스를 평가 합니다.

> [!div class="op_single_selector"]
> * [리소스 관리자](log-analytics-service-fabric-azure-resource-manager.md)
> * [PowerShell](log-analytics-service-fabric.md)
>
>

![Service Fabric 기호](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

이 문서에서는 toouse hello 로그 분석 toohelp에서 서비스 패브릭 솔루션을 식별 하 고 서비스 패브릭 클러스터 전체에서 문제를 해결 하는 방법을 설명 합니다.

서비스 패브릭 솔루션 hello Azure WAD 테이블에서이 데이터를 수집 하 여 서비스 패브릭 Vm에서 Azure 진단 데이터를 사용 합니다. 그러면 Log Analytics에서는 **Reliable Service 이벤트**, **행위자 이벤트**, **작업 이벤트**, **사용자 지정 ETW 이벤트**를 포함한 Service Fabric 프레임워크 이벤트를 읽어옵니다. Hello 솔루션 대시보드를 함께 수 tooview 주목할 만한 문제 및 관련 이벤트 서비스 패브릭 환경입니다.

tooconnect 해야 tooget hello 솔루션 시작, 서비스 패브릭 클러스터 tooa 로그 분석 작업 영역입니다. 다음은 세 가지 시나리오 tooconsider가입니다.

1. 서비스 패브릭 클러스터를 배포 하지 않은 경우의 hello 단계를 사용 하 여 ***연결 된 서비스 패브릭 클러스터 tooa 로그 분석 작업 영역 배포*** toodeploy 새 클러스터 tooreport tooLog 분석 구성 했습니다.
2. 필요한 경우 toocollect ÷ ´ ֹ 호스트 toouse에서 보안과 같은 다른 OMS 솔루션 서비스 패브릭 클러스터를에서 다음과 같이 hello ***VM 확장과 연결 된 서비스 패브릭 클러스터 tooa 로그 분석 작업 영역 배포 설치합니다.***
3. 서비스 패브릭 클러스터를 이미 배포한 경우 및 tooconnect 원하는 것 tooLog 분석, hello 단계에 따라 ***기존 저장소 계정 tooLog 분석을 추가 합니다.***

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a>연결 된 서비스 패브릭 클러스터 tooa 로그 분석 작업 영역을 배포 합니다.
이 서식 파일은 다음 hello지 않습니다.

1. Azure 서비스 패브릭 클러스터를 이미 연결 되어 tooa 로그 분석 작업 영역을 배포합니다. Hello 옵션 toocreate는 새 작업 영역이 있는 hello 템플릿이나 입력된 hello 이름을 이미 기존 로그 분석 작업 영역을 배포 하는 동안 합니다.
2. Hello 진단 저장소 계정 toohello 로그 분석 작업 영역을 추가합니다.
3. 로그 분석 작업 영역에서 hello 서비스 패브릭 솔루션을 사용 하도록 설정 합니다.

[![TooAzure 배포](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)

선택 하 고 나면 hello 위의 단추를 배포, hello Azure 포털이 열리면 tooedit 있습니다에 대 한 매개 변수를 사용 합니다. 새 로그 분석 작업 영역 이름을 입력 하는 경우 있는지 toocreate 새 리소스 그룹을 수 있습니다:

![서비스 패브릭](./media/log-analytics-service-fabric/2.png)

![서비스 패브릭](./media/log-analytics-service-fabric/3.png)

Hello 약관에 동의 하 고 클릭 **만들기** toostart hello 배포 합니다. 새 작업 영역 hello 및 클러스터를 만든 참조 하 고 WADServiceFabric hello 해야 hello 배포가 완료 되 면 * 추가 된 이벤트, WADWindowsEventLogs 및 WADETWEvent 테이블:

![서비스 패브릭](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a>VM 확장 설치에 연결 된 서비스 패브릭 클러스터 tooa 로그 분석 작업 영역을 배포 합니다.

이 서식 파일은 다음 hello지 않습니다.

1. Azure 서비스 패브릭 클러스터를 이미 연결 되어 tooa 로그 분석 작업 영역을 배포합니다. 새 작업 영역을 만들거나 기존 작업 영역을 사용할 수 있습니다.
2. Hello 진단 저장소 계정 toohello 로그 분석 작업 영역을 추가합니다.
3. Hello 로그 분석 작업 영역에서 hello 서비스 패브릭 솔루션을 사용 하도록 설정 합니다.
4. 서비스 패브릭 클러스터에 설정 하는 각 가상 컴퓨터 크기에 hello MMA agent 확장을 설치 합니다. Hello MMA 에이전트를 설치, 해당 노드에 대 한 수 tooview 성능 메트릭이 됩니다.

[![TooAzure 배포](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)

다음 입력된 hello 필요한 매개 변수 위의 동일한 단계를 hello 및 배포를 시작 합니다. 다시 한 번 hello 새 작업 영역, 클러스터 및 생성된 된 모든 WAD 테이블 표시 됩니다.

![서비스 패브릭](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a>성능 데이터 보기

성능 데이터를 프로그램 노드에서 tooview:


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- Hello Azure 포털에서에서 hello 로그 분석 작업 영역을 시작 합니다.
  ![서비스 패브릭](./media/log-analytics-service-fabric/6.png)
- TooSettings hello 왼쪽된 창에서 이동 하 고 데이터 선택 >> Windows 성능 카운터 >> "추가 hello 선택한 성능 카운터": ![서비스 패브릭](./media/log-analytics-service-fabric/7.png)
- 로그 검색에 사용 하 여 hello 다음에 해당 노드에 대 한 주요 메트릭을 toodelve를 쿼리합니다.

    a. 비교의 노드를 문제가 있는 hello 마지막 1 시간 toosee 프로그램 모든 노드에서 평균 CPU 사용률 hello 했으며 어떤 시간 간격 노드 스파이크가:

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![서비스 패브릭](./media/log-analytics-service-fabric/10.png)

    b. 다음 쿼리로 각 노드에서 사용 가능한 메모리에 대한 비슷한 꺾은선형 차트를 확인합니다.

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    이 쿼리를 사용 하는 각 노드에 대 한 사용 가능한 공간 (mb)에 대 한 hello 정확한 평균 값을 표시 하면 모든 노드 목록이 tooview:

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![서비스 패브릭](./media/log-analytics-service-fabric/11.png)

    c. Hello 시간별 평균을 검사 하 여 특정 노드로 아래로 toodrill를 원하는 hello 경우 최소, 최대 및 75 백분위 수 CPU 사용 하는 수 toodo 하 여이이 쿼리 (대체 컴퓨터 필드)를 사용 하 여:

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![서비스 패브릭](./media/log-analytics-service-fabric/12.png)

Hello에 로그 분석에서 성능 메트릭에 대 한 자세한 내용을 살펴볼 [Operations Management Suite 블로그](https://blogs.technet.microsoft.com/msoms/tag/metrics/)합니다.


## <a name="adding-an-existing-storage-account-toolog-analytics"></a>기존 저장소 계정 tooLog 분석 추가

이 서식 파일에는 단순히 기존 저장소 계정을 tooa 새로운 또는 기존 로그 분석 작업 영역에 추가합니다.

[![TooAzure 배포](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)

> [!NOTE]
> 리소스 그룹 선택에 이미 기존 로그 분석 작업 영역을 사용 하는 경우 "기존 테이블 사용" 및 선택 hello 로그 분석 작업 영역을 포함 하는 hello 리소스 그룹에 대 한 검색 합니다. 그렇지 않은 경우 새 작업 영역을 만듭니다.
> ![서비스 패브릭](./media/log-analytics-service-fabric/8.png)
>
>

이 서식 파일을 배포한 후 수 toosee hello 저장소 계정 연결 tooyour 로그 분석 작업 영역 수 있습니다. 이 인스턴스에서 하나 이상의 저장소 계정 toohello Exchange 작업 영역 I 위에서 만든 추가 했습니다.
![서비스 패브릭](./media/log-analytics-service-fabric/9.png)

## <a name="view-service-fabric-events"></a>Service Fabric 이벤트 보기

Hello 배포 완료 되 면 hello 솔루션 서비스 패브릭 작업 영역에서 설정 되어 선택 hello **서비스 패브릭** hello 로그 분석 포털 toolaunch hello 서비스 패브릭 대시보드 타일입니다. hello 대시보드는 다음 표에 hello에 hello 열을 포함 합니다. 각 열 개수를 비교 하 hello에 대 한 열의 기준을 시간 범위를 지정 하 여 hello 상위 10 개의 이벤트를 나열 합니다. 클릭 하 여 hello 전체 목록을 제공 하는 로그 검색을 실행할 수 있습니다 **스크롤하게** 각 열의 또는 hello 열 머리글을 클릭 하 여 hello 오른쪽 아래에 있습니다.

| **Service Fabric 이벤트** | **description** |
| --- | --- |
| 주목할 만한 문제 |RunAsyncFailures RunAsynCancellations 및 노드 다운 같은 문제를 표시합니다. |
| 작업 이벤트 |응용 프로그램 업그레이드 및 배포와 같은 주목할 만한 작업 이벤트입니다. |
| Reliable Service 이벤트 |Runasyncinvocations와 같은 주목할 만한 Reliable Service 이벤트입니다. |
| 행위자 이벤트 |행위자 메서드, 행위자 활성화 및 비활성화 등에 의해 throw된 예외와 같은 마이크로 서비스에 의해 생성된 주목할 만한 행위자 이벤트입니다. |
| 응용 프로그램 이벤트 |응용 프로그램으로 생성된 모든 사용자 지정 ETW 이벤트입니다. |

![Service Fabric 대시보드](./media/log-analytics-service-fabric/sf3.png)

![Service Fabric 대시보드](./media/log-analytics-service-fabric/sf4.png)

hello 다음 표에서 데이터 수집 방법과 서비스 패브릭에 대 한 데이터 수집 방법에 대 한 기타 세부 정보.

| 플랫폼 | 직접 에이전트 | Operations Manager 에이전트 | Azure 저장소 | Operations Manager 필요 여부 | 관리 그룹을 통해 전송되는 Operations Manager 에이전트 데이터 | 수집 빈도 |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |  |  | &#8226; |  |  |10분 |

> [!NOTE]
> 클릭 하 여 hello 서비스 패브릭 솔루션에서에서 이러한 이벤트의 hello 범위를 변경할 수 **지난 7 일을 기준으로 데이터** hello hello 대시보드 위쪽에 있습니다. 6 시간 또는 1 일, 지난 7 일 hello 내에서 생성 된 이벤트를 표시할 수 있습니다. 선택할 수 있습니다 또는 **사용자 지정** toospecify 사용자 지정 날짜 범위입니다.
>
>

## <a name="next-steps"></a>다음 단계

* 사용 하 여 [로그 분석에서 로그 검색](log-analytics-log-searches.md) tooview 서비스 패브릭 이벤트 데이터를 자세히 설명 합니다.
