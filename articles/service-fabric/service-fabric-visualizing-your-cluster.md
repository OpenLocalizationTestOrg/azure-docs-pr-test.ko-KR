---
title: "aaaVisualizing 서비스 패브릭 탐색기를 사용 하 여 클러스터 | Microsoft Docs"
description: "서비스 패브릭 탐색기는 Microsoft Azure 서비스 패브릭 클러스터에서 클라우드 응용 프로그램 및 노드를 검사 및 관리하기 위한 웹 기반 도구입니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a>서비스 패브릭 탐색기로 클러스터 시각화
서비스 패브릭 탐색기는 Azure 서비스 패브릭 클러스터에서 응용 프로그램 및 노드를 검사 및 관리하기 위한 웹 기반 도구입니다. 서비스 패브릭 탐색기 클러스터 실행 되 고 있는 관계 없이 사용할 수는 항상 hello 클러스터 내에서 직접 호스트 됩니다.

## <a name="video-tutorial"></a>비디오 자습서

서비스 패브릭 탐색기 toouse 시청 어떻게 toolearn Microsoft Virtual Academy 비디오 다음 hello:

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a>TooService 패브릭 탐색기를 연결 합니다.
너무 hello 지시를 따른 경우[개발 환경을 준비](service-fabric-get-started.md), toohttp://localhost:19080 이동 하 여 로컬 클러스터에 대해 서비스 패브릭 탐색기를 시작할 수 있습니다 / 탐색기.

## <a name="understand-hello-service-fabric-explorer-layout"></a>서비스 패브릭 탐색기 레이아웃 hello 이해
서비스 패브릭 탐색기 hello 왼쪽에 hello 트리를 사용 하 여 탐색할 수 있습니다. Hello hello 트리의 루트에 hello 클러스터 대시보드는 응용 프로그램 및 노드 상태 요약을 포함 하 여 클러스터에 대 한 개요를 제공 합니다.

![서비스 패브릭 탐색기 클러스터 대시보드][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a>Hello 클러스터의 레이아웃을 보려면
서비스 패브릭 클러스터의 노드는 장애 도메인 및 업그레이드 도메인의 2차원 그리드에 배치됩니다. 이 배치 응용 프로그램의 하드웨어 오류 및 응용 프로그램 업그레이드 hello 현재 상태에서 사용할 수 있는 남아 있는지 확인 합니다. Hello 클러스터 맵을 사용 하 여 hello 현재 클러스터 레이아웃 방법을 볼 수 있습니다.

![서비스 패브릭 탐색기 클러스터 맵][sfx-cluster-map]

### <a name="view-applications-and-services"></a>응용 프로그램 및 서비스 보기
hello 클러스터에 두 개의 하위: 응용 프로그램 및 노드 관리를 위한 하나 있습니다.

서비스 패브릭의 논리적 계층 구조를 통해 응용 프로그램 보기 toonavigate hello를 사용할 수 있습니다: 응용 프로그램, 서비스, 파티션 및 복제본입니다.

Hello 아래의 예제에서는 응용 프로그램을 hello **MyApp** 두 서비스의 구성 **MyStatefulService** 및 **WebService**합니다. **MyStatefulService** 는 상태 저장이므로 한 개의 주 복제본과 두 개의 보조 복제본이 있는 파티션을 포함합니다. 이와 반대로 WebSvcService는 상태 비저장이며 단일 인스턴스가 들어 있습니다.

![서비스 패브릭 탐색기 응용 프로그램 보기][sfx-application-tree]

Hello 트리의 각 수준 hello 주 창 hello 항목에 대 한 관련 정보를 표시 합니다. 예를 들어 hello 상태 및 특정 서비스에 대 한 버전을 볼 수 있습니다.

![서비스 패브릭 탐색기 기능 창][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a>Hello 클러스터의 노드를 확인
hello 노드 보기 hello hello 클러스터의 실제 레이아웃을 표시합니다. 지정된 노드의 경우 해당 노드에 배포된 코드를 가진 응용 프로그램을 검사할 수 있습니다. 특히 현재 실행되고 있는 복제본을 확인할 수 있습니다.

## <a name="actions"></a>작업
서비스 패브릭 탐색기 신속 하 게 tooinvoke 노드, 응용 프로그램 및 클러스터 서비스에 대 한 작업을 제공합니다.

예를 들어 toodelete 응용 프로그램 인스턴스 hello 응용 프로그램 hello 왼쪽에 hello 트리에서 선택한 다음 선택 **동작** > **응용 프로그램 삭제**합니다.

![서비스 패브릭 탐색기에서 응용 프로그램 삭제][sfx-delete-application]

> [!TIP]
> 수행할 수 있습니다 hello 줄임표 다음 tooeach 요소를 클릭 하 여 동일한 작업을 hello 합니다.
>
>

hello 다음 표에 각 엔터티에 대해 사용할 수 있는 hello 작업.

| **엔터티** | **작업** | **설명** |
| --- | --- | --- |
| 응용 프로그램 형식 |프로 비전 해제 형식 |Hello 클러스터 이미지 저장소에서 hello 응용 프로그램 패키지를 제거합니다. 모든 응용 프로그램의 해당 형식 toobe 먼저 제거 해야 합니다. |
| 응용 프로그램 |응용 프로그램 삭제 |(있는 경우) 모든 서비스와 해당 상태를 포함 하 여 hello 응용 프로그램을 삭제 합니다. |
| 부여 |서비스 삭제 |(있는 경우) hello 서비스 및 해당 상태를 삭제 합니다. |
| 노드 |활성화 |Hello 노드를 활성화 합니다. |
| 노드 | 비활성화(일시 중지) | 현재 상태의 hello 노드를 일시 중지 합니다. 서비스 계속 toorun 하지만 서비스 패브릭 이동 하지 않습니다 사전 아무 것도으로 끌거나 것 필요한 tooprevent 가동 중단 또는 데이터 불일치가 아닌 경우. 이 작업은 일반적으로 사용 되는 tooenable 검사 하는 동안 이동 하지 않는 특정 노드 tooensure에서 서비스를 디버깅 합니다. | |
| 노드 | 비활성화(다시 시작) | 안전하게 노드에서 모든 메모리 내 서비스를 이동하고 영구 서비스를 닫습니다. 일반적으로 컴퓨터 필요 toobe 또는 hello 호스트 프로세스 다시 시작 될 때 사용 합니다. | |
| 노드 | 비활성화(데이터 제거) | 안전 하 게 충분 한 예비 복제본을 빌드한 후 hello 노드에서 실행 되는 모든 서비스를 닫습니다. 노드(또는 최소한 저장소)가 위원회에서 영구적으로 제거될 때 일반적으로 사용됩니다. | |
| 노드 | 노드 상태 제거 | Hello 클러스터에서 기술 노드의 복제본을 제거 합니다. 이미 실패한 노드를 복구할 수 없다고 간주하는 경우 일반적으로 사용됩니다. | |
| 노드 | 다시 시작 | Hello 노드를 다시 시작 하 여 노드 오류를 시뮬레이트하십시오. 자세한 내용은 [여기](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)를 참조하세요. | |

파괴적 많은 작업 이므로 수 전에 질문을 tooconfirm 의도 했던 hello 동작이 완료 합니다.

> [!TIP]
> 서비스 패브릭 탐색기를 통해 수행할 수 있는 모든 작업은 PowerShell 또는 REST API를 tooenable 자동화를 통해 수행할 수도 있습니다.
>
>

또한 특정된 응용 프로그램 유형 및 버전에 대 한 서비스 패브릭 탐색기 toocreate 응용 프로그램 인스턴스를 사용할 수 있습니다. Hello 트리 뷰에서 hello 응용 프로그램 유형을 선택 하 고 hello 클릭 **앱 인스턴스 만들기** hello 오른쪽 창에서 원하는 링크 다음 toohello 버전입니다.

![Service Fabric Explorer에서 응용 프로그램 인스턴스 만들기][sfx-create-app-instance]

> [!NOTE]
> Service Fabric Explorer를 통해 만든 응용 프로그램 인스턴스는 현재 매개 변수화될 수 없습니다. 이러한 프로그램은 기본 매개 변수 값을 사용하여 만들어집니다.
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a>Tooa 원격 서비스 패브릭 클러스터에 연결
Hello 클러스터 끝점을 알고 있고 충분 한 권한이 있으면 모든 브라우저에서 서비스 패브릭 탐색기를 액세스할 수 있습니다. 서비스 패브릭 탐색기는 hello 클러스터에서 실행 되는 또 다른 서비스 때문입니다.

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a>원격 클러스터에 대 한 hello 서비스 패브릭 탐색기 끝점을 검색
서비스 패브릭 탐색기 tooreach 특정된 클러스터에 대 한 브라우저를 가리킵니다.

http://&lt;your-cluster-endpoint&gt;:19080/Explorer

Azure의 클러스터에 대 한 전체 URL hello hello Azure 포털의 hello 클러스터 essentials 창에서 사용할 수도 있습니다.

### <a name="connect-tooa-secure-cluster"></a>Tooa 보안 클러스터에 연결
인증서 또는 Azure Active Directory (AAD)를 사용 하 여 사용 하 여 클라이언트 액세스 tooyour 서비스 패브릭 클러스터를 제어할 수 있습니다.

Tooconnect tooService 패브릭 탐색기 보안 클러스터에서 사용 하려는 경우 한 다음 hello 클러스터 구성에 따라 됩니다 클라이언트 인증서 필요 toopresent 여야 하거나 AAD를 사용 하 여 로그인 합니다.

## <a name="next-steps"></a>다음 단계
* [테스트 용이성 개요](service-fabric-testability-overview.md)
* [Visual Studio에서 서비스 패브릭 응용 프로그램 관리](service-fabric-manage-application-in-visual-studio.md)
* [PowerShell을 사용하여 서비스 패브릭 응용 프로그램 배포](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
