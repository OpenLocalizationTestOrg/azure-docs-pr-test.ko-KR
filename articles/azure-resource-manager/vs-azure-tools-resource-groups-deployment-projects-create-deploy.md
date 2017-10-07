---
title: "aaaVisual Studio Azure 리소스 그룹 프로젝트 | Microsoft Docs"
description: "Visual Studio toocreate Azure 리소스 그룹 프로젝트를 사용 하 하 고 hello 리소스 tooAzure 배포."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 4bd084c8-0842-4a10-8460-080c6a085bec
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: tomfitz
ms.openlocfilehash: 672c1e71fb809b3b547f0fad30240d45de1ba923
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-deploying-azure-resource-groups-through-visual-studio"></a>Visual Studio를 통해 Azure 리소스 그룹 만들기 및 배포
Visual Studio 및 hello [Azure SDK](https://azure.microsoft.com/downloads/), 인프라 및 코드 tooAzure를 배포 하는 프로젝트를 만들 수 있습니다. 예를 들어 응용 프로그램에 대 한 hello 웹 호스트, 웹 사이트 및 데이터베이스를 정의 하 고 hello 코드와 함께 해당 인프라를 배포할 수 있습니다. 또는 가상 컴퓨터, 가상 네트워크 및 저장소 계정을 정의하고 가상 컴퓨터에서 실행되는 스크립트와 함께 해당 인프라를 배포할 수 있습니다. hello **Azure 리소스 그룹** 배포 프로젝트를 반복 가능한 단일 작업에서 모든 필요한 hello 리소스가 toodeploy 있습니다 수 있습니다. 리소스 배포 및 관리에 대한 자세한 내용은 [Azure 리소스 관리자 개요](resource-group-overview.md)를 참조하세요.

Azure 리소스 그룹 프로젝트 tooAzure를 배포 하는 hello 리소스를 정의 하는 Azure 리소스 관리자 JSON 템플릿이 포함 됩니다. toolearn hello 리소스 관리자 템플릿 hello 요소에 대 한 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다. Visual Studio tooedit 있습니다 이러한 서식 파일을 사용 하 고 서식 파일 사용을 단순화 하는 도구를 제공 합니다.

이 문서에서는 웹앱 및 SQL Database를 배포합니다. 그러나 hello 단계 거의 모든 종류의 리소스에 대 한 동일한 hello 됩니다. 가상 컴퓨터와 관련된 리소스를 손쉽게 배포할 수 있습니다. Visual Studio는 일반 시나리오를 배포하기 위한 다양한 서로 다른 시작 템플릿을 제공합니다.

이 문서에서는 Visual Studio 2017을 보여 줍니다. .NET 2.9에 대 한 Visual Studio 2015 업데이트 2와 Microsoft Azure SDK를 사용 하거나 Azure SDK 2.9에서는 환경 Visual Studio 2013은 주로 경우 hello 동일 합니다. Hello Azure SDK 2.6 이상;의 버전을 사용할 수 있습니다. 그러나 hello 사용자 인터페이스의 경험이이 문서에 표시 된 hello 사용자 인터페이스 보다 다를 수 있습니다. 최신 버전의 hello hello를 설치 하는 것이 좋습니다 [Azure SDK](https://azure.microsoft.com/downloads/) hello 단계를 시작 하기 전에. 

## <a name="create-azure-resource-group-project"></a>Azure 리소스 그룹 프로젝트 만들기
이 절차에서 **웹앱 + SQL** 템플릿으로 Azure 리소스 그룹 프로젝트를 만듭니다.

1. Visual Studio에서 **파일**, **새 프로젝트**를 선택하고 **C#** 또는 **Visual Basic**을 선택합니다. 그런 다음 **클라우드**, **Azure 리소스 그룹** 프로젝트를 차례로 선택합니다.
   
    ![Cloud Deployment 프로젝트](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-project.png)
2. Hello 템플릿 선택 toodeploy tooAzure 리소스 관리자 되도록 합니다. 프로젝트의 다양 한 옵션 hello에 따라 입력는 공지 toodeploy를 원하는 합니다. 이 문서에 대 한 선택 hello **웹 응용 프로그램 + SQL** 템플릿.
   
    ![템플릿 선택](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-project.png)
   
    선택 하는 hello 서식 파일은 이제 시작 지점입니다. 추가 하 고 리소스 toofulfill 시나리오를 제거할 수 있습니다.
   
   > [!NOTE]
   > Visual Studio은 온라인에서 사용 가능한 템플릿 목록을 검색합니다. hello 목록 변경 될 수 있습니다.
   > 
   > 
   
    Visual Studio hello web app 및 SQL 데이터베이스에 대 한 리소스 그룹 배포 프로젝트를 만듭니다.
3. toosee 작성, 봐 hello 배포 프로젝트의 hello 노드에서 합니다.
   
    ![노드 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-items.png)
   
    이 예제에 대 한 SQL 템플릿 + hello 웹 응용 프로그램을 선택 했으므로 hello 다음 파일이 표시 됩니다. 
   
   | 파일 이름 | 설명 |
   | --- | --- |
   | Deploy-AzureResourceGroup.ps1 |PowerShell 명령 toodeploy tooAzure 리소스 관리자를 호출 하는 PowerShell 스크립트입니다.<br />**참고** Visual Studio에서는이 PowerShell 스크립트 toodeploy 서식 파일에 있습니다. 모든 변경 사항은 toothis 스크립트 Visual Studio에서 배포에 영향을 주의 기울여야 합니다. |
   | WebSiteSQLDatabase.json |tooAzure, 배포할 hello 인프라 및 배포 하는 동안 제공할 수 있습니다 hello 매개 변수를 정의 하는 hello 리소스 관리자 템플릿을 합니다. 또한 리소스 관리자 hello 올바른 순서로 hello 리소스를 배포 하도록 hello 리소스 간의 hello 종속성을 정의 합니다. |
   | WebSiteSQLDatabase.parameters.json |Hello 서식 파일에 필요한 값을 포함 하는 매개 변수 파일입니다. 각 배포 매개 변수 값 toocustomize에 전달합니다. |
   
    모든 리소스 그룹 배포 프로젝트는 이러한 기본 파일을 포함합니다. 다른 프로젝트는 다른 기능 추가 파일 toosupport 포함 될 수 있습니다.

## <a name="customize-hello-resource-manager-template"></a>Hello 리소스 관리자 템플릿을 사용자 지정
원하는 toodeploy hello 리소스를 설명 하는 hello JSON 템플릿을 수정 하 여 배포 프로젝트를 사용자 지정할 수 있습니다. JSON에 대 한 JavaScript 개체 Object Notation 의미 하 고는와 쉽게 toowork 있는 serialize 된 데이터 형식입니다. hello JSON 파일에서 각 파일의 맨 위에 hello 참조 하는 스키마를 사용 합니다. Toounderstand hello 스키마를 사용 하도록 하려는 경우 다운로드 하 고 분석할 수 있습니다. hello 스키마 정의 어떤 요소가 유효한 hello 형식 및 필드의 형식 열거형된 값의 가능한 값 hello 하 고, 합니다. toolearn hello 리소스 관리자 템플릿 hello 요소에 대 한 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.

서식 파일을에 toowork 열고 **WebSiteSQLDatabase.json**합니다.

hello 편집기에서는 Visual Studio 도구 tooassist 리소스 관리자 템플릿을 hello 편집 하면 합니다. hello **JSON 개요** 창을 사용 하 여 서식 파일에 정의 된 쉽게 toosee hello 요소입니다.

![JSON 개요 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-json-outline.png)

Hello 개요에서 hello 요소 중 하나를 선택 하면 hello 템플릿의 toothat 일부를 사용 하 고 JSON에 해당 하는 hello를 강조 표시 합니다.

![JSON로 이동](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/navigate-json.png)

중 하나가 선택 hello 여 리소스를 추가할 수 있습니다 **리소스 추가** hello JSON 개요 창의 하거나 마우스 오른쪽 단추로 클릭 하 여 hello 위쪽에 단추 **리소스** 선택 하 고 **새 리소스 추가**.

![리소스 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource.png)

이 자습서의 경우 **저장소 계정** 을 선택하고 이름을 지정합니다. 11개 미만의 문자이며 숫자 및 소문자만을 포함하는 이름을 제공합니다.

![저장소 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-storage.png)

Hello 리소스 추가 된 뿐만 아니라 hello에 대 한 매개 변수 입력 저장소 계정과의 hello 저장소 계정 이름 hello에 대 한 변수를 확인 합니다.

![개요 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-new-items.png)

hello **storageType** 매개 변수는 미리 정의 된 허용된 유형 및 기본 형식을 사용 합니다. 이러한 값을 유지하거나 시나리오에 대해 편집할 수 있습니다. 하지 않을 경우 모든 사용자 toodeploy는 **Premium_LRS** 이 서식 파일을 통해 저장소 계정 hello 허용 되는 형식에서에서 제거 합니다. 

```json
"storageType": {
  "type": "string",
  "defaultValue": "Standard_LRS",
  "allowedValues": [
    "Standard_LRS",
    "Standard_ZRS",
    "Standard_GRS",
    "Standard_RAGRS"
  ]
}
```

Visual Studio intellisense toohelp 어떤 속성을 이해 하는 hello 템플릿을 편집 하는 경우에 사용할 수 또한 제공 합니다. 앱 서비스 계획에 대 한 tooedit hello 속성 toohello를 이동 하는 예를 들어 **HostingPlan** 리소스 hello에 대 한 값을 추가 하 고 **속성**합니다. Hello 사용 가능한 값을 표시 하 고 해당 값에 대 한 설명을 제공 하는 intellisense를 확인 합니다.

![intellisense 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-intellisense.png)

설정할 수 있습니다 **작업자** too1 합니다.

```json
"properties": {
  "name": "[parameters('hostingPlanName')]",
  "numberOfWorkers": 1
}
```

## <a name="deploy-hello-resource-group-project-tooazure"></a>리소스 그룹 프로젝트 tooAzure hello 배포
사용자는 이제 준비 toodeploy 프로젝트입니다. Azure 리소스 그룹 프로젝트를 배포 하면 tooan Azure 리소스 그룹을 배포 합니다. hello 리소스 그룹은 일반적인 수명 주기를 공유 하는 리소스의 논리적 그룹입니다.

1. Hello hello 배포 프로젝트 노드의 바로 가기 메뉴를 선택 **배포** > **새로**합니다.
   
    ![배포, 새 배포 메뉴 항목](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/deploy.png)
   
    hello **tooResource 그룹 배포** 대화 상자가 나타납니다.
   
    ![TooResource 그룹 대화 상자 배포](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployment.png)
2. Hello에 **리소스 그룹** 드롭다운 상자에서 기존 리소스 그룹을 선택 하거나 새로 만듭니다. 리소스 그룹 toocreate 열기 hello **리소스 그룹** 드롭다운 확인란을 선택한 **새로 만들기**합니다.
   
    ![TooResource 그룹 대화 상자 배포](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-new-group.png)
   
    hello **리소스 그룹 만들기** 대화 상자가 나타납니다. 이름 및 위치, 사용자 그룹을 지정 하 고 hello 선택 **만들기** 단추입니다.
   
    ![리소스 그룹 만들기 대화 상자](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-resource-group.png)
3. Hello를 선택 하 여 hello 배포에 대 한 hello 매개 변수를 편집 **매개 변수 편집** 단추입니다.
   
    ![매개 변수 편집 단추](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/edit-parameters.png)
4. Hello 빈 매개 변수 값을 제공 하 고 hello 선택 **저장** 단추입니다. hello 빈 매개 변수는 **hostingPlanName**, **administratorLogin**, **administratorLoginPassword**, 및 **databaseName**합니다.
   
    **hostingPlanName** hello에 대 한 이름을 지정 [앱 서비스 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) toocreate 합니다. 
   
    **administratorLogin** hello SQL Server 관리자에 대 한 hello 사용자 이름을 지정 합니다. **sa** 또는 **admin**과 같은 일반 관리자 이름을 사용하지 않습니다. 
   
    hello **administratorLoginPassword** SQL Server 관리자에 대 한 암호를 지정 합니다. hello **hello 매개 변수 파일에 일반 텍스트로 암호를 저장** 옵션 없는 보안; 이므로이 옵션을 선택 하지 마십시오. Hello 암호를 일반 텍스트로 저장 되지 않으면 해야 tooprovide이이 암호 다시 배포 하는 동안. 
   
    **databaseName** 데이터베이스 toocreate hello에 대 한 이름을 지정 합니다. 
   
    ![매개 변수 편집 대화 상자](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/provide-parameters.png)
5. Hello 선택 **배포** 단추 toodeploy hello 프로젝트 tooAzure 합니다. Hello Visual Studio 인스턴스 외부에서 PowerShell 콘솔을 엽니다. 메시지가 표시 되 면 hello PowerShell 콘솔에 hello SQL Server 관리자 암호를 입력 합니다. **PowerShell 콘솔 다른 항목 뒤 숨기 거 나 hello 작업 표시줄에 최소화 될 수 있습니다.** 이 콘솔 살펴보고 tooprovide hello 암호를 선택 합니다.
   
   > [!NOTE]
   > Visual Studio tooinstall hello Azure PowerShell cmdlet을 요청할 수 있습니다. Azure PowerShell hello 필요한 cmdlet toosuccessfully 리소스 그룹을 배포 합니다. 메시지가 표시되면 설치합니다.
   > 
   > 
6. hello 배포는 몇 분 정도 걸릴 수 있습니다. Hello에 **출력** windows hello 배포의 hello 상태를 표시 합니다. Hello 배포 완료 되 면 hello 마지막 메시지와 유사한 항목을 성공적으로 배포를 나타냅니다.
   
        ... 
        18:00:58 - Successfully deployed template 'websitesqldatabase.json' tooresource group 'DemoSiteGroup'.
7. 브라우저를 열고 hello [Azure 포털](https://portal.azure.com/) tooyour 계정에 로그인 합니다. toosee hello 리소스 그룹을 선택 **리소스 그룹** 및 hello 리소스 그룹에 배포 합니다.
   
    ![그룹 선택](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-group.png)
8. 배포 된 hello 리소스를 모두 표시 합니다. 저장소 계정이 아닙니다 정확히 어떤 사용자가 해당 리소스를 추가할 때 지정한 hello의 해당 hello 이름을 확인 합니다. hello 저장소 계정은 고유 해야 합니다. hello 템플릿을 자동으로 추가 하는 문자열 문자 toohello 이름의 있습니다 tooprovide 고유 이름을 제공 합니다. 
   
    ![리소스 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-resources.png)
9. 변경을 수행 하 고 프로젝트 tooredeploy를 원하는 경우 hello Azure 리소스 그룹 프로젝트 바로 가기 메뉴에서 hello 기존 리소스 그룹을 선택 합니다. Hello 바로 가기 메뉴에서 선택 **배포**, 배포 된 hello 리소스 그룹을 선택 합니다.
   
    ![배포된 Azure 리소스 그룹](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/redeploy.png)

## <a name="deploy-code-with-your-infrastructure"></a>인프라를 사용하여 코드 배포
이 시점에서 응용 프로그램에 대 한 hello 인프라를 배포한 있지만 hello 프로젝트와 함께 배포 실제 코드가 없습니다. 이 문서에서는 어떻게 toodeploy 웹 응용 프로그램 및 SQL 데이터베이스 테이블을 배포 하는 동안 보여 줍니다. 웹 앱 대신 가상 컴퓨터를 배포 하는 경우 배포의 일부로 hello 시스템에서 일부 코드 toorun 할 수 있습니다. 웹 앱에 대 한 코드를 배포 하기 위한 프로세스 hello 또는 거의 가상 컴퓨터를 설정에 대 한 hello 동일 합니다.

1. 프로젝트 tooyour Visual Studio 솔루션을 추가 합니다. Hello 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** > **새 프로젝트**합니다.
   
    ![프로젝트 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-project.png)
2. **ASP.NET 웹 응용 프로그램**을 추가합니다. 
   
    ![웹앱 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-app.png)
3. **MVC**를 선택합니다.
   
    ![MVC 선택](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-mvc.png)
4. Visual Studio에서 웹 앱을 만드는 hello 솔루션의 두 프로젝트가 모두 표시 됩니다.
   
    ![프로젝트 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-projects.png)
5. 이제, 리소스 그룹 프로젝트는 hello 새 프로젝트를 인식 하는지 toomake를 해야 합니다. Tooyour 리소스 그룹 프로젝트 (AzureResourceGroup1)로 돌아갑니다. **참조**를 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 선택합니다.
   
    ![참조 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-new-reference.png)
6. 만든 hello 웹 응용 프로그램 프로젝트를 선택 합니다.
   
    ![참조 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-reference.png)
   
    참조를 추가 하 여 hello 웹 응용 프로그램 프로젝트 toohello 리소스 그룹 프로젝트를 연결 하 고 자동으로 세 가지 주요 속성을 설정 합니다. Hello에서 이러한 속성을 참조 **속성** hello 참조에 대 한 창.
   
      ![참조 보기](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/see-reference.png)
   
    hello 속성은 같습니다.
   
   * hello **추가 속성** hello 웹 배포 패키지를 스테이징 밀어넣어 toohello Azure 저장소 위치를 포함 합니다. 참고 hello 폴더 (ExampleApp) 및 (package.zip) 파일입니다. 이 값이 필요 하면 tooknow 이러한 제공 하기 때문에 이러한 매개 변수를 배포할 때 hello 응용 프로그램으로 합니다. 
   * hello **포함 파일 경로** hello 경로 hello 패키지를 만들 위치를 포함 합니다. hello **포함 대상** 배포를 실행 하는 hello 명령이 포함 되어 있습니다. 
   * 기본값을 hello **빌드합니다. 패키지** 배포 toobuild hello를 사용 하 고 웹 배포 패키지 (package.zip)를 만듭니다.  
     
     Hello 배포 hello 속성 toocreate hello 패키지에서 필요한 정보를 hello 가져옵니다으로 게시 프로필을 않아도 됩니다.
7. TooWebSiteSQLDatabase.json 돌아가서 리소스 toohello 템플릿을 추가 하십시오.
   
    ![리소스 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource-2.png)
8. 이번에는 **Web Apps에 대한 웹 배포**를 선택합니다. 
   
    ![웹 배포 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-web-deploy.png)
9. 리소스 그룹 프로젝트 toohello 리소스 그룹을 다시 배포 합니다. 이번에는 몇 가지 새로운 매개 변수가 있습니다. Tooprovide 값에 대 한 불필요 **_artifactsLocation** 또는 **_artifactsLocationSasToken** Visual Studio 해당 값을 자동으로 생성 하기 때문입니다. 그러나 tooset hello 폴더 및 hello 배포 패키지를 포함 하는 파일 이름 toohello 경로 있을 (으로 표시 **ExampleAppPackageFolder** 및 **ExampleAppPackageFileName** hello 이미지 뒤에 ). 이전에 본 hello 값 hello 참조 속성을 제공 (**ExampleApp** 및 **package.zip**).
   
    ![웹 배포 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/set-new-parameters.png)
   
    Hello에 대 한 **아티팩트 저장소 계정**, 선택 hello 하나이 리소스 그룹을 사용 하 여 배포 합니다.
10. Hello 배포가 완료 된 후 hello 포털에서 웹 앱을 선택 합니다. Hello URL toobrowse toohello 사이트를 선택 합니다.
    
     ![사이트 찾아보기](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/browse-site.png)
11. Hello 기본 ASP.NET 앱을 정상적으로 배포 된 것을 확인 합니다.
    
     ![배포된 앱 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-app.png)

## <a name="next-steps"></a>다음 단계
* toolearn hello 포털을 통해 리소스를 관리 하는 방법에 대 한 참조 [사용 하 여 Azure 리소스를 Azure 포털 toomanage hello](resource-group-portal.md)합니다.
* 서식 파일에 대해 자세히 toolearn 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.

