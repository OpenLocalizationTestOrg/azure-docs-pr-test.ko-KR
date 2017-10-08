---
title: "aaaCreate C#과 함께 사용 되는 Azure 서비스 패브릭 신뢰할 수 있는 서비스"
description: "Visual Studio를 사용하여 Azure Service Fabric을 기반으로 하는 Reliable Service 응용 프로그램을 만들고, 배포하고, 디버깅합니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a>첫 번째 C# Service Fabric 상태 저장 Reliable Services 응용 프로그램 만들기

자세한 내용은 방법 toodeploy 첫 번째 서비스 패브릭 응용 프로그램을 Windows에서.NET 단 몇 분 후에 있습니다. 완료된 경우 로컬 클러스터가 Reliable Service 응용 프로그램과 실행됩니다.

## <a name="prerequisites"></a>필수 조건

시작하기 전에 [개발 환경을 설정](service-fabric-get-started.md)하도록 합니다. 여기에 hello 서비스 패브릭 SDK 및 Visual Studio 2017 또는 2015를 설치 합니다.

## <a name="create-hello-application"></a>Hello 응용 프로그램 만들기

**관리자** 권한으로 Visual Studio를 시작합니다.

`CTRL`+`SHIFT`+`N`를 사용하여 프로젝트 만들기

Hello에 **새 프로젝트** 대화 상자에서 선택 **클라우드 > 서비스 패브릭 응용 프로그램**합니다.

Hello 응용 프로그램 이름을 **MyApplication** 누릅니다 **확인**합니다.

   
![Visual Studio의 새 프로젝트 대화 상자][1]

Hello 다음 대화 상자에서 모든 유형의 서비스 패브릭 응용 프로그램을 만들 수 있습니다. 이 빠른 시작에서 **상태 저장 서비스**를 선택합니다.

Hello 서비스 이름을 **MyStatefulService** 누릅니다 **확인**합니다.

![Visual Studio의 새 서비스 대화 상자][2]


Visual Studio hello 응용 프로그램 프로젝트 만들고 hello 상태 저장 서비스 프로젝트 및 솔루션 탐색기에 표시 합니다.

![상태 저장 서비스를 사용하여 응용 프로그램 만들기를 수행하는 솔루션 탐색기][3]

hello 응용 프로그램 프로젝트 (**MyApplication**) 코드는 직접 포함 하지 않습니다. 대신 서비스 프로젝트의 집합을 참조합니다. 추가로 3가지 다른 형식을 포함합니다.

* **게시 프로필**  
Toodifferent 환경 배포에 대 한 프로필입니다.

* **스크립트**  
응용 프로그램을 배포/업그레이드하기 위한 PowerShell 스크립트입니다.

* **응용 프로그램 정의**  
Hello ApplicationManifest.xml 파일에서 포함 *ApplicationPackageRoot* 설명 하는 응용 프로그램의 컴퍼지션입니다. 아래에서 관련된 응용 프로그램 매개 변수 파일은 *ApplicationParameters*역할 환경 관련 매개 변수로 사용 되는 toospecify를 지정할 수 있습니다. Visual Studio가 선택 되어 hello에 지정 된 응용 프로그램 매개 변수 파일에 연결 된 게시 프로필 배포 tooa 특정 환경 중.
    
Hello 서비스 프로젝트의 hello 내용에 대 한 개요를 참조 하십시오. [신뢰할 수 있는 서비스 시작](service-fabric-reliable-services-quick-start.md)합니다.

## <a name="deploy-and-debug-hello-application"></a>배포 및 hello 응용 프로그램 디버깅

이제 응용 프로그램이 설치되었으니 실행합니다.

키를 눌러 Visual Studio에서 `F5` toodeploy hello 응용 프로그램을 디버깅 합니다.

>[!NOTE]
>hello 처음으로 실행 하 고 hello 응용 프로그램 배포를 로컬로 Visual Studio 디버깅에 대 한 로컬 클러스터를 만듭니다. 다소 시간이 걸릴 수 있습니다. hello 클러스터 만들기 상태 hello Visual Studio 출력 창에 표시 됩니다.

Hello 클러스터 준비 되 면 hello 로컬 클러스터 시스템 트레이 관리자 응용 프로그램 으로부터 hello SDK에 포함 된 알림을 받게 됩니다.
   
![로컬 클러스터 시스템 트레이 알림][4]

한 번 hello 응용 프로그램이 시작 Visual Studio 자동으로 표시 hello **진단 이벤트 뷰어**서비스에서 추적 출력을 볼 수 있습니다.
   
![진단 이벤트 뷰어][5]

hello 사용 하는 상태 저장 서비스 템플릿을 보여 줍니다 hello에 카운터 값 증분 `RunAsync` 방식의 **MyStatefulService.cs**합니다.

Hello 코드가 실행 되 고 hello 노드를 포함 한 자세한 정보를 hello 이벤트 toosee 중 하나를 확장 합니다. 이 경우에 \_Node\_2이지만 컴퓨터에서 달라질 수 있습니다.
   
![진단 이벤트 뷰어 세부 정보][6]

hello 로컬 클러스터에는 단일 컴퓨터에서 호스트 되는 5 개의 노드가 포함 됩니다. 프로덕션 환경에서 각 노드는 고유한 물리적 컴퓨터 또는 가상 컴퓨터에서 호스팅됩니다. hello에서 toosimulate hello 손실 hello Visual Studio를 실행 하는 동안 컴퓨터의 디버거 같은 시간, hello 로컬 클러스터에 있는 hello 노드 중 하나를 살펴보겠습니다.

Hello에 **솔루션 탐색기** 창을 열어 **MyStatefulService.cs**합니다. 

Hello `RunAsync` 메서드와 hello hello 메서드의 첫 번째 줄에 중단점을 설정 합니다.

![상태 저장 서비스 RunAsync 메서드의 중단점][7]

Hello 시작 **서비스 패브릭 탐색기** hello를 마우스 오른쪽 단추로 클릭 하 여 도구 **로컬 클러스터 관리자** 시스템 트레이 응용 프로그램을 선택 하 고 **로컬 클러스터 관리**합니다.

![Hello 로컬 클러스터 관리자에서에서 서비스 패브릭 탐색기를 실행 합니다.][systray-launch-sfx]

[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md)는 클러스터의 시각적 표현을 제공합니다. 배포 된 응용 프로그램 tooit 집합이 hello 및 hello 구성 하는 실제 노드 집합이 포함 됩니다.

Hello 왼쪽된 창에서 **클러스터 > 노드** 및 코드를 실행 하는 찾기 hello 노드.

클릭 **작업 > 비활성화 (다시 시작)** toosimulate 컴퓨터 다시 시작 합니다.

![서비스 패브릭 탐색기에서 노드 중지][sfx-stop-node]

중단점을 일시적으로 표시 되어야 tooanother로 장애 조치를 수행 하 고 한 노드에서 원활 하 게 hello 계산 하는 대로 Visual Studio에서 적중 합니다.


다음을 toohello 진단 이벤트 뷰어를 반환 하 고 hello 메시지를 관찰 합니다. hello 카운터 지속적 증가 hello 이벤트가 실제로 다른 노드에서 들어오는 경우에 있습니다.

![장애 조치 후 진단 이벤트 뷰어][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a>(옵션) 로컬 클러스터 hello 정리

이 로컬 클러스터는 실제입니다. Hello 디버거를 중지 합니다. 응용 프로그램 인스턴스를 제거 하 고 hello 응용 프로그램 종류의 등록을 취소 합니다. 그러나 hello 클러스터 toorun hello 백그라운드에서 계속 됩니다. 준비 toostop hello 로컬 클러스터를 사용 하는 경우에 몇 가지 옵션이 있습니다.

### <a name="keep-application-and-trace-data"></a>응용 프로그램 및 추적 데이터 유지

Hello를 마우스 오른쪽 단추로 클릭 하 여 hello 클러스터를 종료 **로컬 클러스터 관리자** 시스템 트레이 응용 프로그램 선택 **로컬 클러스터 중지**합니다.

### <a name="delete-hello-cluster-and-all-data"></a>Hello 클러스터 및 모든 데이터 삭제

Hello를 마우스 오른쪽 단추로 클릭 하 여 hello 클러스터를 제거 **로컬 클러스터 관리자** 시스템 트레이 응용 프로그램 선택 **로컬 클러스터 제거**합니다. 

이 옵션을 선택 하면 다음 번 실행 하면 응용 프로그램 hello Visual Studio hello 클러스터 hello를 재배포 됩니다. 일정 시간 동안 toouse hello 로컬 클러스터 않으려는 경우 또는 tooreclaim 리소스가 필요한 경우이 옵션을 선택 합니다.

## <a name="next-steps"></a>다음 단계
[Reliable Services](service-fabric-reliable-services-introduction.md)에 대해 자세히 알아보세요.
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
