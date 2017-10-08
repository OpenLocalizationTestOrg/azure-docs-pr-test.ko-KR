---
title: "Azure 진단의 aaaOverview | Microsoft Docs"
description: "클라우드 서비스, 가상 컴퓨터 및 서비스 패브릭에서 디버깅, 성능 측정, 모니터링, 트래픽 분석을 위해 Azure 진단 사용"
services: multiple
documentationcenter: .net
author: rboucher
manager: 
editor: 
ms.assetid: baad40d8-c915-4f93-b486-8b160bf33463
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/18/2017
ms.author: robb
ms.openlocfilehash: 2a03a96a37091894d7ab16120c125116e4bf462a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-diagnostics"></a>Azure 진단이란?
Azure 진단은 hello 배포 된 응용 프로그램에서 진단 데이터 수집을 사용 하면 Azure 내에서 hello 기능입니다. 다양 한 서로 다른 소스에서에서 hello 진단 확장을 사용할 수 있습니다. Azure 클라우드 서비스 웹 및 작업자 역할, Microsoft Windows 및 서비스 패브릭을 실행하는 Azure 가상 컴퓨터에서 현재 지원되고 있습니다. 다른 Azure 서비스에는 별도의 자체 진단이 있습니다.

## <a name="data-you-can-collect"></a>수집할 수 있는 데이터
Azure 진단 hello 다음 유형의 데이터를 수집할 수 있습니다.

| 데이터 원본 | 설명 |
| --- | --- |
| 성능 카운터 |운영 체제 및 사용자 지정 성능 카운터 |
| 응용 프로그램 로그 |응용 프로그램에서 작성한 메시지 추적 |
| Windows 이벤트 로그 |Toohello Windows 이벤트 로깅 시스템에 전송 되는 정보 |
| .NET 이벤트 원본 |Hello.NET을 사용 하 여 이벤트를 쓰는 코드 [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) 클래스 |
| IIS 로그 |IIS 웹 사이트에 대한 정보 |
| 매니페스트 기반 ETW |모든 프로세스에서 생성된 Windows 이벤트용 이벤트 추적 |
| 크래시 덤프 |응용 프로그램 크래시가의 hello 이벤트에서 hello 프로세스의 hello 상태에 대 한 정보 |
| 사용자 지정 오류 로그 |응용 프로그램 또는 서비스에서 생성한 로그 |
| Azure 진단 인프라 로그 |진단 자체에 대한 정보입니다. |

hello Azure 진단 확장 Azure 저장소 계정에이 데이터 tooan 전송 하거나 같은 tooservices 보낼 수 [Application Insights](../application-insights/app-insights-cloudservices.md)합니다. 및에 대 한 디버깅 및 문제 해결, 성능 측정, 리소스 사용 모니터링, 트래픽 분석 및 용량 계획, 감사 hello 데이터를 사용할 수 있습니다.

## <a name="versioning"></a>버전 관리
[Azure Diagnostics Versioning History(Azure 진단 버전 관리 기록)](azure-diagnostics-versioning-history.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계
어떤 서비스 고치려는 toocollect 진단을 선택 하 고 다음 시작 문서 tooget hello를 사용 하 여 키를 누릅니다. Hello 일반 Azure 진단 링크를 사용 하 여 특정 작업에 대 한 참조입니다.

## <a name="web-apps"></a>웹앱
웹앱에서는 Azure 진단을 사용하지 마세요. Hello에 해당 하는 정보를 찾을 [웹 응용 프로그램](../app-service-web/web-sites-enable-diagnostic-log.md)

## <a name="cloud-services-using-azure-diagnostics"></a>Azure 진단을 사용하는 클라우드 서비스
* Visual Studio를 사용 하는 경우 참조 [Visual Studio를 사용 하 여 클라우드 서비스 응용 프로그램 tootrace](../vs-azure-tools-debug-cloud-services-virtual-machines.md) tooget 시작 합니다. 그렇지 않은 경우 다음을 참조하세요.
* [Azure 진단을 사용 하 여 클라우드 toomonitor을 서비스 하는 방법](../cloud-services/cloud-services-how-to-monitor.md)
* [클라우드 서비스 응용 프로그램에서 Azure 진단 설정](../cloud-services/cloud-services-dotnet-diagnostics.md)

고급 항목의 경우 다음을 참조하세요.

* [클라우드 서비스용 Application Insights에서 Azure 진단 사용](../application-insights/app-insights-cloudservices.md)
* [Azure 진단으로 클라우드 서비스 응용 프로그램의 hello 흐름 추적](../cloud-services/cloud-services-dotnet-diagnostics-trace-flow.md)
* [클라우드 서비스에 대 한 진단 사용 하 여 PowerShell tooset](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="virtual-machines-using-azure-diagnostics"></a>Azure 진단을 사용하는 가상 컴퓨터
* Visual Studio를 사용 하는 경우 참조 [Visual Studio를 사용 하 여 Azure 가상 컴퓨터 tootrace](../vs-azure-tools-debug-cloud-services-virtual-machines.md) tooget 시작 합니다. 그렇지 않은 경우 다음을 참조하세요.
* [Azure Virtual Machine에서 Azure 진단 설정](../virtual-machines-dotnet-diagnostics.md)

고급 항목의 경우 다음을 참조하세요.

* [Azure 가상 컴퓨터에서 PowerShell tooset 한 진단 사용](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Azure Resource Manager 템플릿을 사용하여 모니터링 및 진단 기능으로 Windows 가상 컴퓨터 만들기](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="service-fabric-using-azure-diagnostics"></a>Azure 진단을 사용하는 서비스 패브릭
[Service Fabric 응용 프로그램 모니터링](../service-fabric/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)에서 시작합니다. 다른 많은 서비스 패브릭 진단 문서 hello toothis 문서를 가져오면 왼쪽 탐색 트리에서 hello 제공 됩니다.

## <a name="general-azure-diagnostics-articles"></a>일반 Azure 진단 문서
* [Azure 진단 스키마 구성](https://msdn.microsoft.com/library/azure/mt634524.aspx) -toochange 스키마 파일 toocollect hello 하는 방법에 대해 알아봅니다 하 고 진단 데이터를 라우팅합니다. 참고가 Visual Studio toochange hello 스키마 파일 사용할 수도 있습니다.
* [Azure 저장소에 Azure 진단 데이터 저장 방식이](../cloud-services/cloud-services-dotnet-diagnostics-storage.md) -hello hello 테이블과 hello 진단 데이터가 기록 되는 blob 이름을 알아야 합니다.
* 너무 자세한[성능 카운터를 사용 하 여 Azure 진단에서](../cloud-services/cloud-services-dotnet-diagnostics-performance-counters.md)합니다.
* 너무 자세한[경로 Azure 진단 정보 tooApplication Insights](azure-diagnostics-configure-application-insights.md)
* 진단을 시작하거나 Azure Storage 테이블에서 데이터를 찾는 데 문제가 있는 경우 [Azure 진단 문제 해결](azure-diagnostics-troubleshooting.md)을 참조하세요.
