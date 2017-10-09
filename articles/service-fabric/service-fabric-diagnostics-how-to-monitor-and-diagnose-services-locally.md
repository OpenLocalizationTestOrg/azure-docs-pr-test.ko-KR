---
title: "windows에서 Azure microservices aaaDebug | Microsoft Docs"
description: "자세한 방법을 toomonitor 하 고 로컬 개발 컴퓨터에서 Microsoft Azure Service Fabric을 사용 하 여 작성 하 여 서비스를 진단 합니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: edcc0631-ed2d-45a3-851d-2c4fa0f4a326
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/24/2017
ms.author: dekapur
ms.openlocfilehash: 24868aa194b8a28fa3e6de95c1de5506d912a544
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>로컬 컴퓨터 개발 설정에서의 모니터링 및 진단 서비스
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
> 
> 

모니터링, 검색, 진단 및 문제 해결 중단을 최소화 toohello 사용자 환경을 서비스 toocontinue 허용 합니다. 모니터링 및 진단을 하지만 배포 된 실제 프로덕션 환경에서 필수적인, hello 효율성 tooa 실제 설치 프로그램을 이동 하면 작동 하는 서비스 tooensure 개발 하는 동안 비슷한 모델을 채택 달라 집니다. 서비스 패브릭을 사용 하면 단일 컴퓨터의 로컬 개발 한 설정 및 실제 생산 클러스터 설치 모두에서 원활 하 게 사용할 수 있는 서비스 개발자가 tooimplement 진단 쉬워집니다.

## <a name="event-tracing-for-windows"></a>Windows용 이벤트 추적
[Windows 용 이벤트 추적](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW)는 hello 서비스 패브릭에서 추적 메시지에 대 한 기술 권장 합니다. ETW를 사용하면 다음과 같은 이점이 있습니다.

* **ETW는 속도가 빠릅니다.** 코드 실행 시간에 미치는 영향을 최소화하도록 설계된 추적 기술입니다.
* **ETW 추적은 로컬 개발 환경 및 실제 사용 클러스터 설정에서도 매끄럽게 작동합니다.** 이 없는 추적 코드 준비 toodeploy 있을 때는 toorewrite 코드 tooa 실제 클러스터 것을 의미 합니다.
* **서비스 패브릭은 내부 추적에도 ETW를 사용합니다.** 이렇게 하면 서비스 패브릭 시스템 추적으로 인터리빙 된 응용 프로그램 추적 tooview 있습니다. 또한 toomore hello 기본 시스템의 hello 시퀀스와 응용 프로그램 코드 및 이벤트 간의 상호 관계를 쉽게 이해할 수 있습니다.
* **Tooview ETW 이벤트는 서비스 패브릭 Visual Studio 도구에서 기본적으로 지원 합니다.** Visual Studio 서비스 패브릭 올바르게 구성 되 면 ETW 이벤트 hello Visual Studio의 진단 이벤트 보기에에서 나타납니다. 

## <a name="view-service-fabric-system-events-in-visual-studio"></a>Visual Studio에서 서비스 패브릭 시스템 이벤트 보기
서비스 패브릭 응용 프로그램 개발자가 toohelp hello 플랫폼에서 일어나는 이해 하는 ETW 이벤트를 내보냅니다. 그렇게 이미 하지 않은 경우 계속 진행 하 고 hello 단계에 따라 [Visual Studio에서 응용 프로그램 처음 만들기](service-fabric-create-your-first-application-in-visual-studio.md)합니다. 이 정보를 참조할 수 문제 없이 응용 프로그램 진단 이벤트 뷰어 hello 추적 메시지를 보여 주는 hello로 합니다.

1. Hello 진단 이벤트 창을 자동으로 표시 되지 않습니다 toohello 전환 되는 경우 **보기** Visual Studio에서 탭을 선택 **다른 창** 차례로 **진단 이벤트 뷰어**합니다.
2. 각 이벤트에 hello 노드, 응용 프로그램 및 서비스 hello 이벤트에서 온 것인지를 알려 주는 표준 메타 데이터 정보입니다. Hello를 사용 하 여 hello 목록은 이벤트를 필터링 할 수도 있습니다 **이벤트를 필터링** hello 이벤트 창의 hello 상단 상자입니다. 예를 들어 **노드 이름**이나 **서비스 이름**으로 필터링할 수 있습니다. 이벤트 세부 정보를 찾고자 하는 경우 또한 놓으면 hello를 사용 하 여 및 **일시 중지** hello hello 이벤트 창 위쪽에 단추를 선택한 이벤트의 손실 없이 나중에 다시 시작 합니다.
   
   ![Visual Studio 진단 이벤트 뷰어](./media/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally/DiagEventsExamples2.png)

## <a name="add-your-own-custom-traces-toohello-application-code"></a>사용자 고유의 사용자 지정 추적은 toohello 응용 프로그램 코드를 추가 합니다.
hello 서비스 패브릭 Visual Studio 프로젝트 템플릿 샘플 코드가 들어 있습니다. hello 코드 방법을 tooadd 사용자 지정 응용 프로그램 코드 ETW 추적을 보여 주는를 서비스 패브릭에서 시스템 추적 함께 hello Visual Studio ETW 뷰어에서 보여 줍니다. hello이 방법의 장점은 메타 데이터는 tootraces, 자동으로 추가 하 고 Visual Studio 진단 이벤트 뷰어는 이미 hello 구성 toodisplay 해당 합니다.

Hello에서 만든 프로젝트에 대 한 **서비스 템플릿은** hello에 대 한 정당한 검색 (상태 비저장 또는 상태 저장) `RunAsync` 구현:

1. 호출을 너무 hello`ServiceEventSource.Current.ServiceMessage` hello에 `RunAsync` 메서드 hello 응용 프로그램 코드 로부터 사용자 정의 ETW 추적의 예를 보여 줍니다.
2. Hello에 **ServiceEventSource.cs** 파일인 hello에 대 한 오버 로드를 찾을 수 있습니다 `ServiceEventSource.ServiceMessage` tooperformance 이유로 인해 고주파 이벤트에 사용 해야 하는 메서드입니다.

Hello에서 만든 프로젝트에 대 한 **행위자 템플릿** (상태 비저장 또는 상태 저장):

1. 열기 hello **"ProjectName".cs** 파일 *p r o j* Visual Studio 프로젝트에 대해 선택한 hello 이름입니다.  
2. Hello 코드 찾기 `ActorEventSource.Current.ActorMessage(this, "Doing Work");` hello에 *DoWorkAsync* 메서드.  이는 응용 프로그램 코드에서 작성된 사용자 지정 ETW의 예제입니다.  
3. 파일에 **ActorEventSource.cs**, hello에 대 한 오버 로드를 찾을 수 있습니다 `ActorEventSource.ActorMessage` tooperformance 이유로 인해 고주파 이벤트에 사용 해야 하는 메서드입니다.

Tooyour 서비스 코드를 추적 하는 사용자 지정 ETW를 추가한 후 수 빌드, 배포 및 실행 hello 응용 프로그램 다시 toosee 진단 이벤트 뷰어 hello에 사용자 이벤트입니다. Hello 응용 프로그램을 디버깅 하는 경우 **F5**, hello 진단 이벤트 뷰어를 자동으로 열립니다.

## <a name="next-steps"></a>다음 단계
hello 동일한 추적 코드를 로컬 진단에 대 한 위의 tooyour 응용 프로그램 추가 작동할지 tooview를 사용할 수 있는 도구와 함께 Azure 클러스터에서 응용 프로그램을 실행할 때 이러한 이벤트입니다. Hello hello 도구에 대 한 다른 옵션에 설명 하 고를를 설정 하는 방법을 설명 하는 다음이 문서를 확인해 보세요.

* [Azure 진단으로 toocollect 기록 하는 방법](service-fabric-diagnostics-how-to-setup-wad.md)
* [EventFlow를 사용하여 이벤트 집계 및 수집](service-fabric-diagnostics-event-aggregation-eventflow.md)

