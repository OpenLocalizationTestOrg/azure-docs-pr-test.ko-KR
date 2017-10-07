---
title: ".NET 앱 컨테이너 tooAzure 서비스 패브릭에서에서 aaaDeploy | Microsoft Docs"
description: "방법에 대해 설명 toopackage Docker 컨테이너에서 Visual Studio에서.NET 응용 프로그램입니다. 이 새로운 \"container\" 앱을 배포한 다음 tooa 서비스 패브릭 클러스터입니다."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: mikhegn
ms.openlocfilehash: 094b0e71d76b2e56ffb9b23638dd8154b3aff5fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a>Windows 컨테이너 tooAzure 서비스 패브릭에서에서.NET 응용 프로그램 배포

이 자습서에서는 Azure에서 Windows 컨테이너에서 기존 ASP.NET 응용 프로그램 toodeploy 합니다.

이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Visual Studio에서 Docker 프로젝트 만들기
> * 기존 응용 프로그램 컨테이너화
> * Visual Studio 및 VSTS와의 연속 통합 설정

## <a name="prerequisites"></a>필수 조건

1. Windows 10에서 컨테이너를 실행할 수 있도록 [Windows용 Docker CE](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description)를 설치합니다.
2. Hello를 숙지 [Windows 10 컨테이너 빠른 시작][link-container-quickstart]합니다.
3. Hello 다운로드 [Fabrikam Fiber CallCenter] [ link-fabrikam-github] 샘플 응용 프로그램입니다.
4. [Azure PowerShell][link-azure-powershell-install]을 설치합니다.
5. Hello 설치 [Visual Studio 2017에 대 한 지속적인 배달 도구 확장][link-visualstudio-cd-extension]
6. [Azure 구독][link-azure-subscription] 및 [Visual Studio Team Services 계정][link-vsts-account]을 만듭니다. 
7. [Azure에서 클러스터 만들기](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-hello-application"></a>Hello 응용 프로그램을 컨테이너 화합니다

이제는 [Azure에서 실행 중인 서비스 패브릭 클러스터](service-fabric-tutorial-create-cluster-azure-ps.md) toocreate 준비를 하 고 컨테이너 화 된 응용 프로그램을 배포 합니다. 컨테이너에서 응용 프로그램을 실행 하는 toostart tooadd 필요 **Docker 지원** Visual Studio에서 toohello 프로젝트. 추가 하는 경우 **Docker 지원** toohello 응용 프로그램을 두 가지 동작이 발생 합니다. 첫째, 한 _Dockerfile_ toohello 프로젝트에 추가 됩니다. 이 새로운 파일 hello 컨테이너 이미지 작성 toobe는 하는 방법을 설명 합니다. 다음의 두 번째, 새 _docker 작성_ 프로젝트가 toohello 솔루션에 추가 됩니다. hello 새 프로젝트에 포함 되어 일부 docker 구성 파일입니다. Docker 구성 파일에는 hello 컨테이너 실행 방법을 사용 하는 toodescribe 수 있습니다.

[Visual Studio 컨테이너 도구][link-visualstudio-container-tools] 작업에 대한 자세한 정보

>[!NOTE]
>이면 hello Windows 컨테이너 이미지를 실행 하는 컴퓨터에 처음으로 Docker CE hello 사용자 컨테이너에 대 한 기본 이미지를 끌어올 해야 합니다. 이 자습서에 사용 하는 hello 이미지는 14 GB입니다. 계속 해 hello 다음 터미널 명령 toopull hello에 대 한 기본 이미지를 실행 합니다.
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a>Docker 지원 추가

열기 hello [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] Visual Studio에서 파일입니다.

마우스 오른쪽 단추로 클릭 hello **FabrikamFiber.Web** 프로젝트 > **추가** > **Docker 지원**합니다.

### <a name="add-support-for-sql"></a>SQL 지원 추가

이 응용 프로그램 SQL server에 필요한 toorun hello 응용 프로그램 이므로 hello 데이터 공급자로 SQL을 사용 합니다. docker-compose.override.yml 파일의 SQL Server 컨테이너 이미지를 참조하세요.

Visual Studio에서 열고 **솔루션 탐색기**, 찾을 **docker 구성**, 및 열기 hello 파일 **docker compose.override.yml**합니다.

Toohello 이동 `services:` 노드를 명명 된 노드 추가 `db:` hello 컨테이너에 대 한 hello SQL Server 항목을 정의 하는 합니다.

```yml
  db:
    image: microsoft/mssql-server-windows-developer
    environment:
      sa_password: "Password1"
      ACCEPT_EULA: "Y"
    ports:
      - "1433"
    healthcheck:
      test: [ "CMD", "sqlcmd", "-U", "sa", "-P", "Password1", "-Q", "select 1" ]
      interval: 1s
      retries: 20
```

>[!NOTE]
>호스트에서 연결할 수 있기만 하면 어떤 SQL Server든지 로컬 디버깅에 사용할 수 있습니다. 그러나 **localdb**는 `container -> host` 통신을 지원하지 않습니다.

>[!WARNING]
>컨테이너에서 SQL Server를 실행할 때 데이터가 지속되지 않습니다. Hello 컨테이너가 중지 되 면 데이터가 지워집니다. 프로덕션 환경에서는 이 구성을 사용하지 마세요.

Toohello 이동 `fabrikamfiber.web:` 노드 명명 된 자식 노드를 추가할 `depends_on:`합니다. 이렇게 하면 해당 hello `db` 웹 응용 프로그램 (fabrikamfiber.web) 하기 전에 서비스 (SQL Server 컨테이너 hello)를 시작 합니다.

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a>Hello 웹 구성 업데이트

Hello에 다시 **FabrikamFiber.Web** 프로젝트를 업데이트 hello 연결 문자열 hello에 **web.config** 파일, toopoint toohello hello 컨테이너에서 SQL Server.

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
>웹 응용 프로그램의 다른 SQL Server 릴리스를 빌드할 때 빌드 toouse를 원하는 다른 연결 문자열 tooyour web.release.config 파일을 추가 합니다.

### <a name="test-your-container"></a>컨테이너 테스트

키를 눌러 **F5** 컨테이너의 toorun 및 디버그 hello 응용 프로그램입니다.

가장자리는 hello 컨테이너의 hello IP 주소를 사용 하 여 hello 내부 NAT 네트워크 (일반적으로 172.x.x.x)에서 응용 프로그램의 정의 된 시작 페이지를 엽니다. Visual Studio 2017 년을 사용 하 여 컨테이너에서 응용 프로그램 디버깅에 대해 자세히 toolearn 참조 [이 여기서][link-debug-container]합니다.

![컨테이너의 fabrikam 예][image-web-preview]

hello 컨테이너 빌드되고 서비스 패브릭 응용 프로그램에 패키지 준비 toobe 포함 되었습니다. 컴퓨터에 빌드한 hello 컨테이너 이미지를 만든 후에 tooany 컨테이너 레지스트리 푸시 수 있으며 tooany 호스트 toorun 끌어올 수 있습니다.

## <a name="get-hello-application-ready-for-hello-cloud"></a>Hello 클라우드에 대 한 hello 응용 프로그램 사용 준비

tooget hello 응용 프로그램에서 Azure 서비스 패브릭에서 실행 하기 위한 준비, toocomplete 두 단계가 필요 합니다.

1. Hello 포트를 원하는 위치로 toobe 수 tooreach hello 서비스 패브릭 클러스터에서 해당 웹 응용 프로그램을 노출 합니다.
2. 응용 프로그램을 위해 프로덕션 준비가 된 SQL 데이터베이스를 제공합니다.

### <a name="expose-hello-port-for-hello-app"></a>Hello 앱에 대 한 hello 포트 노출
hello 서비스 패브릭 클러스터를 구성 했습니다 포트가 *80* 들어오는 트래픽을 toohello 클러스터를 분산 하는 hello Azure 부하 분산 장치에서에서 기본적으로 열려 있습니다. docker-compose.yml 파일을 통해 이 포트에 컨테이너를 노출시킬 수 있습니다.

Visual Studio에서 열고 **솔루션 탐색기**, 찾을 **docker 구성**, 및 열기 hello 파일 **docker compose.override.yml**합니다.

Hello 수정 `fabrikamfiber.web:` 노드를 명명 된 자식 노드 추가 `ports:`합니다.

문자열 항목 `- "80:80"`을 추가합니다.

```yml
  version: '3'

  services:
    fabrikamfiber.web:
      image: fabrikamfiber.web
      build:
        context: .\FabrikamFiber.Web
        dockerfile: Dockerfile
      ports:
        - "80:80"
```

### <a name="use-a-production-sql-database"></a>프로덕션 SQL 데이터베이스 사용
프로덕션 환경에서 실행하는 경우에는 데이터를 데이터베이스에 유지해야 합니다. 현재 방법은 tooguarantee 영구 데이터 컨테이너에서를 따라서 컨테이너에서 SQL Server에서 프로덕션 데이터를 저장할 수 없습니다.

Azure SQL Database를 활용하는 것이 좋습니다. tooset 및 azure에서 관리 되는 SQL Server 실행 방문 hello [Azure SQL 데이터베이스 빠른 시작] [ link-azure-sql] 문서.

>[!NOTE]
>Hello toochange hello 연결 문자열 toohello SQL server를 기억 **web.release.config** hello에 대 한 파일 **FabrikamFiber.Web** 프로젝트.
>
>SQL Database에 연결할 수 없는 경우 이 응용 프로그램은 정상적으로 실패합니다. Toogo 계속 선택할 수 있으며 없는 SQL server와 함께 hello 응용 프로그램을 배포 합니다.

## <a name="deploy-with-visual-studio-team-services"></a>Visual Studio Team Services를 사용하여 배포

Visual Studio Team Services를 사용 하 여 배포를 tooset, 해야 tooinstall hello [Visual Studio 2017에 대 한 지속적인 배달 도구 확장][link-visualstudio-cd-extension]합니다. 이 확장 쉽게 toodeploy tooAzure Visual Studio Team Services를 구성 하 여 있고에서는 응용 프로그램 배포 tooyour 서비스 패브릭 클러스터 합니다.

tooget 시작 코드를 소스 제어에서 호스트 되어야 합니다. 이 섹션의 나머지 부분 hello 가정 **git** 사용 중입니다.

### <a name="set-up-a-vsts-repo"></a>VSTS 리포지토리 설정
Visual Studio의 hello 오른쪽 아래 모서리를 클릭 **tooSource 컨트롤 추가** > **Git** (또는 원하는 어떤 옵션).

![hello 소스 제어 단추를 누릅니다.][image-source-control]

Hello에 _팀 탐색기_ 창, 키를 눌러 **Git 리포지토리를 게시**합니다.

VSTS 리포지토리 이름을 선택하고 **리포지토리**를 누릅니다.

![리포지토리 tooVSTS 게시][image-publish-repo]

이제 코드가 VSTS 소스 리포지토리와 동기화되었으므로 연속 통합 및 지속적인 업데이트를 구성할 수 있습니다.

### <a name="setup-continuous-delivery"></a>지속적인 업데이트 설정

_솔루션 탐색기_를 마우스 오른쪽 단추로 클릭 hello **솔루션** > **지속적인 배달 구성**합니다.

Hello Azure 구독을 선택 합니다.

설정 **호스트 유형** 너무**서비스 패브릭 클러스터**합니다.

설정 **대상 호스트** hello 이전 섹션에서 만든 toohello 서비스 패브릭 클러스터입니다.

선택 된 **컨테이너 레지스트리** toopublish 컨테이너에서 합니다.

>[!TIP]
>사용 하 여 hello **편집** 단추 toocreate 컨테이너 레지스트리 합니다.

**확인**을 누릅니다.

![Service Fabric 연속 통합 설정][image-setup-ci]
   
   Hello 구성이 완료 되 면 컨테이너는 배포 된 tooService 패브릭입니다. 업데이트 toohello 리포지토리에 푸시 될 때마다 새 빌드 및 릴리스 실행 됩니다.
   
   >[!NOTE]
   >건물 hello 컨테이너 이미지 약 15 분이 소요 합니다.
   >hello 첫 번째 배포 toohello 서비스 패브릭 클러스터 hello 기본 Windows Server Core 컨테이너 이미지 toobe 다운로드 하면 됩니다. hello 다운로드 toocomplete를 추가 5-10 분 걸립니다.

클러스터의 hello url을 사용 하 여 toohello Fabrikam 콜 센터 응용 프로그램 찾아보기: 예를 들어 *http://mycluster.westeurope.cloudapp.azure.com*

컨테이너 화 된 하 고 hello 콜 센터 Fabrikam 솔루션을 배포 했으므로 hello를 열 수 있습니다 [Azure 포털] [ link-azure-portal] 참조 서비스 패브릭에서 실행 되는 hello 응용 프로그램 및입니다. tootry hello 응용 프로그램 웹 브라우저를 열고 서비스 패브릭 클러스터의 toohello URL로 이동 합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * Visual Studio에서 Docker 프로젝트 만들기
> * 기존 응용 프로그램 컨테이너화
> * Visual Studio 및 VSTS와의 연속 통합 설정

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooit.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate tooAzure Web Apps](app-service-web-tutorial-custom-ssl.md)

## Next steps

- [Container Tooling in Visual Studio][link-visualstudio-container-tools]
- [Get started with containers in Service Fabric][link-servicefabric-containers]
- [Creating Service Fabric applications][link-servicefabric-createapp]
-->

[link-debug-container]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-fabrikam-github]: https://aka.ms/fabrikamcontainer
[link-container-quickstart]: /virtualization/windowscontainers/quick-start/quick-start-windows-10
[link-visualstudio-container-tools]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-azure-powershell-install]: /powershell/azure/install-azurerm-ps
[link-servicefabric-create-secure-clusters]: service-fabric-cluster-creation-via-arm.md
[link-visualstudio-cd-extension]: https://aka.ms/cd4vs
[link-servicefabric-containers]: service-fabric-get-started-containers.md
[link-servicefabric-createapp]: service-fabric-create-your-first-application-in-visual-studio.md
[link-azure-portal]: https://portal.azure.com
[link-sf-clustertemplate]: https://aka.ms/securepreviewonelineclustertemplate
[link-azure-pricing-calculator]: https://azure.microsoft.com/en-us/pricing/calculator/
[link-azure-subscription]: https://azure.microsoft.com/en-us/free/
[link-vsts-account]: https://www.visualstudio.com/team-services/pricing/
[link-azure-sql]: /azure/sql-database/

[image-web-preview]: media/service-fabric-host-app-in-a-container/fabrikam-web-sample.png
[image-source-control]: media/service-fabric-host-app-in-a-container/add-to-source-control.png
[image-publish-repo]: media/service-fabric-host-app-in-a-container/publish-repo.png
[image-setup-ci]: media/service-fabric-host-app-in-a-container/configure-continuous-integration.png
