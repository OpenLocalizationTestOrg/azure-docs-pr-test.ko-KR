---
title: "OMS와 함께 서비스 패브릭 이벤트 분석 aaaAzure | Microsoft Docs"
description: "Azure Service Fabric 클러스터의 모니터링 및 진단을 위해 OMS를 사용하여 이벤트를 시각화 및 분석하는 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 526519293e70982c95e31241465b87f190096f74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-oms"></a>OMS를 사용하여 이벤트 분석 및 시각화

Operations Management Suite (OMS)은 관리 서비스 모니터링 및 응용 프로그램에 대 한 진단을 도와주는 및 hello 클라우드에서 호스트 되는 서비스의 컬렉션입니다. OMS와 그 제공 하는 기능, 보다 자세한 개요 tooget 읽을 [OMS는 무엇입니까?](../operations-management-suite/operations-management-suite-overview.md)

## <a name="log-analytics-and-hello-oms-workspace"></a>로그 분석 및 hello OMS 작업 영역

Log Analytics는 Azure Storage 테이블이나 에이전트를 비롯한 관리 리소스에서 데이터를 수집하여 중앙 리포지토리에서 유지 관리합니다. hello 데이터 분석, 경고 및 시각화에 대 한 사용 하거나 더 이상 내보낼 수 있습니다. Log Analytics는 이벤트, 성능 데이터 또는 기타 사용자 지정 데이터를 지원합니다.

OMS를 구성 하는 경우 액세스 tooa 특정 것 *OMS 작업 영역*에서 데이터를 쿼리할 하거나 대시보드에 시각화 수 있는 합니다.

OMS에 여러 개의 로그 분석에서 데이터를 받으면 *관리 솔루션* 미리 솔루션 toomonitor 들어오는 데이터를 사용자 지정 된 tooseveral 시나리오는입니다. 여기에 *서비스 패브릭 분석* 솔루션 및 *컨테이너* 솔루션은 두 개의 가장 관련성이 높은 것 hello toodiagnostics 및 모니터링 서비스 패브릭 클러스터를 사용 하는 경우입니다. 여러 다른도으로 되 고 OMS hello에 대 한 자세한 내용은 사용자 지정 솔루션을 만들 수도 있습니다 [여기](../operations-management-suite/operations-management-suite-solutions.md)합니다. 클러스터는 hello에서 구성에 대 한 toouse를 선택 하는 각 솔루션 로그 분석와 함께 동일한 OMS 작업 영역입니다. 작업 영역 사용자 지정 대시보드 및 데이터를 시각화 하 고 수정 toohello 데이터가 toocollect, 처리 및 분석 합니다.

## <a name="setting-up-an-oms-workspace-with-hello-service-fabric-solution"></a>서비스 패브릭 솔루션 hello로 OMS 작업 영역 설정

유용한 대시보드를 제공 하므로 보여 주는 hello hello 플랫폼 및 응용 프로그램 수준 및 hello 수 tooquery 서비스 패브릭에서 들어오는 로그 채널을 다양 한 특정, OMS 작업 영역에서 hello 서비스 패브릭 솔루션을 포함 하는 것이 좋습니다. 기록합니다. Hello 클러스터에 배포 하는 단일 응용 프로그램 포함 비교적 간단한 서비스 패브릭 솔루션 모양은 다음과 같습니다.

![OMS SF 솔루션](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-solution.png)

두 가지 방법으로 tooprovision 하 고 OMS 작업 영역, 리소스 관리자 템플릿을 통해 또는 Azure Marketplace에서 직접 구성 합니다. 클러스터를 배포 하 고 hello 진단 유틸리티를 사용 하 여 배포 하는 클러스터에 이미 있는 경우 후자를 사용 하도록 설정 하는 경우에 hello 이전을 사용 합니다.

### <a name="deploying-oms-using-a-resource-management-template"></a>Resource Management 템플릿을 사용하여 OMS 배포

Hello 클러스터 만들기 단계에서 이런-리소스 관리자 템플릿, hello 서식 파일을 사용 하 여 클러스터 배포 새 OMS 작업 영역을 만들 수도 때 hello 서비스 패브릭 솔루션 tooit를 추가 하 고 hello 적절 한 저장소에서 tooread 데이터 구성 테이블입니다.

>[!NOTE]
>이 toowork에 대 한 진단에 hello Azure 저장소 테이블 tooexist OMS에 대 한 활성화 toobe /에서 로그 분석 tooread 정보입니다.

위의 작업을 수행하는 샘플 템플릿은 [여기](https://azure.microsoft.com/resources/templates/service-fabric-oms/)에 있으며 요구 사항에 따라 사용하고 수정할 수 있습니다. Hello 경우는 더 많은 옵션을 원하는 hello 프로세스에서 있습니다 수 있는 OMS 작업 영역 설정에 따라 다른 옵션을 제공 하는 몇 가지 더 많은 템플릿이-에서 찾을 수 있습니다 [서비스 패브릭 및 OMS 템플릿](https://azure.microsoft.com/resources/templates/?term=service+fabric+OMS).

### <a name="deploying-oms-using-through-azure-marketplace"></a>Azure Marketplace를 통해 OMS 배포

클러스터를 배포한 후 tooadd OMS 작업 영역을 원하는 경우 tooAzure 마켓플레이스를 통해 헤드를 찾아서 *"서비스 패브릭 분석"*합니다. Hello "+ 관리 모니터링" 범주 아래 그림에 표시 되는 하나의 리소스만 있어야 합니다.

![Marketplace의 OMS SF 분석](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-analytics.png)

**만들기**를 클릭하면 OMS 작업 영역에 대한 메시지가 표시됩니다. **작업 영역 선택** 및 **새 작업 영역 만들기**를 차례로 선택합니다. 필요한 hello 항목 작성-hello 유일한 요구 사항은 여기서은 서비스 패브릭 클러스터와 hello OMS 작업 영역 해야 hello에 대 한 hello 구독 동일을 hello 합니다. 입력 항목의 유효성이 검사되면 OMS 작업 영역이 몇 분 안에 배포됩니다. 배포를 마무리 하는 동안 hello 서비스 패브릭 솔루션 블레이드의 hello 생성 계속 열려 유지 됩니다. 동일한 작업 영역 나타남 아래 hello 하 고 있는지 확인 *OMS 작업 영역* 적중 및 **만들기** hello 맨 아래에 tooadd hello 서비스 패브릭 솔루션 toohello 작업 영역입니다.

## <a name="using-hello-oms-agent"></a>Hello OMS 에이전트를 사용 하 여

Toouse EventFlow 좋습니다 모듈식 방법 toodiagnostics에 대 한 수 있기 때문에 집계 솔루션으로 WAD 및 모니터링 합니다. 예를 들어 프로그램 출력을 EventFlow toochange 원하는 없는 변경 tooyour 실제 계측을 간단히 수정 tooyour config 파일 바로 필요 합니다. 하지만 tooinvest OMS를 사용 하 여 결정을 감수 하는 경우 사용 하 여 이벤트 분석을 위한 toocontinue (에 toobe hello 플랫폼 사용 되지만 대신 한다는 hello 플랫폼 중 하나 이상에) hello설정을확인하는것이좋습니다[</c0>OMS에이전트<spanclass="notranslate">](../log-analytics/log-analytics-windows-agents.md)합니다.</span> 또한 사용 해야 hello OMS 에이전트 컨테이너 tooyour 클러스터를 배포 하는 경우 아래 설명 된 대로 합니다.

이 작업을 위한 hello 프로세스는 하기만 하면 tooadd hello 에이전트는 가상 컴퓨터 크기 집합 확장 tooyour 리소스 관리자 템플릿을 대로 가져옵니다 노드가 각각에 설치 되어 있는지 확인 하므로, 비교적 간단 합니다. 서비스 패브릭 솔루션 (위에서) hello로 hello OMS 작업 영역을 배포 하 고 hello 에이전트 tooyour 노드를 추가 하는 샘플 리소스 관리자 템플릿을 실행 하는 클러스터에 대 한 있습니다 [Windows](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Windows) 또는 [Linux](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Linux)합니다.

이 hello 장점 hello 다음과 같습니다.

* Hello 성능 카운터와 메트릭을 쪽에 있는 다양 한 데이터
* Hello에서 수집 되는 쉽게 tooconfigure 데이터 클러스터 및 응용 프로그램을 다시 배포 하지 않고 변경 내용을 tooit 확인 또는 hello 에이전트의 변경 내용 toohello 설정을 hello OMS 작업 영역에서 수행할 수 있고 하기만 합니다 hello 클러스터 hello 에이전트를 다시 설정 자동으로 합니다. 특정 성능 카운터, 작업 영역 이동 toohello tooconfigure hello OMS 에이전트 toopick **홈 > 설정 > 데이터 > Windows 성능 카운터** 수집 toosee 원하는 hello 데이터를 선택 하 고
* OMS에 의해 선택 되 고 하기 전에 저장 toobe 것 보다 더 빠르게 참석 데이터 / 로그 분석
* 컨테이너 모니터링은 Docker 로그(stdout, stderr) 및 통계(컨테이너 및 노드 수준의 성능 메트릭)를 선택할 수 있기 때문에 훨씬 쉽습니다.

hello 주요 고려 여기는 에이전트 이므로, 배포 될 프로그램 응용 프로그램과 함께 클러스터에 hello 클러스터에서 응용 프로그램의 일부 영향을 최소화 toohello 성능을 있으므로입니다.

## <a name="monitoring-containers"></a>컨테이너 모니터링

컨테이너 tooa 서비스 패브릭 클러스터를 배포할 때는 것이 좋습니다 hello 클러스터 체결 hello OMS 에이전트와 및 해당 hello 컨테이너 솔루션 tooyour OMS 작업 영역 tooenable 모니터링 및 진단 추가 되었습니다. 솔루션 작업 영역에서 다음과 같은 어떤 hello 컨테이너는 다음과 같습니다.

![기본 OMS 대시보드](./media/service-fabric-diagnostics-event-analysis-oms/oms-containers-dashboard.png)

hello 에이전트에서 OMS에 쿼리할 수 있습니다 또는 toovisualized 성능 표시기를 사용 하는 몇 가지 컨테이너별 로그 hello 컬렉션을 수 있습니다. hello 로그 수집 되는 유형은 다음과 같습니다.

* ContainerInventory: 컨테이너 위치, 이름 및 이미지에 대한 정보를 표시합니다.
* ContainerImageInventory: ID 또는 크기를 포함하여 배포된 이미지에 대한 정보를 표시합니다.
* ContainerLog: 특정 오류 로그, docker 로그(stdout 등) 및 기타 항목을 표시합니다.
* ContainerServiceLog: 실행된 docker 디먼 명령을 표시합니다.
* 성능: 성능 카운터 컨테이너를 포함 하 여 cpu, 메모리, 네트워크 소통량, 디스크 i/o 및 컴퓨터를 호스트 하는 hello에서 사용자 지정 메트릭

이 문서에서는 hello 단계 필요한 tooset 클러스터에 대 한 모니터링 하는 컨테이너를 설명 합니다. OMS의 컨테이너 솔루션에 대 한 자세한 toolearn 체크 아웃의 [설명서](../log-analytics/log-analytics-containers.md)합니다.

작업 영역에서 컨테이너 솔루션 hello tooset 위에서 언급 한 hello 단계에 따라 클러스터의 노드에 배포 된 hello OMS 에이전트 있는지 확인 합니다. Hello 클러스터 준비 되 면 컨테이너 tooit를 배포 합니다. Hello 처음으로 컨테이너 이미지를 배포 된 tooa 클러스터가, 크기에 따라 몇 분 toodownload hello 이미지를 사용 합니다.

Azure Marketplace에서 검색할 *컨테이너* 컨테이너 리소스를 만듭니다 (아래에서 모니터링 + 관리 hello 범주)입니다.

![컨테이너 솔루션 추가](./media/service-fabric-diagnostics-event-analysis-oms/containers-solution.png)

Hello 생성 단계에서 OMS 작업 영역을 요청합니다. Hello 위의 hello 배포를 사용 하 여 만든 하나를 선택 합니다. 이 단계는 OMS 작업 영역 내에서 컨테이너 솔루션을 추가 하 고 hello 서식 파일에서 배포 된 hello OMS 에이전트에 의해 자동으로 검색 됩니다. hello 에이전트 hello 클러스터와 15 분 미만의 hello 컨테이너 프로세스에서 데이터 수집을 시작 합니다 또는 위의 hello 대시보드의 hello 이미지와 같이 데이터로 켜 hello 솔루션을 따라서 표시 되어야 합니다.


## <a name="next-steps"></a>다음 단계

다음 작업 영역 tooyour 필요한 OMS 도구와 옵션 toocustomize hello를 살펴봅니다.

* OMS는 온-프레미스 클러스터에 대 한 사용된 toosend 데이터 tooOMS 일 수 있는 게이트웨이 (HTTP 앞으로 프록시)를 제공 합니다. 이 대해 자세히 [OMS 게이트웨이 hello 사용 하 여 인터넷 액세스 tooOMS 하지 않고 컴퓨터에 연결](../log-analytics/log-analytics-oms-gateway.md)
* OMS tooset 구성할 [경고 자동](../log-analytics/log-analytics-alerts.md) tooaid 검색 및 진단
* Hello로 파악 한 다음 가져올 [로그 검색 및 쿼리](../log-analytics/log-analytics-log-searches.md) 로그 분석의 일환으로 제공 하는 기능
