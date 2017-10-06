---
title: "Microsoft Azure에서 aaaMonitoring | Microsoft Docs"
description: "원하는 toomonitor 어느 것에 Microsoft Azure에서 선택할 수 있습니다. Azure Monitor, Application Insights Log Analytics"
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1b962c74-8d36-4778-b816-a893f738f92d
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: f5a4f32525c52613f01a913e09a9fe3fbcbaeb21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-monitoring-in-microsoft-azure"></a>Microsoft Azure 모니터링 개요
이 문서에서는 Microsoft Azure 모니터링에 사용할 수 있는 도구에 대해 간략히 설명합니다. 너무 적용
- Microsoft Azure에서 실행 중인 응용 프로그램 모니터링 
- Azure 외부에서 실행되어 Azure의 개체를 모니터링할 수 있는 도구/서비스 

에 대해 설명 다양 한 제품 및 서비스를 사용할 수 있는 hello 및 방식과 함께 작동 합니다. 가장 적절 한 어떤 경우에는 도구는 toodetermine를 지원할 수 있습니다.  

## <a name="why-use-monitoring-and-diagnostics"></a>모니터링 및 진단을 사용하는 이유는?

클라우드 앱의 성능 문제는 비즈니스에 영향을 미칠 수 있습니다. 상호 연결된 여러 구성 요소와 자주 제공되는 릴리스를 사용하면 언제든지 성능 저하가 발생할 수 있습니다. 앱을 개발하는 경우 사용자는 일반적으로 테스트에서 찾지 못한 문제를 발견합니다. 이러한 문제를 즉시 알아야 하 고 hello 문제 진단 및 해결에 대 한 도구를 설치 해야 합니다. Microsoft Azure에는 이러한 문제를 식별할 수 있는 다양한 도구가 있습니다.

## <a name="how-do-i-monitor-my-azure-cloud-apps"></a>Azure 클라우드 앱을 모니터링하는 방법은?

Azure 응용 프로그램과 서비스를 모니터링하기 위한 다양한 도구가 있습니다. 일부 기능은 겹칩니다. 기록 상의 용도로 부분적와 부분적으로 개발 및 응용 프로그램의 작업 간의 뜨 리고 toohello 때문입니다. 

Hello 주 도구는 다음과 같습니다.

-   **Azure Monitor** - Azure에서 실행되는 서비스를 모니터링하는 기본 도구입니다. 서비스와 환경 주변 hello hello 처리량에 대 한 인프라 수준의 데이터 제공 합니다. Azure에서 모든 앱을 관리 하는 경우 여부를 리소스를 위아래로 tooscale, 다음 Azure 모니터 제공 사용 하 여 결정 toostart 합니다.

-   **Application Insights** - 개발을 위해 사용하거나 프로덕션 모니터링 솔루션으로 사용할 수 있습니다. 앱에 패키지를 설치하여 작동하므로 진행 상황에 대한 자세한 내부 보기를 제공합니다. 이 데이터에는 종속성, 예외 추적, 디버깅 스냅숏, 실행 프로필의 응답 시간이 포함됩니다. 앱과 함께 수행 하는 사용자가 이해 하는 toohelp 디버그 두 toohelp 강력한 스마트 도구가 모든 원격이 분석 분석을 위해 제공 합니다. 응답 시간이 급증 때문 인지를 알 수는 응용 프로그램 또는 일부 외부 resourcing 문제에서 toosomething 합니다. Visual Studio를 사용 하는 경우 잘못 hello 앱은 있습니다 수 수 가져오므로 오른쪽 toohello 문제 줄을 코드의 문제를 해결할 수 있습니다.  

-   **로그 분석** 은 프로덕션 환경에서 실행 중인 응용 프로그램에서 tootune 성능 및 계획 유지 관리 해야 합니다. 이는 Azure에 기반을 두고 있습니다. 수집 하 고 10 too15 분 간의 지연이 사항이 있는 여러 소스에서 데이터를 집계 합니다. Azure, 온-프레미스 및 타사 클라우드 기반 인프라(예: Amazon Web Services)에 대한 전체적인 IT 관리 솔루션을 제공합니다. 제공 다양 한 도구 tooanalyze 데이터 자세한 소스 간에, 모든 로그에서 복잡 한 쿼리를 허용 하 고 지정 된 조건에 적극적으로 경고할 수 있습니다.  사용자 지정 데이터를 해당되는 중앙의 리포지토리에 수집하여 쿼리하고 시각화할 수도 있습니다. 

-   **SCOM(System Center Operations Manager)** - 대규모 클라우드 설치를 관리하고 모니터링하기 위한 것입니다. 온-프레미스 Windows Sever 및 Hyper-V 기반 클라우드를 위한 관리 도구로 이미 친숙해 있을 수 있지만, Azure 앱과 통합하여 이러한 앱을 관리할 수도 있습니다. 무엇보다도 기존의 라이브 앱에 Application Insights를 설치할 수 있습니다.  앱 작동이 중단되면 수 초 안에 알려줍니다. Log Analytics는 SCOM을 대체하지 않습니다. 오히려 함께 결합하여 잘 작동합니다.  


## <a name="accessing-monitoring-in-hello-azure-portal"></a>Hello Azure 포털에서에서 모니터링에 액세스
모든 Azure 모니터링 서비스는 이제 하나의 UI 창에서 사용할 수 있습니다. 방법에 대 한 자세한 내용은 tooaccess이이 영역은 참조 [Azure 모니터를 시작](monitoring-get-started.md)합니다. 

또한 특정 리소스를 강조 표시하고 모니터링 옵션을 드릴다운하여 해당 리소스에 대한 모니터링 기능에 액세스할 수 있습니다. 

## <a name="examples-of-when-toouse-which-tool"></a>경우의 예는 도구 toouse 

다음 섹션 hello 몇 가지 기본 시나리오와 함께 사용할 수 있는 도구를 보여 줍니다. 

### <a name="scenario-1--fix-errors-in-an-azure-application-under-development"></a>시나리오 1 - 개발 중인 Azure 응용 프로그램의 오류 수정   

**hello 최선의 선택은 toouse Application Insights, Azure 모니터 및 Visual Studio 함께**

이제 azure hello hello 클라우드에서 hello Visual Studio 디버거의 모든 기능을 제공합니다. Azure 모니터 toosend 원격 분석 tooApplication Insights을 구성 합니다. 응용 프로그램에서 Visual Studio tooinclude hello Application Insights SDK를 사용 하도록 설정 합니다. Application Insights에서 사용할 수 있습니다 hello 응용 프로그램 맵 toodiscover 시각적으로 실행 중인 응용 프로그램의 부분 되지는 않습니다 정상 여부. 정상이 아닌 요소의 경우 이미 오류 및 예외가 탐색에 사용될 수 있습니다. 사용할 수 있습니다 hello Application Insights toogo 하위 수준에서 다양 한 분석 합니다. Hello 오류에 대 한 확실 하지 않은, 경우에 코드 및 pin 지점 문제를 세부적으로 hello Visual Studio 디버거 tootrace를 사용할 수 있습니다. 

자세한 내용은 참조 [웹 응용 프로그램 모니터링](../application-insights/app-insights-azure-web-apps.md) 다양 한 유형의 응용 프로그램 및 언어에 대 한 지침은 hello 왼쪽의 목차 toohello 테이블을 참조 하십시오.  

### <a name="scenario-2--debug-an-azure-net-web-application-for-errors-that-only-show-in-production"></a>시나리오 2 - 프로덕션 환경에서만 표시되는 오류에 대해 Azure .NET 웹 응용 프로그램 디버깅 

> [!NOTE]
> 이러한 기능은 미리 보기에 있습니다. 

**hello 옵션은 toouse Application Insights와 hello에 대 한 Visual Studio의 디버깅 환경을 전체 가능 하면 가장 좋습니다.**

응용 프로그램 통찰력 스냅숏 디버거 toodebug hello 응용 프로그램을 사용 합니다. Hello 시스템 시간 "스냅숏" 라는 windows의 원격 분석을 자동으로 캡처합니다 특정 오류 임계값 프로덕션 구성 요소와 함께 발생 hello 캡처된 amount를 안전 하 게 프로덕션 클라우드 작은 있기 때문에 충분 한 tooaffect 성능이 하지 않은 있지만 중요 한 tooallow 추적 합니다.  hello 시스템 스냅숏이 여러 개를 캡처할 수 있습니다. 시점 hello Azure 포털의에서 지정 시간으로 확인 하거나 Visual Studio를 사용 하 여 hello 전체 경험 수 있습니다. Visual Studio를 사용하면 개발자는 실시간으로 디버그하는 것처럼 스냅숏을 단계별로 진행할 수 있습니다. 로컬 변수, 매개 변수, 메모리 및 프레임을 모두 사용할 수 있습니다. 개발자가 RBAC 역할을 통해 toothis 프로덕션 데이터에 액세스를 부여 되어야 합니다.  

자세한 내용은 [스냅숏 디버깅](../application-insights/app-insights-snapshot-debugger.md)을 참조하세요. 

### <a name="scenario-3--debug-an-azure-application-that-uses-containers-or-microservices"></a>시나리오 3 - 컨테이너 또는 마이크로 서비스를 사용하는 Azure 응용 프로그램 디버깅 

**시나리오 1과 동일합니다. Application Insights, Azure Monitor 및 Visual Studio를 함께 사용합니다.** Application Insights는 컨테이너 내 및 마이크로 서비스(Kubernetes, Docker, Azure Service Fabric)에서 실행되는 프로세스로부터 원격 분석을 수집하는 것도 지원합니다. 자세한 내용은 [여기에 있는 컨테이너 및 마이크로 서비스 디버깅에 대한 비디오를 참조하세요](https://go.microsoft.com/fwlink/?linkid=848184). 


### <a name="scenario-4--fix-performance-issues-in-your-azure-application"></a>시나리오 4 - Azure 응용 프로그램의 성능 문제 해결

hello [Application Insights 프로파일러](../application-insights/app-insights-profiler.md) 은 설계 된 toohelp 이러한 유형의 문제를 해결 합니다. App Services(Web Apps, Logic Apps, Mobile Apps, API Apps) 및 다른 계산 리소스(예: Virtual Machines, VMSS(Virtual Machine Scale Sets), Cloud Services 및 Service Fabric)에서 실행되는 응용 프로그램의 성능 문제를 식별하고 해결할 수 있습니다. 

> [!NOTE]
> 미리 보기 기능 tooprofile 가상 컴퓨터, 가상 컴퓨터 크기 집합 (VMSS) 클라우드 서비스 및 서비스 패브릭입니다.   

또한 미리 알려 줍니다 특정 유형의 느린 페이지 로드 시간 등의 오류에 대 한 전자 메일을 통해 hello 스마트 검색 도구를 통해.  Toodo이이 도구에는 구성이 필요 없습니다. 자세한 내용은 [스마트 검색 - 성능 이상](../application-insights/app-insights-proactive-performance-diagnostics.md) 및 [스마트 검색 - 성능 이상](https://azure.microsoft.com/blog/Enhancments-ApplicationInsights-SmartDetection/preview)을 참조하세요.



## <a name="next-steps"></a>다음 단계
자세한 정보

* [Ignite 2016의 비디오에서 Azure Monitor](https://myignite.microsoft.com/videos/4977)
* [Azure Monitor 시작](monitoring-get-started.md)
* [Azure 진단](../azure-diagnostics.md) toodiagnose 문제 클라우드 서비스, 가상 컴퓨터에서에서 시도 하는 경우 가상 컴퓨터 설정 또는 서비스 패브릭 응용 프로그램을 확장 합니다.
* [Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) 앱 서비스 웹 앱의 toodiagnostic 문제를 사용 하려는 경우.
* [로그 분석](https://azure.microsoft.com/documentation/services/log-analytics/) 및 hello [Operations Management Suite](https://www.microsoft.com/oms/) 프로덕션 모니터링 솔루션