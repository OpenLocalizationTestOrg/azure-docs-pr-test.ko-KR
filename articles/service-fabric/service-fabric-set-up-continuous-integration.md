---
title: "Azure microservices에 대 한 연속 통합을 aaaSet | Microsoft Docs"
description: "가져오기 방법의 개요 tooset 연속 통합 및 VSTS Visual Studio Team Services ()를 사용 하 여 서비스 패브릭 응용 프로그램에 대 한 배포를 구성 합니다."
services: service-fabric
documentationcenter: na
author: mthalman-msft
manager: timlt
editor: 
ms.assetid: 3e8c2290-9e7a-456a-9b2c-db44d1b3988d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 12/06/2016
ms.author: mthalman;mikhegn
ms.openlocfilehash: 041e081f4a42f379394f2d21f07db4f6de045b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-service-fabric-continuous-integration-and-deployment-with-visual-studio-team-services"></a>Visual Studio Team Services로 Service Fabric 연속 통합 및 배포 설정
이 문서에서는 Visual Studio Team Services VSTS ()를 사용 하 여 hello 단계 tooset 연속 통합 및 Azure 서비스 패브릭 응용 프로그램에 대 한 배포를 설명 합니다.

이 문서 hello 현재 프로시저 반영 되며 시간에 따라 예상된 toochange 있습니다.

## <a name="prerequisites"></a>필수 조건
시작 tooget 다음이 단계를 따르십시오.

1. 액세스 tooa Team Services 계정이 있는지 확인 하거나 [만드세요](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services) 직접 합니다.
2. Access tooa Team Services 팀 프로젝트를 해야 또는 [만드세요](https://www.visualstudio.com/docs/setup-admin/create-team-project) 자신입니다.
3. 서비스 패브릭 클러스터 toowhich 응용 프로그램을 배포 하거나 하나를 만들 수 있는지 확인 hello를 사용 하 여 [Azure 포털](service-fabric-cluster-creation-via-portal.md), [Azure 리소스 관리자 템플릿](service-fabric-cluster-creation-via-arm.md), 또는 [Visual Studio ](service-fabric-cluster-creation-via-visual-studio.md).
4. 서비스 패브릭 응용 프로그램(.sfproj) 프로젝트를 이미 만들었는지 확인합니다. 프로젝트를 만들거나 업그레이드 서비스 패브릭 SDK 2.1 이상 있어야 합니다 (hello.sfproj 파일 1.1 이상의 ProjectVersion 속성 값이 포함 되어야) 합니다.

> [!NOTE]
> 사용자 지정 빌드 에이전트는 더 이상 필요하지 않습니다. Team Services 호스트 에이전트는 이제 서비스 패브릭 클러스터 관리 소프트웨어가 미리 설치된 상태로 제공되므로 해당 에이전트에서 직접 응용 프로그램을 배포할 수 있습니다.
> 
> 

## <a name="configure-and-share-your-source-files"></a>소스 파일 구성 및 공유
hello 먼저 toodo은 원하는 Team Services 내에서 실행 되는 hello 배포 프로세스에서 사용 하기 위해 게시 프로필을 준비 합니다.  게시 프로필 hello 이전에 준비한 구성된 tootarget hello 클러스터 여야 합니다.

1. 연속 통합 워크플로에 대 한 toouse 되도록 응용 프로그램 프로젝트 내에서 게시 프로필을 선택 합니다. Hello에 따라 [게시 지침](service-fabric-publish-app-remote-cluster.md) 방법에는 응용 프로그램 tooa 원격 클러스터 toopublish 합니다. 실제로 않아도 toopublish 응용 프로그램 이지만 됩니다. Hello를 클릭할 수 있는 **저장** 적절 하 게 작업을 구성 했으면 hello에 대 한 하이퍼링크 게시 대화 상자.
2. 원하는 tooconfigure hello 프로그램 응용 프로그램 toobe Team Services 내에서 발생 하는 각 배포에 대 한 업그레이드 하려는 경우 프로필 tooenable 업그레이드를 게시 합니다. 1 단계에서 사용 되는 대화를 게시 동일 hello, 해당 hello 확인 **업그레이드 hello 응용 프로그램** 확인란이 선택 되어 있습니다.  [추가 업그레이드 설정 구성](service-fabric-visualstudio-configure-upgrade.md)에 대해 더 자세히 알아봅니다. Hello 클릭 **저장** 하이퍼링크 toosave hello 설정 toohello 게시 프로필.
3. Toohello 게시 변경 내용을 프로필을 저장 하 고 hello 취소 게시 대화 상자.
4. 이제 너무[응용 프로그램 프로젝트 소스 파일을 공유](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#vs) Team Services를 통해 합니다. 소스 파일을 Team Services에 액세스할 수 없으므로 되 면 이제 toohello 빌드 생성의 다음 단계에 이동할 수 있습니다. 

## <a name="create-a-build-definition"></a>빌드 정의 만들기
Team Services 빌드 정의는 순차적으로 실행되는 빌드 단계 집합으로 구성된 워크플로를 설명합니다. 만들고 있는 hello 빌드 정의의 hello 목표 tooproduce 서비스 패브릭 응용 프로그램 패키지 및 사용 되는 toodeploy hello 응용 프로그램 일 수 있는 기타 아티팩트를입니다. Team Services [빌드 정의](https://www.visualstudio.com/docs/build/define/create)에 대해 자세히 알아봅니다.

### <a name="create-a-definition-from-hello-build-template"></a>Hello 빌드 템플릿에서 정의 만들기
1. Visual Studio Team Services에서 팀 프로젝트를 엽니다.
2. 선택 hello **빌드** 탭 합니다.
3. 선택 hello 녹색  **+**  toocreate 새 빌드 정의 등록 합니다.
4. Hello 대화 상자가 열리면 선택 **Azure 서비스 패브릭 응용 프로그램** hello 내 **빌드** 템플릿 범주입니다.
5. **다음**을 선택합니다.
6. Hello 리포지토리와 서비스 패브릭 응용 프로그램과 연결 된 분기를 선택 합니다.
7. 원하는 toouse hello 에이전트 큐를 선택 합니다. 호스트 에이전트가 지원됩니다.
8. **만들기**를 선택합니다.
9. Hello 빌드 정의 저장 하 고 이름을 제공 합니다.
10. hello 다음 단락은 hello 템플릿에서 생성 하는 hello 빌드 단계에 대 한 설명을:

| 빌드 단계 | 설명 |
| --- | --- |
| NuGet 복원 |Hello 솔루션에 대 한 hello NuGet 패키지를 복원합니다. |
| 솔루션 \*.sln 빌드 |Hello 전체 솔루션을 빌드합니다. |
| 솔루션 \*.sfproj 빌드 |Hello 서비스 패브릭 응용 프로그램 패키지를 사용 하는 toodeploy hello 응용 프로그램을 생성 합니다. hello 응용 프로그램 패키지 위치는 hello 빌드 아티팩트 디렉터리 내에서 지정 된 toobe입니다. |
| 서비스 패브릭 앱 버전 업데이트 |업그레이드 지원에 대 한 매니페스트 파일 tooallow hello 응용 프로그램 패키지에에서 포함 된 hello 버전 값을 업데이트 합니다. Hello 참조 [작업 설명서 페이지](https://go.microsoft.com/fwlink/?LinkId=820529) 자세한 정보에 대 한 합니다. |
| 파일 복사 |복사본 hello 프로필 및 배포에 사용 된 응용 프로그램 매개 변수 파일 toohello 빌드 아티팩트 toobe 게시 합니다. |
| 아티팩트 게시 |Hello 빌드 아티팩트 게시합니다. 릴리스 정의 tooconsume hello 빌드 아티팩트를 허용합니다. |

### <a name="verify-hello-default-set-of-tasks"></a>작업의 기본 집합 hello를 확인 합니다.
1. Hello 확인 **솔루션** hello에 대 한 입력된 필드 **NuGet 복원** 및 **솔루션 빌드** 빌드 단계입니다.  기본적으로 다음의 빌드 단계 hello 연결 된 저장소에 포함 된 모든 솔루션 파일을 실행 합니다.  이러한 솔루션 파일 중 하나에 hello 빌드 정의 toooperate만 하려는 경우 tooexplicitly 업데이트 hello 경로 toothat 파일이 필요 합니다.
2. Hello 확인 **솔루션** hello에 대 한 입력된 필드 **응용 프로그램 패키지** 빌드 단계입니다.  기본적으로이 빌드 단계 hello 리포지토리에 서비스 패브릭 응용 프로그램 프로젝트 (.sfproj)를 하나만 있다고 가정 합니다.  이러한 여러 파일 저장소에 있고 둘 중 하나만 tootarget이 빌드 정의 대 한, tooexplicitly 업데이트 hello 경로 toothat 파일이 필요 합니다.  저장소에서 여러 응용 프로그램 프로젝트 toopackage 하려는 경우 필요한 toocreate 추가 **Visual Studio 빌드** 응용 프로그램 프로젝트를 대상 각각 hello 빌드 정의의 단계입니다.  다음도 필요 tooupdate hello **MSBuild 인수** 이들의 각 필드 빌드 단계 hello 패키지 위치는 각 끝점에 고유 합니다.
3. Hello에 정의 된 hello 버전 관리 동작을 확인할 **업데이트 서비스 패브릭 응용 프로그램 버전** 빌드 단계입니다.  기본적으로이 빌드 단계 hello 빌드 번호 tooall 버전 값 hello 응용 프로그램 패키지의 매니페스트 파일에 추가합니다. Hello 참조 [작업 설명서 페이지](https://go.microsoft.com/fwlink/?LinkId=820529) 자세한 정보에 대 한 합니다. 이 각 업그레이드 배포 hello 이전 배포에서 다른 버전 값이 필요 하므로 응용 프로그램의 업그레이드를 지 원하는 데 유용 합니다. 워크플로에 toouse 응용 프로그램 업그레이드를 의도 하지 않은 하는 경우이 빌드 단계를 사용 하지 않도록 설정 하는 것이 좋습니다. 의도 라면 tooproduce 사용된 toooverwrite 기존 서비스 패브릭 응용 프로그램 일 수 있는 빌드를 비활성화 해야 합니다. hello 배포가 hello 버전 hello 빌드에서 생성 된 hello 응용 프로그램의 hello 클러스터의 hello 응용 프로그램의 hello 버전이 일치 하지 않는 경우 실패 합니다.
4. 솔루션에는.NET Core 프로젝트 hello 종속성 복원 빌드 단계를 빌드 정의 포함 되어 있는지 확인 해야 합니다.
   1. **빌드 단계 추가...**를 선택합니다.
   2. Hello 찾을 **명령줄** hello 유틸리티 탭 내에서 작업 하 고 해당 추가 단추를 클릭 합니다.
   3. Hello 작업의 입력된 필드에 대 한 다음 값에는 hello를 사용 합니다.
   4. 도구: dotnet
   5. 인수: restore
   6. Hello 직후에 hello 작업을 끌어 **NuGet 복원** 단계입니다.
5. 변경 내용을 저장 toohello 빌드 정을 했습니다.

### <a name="try-it"></a>시도
선택 **빌드 큐 대기** toomanually 빌드를 시작 합니다. 푸시 또는 체크 인 시 트리거도 빌드합니다. Hello 빌드 성공적으로 실행을 확인 한 후 이동할 수 있습니다 이제 toodefining 응용 프로그램 tooa 클러스터를 배포 하는 릴리스 정의 합니다.

## <a name="create-a-release-definition"></a>릴리스 정의 만들기
Team Services 릴리스 정의는 순차적으로 실행되는 작업 집합으로 구성된 워크플로를 설명합니다. 만들고 있는 hello 릴리스 정의의 hello 목표는 tootake 응용 프로그램 패키지 및 tooa 클러스터를 배포 합니다. Hello 빌드 정의 함께 사용 하면 및 릴리스 정의를 소스 파일 tooending 클러스터에서 실행 중인 응용 프로그램으로 시작 hello 전체 워크플로 실행할 수 있습니다. Team Services [릴리스 정의](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition)에 대해 자세히 알아봅니다.

### <a name="create-a-definition-from-hello-release-template"></a>Hello 릴리스 템플릿에서 정의 만들기
1. Visual Studio Team Services에서 프로젝트를 엽니다.
2. 선택 hello **릴리스** 탭 합니다.
3. 선택 hello 녹색  **+**  toocreate 새 릴리스 정의 서명 하 고 선택 **만들기 릴리스 정의** hello 메뉴에 있습니다.
4. Hello 대화 상자가 열리면 선택 **Azure 서비스 패브릭 배포** hello 내 **배포** 템플릿 범주입니다.
5. **다음**을 선택합니다.
6. 이 릴리스 정의의 hello 소스로 toouse 원하는 hello 빌드 정의 선택 합니다.  hello 릴리스 정의 참조 hello 아티팩트를 선택 하는 hello에 의해 생성 된 빌드 정의 합니다.
7. Hello 확인 **연속 배포** toohave 하려는 경우 확인란 Team Services 자동으로 새 릴리스 만들기 및 빌드 완료 될 때마다 hello 서비스 패브릭 응용 프로그램을 배포 합니다.
8. 원하는 toouse hello 에이전트 큐를 선택 합니다. 호스트 에이전트가 지원됩니다.
9. **만들기**를 선택합니다.
10. Hello hello 페이지 위쪽에 hello 연필 아이콘을 클릭 하 여 hello 정의 이름을 편집 합니다.
11. 응용 프로그램을 배포 해야 하는 hello 클러스터 toowhich hello에서 선택 **클러스터 연결** hello 작업의 필드를 입력된 합니다. hello 클러스터 연결 hello 배포 작업 tooconnect toohello 클러스터를 허용 하는 hello 필요한 정보를 제공 합니다. 클러스터에 대 한 클러스터 연결을 아직 되어 있지 않으면 경우 선택 hello **관리** 하이퍼링크 다음 toohello 필드 tooadd 하나입니다. 열리는 hello 페이지 hello 다음 단계를 수행 합니다.
    1. 선택 **새 서비스 끝점** 선택한 후 **Azure 서비스 패브릭** hello 메뉴에서 합니다.
    2. 이 끝점에서 대상으로 하는 hello 클러스터에서 사용 중인 인증 hello 유형을 선택 합니다.
    3. Hello에서 연결에 대 한 이름을 정의 **연결 이름** 필드입니다.  일반적으로 클러스터의 hello 이름을 사용 합니다.
    4. Hello에 hello 클라이언트 연결 끝점 URL은 정의 **클러스터 끝점** 필드입니다.  예: tcp://contoso.westus.cloudapp.azure.com:19000.
    5. Azure Active Directory 자격 증명에 대 한 hello에 toouse tooconnect toohello 클러스터를 구축할 hello 자격 증명을 정의 **Username** 및 **암호** 필드입니다.
    6. Hello에 hello 클라이언트 인증서 파일의 hello Base64 인코딩을 정의 하 여 인증서 기반 인증을 위해 **클라이언트 인증서** 필드입니다.  해당 필드는 방법에 대 한 정보에 hello 도움말 팝업을 참조 하십시오. 해당 값을 tooget 합니다.  인증서가 암호 보호 하는 경우 hello 암호 hello에서 정의 **암호** 필드입니다.
    7. **확인**을 클릭하여 변경을 확인합니다. 뒤로 tooyour 탐색 한 후 정의 해제할 hello에 hello 새로 고침 아이콘을 클릭 **클러스터 연결** 방금 추가한 필드 toosee hello 끝점입니다.
12. Hello 릴리스 정의 저장 합니다.

> [!NOTE]
> Microsoft 계정(예: @hotmail.com 또는 @outlook.com)은 Azure Active Directory 인증이 지원되지 않습니다.
> 
> 

만들어진 hello 정의 형식의 하나 이상의 태스크로 구성 됩니다 **서비스 패브릭 응용 프로그램 배포**합니다. Hello 참조 [작업 설명서 페이지](https://go.microsoft.com/fwlink/?LinkId=820528) 이 작업에 대 한 자세한 내용은 합니다.

### <a name="verify-hello-template-defaults"></a>Hello 템플릿 기본값 확인
1. Hello 확인 **게시 프로필** hello에 대 한 입력된 필드 **서비스 패브릭 응용 프로그램 배포** 작업 합니다. 기본적으로이 필드는 Cloud.xml hello 빌드 아티팩트에 포함 된 명명 된 게시 프로필을 참조 합니다. Tooreference 다른 게시 프로필을 하려는 경우 또는 hello 빌드 아티팩트의 여러 응용 프로그램 패키지를 포함 하는 경우 tooupdate hello 경로가 적절 하 게 필요 합니다.
2. Hello 확인 **응용 프로그램 패키지** hello에 대 한 입력된 필드 **서비스 패브릭 응용 프로그램 배포** 작업 합니다. 기본적으로이 필드는 hello 빌드 정의 서식 파일에서 사용 하는 hello 기본 응용 프로그램 패키지 경로 참조 합니다.  Hello 기본 응용 프로그램 패키지 경로 수정한 경우 hello에 빌드 정의 여기에 필요한 tooupdate hello 경로 적절 하 게도 합니다.

### <a name="try-it"></a>시도
선택 **릴리스 만들기** hello에서 **릴리스** 단추 메뉴 toomanually 릴리스를 만듭니다. Hello 열린 대화 상자에서 toobase hello 릴리스에서 원하는 하 고 클릭 hello 빌드 선택 **만들기**합니다. 연속 배포를 활성화 한 경우 관련 된 hello 빌드 정의 빌드 완료 되 면 릴리스 자동으로 생성 됩니다.

## <a name="next-steps"></a>다음 단계
서비스 패브릭 응용 프로그램에서는 hello 다음 문서를 읽을 연속 통합에 대 한 자세한 toolearn:

* [Team Services 문서 홈](https://www.visualstudio.com/docs/overview)
* [Team Services에서 빌드 관리](https://www.visualstudio.com/docs/build/overview)
* [Team Services에서 릴리스 관리](https://www.visualstudio.com/docs/release/overview)

