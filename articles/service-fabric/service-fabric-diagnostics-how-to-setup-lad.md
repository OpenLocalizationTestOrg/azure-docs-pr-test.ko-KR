---
title: "Linux Azure 진단을 사용 하 여 로그 aaaCollect | Microsoft Docs"
description: "이 문서에서는 Azure에서 실행 되는 서비스 패브릭 Linux 클러스터에서 Azure 진단을 toocollect tooset 기록 하는 방법을 설명 합니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a160d469-8b7d-4560-82dd-8500db34a44a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/28/2017
ms.author: subramar
ms.openlocfilehash: f61172876e744ea3e361f9ae513254239d6ba27f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Azure 진단을 사용하여 로그 수집
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Azure 서비스 패브릭 클러스터를 실행 하는 경우 중앙 위치에 있는 모든 hello 노드에서 것이 좋습니다 toocollect hello가 있습니다. Hello 로그를 중앙 위치에 있으면 쉽게 tooanalyze 있고,이 든 상관 없이 서비스, 응용 프로그램 또는 hello 클러스터 자체의 문제를 해결 합니다. 한 가지 방법은 tooupload 및 수집 로그는 업로드 로그 저장소, Azure Application Insights 또는 Azure 이벤트 허브 tooAzure toouse hello Azure 진단 확장입니다. 또한 저장소 또는 이벤트 허브에서 hello 이벤트를 읽을 수 있으며와 같은 제품에 배치 [로그 분석](../log-analytics/log-analytics-service-fabric.md) 또는 다른 로그 구문 분석 솔루션입니다. [Azure Application Insights](https://azure.microsoft.com/services/application-insights/)에는 포괄적인 로그 검색 및 분석 서비스가 기본 제공됩니다.

## <a name="log-sources-that-you-might-want-toocollect"></a>Toocollect 알았으므로 로그 원본
* **서비스 패브릭 로그**: 통해 hello 플랫폼에서 내보낸 [LTTng](http://lttng.org) tooyour 저장소 계정에 업로드 합니다. 로그는 작동 관련 이벤트를 사용할 수 있습니다 또는 플랫폼 hello 런타임 이벤트를 내보냅니다. 이러한 로그에 저장 된 hello 위치에 해당 hello 클러스터 매니페스트를 지정 합니다. (tooget hello 저장소 계정 세부 정보 hello 태그에 대 한 검색 **AzureTableWinFabETWQueryable** 를 찾아서 **StoreConnectionString**.)
* **응용 프로그램 이벤트:** 서비스 코드에서 내보낸 이벤트입니다. 텍스트 기반 로그 파일을 작성하는 모든 로깅 솔루션을 사용할 수 있습니다(예: LTTng). 자세한 내용은 응용 프로그램 추적에서 hello LTTng 설명서를 참조 합니다.  

## <a name="deploy-hello-diagnostics-extension"></a>Hello 진단 확장 배포
로그를 수집 hello 첫 번째 단계는 hello 서비스 패브릭 클러스터에 있는 hello Vm의 각 toodeploy hello 진단 확장입니다. hello 진단 확장 각 VM에서 로그를 수집 하 고 사용자가 지정한 toohello 저장소 계정으로 업로드 합니다. hello 단계 hello Azure 포털 또는 Azure 리소스 관리자를 사용 하는지 여부에 따라 다릅니다.

클러스터 만들기의 일부로 hello 클러스터의 toodeploy hello 진단 확장 toohello Vm 설정 **진단** 너무**에**합니다. Hello 클러스터를 만드는 hello 포털을 사용 하 여이 설정을 변경할 수 없습니다.

그런 다음 Linux Azure 진단 (했다) toocollect hello 파일을 구성 하 고 저장소 계정에 배치 합니다. 이 과정은 시나리오에 해당 3 ("업로드 하세요. 로그 파일을 직접") hello 문서에 설명 되어 [를 사용 하 여 했다 toomonitor 고 Linux Vm의 경우 진단](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다. 추적 프로세스 다가갈 수 있고, toohello 액세스를 수행 합니다. 사용자가 선택한 hello 추적 tooa 시각화 도우미를 업로드할 수 있습니다.

또한 Azure 리소스 관리자를 사용 하 여 hello 진단 확장을 배포할 수 있습니다. hello 프로세스는 Windows 및 Linux에 대 한 유사 하며 Windows에서 클러스터에 대 한 설명 [toocollect Azure 진단으로 기록 하는 방법을](service-fabric-diagnostics-how-to-setup-wad.md)합니다.

또한 [Linux와 함께 사용하는 Operations Management Suite Log Analytics](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/)에 설명된 대로 Operations Management Suite를 사용할 수 있습니다.

이 구성에서는 완료 된 후 hello 했다 에이전트 모니터링 hello 로그 파일을 지정된 합니다. 때마다 새 줄에는 추가 된 toohello 파일에는 사용자가 지정한 보낸된 toohello 저장소 syslog 항목을 만듭니다.

## <a name="next-steps"></a>다음 단계
자세히 toounderstand 문제를 해결 하는 동안 검사 해야 이벤트 참조 [LTTng 설명서](http://lttng.org/docs) 및 [를 사용 하 여 했다](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.

