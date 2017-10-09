---
title: "aaaAzure 모니터 개요 | Microsoft Docs"
description: "Azure Monitor는 경고, webhook, 자동 크기 조정 및 자동화를 사용하기 위해 통계를 수집합니다. 또한 문서에서는 다른 Microsoft 모니터링 옵션을 나열합니다."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: ffa304e7b158f0fceb7f60ab88fab291976aa0e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-monitor"></a>Azure Monitor 개요
이 문서에서는 hello Azure 모니터 서비스를 Microsoft Azure에 대 한 개요를 제공 합니다. Azure 모니터 않습니다 및 방법에 대해 포인터 tooadditional 설명에 대해 설명 toouse Azure 모니터입니다.  한 비디오 소개를 선호 하는 경우이 문서의 hello 맨 아래에 다음 단계 링크를 참조 합니다. 

## <a name="why-monitor-your-application-or-system"></a>응용 프로그램 또는 시스템을 모니터링해야 하는 이유
클라우드 응용 프로그램은 이동하는 부분이 많아 복잡합니다. 모니터링 없이 계속 응용 프로그램 데이터 tooensure 정상 상태에서 실행 되 고 제공 합니다. 또한 있습니다 toostave 잠재적 문제를 해제 하거나 문제를 해결 하십시오. 지난 수 있습니다. 또한 응용 프로그램에 대 한 모니터링 데이터 toogain 깊은 통찰력을 사용할 수 있습니다. 이 정보는 tooimprove 응용 프로그램 성능이 나 유지 관리의 편의성 하는 데 도움이 하거나 수동 개입 해야 하는 작업을 자동화할 수 있습니다.


## <a name="azure-monitor-and-microsofts-other-monitoring-products"></a>Azure Monitor 및 다른 Microsoft 모니터링 제품
Azure Monitor는 대부분의 Microsoft Azure 서비스에 대한 기본 수준의 인프라 메트릭과 로그를 제공합니다. Azure 서비스를 Azure 모니터도 해당 데이터를 저장 하지 않는 것이 있으면에 넣습니다 hello 이후.

Microsoft는 온-프레미스 설치도 사용하는 개발자, DevOps 또는 IT 작업에 추가 모니터링 기능을 제공하는 추가 제품과 서비스를 제공합니다. 이와 같이 다양한 제품과 서비스가 작동하는 방법에 대한 개요와 이해는 [Microsoft Azure 모니터링](monitoring-overview.md)을 참조하세요.

## <a name="monitoring-sources---compute"></a>모니터링 소스 - Compute

![비 계산 리소스의 모니터링 및 진단을 위한 모델](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-compute_v6.png)

hello 계산 서비스 포함 
- 클라우드 서비스 
- 가상 컴퓨터 
- 가상 컴퓨터 확장 집합 
- 서비스 패브릭

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a>응용 프로그램 - 진단 로그, 응용 프로그램 로그 및 메트릭
응용 프로그램 hello 계산 모델에 게스트 OS hello를 기반으로 실행할 수 있습니다. 고유한 로그 및 메트릭 집합을 제공합니다. 대부분의 응용 프로그램 수준 메트릭 및 로그 azure 모니터 hello Azure 진단 확장 (Windows 또는 Linux) toocollect에 의존합니다. hello 유형에

* 성능 카운터
* 응용 프로그램 로그
* Windows 이벤트 로그
* .NET 이벤트 원본
* IIS 로그
* 매니페스트 기반 ETW
* 크래시 덤프
* 고객 오류 로그

Hello 진단 확장 없으면 CPU 사용량와 같은 몇 가지 메트릭만 사용할 수 있습니다. 

### <a name="host-and-guest-vm-metrics"></a>호스트 및 게스트 VM 메트릭
hello 앞에 나열 된 계산 된 리소스 VM 전용된 호스트와 게스트 OS 상호 작용 하는 있습니다. VM hello 호스트와 게스트 OS는 VM 루트의 hello 서로 동일 하며 hello Hyper-v 하이퍼바이저 모델에서 게스트 VM입니다. 둘 다에서 메트릭을 수집할 수 있습니다. Hello 게스트 OS에 진단 로그를 수집할 수도 있습니다.   

### <a name="activity-log"></a>활동 로그
Hello Azure 인프라와 같이 리소스에 대 한 자세한 내용은 hello (이전에 운영 또는 감사 로그 호출) 활동 로그를 검색할 수 있습니다. hello 로그 리소스는 만들거나 제거할 시간 등의 정보를 포함 합니다.  자세한 내용은 [활동 로그 개요](monitoring-overview-activity-logs.md)를 참조하세요. 

## <a name="monitoring-sources---everything-else"></a>모니터링 소스 - 기타 등등

![계산 리소스의 모니터링 및 진단을 위한 모델](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-non-compute_v6.png)


### <a name="resource---metrics-and-diagnostics-logs"></a>리소스 - 메트릭 및 진단 로그
수집 가능한 메트릭 및 진단 로그 hello 리소스 종류에 따라 다릅니다. 예를 들어 웹 응용 프로그램 hello 디스크 IO 및 %CPU 통계를 제공합니다. 이러한 메트릭은 큐 크기 및 메시지 처리량과 같은 메트릭을 대신 제공하는 Service Bus 큐에는 존재하지 않습니다. 각 리소스에 대해 수집 가능한 메트릭 목록은 [지원되는 메트릭](monitoring-supported-metrics.md)에서 제공됩니다. 

### <a name="host-and-guest-vm-metrics"></a>호스트 및 게스트 VM 메트릭
리소스와 특정 호스트 VM 또는 게스트 VM 간에는 일대일 매핑이 반드시 필요하지는 않으므로 메트릭을 사용할 수 없습니다.

### <a name="activity-log"></a>활동 로그
hello 활동 로그 계산 리소스와 같지만 hello 됩니다.  

## <a name="uses-for-monitoring-data"></a>모니터링 데이터 사용
데이터를 수집한 후 할 수 있는 Azure 모니터에서 함께 다음 hello

### <a name="route"></a>라우팅
실시간으로 모니터링 데이터 tooother 위치를 스트리밍할 수 있습니다.

예를 들면 다음과 같습니다.

- 다양 한 시각화 및 분석 도구를 사용할 수 있도록 tooApplication Insights를 보냅니다.
- Toothird 타사 도구를 라우팅할 수 있도록 tooEvent 허브를 보냅니다. 

### <a name="store-and-archive"></a>저장 및 보관
일부 모니터링 데이터는 이미 설정된 시간 동안 Azure Monitor에 저장되어 사용할 수 있습니다. 
- 메트릭은 30일 동안 저장됩니다. 
- 활동 로그 항목은 90일 동안 저장됩니다. 
- 진단 로그는 전혀 저장되지 않습니다. 

위에 나열 된 기간 동안 hello 보다 길게 toostore 데이터 하려는 경우에 Azure 저장소를 사용할 수 있습니다. 모니터링 데이터는 설정한 보존 정책에 따라 저장소 계정에 보관됩니다. 사용자에 게 Azure 저장소의 데이터가 차지 하는 hello 공간 hello에 대 한 toopay. 

몇 가지 방법으로 toouse이이 데이터:

- 기록된 경우 Azure 내부 또는 외부의 다른 도구를 사용하여 데이터를 읽고 처리할 수 있습니다.
- 로컬 보관에 대 한 로컬 hello 데이터 다운로드 또는 오랜 시간에 대 한 hello 클라우드 tookeep 데이터에서 보존 정책을 변경 합니다.  
- 무한정 보관을 위해 Azure 저장소에 hello 데이터를 유지 합니다. 

### <a name="query"></a>쿼리
Hello Azure 모니터 REST API, 크로스 플랫폼 명령줄 인터페이스 (CLI) 명령, PowerShell cmdlet을 사용할 수 있습니다 또는 hello.NET SDK tooaccess hello 시스템 또는 Azure 저장소에 데이터를 환영

예를 들면 다음과 같습니다.

* 작성한 사용자 지정 모니터링 응용 프로그램에 대한 데이터 가져오기
* 사용자 지정 쿼리를 만들고 해당 데이터 tooa 타사 응용 프로그램 보내는 합니다.

### <a name="visualize"></a>시각화
그래픽 및 차트에 모니터링 데이터를 시각화 하면 추세를 hello 데이터 자체를 통해 보고 보다 더 빠르게 찾을 있습니다.  

몇 가지 시각화 방법은 다음과 같습니다.

* Hello Azure 포털을 사용 하 여
* 경로 데이터 tooAzure Application Insights
* 경로 데이터 tooMicrosoft PowerBI
* 라이브 스트리밍 하거나 경로 hello 데이터 tooa 제 3 자 시각화 도구를 사용 하 여 함으로써 hello 도구에서에서 또는 Azure 저장소에 보관


### <a name="automate"></a>자동화
모니터링 데이터 tootrigger 경고를 사용 하거나 포함 하 여 전체 프로세스입니다. 예를 들면 다음과 같습니다.

* 사용 데이터 tooautoscale 계산 인스턴스 위로 또는 아래로 응용 프로그램 부하에 따라 합니다.
* 메트릭이 미리 결정된 임계값을 초과하는 경우 전자 메일 보내기
* Azure 외부 시스템의 웹 URL (webhook) tooexecute 동작을 호출 합니다.
* 다양 한 작업 tooperform Azure 자동화에서에서 runbook을 시작

## <a name="methods-of-accessing-azure-monitor"></a>Azure Monitor에 액세스하는 방법
일반적으로 추적 데이터, 라우팅 및 hello 메서드를 다음 중 하나를 사용 하 여 검색을 조작할 수 있습니다. 일부 방법은 일부 동작 및 데이터 형식에 사용할 수 없습니다.

* [Azure 포털](https://portal.azure.com)
* [PowerShell](insights-powershell-samples.md)  
* [CLI(플랫폼 간 명령줄 인터페이스)](insights-cli-samples.md)
* [REST API](https://docs.microsoft.com/rest/api/monitor/)
* [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a>다음 단계
자세한 정보
- Azure Monitor 비디오 연습은  
[Azure Monitor 시작](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor)에서 제공됩니다. Azure Monitor를 사용할 수 있는 시나리오를 설명하는 추가 비디오는 [Microsoft Azure 모니터링 및 진단 탐색](https://channel9.msdn.com/events/Ignite/2016/BRK2234)(영문) 및 [Azure Monitor(Ignite 2016 비디오)](https://myignite.microsoft.com/videos/4977)(영문)에서 제공됩니다.
- hello Azure 모니터 인터페이스를 통해 실행 [Azure 모니터 시작](monitoring-get-started.md)
- Hello 설정 [Azure 진단 확장](../azure-diagnostics.md) toodiagnose 문제 클라우드 서비스, 가상 컴퓨터에서에서 시도 하는 경우 가상 컴퓨터의 크기를 조정 하거나 설정 또는 서비스 패브릭 응용 프로그램입니다.
- [Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) 앱 서비스 웹 앱의 toodiagnostic 문제를 사용 하려는 경우.
- [Azure Storage 문제 해결](../storage/common/storage-e2e-troubleshooting.md) - 저장소 Blob, 테이블 및 큐를 사용하는 경우
- [로그 분석](https://azure.microsoft.com/documentation/services/log-analytics/) 및 hello [Operations Management Suite](https://www.microsoft.com/oms/)
