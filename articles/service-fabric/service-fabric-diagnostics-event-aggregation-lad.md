---
title: "서비스 패브릭 이벤트 집계 Linux Azure 진단으로 aaaAzure | Microsoft Docs"
description: "Azure Service Fabric 클러스터 모니터링 및 진단을 위해 LAD를 사용하여 이벤트를 집계 및 수집하는 방법에 대해 알아봅니다."
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
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: aefa869219a0dd219e01e6574816fe3ce47fe472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-linux-azure-diagnostics"></a>Linux Azure 진단을 사용하여 이벤트 집계 및 수집
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Azure 서비스 패브릭 클러스터를 실행 하는 경우 중앙 위치에 있는 모든 hello 노드에서 것이 좋습니다 toocollect hello가 있습니다. Hello 로그를 중앙 위치에 있는 분석 및 클러스터의 문제 또는 hello 응용 프로그램 및 해당 클러스터에서 실행 되는 서비스의 문제를 해결 하는 데 도움이 됩니다.

한 가지 방법은 tooupload 및 수집 로그는 로그 tooAzure 저장소에 업로드 하 고 hello 옵션 toosend 로그 tooAzure Application Insights 또는 이벤트 허브에는 toouse hello Linux Azure 진단 (했다) 확장입니다. 저장소에서 외부 프로세스 tooread hello 이벤트를 사용 하 고와 같은 분석 플랫폼 제품에 배치할 수도 있습니다 [OMS 로그 분석](../log-analytics/log-analytics-service-fabric.md) 또는 다른 로그 구문 분석 솔루션입니다.

## <a name="log-and-event-sources"></a>로그 및 이벤트 원본

### <a name="service-fabric-platform-events"></a>Service Fabric 플랫폼 이벤트
Service Fabric은 운영 이벤트 또는 런타임 이벤트를 포함하여 [LTTng](http://lttng.org)를 통해 몇 가지 기본 제공 로그를 생성합니다. 이러한 로그는 서식 파일을 지정 하는 클러스터의 리소스 관리자 hello hello 위치에 저장 됩니다. tooget hello 태그에 대 한 검색을 hello 저장소 계정 세부 정보를 설정 또는 **AzureTableWinFabETWQueryable** 를 찾아서 **StoreConnectionString**합니다.

### <a name="application-events"></a>응용 프로그램 이벤트
 소프트웨어를 계측할 때 지정한 대로 응용 프로그램 및 서비스 코드에서 발생되는 이벤트입니다. 텍스트 기반 로그 파일을 작성하는 모든 로깅 솔루션을 사용할 수 있습니다(예: LTTng). 자세한 내용은 응용 프로그램 추적에서 hello LTTng 설명서를 참조 합니다.

[로컬 컴퓨터 개발 설정에서의 모니터링 및 진단 서비스](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

## <a name="deploy-hello-diagnostics-extension"></a>Hello 진단 확장 배포
로그를 수집 hello 첫 번째 단계는 hello 서비스 패브릭 클러스터에 있는 hello Vm의 각 toodeploy hello 진단 확장입니다. hello 진단 확장 각 VM에서 로그를 수집 하 고 사용자가 지정한 toohello 저장소 계정으로 업로드 합니다. hello 단계 hello Azure 포털 또는 Azure 리소스 관리자를 사용 하는지 여부에 따라 다릅니다.

클러스터 만들기의 일부로 hello 클러스터의 toodeploy hello 진단 확장 toohello Vm 설정 **진단** 너무**에**합니다. Hello 클러스터를 만드는 hello 포털을 사용 하 여이 설정을 변경할 수 없습니다.

그런 다음 Linux Azure 진단 (했다) toocollect hello 파일을 구성 하 고 저장소 계정에 배치 합니다. 이 과정은 시나리오에 해당 3 ("업로드 하세요. 로그 파일을 직접") hello 문서에 설명 되어 [를 사용 하 여 했다 toomonitor 고 Linux Vm의 경우 진단](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다. 추적 프로세스 다가갈 수 있고, toohello 액세스를 수행 합니다. 사용자가 선택한 hello 추적 tooa 시각화 도우미를 업로드할 수 있습니다.

또한 Azure 리소스 관리자를 사용 하 여 hello 진단 확장을 배포할 수 있습니다. hello 프로세스는 Windows 및 Linux에 대 한 유사 하며 Windows에서 클러스터에 대 한 설명 [toocollect Azure 진단으로 기록 하는 방법을](service-fabric-diagnostics-how-to-setup-wad.md)합니다.

또한 [Linux와 함께 사용하는 Operations Management Suite Log Analytics](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/)에 설명된 대로 Operations Management Suite를 사용할 수 있습니다.

이 구성에서는 완료 된 후 hello 했다 에이전트 모니터링 hello 로그 파일을 지정된 합니다. 때마다 새 줄에는 추가 된 toohello 파일에는 사용자가 지정한 보낸된 toohello 저장소 syslog 항목을 만듭니다.

## <a name="next-steps"></a>다음 단계

자세히 toounderstand 문제를 해결 하는 동안 검사 해야 이벤트 참조 [LTTng 설명서](http://lttng.org/docs) 및 [를 사용 하 여 했다](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.
