---
title: "aaaProvision microservices 예측 가능한 방식으로 Azure에 배포"
description: "Microservices 하나의 단위로 Azure 앱 서비스의 및 리소스 그룹 템플릿 JSON 및 PowerShell 스크립트를 사용 하 여 예측 가능한 방식으로 toodeploy 응용 프로그램을 구성 하는 방법에 대해 알아봅니다."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: bb51e565-e462-4c60-929a-2ff90121f41d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2016
ms.author: cephalin
ms.openlocfilehash: d32c2fc82a8b09e89224ec437e5819b65b2e9e78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-and-deploy-microservices-predictably-in-azure"></a>Azure에서 마이크로 서비스를 예측 가능하게 프로비전 및 배포
이 자습서에서는 어떻게 tooprovision 이루어진 응용 프로그램 및 배포 [microservices](https://en.wikipedia.org/wiki/Microservices) 에 [Azure 앱 서비스](/services/app-service/) 하나의 단위로 및 JSON 리소스 그룹 템플릿을 사용 하 여 예측 가능한 방식에서 및 PowerShell 스크립팅 합니다. 

프로비저닝과 고도로 분리 microservices의 구성 된 확장성이 뛰어난 응용 프로그램을 배포 하는 경우 반복성 및 예측 가능 중요 toosuccess 됩니다. [Azure 앱 서비스](/services/app-service/) toocreate microservices 웹 앱, 모바일 앱, API 앱 및 논리 앱을 포함 하는 수 있도록 합니다. [Azure 리소스 관리자](../azure-resource-manager/resource-group-overview.md) 데이터베이스, 소스 제어 설정 등 리소스 종속성과 함께 한 단위로 모든 hello microservices toomanage 있습니다 수 있도록 합니다. 이제 JSON 템플릿과 간단한 PowerShell 스크립팅을 사용하여 이러한 응용 프로그램을 배포할 수 있습니다. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>수행할 사항
Hello 자습서에서는 포함 된 응용 프로그램을 배포 합니다.

* 두 가지 웹앱(즉, 두 개의 마이크로 서비스)
* 백 엔드 SQL 데이터베이스
* 앱 설정, 연결 문자열 및 소스 제어
* Application insights, 경고, 자동 크기 조정 설정

## <a name="tools-you-will-use"></a>사용할 도구
이 자습서에서는 hello 다음 도구를 사용 합니다. 도구에 대 한 포괄적인 설명은 되지 않으므로 I toostick toohello 종단 간 시나리오 서 주며 방금 간략 한 소개 tooeach에 자세한 정보를 찾을 수 있습니다. 

### <a name="azure-resource-manager-templates-json"></a>Azure 리소스 관리자 템플릿(JSON)
Azure 앱 서비스의 웹 응용 프로그램을 만들 때마다 Azure 리소스 관리자 JSON 템플릿이 toocreate hello 전체 리소스 그룹 hello 구성 요소 리소스 사용 예를 들어 합니다. Hello에서 복잡 한 템플릿 [Azure 마켓플레이스](/marketplace) hello 같은 [확장 가능한 WordPress](/marketplace/partners/wordpress/scalablewordpress/) 앱 hello MySQL 데이터베이스, 저장소 계정, hello 앱 서비스 계획, hello 웹 응용 프로그램 자체가, 경고 규칙, 응용 프로그램 포함 될 수 있습니다 설정, 자동 크기 조정 설정 및 이러한 템플릿은 점점 모든 PowerShell 통해 사용할 수 있는 tooyou 됩니다. Toodownload 및 사용 하 여 이러한 템플릿을 참조에 대 한 내용은 [Azure PowerShell 사용 하 여 Azure 리소스 관리자와](../powershell-azure-resource-manager.md)합니다.

Hello Azure Resource Manager 템플릿에 대 한 자세한 내용은 참조 하세요. [Azure 리소스 관리자 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)

### <a name="azure-sdk-26-for-visual-studio"></a>Visual Studio용 Azure SDK 2.6
hello 최신 SDK 포함 개선 toohello hello JSON 편집기에서 리소스 관리자 템플릿 지원 합니다. 이 tooquickly에서는 리소스 그룹 템플릿을 처음부터 만들거나 수정 하기 위해 (예: 다운로드 한 갤러리 템플릿) 기존 JSON 템플릿, hello 매개 변수 파일을 채울 열고도 Azure에서 직접 hello 리소스 그룹을 배포 리소스 그룹 솔루션입니다.

자세한 내용은 [Visual Studio용 Azure SDK 2.6](https://azure.microsoft.com/blog/2015/04/29/announcing-the-azure-sdk-2-6-for-net/)을 참조하세요.

### <a name="azure-powershell-080-or-later"></a>Azure PowerShell 0.8.0 또는 이후
버전 0.8.0부터, Azure PowerShell 설치 hello 더하기 toohello Azure 모듈에에서 hello Azure 리소스 관리자 모듈을 포함 합니다. 이 새 모듈을 통해 리소스 그룹의 tooscript hello 배포할 수 있습니다.

자세한 내용은 [Azure 리소스 관리자로 Azure PowerShell 사용](../powershell-azure-resource-manager.md)

### <a name="azure-resource-explorer"></a>Azure 리소스 탐색기
이 [미리 보기 도구](https://resources.azure.com) 구독 및 hello 개별 리소스에 모든 hello 리소스 그룹의 tooexplore hello JSON 정의 사용 하면 됩니다. Hello 도구에서 리소스의 hello JSON 정의 편집, 리소스의 전체 계층을 삭제 및 새 리소스를 만들 수 있습니다.  hello 정보를이 도구에서 사용할 수는 템플릿 표시 되므로 작업을 작성 하는 데 매우 유용 tooset에 필요한 리소스에는 특정 유형의 hello 속성 값 등을 수정 합니다. Hello에도 리소스 그룹을 만들 수 있습니다 [Azure 포털](https://portal.azure.com/), 해당 JSON 정의 검사 hello 리소스 그룹을 templatize hello 탐색기 도구 toohelp에 있습니다.

### <a name="deploy-tooazure-button"></a>배포 tooAzure 단추
소스 제어에 GitHub를 사용 하는 경우 넣을 수 있습니다는 [배포 tooAzure 단추](https://azure.microsoft.com/blog/2014/11/13/deploy-to-azure-button-for-azure-websites-2/) 프로그램 추가 정보에 있습니다. MD 턴키 배포 UI tooAzure 수 있도록 합니다. 이렇게 하려면 모든 단순한 웹 앱에 대 한를 하는 동안이 tooenable azuredeploy.json 파일 hello 리포지토리 루트에 배치 하 여 전체 리소스 그룹 배포를 확장할 수 있습니다. Hello 리소스 그룹 템플릿, 포함 하는이 JSON 파일로 hello 배포 tooAzure 단추 toocreate hello 리소스 그룹에 의해 사용 됩니다. 예를 들어 hello를 참조 하십시오. [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) 샘플이이 자습서에서 사용 합니다.

## <a name="get-hello-sample-resource-group-template"></a>Hello 샘플 리소스 그룹 템플릿 가져오기
이제 오른쪽 tooit 해 보겠습니다.

1. Toohello 이동 [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) 응용 프로그램 서비스 예제 추가 정보입니다.
2. Readme.md, 클릭 **tooAzure 배포**합니다.
3. Toohello 이동 하 [azure 배포](https://deploy.azure.com) 사이트와 자주 묻는 tooinput 배포 매개 변수입니다. Hello 필드 대부분 채워지도록 hello 저장소 이름 및 일부 임의 문자열을 확인 합니다. 원하는 하지만 hello 작업만 tooenter 있는 hello 암호와 hello SQL Server 관리 로그인 한 다음 클릭 하는 경우 모든 hello 필드를 변경할 수 있습니다 **다음**합니다.
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-1-deploybuttonui.png)
4. 그런 다음 클릭 **배포** toostart hello 배포 프로세스입니다. Hello 프로세스 toocompletion 실행 되 면 hello http://todoapp 클릭*XXXX*. azurewebsites.net 링크 toobrowse hello 응용 프로그램을 배포 합니다. 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-2-deployprogress.png)
   
   hello UI hello 앱을 시작 하지만 완벽 하 게 작동 하는 응용 프로그램 인지 직접 유도 하기 때문에 먼저 tooit를 찾아볼 때 약간 느려질 것입니다.
5. Hello 배포 페이지에서 클릭 hello **관리** toosee hello 새 응용 프로그램 hello Azure 포털에에서 연결 합니다.
6. Hello에 **Essentials** 드롭다운에서 hello 리소스 그룹 링크를 클릭 합니다. 또한 해당 hello 웹 앱은 이미 참고에서 toohello GitHub 리포지토리 연결 **외부 프로젝트**합니다. 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-3-portalresourcegroup.png)
7. Hello 리소스 그룹 블레이드 개가 이미 두 개의 웹 앱 및 hello 리소스 그룹에서 하나의 SQL 데이터베이스를 note 합니다.
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-4-portalresourcegroupclicked.png)

방금 짧은 잠시 후에는 완벽 하 게 배포 된 두 마이크로 서비스 응용 프로그램을 모든 hello 구성 요소, 종속성, 설정, 데이터베이스 및 지속적인 게시에서는 Azure 리소스 관리자는 자동화 된 오케스트레이션에 의해 본 것과 모든 것입니다. 이 모든 작업은 두 가지로 수행되었습니다.

* hello 배포 tooAzure 단추
* hello 리 포 루트에 azuredeploy.json

이 동일한 응용 프로그램을 배포할 수 있습니다 수십, 수백 또는 수천 번 하며 hello 정확히 동일한 구성이 될 때마다 합니다. 이 방법의 hello 반복성 및 hello 예측 toodeploy 확장성이 뛰어난 응용 프로그램 사용 하면 쉽고 자신 있게 있습니다.

## <a name="examine-or-edit-azuredeployjson"></a>AZUREDEPLOY.JSON 검사(또는 편집)
이제 hello GitHub 리포지토리 설정 된 방법에 대해 살펴보겠습니다. 사용 하려는 JSON 편집기 hello hello Azure.NET SDK에에서 아직 설치 하지 않은 경우 [Azure.NET SDK 2.6](/downloads/), 지금 합니다.

1. 복제 hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) 즐겨 찾는 git 도구를 사용 하 여 리포지토리 합니다. Hello, 스크린 샷에 아래에서 수행 하 고이 hello Visual Studio 2013에서 팀 탐색기에에서 있습니다.
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-1-vsclone.png)
2. Hello 리포지토리 루트 로부터의 azuredeploy.json Visual Studio에서 엽니다. Hello JSON 개요 창을 보이지 않으면 Azure.NET SDK tooinstall을 해야 합니다.
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-2-vsjsoneditor.png)

진행 중인 toodescribe 하지 hello JSON 형식으로 모든 세부 정보 중 했지만 hello [더 리소스](#resources) 섹션의 hello 리소스 그룹 템플릿 언어를 학습 하기 위한 링크를 포함 합니다. 여기에서는 두 개의 컨테이너 응용 프로그램 배포에 대 한 사용자 지정 템플릿을 만들 때의 사용할 수 있는 기능이 흥미로운 hello tooshow 시작 합니다.

### <a name="parameters"></a>매개 변수
대부분의 이러한 매개 변수는 어떤 hello hello 매개 변수 섹션 toosee 살펴보시기 바랍니다 **tooAzure 배포** 단추 묻는 tooinput 합니다. hello 뒤 hello 사이트 **tooAzure 배포** 단추 hello 입력 UI 채웁니다 azuredeploy.json에 정의 된 hello 매개 변수를 사용 합니다. 이러한 매개 변수는 리소스 이름, 속성 값 등의 hello 리소스 정의에서 사용 됩니다.

### <a name="resources"></a>리소스
Hello 리소스 노드를 SQL Server 인스턴스, 앱 서비스 계획 및 두 개의 웹 앱을 포함 하 여 4 최상위 리소스 정의 볼 수 있습니다. 

#### <a name="app-service-plan"></a>앱 서비스 계획
Hello JSON에서에서 단순 루트 수준의 리소스를 시작 하겠습니다. JSON 개요 hello 클릭 이라는 hello 앱 서비스 계획 **[hostingPlanName]** toohighlight hello 해당 JSON 코드입니다. 

![](./media/app-service-deploy-complex-application-predictably/examinejson-3-appserviceplan.png)

해당 hello 참고 `type` 요소 (호출한 서버 팜을 전 long, long 시간)는 앱 서비스 계획에 대 한 hello 문자열을 지정 하 고 hello JSON 파일에 정의 된 hello 매개 변수를 사용 하 여 다른 요소 및 속성 채워집니다 없는 경우이 리소스 모든 중첩 된 리소스입니다.

> [!NOTE]
> 또한 해당 hello 값을 기록해 둡니다 `apiVersion` Azure hello REST API toouse hello JSON 리소스 정의 그리고 버전 어떻게 hello 리소스 형식을 지정 하는 hello 내에 영향을 줄 수를 알려 줍니다 `{}`합니다. 
> 
> 

#### <a name="sql-server"></a>SQL Server
Hello SQL Server 리소스 이름이 차례 대로 클릭 **SQLServer** hello JSON 개요에서에서.

![](./media/app-service-deploy-complex-application-predictably/examinejson-4-sqlserver.png)

참고 hello hello에 대 한 다음 JSON 코드를 강조 표시.

* hello 매개 변수를 사용 하면 만든 hello 리소스는 명명 된 서로와 일치 하 게 만드는 방식으로 구성.
* sql Server 리소스 hello 두 중첩 된 리소스에 다른 값을이 각각 `type`합니다.
* hello 내부 리소스에 중첩 `“resources”: […]`, hello 데이터베이스와 hello 방화벽 규칙이 정의 되어 있는,는 `dependsOn` hello 루트 수준의 sql Server 리소스의 hello 리소스 ID를 지정 하는 요소입니다. 이렇게 하면 Azure 리소스 관리자 "는 다른 리소스가 이미 존재 해야 합니다;이 리소스를 만들기 전에 만들고 해당 다른 리소스 hello 서식 파일에 정의 된 경우 다음 하나를 먼저 "합니다.
  
  > [!NOTE]
  > 에 대 한 자세한 내용은 방법 toouse hello `resourceId()` 함수, 참조 [Azure 리소스 관리자 템플릿 함수](../azure-resource-manager/resource-group-template-functions-resource.md#resourceid)합니다.
  > 
  > 
* hello의 효과 hello `dependsOn` 요소는 동시에 리소스를 만들 수 있으며 리소스를 순차적으로 만들어야 합니다 Azure 리소스 관리자 파악할 수 있습니다. 

#### <a name="web-app"></a>웹앱
이제 toohello 실제 웹 응용 프로그램 자체에 더 복잡 한에 대해 알아보겠습니다. JSON 코드 hello JSON 개요 toohighlight의 웹 앱 hello [variables('apiSiteName')]를 클릭 합니다. 상황이 훨씬 더 흥미로워집니다. 이 작업을 위해 개별적으로 hello 기능에 대 한 하겠습니다.

##### <a name="root-resource"></a>루트 리소스
hello 웹 앱은 두 개의 다른 리소스에 따라 달라 집니다. 이 Azure 리소스 관리자는 앱 서비스 계획 및 SQL Server 인스턴스 hello 만들어집니다 두 hello 한 후에 hello 웹 앱을 만들 것을 의미 합니다.

![](./media/app-service-deploy-complex-application-predictably/examinejson-5-webapproot.png)

##### <a name="app-settings"></a>앱 설정
중첩 된 리소스로 hello 응용 프로그램 설정이 정의 됩니다.

![](./media/app-service-deploy-complex-application-predictably/examinejson-6-webappsettings.png)

Hello에 `properties` 요소에 대 한 `config/appsettings`, hello 형식에 두 개의 응용 프로그램 설정이 있습니까 `“<name>” : “<value>”`합니다.

* `PROJECT`이 [KUDU 설정](https://github.com/projectkudu/kudu/wiki/Customizing-deployments) 다중 프로젝트 Visual Studio 솔루션에서 Azure 배포 프로젝트 toouse 어떤 알려주는 합니다. 살펴본 다음 소스 제어 구성 된 방식에 나중에 있지만이 설정을 hello ToDoApp 코드 다중 프로젝트 Visual Studio 솔루션에 존재 하므로 필요 합니다.
* `clientUrl`해당 hello 응용 프로그램 코드를 설정 하기만 하면 앱에서 사용 됩니다.

##### <a name="connection-strings"></a>연결 문자열
hello 연결 문자열은 중첩 된 리소스로 정의 됩니다.

![](./media/app-service-deploy-complex-application-predictably/examinejson-7-webappconnstr.png)

Hello에 `properties` 요소에 대 한 `config/connectionstrings`, 각각의 연결 문자열의 hello 특정 형식으로 이름: 값 쌍으로 정의 되 `“<name>” : {“value”: “…”, “type”: “…”}`합니다. Hello에 대 한 `type` 요소의 가능한 값은 `MySql`, `SQLServer`, `SQLAzure`, 및 `Custom`합니다.

> [!TIP]
> Hello 연결 문자열 형식 목록은 선언적 hello 다음 Azure PowerShell에서 명령을 실행: \[Enum]::GetNames("Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.DatabaseType")
> 
> 

##### <a name="source-control"></a>소스 제어
중첩 된 리소스로 hello 소스 제어 설정이 정의 됩니다. 이 리소스 tooconfigure 지속적인 게시를 사용 하는 azure 리소스 관리자 (에 주의 참조 하십시오. `IsManualIntegration` 나중) 및 hello JSON 파일의 hello 처리 하는 동안 자동으로 응용 프로그램 코드의 hello 배포 해제 tookick도 합니다.

![](./media/app-service-deploy-complex-application-predictably/examinejson-8-webappsourcecontrol.png)

`RepoUrl`및 `branch` 매우 직관적인 속해 있어야 하며에서 hello 분기 toopublish의 toohello Git 리포지토리 및 hello 이름을 가리켜야 합니다. 다시, 입력 매개 변수에 의해 정의됩니다. 

Hello에 대 한 참고 `dependsOn` 하는 추가 toohello 웹 응용 프로그램 리소스 자체 요소 `sourcecontrols/web` 에 의존 `config/appsettings` 및 `config/connectionstrings`합니다. 때문에 이것이 되 면 `sourcecontrols/web` 가 구성 hello Azure 배포 프로세스는 자동으로 시도 toodeploy, 빌드 및 hello 응용 프로그램 코드를 시작 합니다. 따라서 삽입 되도록이 종속성 사용 하면 해당 hello 응용 프로그램에 액세스 toohello 필요한 응용 프로그램 설정 및 연결 문자열 hello 응용 프로그램 코드를 실행 하기 전에 있습니다. 

> [!NOTE]
> 또한 `IsManualIntegration` 너무 설정`true`합니다. Hello GitHub 리포지토리를 실제로 소유 하지 않았으며 따라서 권한을 tooAzure tooconfigure에서 지속적인 게시를 부여할 실제로 수 때문에이 속성은이 자습서에서는 필요 [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) (즉, 푸시 자동 리포지토리 업데이트 tooAzure) 합니다. Hello 기본값을 사용할 수 있습니다 `false` hello에 hello 소유자 GitHub 자격 증명을 구성한 경우에 지정 된 리포지토리 hello에 대 한 [Azure 포털](https://portal.azure.com/) 하기 전에. 즉, 모든 앱 hello에 대 한 소스 제어 tooGitHub 또는 BitBucket을 설정한 경우 [Azure 포털](https://portal.azure.com/) 이전에 사용자를 사용 하 여 자격 증명, Azure hello 자격 증명 기억 하 고 모든 앱에서 배포 될 때마다 사용할 것 GitHub 또는 BitBucket hello 앞에 있습니다. 그러나이 이미 수행 하지 않은, hello JSON 템플릿 배포할 Azure 리소스 관리자 hello 리포지토리 소유자의 자격 증명으로 GitHub 또는 BitBucket에 로그인 하기 때문에 tooconfigure hello 웹 앱의 소스 제어 설정 하려고 할 때 실패 합니다.
> 
> 

## <a name="compare-hello-json-template-with-deployed-resource-group"></a>배포 된 리소스 그룹으로 hello JSON 템플릿을 비교합니다
여기에서는 hello에서 모든의 hello 웹 앱 블레이드를 살펴볼 수 있습니다 [Azure 포털](https://portal.azure.com/), 없는 경우에 유용 하 게 것 처럼 더 다른 도구는 하지만 합니다. Toohello 이동 [Azure 리소스 탐색기](https://resources.azure.com) 미리 보기 도구를 사용 하면 모든 hello 리소스 그룹의 JSON 표현을의 구독을 hello Azure 백 엔드에에서 실제로 존재 하는 대로 합니다. Azure의 hello 리소스 그룹의 JSON 계층 구조를 갖는지 toocreate 사용 hello 템플릿 파일에 hello 계층 구조와 것을 볼 수 있습니다.

예를 들어 toohello 라인이 될 때 [Azure 리소스 탐색기](https://resources.azure.com) 도구 및 hello 탐색기의 hello 노드를 확장 하 고, hello 리소스 그룹 및 해당 해당 리소스 종류에서 수집 하는 hello 루트 수준의 리소스를 볼 수 있습니다.

![](./media/app-service-deploy-complex-application-predictably/ARM-1-treeview.png)

웹 응용 프로그램 tooa 드릴 하는 경우 수 toosee 웹 응용 프로그램 구성 세부 정보 비슷한 toohello 아래 스크린샷은 수 있어야 합니다.

![](./media/app-service-deploy-complex-application-predictably/ARM-2-jsonview.png)

다시 hello 중첩 된 계층 구조와 매우 유사 toothose JSON 템플릿 파일에 하 고 있어야 하며 hello 앱 설정, 연결 문자열 등 hello JSON 창에도 반영 제대로 표시 되어야 합니다. hello 없을 경우 여기에서 설정 JSON 파일에 문제가 있음을 나타낼 수 있습니다 및 JSON 템플릿 파일 문제를 해결 하는 데 도움이 됩니다.

## <a name="deploy-hello-resource-group-template-yourself"></a>사용자가 직접 hello 리소스 그룹 템플릿 배포
hello **tooAzure 배포** 단추는 뛰어나지만 있습니다 toodeploy hello 리소스 그룹 템플릿 azuredeploy.json에 azuredeploy.json tooGitHub가 이미 푸시 하는 경우에 합니다. 또한 hello Azure.NET SDK hello 도구 로컬 컴퓨터에서 직접 JSON 템플릿 파일 toodeploy 있습니다를 제공 합니다. toodo 다음,이 따라 hello 단계:

1. Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 클릭합니다.
2. **Visual C#** > **클라우드** > **Azure 리소스 그룹**을 클릭한 후에 **확인**을 클릭합니다.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-1-vsproject.png)
3. **Azure 템플릿 선택**에서 **빈 템플릿**을 선택하고 **확인**을 클릭합니다.
4. Hello azuredeploy.json 끌어 **템플릿** 새 프로젝트의 폴더입니다.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-2-copyjson.png)
5. 솔루션 탐색기에서 복사 하는 hello azuredeploy.json를 엽니다.
6. Hello 데모의 쉽도록 hello에 대 한 추가 해 보겠습니다 일부 표준 응용 프로그램 통찰력 리소스 tooour JSON 파일을 클릭 하 여 **리소스 추가**합니다. 관심이 있다면 방금 hello JSON 파일을 배포 하는 경우를 건너뜁니다 toohello 배포 단계입니다.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-3-newresource.png)
7. **Web Apps용 Application Insights**를 선택한 다음 기존 App Service 계획 및 웹앱을 선택했는지 확인하고 **추가**를 클릭합니다.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-4-newappinsight.png)
   
   이제 살펴볼 수 toosee 몇 가지 새로운 리소스 수, 어느 hello 앱 서비스 계획 또는 hello 웹 응용 프로그램에 종속 된 hello 리소스 및 역할에 따라, 합니다. 이러한 리소스의 기존 정의에서 활성화 되지 않으며 toochange 거입니다.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-5-appinsightresources.png)
8. JSON 개요 hello 클릭 **appInsights 자동 크기 조정** toohighlight JSON 코드입니다. 이 hello 배율 앱 서비스 계획에 대 한 설정입니다.
9. 강조 표시 된 JSON 코드 hello 하 hello 찾을 `location` 및 `enabled` 속성 아래 표시 된 것과 같이 설정 합니다.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-6-autoscalesettings.png)
10. JSON 개요 hello 클릭 **CPUHigh appInsights** toohighlight JSON 코드입니다. 이것은 경고입니다.
11. Hello 찾을 `location` 및 `isEnabled` 속성 아래 표시 된 것과 같이 설정 합니다. 마십시오 hello 동일 hello에 대 한 다른 3 개 경고 (자주색 전구).
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-7-alerts.png)
12. 이제 준비 toodeploy 것입니다. Hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **배포** > **새 배포**합니다.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-8-newdeployment.png)
13. 아직 수행하지 않은 경우 Azure 계정에 로그인합니다.
14. 구독에서 기존 리소스 그룹을 선택하거나 새 리소스 그룹을 만들고 **azuredeploy.json**을 클릭한 다음 **매개 변수 편집**을 클릭합니다.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-9-deployconfig.png)
    
    이제 좋은 테이블에서 템플릿 파일의 hello에 정의 된 모든 hello 매개 변수 수 tooedit 수 수 있습니다. 기본값을 정의하는 매개 변수는 기본값이 이미 있고 허용된 값의 목록을 정의하는 매개 변수는 드롭다운으로 표시됩니다.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-10-parametereditor.png)
15. 모든 hello 빈 매개 변수를 입력 하 고 hello를 사용 하 여 [ToDoApp에 대 한 GitHub 리포지토리에 주소](https://github.com/azure-appservice-samples/ToDoApp.git) 에 **repoUrl**합니다. 그런 다음 **저장**을 클릭합니다.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-11-parametereditorfilled.png)
    
    > [!NOTE]
    > 자동 크기 조정에서 제공 되는 기능은 **표준** 계층 또는 이상, 및 계획 수준 경고 기능에서 제공 되는 **기본** 계층 또는 tooset hello 필요 이상 **sku** 매개 변수가 너무**표준** 또는 **프리미엄** 의 순서로 toosee 모든 새 App Insights 리소스 켜 합니다.
    > 
    > 
16. **배포**를 클릭합니다. 선택한 경우 **암호를 저장**, hello 암호 hello 매개 변수 파일에 저장 됩니다 **일반 텍스트로**합니다. 그렇지 않으면 만들라는 메시지가 tooinput hello 데이터베이스 암호 hello 배포 프로세스 중입니다.

끝났습니다. Toogo toohello 하기만 하면 이제 [Azure 포털](https://portal.azure.com/) 및 hello [Azure 리소스 탐색기](https://resources.azure.com) 도구 toosee hello 새 경고 및 자동 크기 조정 설정이 tooyour JSON 배포 응용 프로그램을 추가 합니다.

이 섹션의 단계를 hello 다음 주로 수행 됩니다.

1. 준비 된 hello 템플릿 파일
2. Hello 템플릿 파일을 사용 하 여 매개 변수 파일 toogo 만든
3. Hello 매개 변수 파일이 있는 배포 된 hello 서식 파일

hello 마지막 단계는 PowerShell cmdlet에서 쉽게 이루어집니다. toosee Visual Studio 사용자 응용 프로그램을 열고 Scripts\Deploy-AzureResourceGroup.ps1 배포 때 않았습니다. 많은 코드, 있지만 두 개의 컨테이너 toohighlight 모든 hello 관련 코드 hello 매개 변수 파일이 있는 toodeploy hello 서식 파일이 필요 합니다.

![](./media/app-service-deploy-complex-application-predictably/deploy-12-powershellsnippet.png)

마지막 cmdlet hello `New-AzureResourceGroup`는 실제로 hello 작업을 수행 하는 hello 합니다. 이러한 모든를 사용 하 여 hello 도구는 비교적 간단 하므로 toodeploy tooyou 보여 주어 야 하면 예측 가능한 방식으로 응용 프로그램을 클라우드입니다. 동일한 hello에서 hello cmdlet을 실행 될 때마다 동일한 템플릿을 hello 매개 변수 파일 거 tooget hello 동일한 결과입니다.

## <a name="summary"></a>요약
DevOps, 반복성 및 예측 가능는 microservices로 구성 하는 확장성이 뛰어난 응용 프로그램의 키 tooany 성공적으로 배포 합니다. 이 자습서에서는 두 마이크로 서비스 응용 프로그램 tooAzure hello Azure 리소스 관리자 템플릿을 사용 하 여 단일 리소스 그룹으로 배포 했습니다. 지금까지 것가 제공한 hello 하면 Azure에서 응용 프로그램을 템플릿으로 변환 하는 순서 toostart에 필요한 수 프로 비전 하 고 예측 가능한 방식으로 기술 합니다. 

## <a name="next-steps"></a>다음 단계
너무 방법을 보려면[agile 방법론을 적용 하 고 지속적으로 쉽게 microservices 응용 프로그램을 게시](app-service-agile-software-development.md) 같은 배포 기술을 고급 [플 라이팅 배포](app-service-web-test-in-production-controlled-test-flight.md) 쉽게 합니다.

<a name="resources"></a>

## <a name="more-resources"></a>추가 리소스
* [Azure 리소스 관리자 템플릿 언어](../azure-resource-manager/resource-group-authoring-templates.md)
* [Azure 리소스 관리자 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)
* [Azure 리소스 관리자 템플릿 함수](../azure-resource-manager/resource-group-template-functions.md)
* [Azure 리소스 관리자 템플릿으로 응용 프로그램 배포](../azure-resource-manager/resource-group-template-deploy.md)
* [Azure 리소스 관리자로 Azure PowerShell 사용](../azure-resource-manager/powershell-azure-resource-manager.md)
* [Azure에서 리소스 그룹 배포 문제 해결](../azure-resource-manager/resource-manager-common-deployment-errors.md)

