---
title: "aaaQuickly 기존 앱 tooan Azure 서비스 패브릭 클러스터를 배포 합니다."
description: "Visual Studio와 함께 Azure 서비스 패브릭 클러스터 toohost 기존 Node.js 응용 프로그램을 사용 합니다."
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a>Azure Service Fabric에서 Node.js 응용 프로그램 호스트

이 퀵 스타트를 사용 하면 Azure에서 실행 하는 기존 응용 프로그램 (이 예제의 Node.js) tooa 서비스 패브릭 클러스터를 배포할 수 있습니다.

## <a name="prerequisites"></a>필수 조건

시작하기 전에 [개발 환경을 설정](service-fabric-get-started.md)하도록 합니다. 포함 된 hello 서비스 패브릭 SDK 및 Visual Studio 2017 또는 2015를 설치 합니다.

또한 toohave 기존 Node.js 응용 프로그램 배포에 필요한 합니다. 이 빠른 시작은 [여기][download-sample]에서 다운로드할 수 있는 간단한 Node.js 웹 사이트를 사용합니다. 이 파일 tooyour 추출 `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` hello 다음 단계에서 hello 프로젝트를 만든 후 폴더입니다.

Azure 구독이 아직 없는 경우 [체험 계정][create-account]을 만듭니다.

## <a name="create-hello-service"></a>Hello 서비스 만들기

**관리자** 권한으로 Visual Studio를 시작합니다.

`CTRL`+`SHIFT`+`N`를 사용하여 프로젝트 만들기

Hello에 **새 프로젝트** 대화 상자에서 선택 **클라우드 > 서비스 패브릭 응용 프로그램**합니다.

Hello 응용 프로그램 이름을 **MyGuestApp** 누릅니다 **확인**합니다.

>[!IMPORTANT]
>Node.js는 hello 260 자까지 가능 windows에는 경로에 때 쉽게 중단 수입니다. 와 같은 hello 프로젝트 자체에 대 한 짧은 경로 사용 **c:\code\svc1**합니다.
   
![Visual Studio의 새 프로젝트 대화 상자][new-project]

Hello 다음 대화 상자에서 모든 유형의 서비스 패브릭 서비스를 만들 수 있습니다. 이 빠른 시작에서 **게스트 실행 파일**을 선택합니다.

Hello 서비스 이름을 **MyGuestService** hello 오른쪽 toohello에서 hello 옵션 설정에 따라 값:

| 설정                   | 값 |
| ------------------------- | ------ |
| 코드 패키지 폴더       | _&lt;Node.js 응용 프로그램과 함께 hello 폴더&gt;_ |
| 코드 패키지 동작     | 폴더 내용을 tooproject 복사 |
| 프로그램                   | node.exe |
| 인수                 | server.js |
| 작업 폴더            | CodePackage |

**확인**을 누릅니다.

![Visual Studio의 새 서비스 대화 상자][new-service]

Visual Studio hello 응용 프로그램 프로젝트 만들고 hello 행위자 서비스 프로젝트 및 솔루션 탐색기에 표시 합니다.

hello 응용 프로그램 프로젝트 (**MyGuestApp**) 코드는 직접 포함 하지 않습니다. 대신 서비스 프로젝트의 집합을 참조합니다. 추가로 3가지 다른 형식을 포함합니다.

* **게시 프로필**  
다양한 환경에 대한 도구 기본 설정입니다.

* **스크립트**  
응용 프로그램을 배포/업그레이드하기 위한 PowerShell 스크립트입니다.

* **응용 프로그램 정의**  
응용 프로그램 매니페스트 hello 포함 *ApplicationPackageRoot*합니다. 연결 된 응용 프로그램 매개 변수 파일이 *ApplicationParameters*, hello 응용 프로그램을 정의 하 고 tooconfigure를 사용 하는 지정된 된 환경에 대해 구체적으로 합니다.
    
Hello 서비스 프로젝트의 hello 내용에 대 한 개요를 참조 하십시오. [신뢰할 수 있는 서비스 시작](service-fabric-reliable-services-quick-start.md)합니다.

## <a name="set-up-networking"></a>네트워킹 설정

Node.js 응용 프로그램에서는 배포 하는 포트를 사용 하는 hello 예제 **80** tootell 해당 포트 표시 해야 하는 서비스 패브릭 필요 합니다.

열기 hello **ServiceManifest.xml** hello 프로젝트 파일에에서 있습니다. Hello 매니페스트의 hello 맨 아래에는 한 `<Resources> \ <Endpoints>` 이미 정의 된 항목이 들어 있는입니다. 해당 항목 tooadd 수정 `Port`, `Protocol`, 및 `Type`합니다. 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a>TooAzure 배포

키를 누르면 **F5** 배포 toohello 로컬 클러스터는 hello 프로젝트를 실행 합니다. 그러나 tooAzure를 대신 배포 해 보겠습니다.

Hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시...**  대화 toopublish tooAzure 열립니다.

![게시 서비스 패브릭 서비스에 대 한 tooazure 대화 상자][publish]

선택 hello **PublishProfiles\Cloud.xml** 프로필 대상으로 합니다.

이전에 하지 않은 경우에 Azure 계정 toodeploy를 선택 합니다. 아직 없는 경우 [하나에 등록][create-account]합니다.

아래 **연결 끝점**를 선택 하려면 서비스 패브릭 클러스터 toodeploy hello 합니다. 선택 하지 않은 경우 하나를  **&lt;새 클러스터 만들기... &gt;**  웹 브라우저 창 toohello Azure 포털을 열립니다. 자세한 내용은 참조 [hello 포털에서 클러스터 만들기](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal)합니다. 

Hello 서비스 패브릭 클러스터를 만들 때 확인 되었는지 tooset hello **사용자 지정 끝점** 너무 설정**80**합니다.

![사용자 지정 끝점이 있는 Service Fabric 노드 형식 구성][custom-endpoint]

새 서비스 패브릭 클러스터를 만드는 데 몇 시간 toocomplete 걸립니다. 생성 된, 이동 백 toohello 게시 대화 상자 및 선택 경과 했는데도 문제가 있다면 되 면  **&lt;새로 고침&gt;**합니다. 새 클러스터 hello hello 드롭다운 목록 상자에 나열 됩니다. 선택 합니다.

키를 눌러 **게시** hello 배포 toofinish 될 때까지 기다립니다.

몇 분이 걸릴 수 있습니다. 완료 되 면 hello 응용 프로그램 toobe 완벽 하 게 사용할 수에 대 일 분 걸릴 수 있습니다.

## <a name="test-hello-website"></a>테스트 hello 웹 사이트

서비스가 게시된 후에 웹 브라우저에서 테스트합니다. 

서비스 패브릭 서비스를 찾을 hello Azure 포털을 열고 먼저 합니다.

Hello 개요 블레이드에 hello 서비스 주소를 확인 합니다. Hello에서 사용 하 여 hello 도메인 이름 _클라이언트 연결 끝점_ 속성입니다. 예: `http://mysvcfab1.westus2.cloudapp.azure.com`.

![서비스 패브릭 개요 블레이드에 hello Azure 포털에서][overview]

Hello 나타납니다 toothis 주소 이동 `HELLO WORLD` 응답 합니다.

## <a name="delete-hello-cluster"></a>Hello 클러스터를 삭제 합니다.

이러한 리소스에 대 한 요금이 청구 됩니다 때이 퀵 스타트를 만든 후 hello 리소스를 모두 toodelete를 잊지 마십시오.

## <a name="next-steps"></a>다음 단계
[게스트 실행 파일](service-fabric-deploy-existing-app.md)에 대해 자세히 알아보세요.

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F