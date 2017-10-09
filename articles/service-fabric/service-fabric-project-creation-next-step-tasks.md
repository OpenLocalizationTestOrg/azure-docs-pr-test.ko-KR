---
title: "aaaService 패브릭 프로젝트 생성 다음 단계 | Microsoft Docs"
description: "서비스 패브릭 용 핵심 개발 작업의 링크 tooa 집합을 포함 하는이 문서"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 45598bfabedf280fba8af449ef920f40b409a609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a>서비스 패브릭 응용 프로그램 및 다음 단계
Azure 서비스 패브릭 응용 프로그램이 만들어졌습니다. 이 문서에는 몇 가지 잠재적인 다음 단계와 프로젝트의 hello 구성을 설명 합니다.

## <a name="your-application"></a>응용 프로그램
모든 새 응용 프로그램에는 응용 프로그램 프로젝트가 포함되어 있습니다. 선택한 서비스의 hello 유형에 따라 하나 또는 두 개의 추가 프로젝트 있을 수 있습니다.

### <a name="hello-application-project"></a>hello 응용 프로그램 프로젝트
hello 응용 프로그램 프로젝트 이루어져 있습니다.

* 응용 프로그램을 구성 하는 toohello 서비스 참조의 집합입니다.
* 3 개의 게시 프로필 (1 개 노드 로컬, 5 노드 로컬 및 클라우드) toomaintain 설정을 기본 설정 관련된 tooa 클러스터 끝점 및 tooperform 기본적으로 배포를 업그레이드 하는 여부와 같은 다른 환경-작업을 사용할 수 있습니다.
* 세 개의 응용 프로그램 매개 변수 파일 (위 항목과 동일) 서비스에 대 한 파티션 toocreate hello 수와 같이 toomaintain 환경 관련 응용 프로그램 구성을 사용할 수 있습니다.
* 사용할 수 있는 toodeploy hello 명령줄에서 또는 자동화 된 연속 통합 및 배포 파이프라인의 일부로 응용 프로그램 배포 스크립트입니다.
* hello 응용 프로그램 매니페스트 hello 응용 프로그램에 설명 합니다. Hello ApplicationPackageRoot 폴더 hello 매니페스트를 찾을 수 있습니다.

### <a name="stateless-service"></a>상태 비저장 서비스
새 상태 비저장 서비스를 추가 하면 Visual Studio에서 하위 유형을 포함 하는 서비스 프로젝트 tooyour 솔루션 추가 `StatelessService`합니다. hello 서비스 카운터의 지역 변수를 증가 시킵니다.

### <a name="stateful-service"></a>상태 저장 서비스
새 상태 저장 서비스를 추가 하면 Visual Studio에서 하위 유형을 포함 하는 서비스 프로젝트 tooyour 솔루션 추가 `StatefulService`합니다. hello 서비스 카운터를 증가 시키는에 해당 `RunAsync` 메서드 및 저장소 hello 결과에 `ReliableDictionary`합니다.

### <a name="actor-service"></a>행위자 서비스
새 신뢰할 수 있는 작업자를 추가 하면 Visual Studio에서는 두 개의 프로젝트 tooyour 솔루션 추가: 행위자 프로젝트 및 인터페이스 프로젝트.

hello 행위자 프로젝트 설정에 대 한 메서드를 제공 하 고 hello 카운터 값을 가져오는 hello 행위자 상태 내에서 안정적으로 유지 됩니다. hello 인터페이스 프로젝트 인터페이스는 다른 서비스 제공 tooinvoke hello 행위자를 사용할 수 있습니다.

### <a name="stateless-web-api"></a>상태 비저장 웹 API
hello 상태 비저장 웹 API 프로젝트는 기본 제공 웹 서비스를 사용할 수 있는 tooopen tooexternal 클라이언트 응용 프로그램입니다. Hello 프로젝트 구성 방법에 대 한 자세한 내용은 참조 [OWIN 자체 호스트 된 서비스 패브릭 웹 API 서비스](service-fabric-reliable-services-communication-webapi.md)합니다.


### <a name="aspnet-core"></a>ASP.NET core
서비스 패브릭 SDK hello 제공 독립 실행형 ASP.NET Core 프로젝트에 사용할 수 있는 ASP.NET Core 서식 파일의 설정 같은 hello: 비어 있는 경우 [웹 API][aspnet-webapi], 및 [웹 응용 프로그램][aspnet-webapp].

### <a name="guest-executables-and-guest-containers"></a>게스트 실행 파일 및 게스트 컨테이너

서비스 패브릭은 'guest' hello 플랫폼의 프로그래밍 모델을 기본 제공 되지 않는 하는 서비스입니다. 게스트에 대 한 hello 바이너리 하거나 패키지 [hello 응용 프로그램 패키지에 직접](service-fabric-deploy-existing-app.md) 또는 [컨테이너 이미지를 통해](service-fabric-deploy-container.md)합니다. 두 경우 모두 Visual Studio 만듭니다 hello hello에 필요한 아티팩트 **ApplicationPackageRoot** hello 응용 프로그램 프로젝트의 폴더입니다. Visual Studio hello 코드는 이미 다른 곳에서 존재 하므로 새 서비스 프로젝트가 만들어집니다. 게스트 hello 서비스 패브릭 응용 프로그램 프로젝트와 함께 프로젝트 toomanage를 원하는 경우 추가할 수 있습니다 toohello 같은 Visual Studio 솔루션입니다.

## <a name="next-steps"></a>다음 단계
### <a name="create-an-azure-cluster"></a>Azure 클러스터 만들기
서비스 패브릭 SDK hello 개발 및 테스트에 대 한 로컬 클러스터를 제공합니다. Azure에서 클러스터 toocreate 참조 [hello Azure 포털에서에서 서비스 패브릭 클러스터를 설정할][create-cluster-in-portal]합니다.

### <a name="publish-your-application-tooazure"></a>응용 프로그램 tooAzure 게시
Visual Studio tooan Azure 클러스터에서 직접 응용 프로그램을 게시할 수 있습니다. toolearn를 확인 하려면 어떻게 해야 [응용 프로그램 tooAzure 게시][publish-app-to-azure]합니다.

### <a name="use-service-fabric-explorer-toovisualize-your-cluster"></a>클러스터 서비스 패브릭 탐색기 toovisualize를 사용 합니다.
서비스 패브릭 탐색기 클러스터에 배포 된 응용 프로그램 및 물리적 레이아웃을 포함 하 여 쉽게 toovisualize를 제공 합니다. toolearn 더 참조 [서비스 패브릭 탐색기를 사용 하 여 클러스터 시각화][visualize-with-sfx]합니다.

### <a name="version-and-upgrade-your-services"></a>서비스 버전 관리 및 업그레이드
서비스 패브릭을 통해 응용 프로그램에서 독립적인 서비스의 버전 관리 및 업그레이드를 수행할 수 있습니다. toolearn 더 참조 [버전 관리 및 서비스 업그레이드][app-upgrade-tutorial]합니다.

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a>Visual Studio Team Services를 사용하여 지속적인 통합 구성
toolearn 서비스 패브릭 응용 프로그램에 대 한 연속 통합 프로세스를 설정할 수 있습니다 참조 [Visual Studio Team Services와 연속 통합을 구성][ci-with-vso]합니다.

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
