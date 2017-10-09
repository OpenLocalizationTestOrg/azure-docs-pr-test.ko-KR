---
title: "Azure 논리 앱에 대 한 배포 템플릿을 aaaCreate | Microsoft Docs"
description: "논리 앱 배포 및 릴리스 관리용 Azure Resource Manager 템플릿 만들기"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 85928ec6-d7cb-488e-926e-2e5db89508ee
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 2f09445f10a376a745d6acbba94ca29d5f79fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-templates-for-logic-apps-deployment-and-release-management"></a>논리 앱 배포 및 릴리스 관리용 템플릿 만들기

Toocreate 경우가 논리 앱을 만든 후 Azure 리소스 관리자 템플릿으로 것입니다.
이러한 방식으로 할 수 있는 리소스 그룹 또는 hello 논리 앱 tooany 환경을 쉽게 배포할 수 있습니다.
Resource Manager 템플릿에 대한 자세한 내용은 [Azure Resource Manager 작성](../azure-resource-manager/resource-group-authoring-templates.md) 및 [Azure Resource Manager 템플릿을 사용하여 리소스 배포](../azure-resource-manager/resource-group-template-deploy.md)를 확인하세요.

## <a name="logic-app-deployment-template"></a>논리 앱 배포 템플릿

논리 앱은 세 가지 기본 구성 요소가 있습니다.

* **논리 앱 리소스**: 계획, 위치 및 hello 워크플로 정의 가격 등의 작업에 대 한 정보를 포함 합니다.
* **워크플로 정의**: 논리 앱 워크플로 단계 및 hello 논리 앱 엔진 해야 hello 워크플로 실행 하는 방법에 대해 설명 합니다.
논리 앱의 **코드 보기** 창에서 이 정의를 볼 수 있습니다.
Hello 논리 앱 리소스를 찾을 수 있습니다이 정의 hello에 `definition` 속성입니다.
* **연결**: 연결 문자열 및 액세스 토큰 등의 모든 커넥터 연결에 대 한 메타 데이터를 안전 하 게 저장 tooseparate 리소스를 참조 합니다.
논리 앱 hello 논리 앱 리소스에서 hello에 이러한 리소스를 참조 `parameters` 섹션.

[Azure Resource Explorer](http://resources.azure.com)와 같은 도구를 사용하여 기존 Logic Apps에 대한 이런 모든 내용을 볼 수 있습니다.

템플릿 toomake 논리 앱 toouse 리소스 그룹 배포에 대 한 hello 리소스 정의 및 필요에 따라 매개 변수화 해야 합니다.
예를 들어 tooa 개발, 테스트 및 프로덕션 환경을 배포 하는 경우 사용할 수도 있습니다 각 환경에 toouse 다른 연결 문자열 tooa SQL 데이터베이스.
또는 서로 다른 구독 또는 리소스 그룹 내에서 toodeploy 할 수 있습니다.  

## <a name="create-a-logic-app-deployment-template"></a>논리 앱 배포 템플릿 만들기

hello 가장 쉬운 방법은 toohave 유효한 논리 앱 배포 템플릿에 toouse는 [논리 앱 용 도구 Visual Studio](logic-apps-deploy-from-vs.md)합니다.
Visual Studio tools hello 위치 또는 구독에서 사용할 수 있는 올바른 배포 템플릿을 생성 합니다.

논리 앱 배포 템플릿을 만들 때 도움을 받을 수 있는 다른 몇 가지 도구가 있습니다.
직접 작성할 수 있습니다, 즉, hello를 사용 하 여 리소스 이미 여기에 설명 toocreate 매개 변수가 필요에 따라 합니다.
두 번째 방법은 toouse는 [논리 앱 템플릿 작성자](https://github.com/jeffhollan/LogicAppTemplateCreator) PowerShell 모듈입니다. 이 오픈 소스 모듈에는 먼저 hello 논리 앱 및 모든 연결을 사용 하는 다음 배포에 대 한 hello 필요한 매개 변수를 사용 하 여 템플릿 리소스를 생성 하 평가 합니다.
예를 들어 Azure 서비스 버스 큐에서 메시지를 받은 데이터 tooan Azure SQL 데이터베이스를 추가 하는 논리 앱이 있는 경우 hello 도구 모든 hello 오케스트레이션 논리를 유지 하 고 설정할 수 있도록 SQL hello 및 서비스 버스 연결 문자열을 매개 변수화 에 배포 합니다.

> [!NOTE]
> 연결 hello 내에 있어야 합니다. 논리 앱 hello와 동일한 리소스 그룹입니다.
>
>

### <a name="install-hello-logic-app-template-powershell-module"></a>Hello 논리 앱 템플릿을 PowerShell 모듈 설치
hello를 통해 hello 가장 쉬운 방법은 tooinstall hello 모듈은 [PowerShell 갤러리](https://www.powershellgallery.com/packages/LogicAppTemplate/0.1), hello 명령을 사용 하 여 `Install-Module -Name LogicAppTemplate`합니다.  

또한 수동으로 설치할 수 있습니다 hello PowerShell 모듈:

1. Hello 최신 릴리스의 hello 다운로드 [논리 앱 템플릿 작성자](https://github.com/jeffhollan/LogicAppTemplateCreator/releases)합니다.  
2. PowerShell 모듈 폴더에 있는 hello 폴더 (일반적으로 `%UserProfile%\Documents\WindowsPowerShell\Modules`).

모든 테 넌 트 및 구독 액세스 권한이 있는 모듈 toowork hello에 대 한 hello로 사용할 토큰, 권장 [ARMClient](https://github.com/projectkudu/ARMClient) 명령줄 도구입니다.  이 [블로그 게시물](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html)은 ARMClient에 대해 자세히 설명 합니다.

### <a name="generate-a-logic-app-template-by-using-powershell"></a>PowerShell을 사용하여 논리 앱 템플릿 생성
PowerShell을 설치한 후 다음 명령을 hello를 사용 하 여 서식 파일을 생성할 수 있습니다.

`armclient token $SubscriptionId | Get-LogicAppTemplate -LogicApp MyApp -ResourceGroup MyRG -SubscriptionId $SubscriptionId -Verbose | Out-File C:\template.json`

`$SubscriptionId`hello Azure 구독 ID입니다. 이 줄 먼저 액세스 토큰 ARMClient를 통해 다음 toohello PowerShell 스크립트를 통해 파이프을 가져오고 JSON 파일에 hello 서식 파일을 만듭니다.

## <a name="add-parameters-tooa-logic-app-template"></a>Tooa 논리 앱 템플릿은 매개 변수를 추가 합니다.
논리 앱 템플릿을 만든 후 tooadd 계속 하거나 필요할 수 있는 매개 변수를 수정할 수 있습니다. 예를 들어 정의 리소스 ID tooan Azure 함수 또는 toodeploy를 단일 배포를 계획 하는 중첩 된 워크플로 포함 하는 경우 더 많은 리소스 tooyour 서식 파일을 추가 및 필요에 따라 Id를 매개 변수화 수 있습니다. hello 마찬가지 tooany 참조 toocustom Api 또는 Swagger 끝점 toodeploy 각 리소스 그룹으로 예상입니다.

## <a name="deploy-a-logic-app-template"></a>논리 앱 템플릿 배포

PowerShell, REST API와 같은 도구를 사용 하 여 서식 파일을 배포할 수 있습니다 [Visual Studio Team Services Release Management](#team-services), 및 hello Azure 포털을 통해 템플릿 배포 합니다.
또한 toostore hello 매개 변수 값을, 좋습니다 만드는 [매개 변수 파일](../azure-resource-manager/resource-group-template-deploy.md#parameter-files)합니다.
너무 방법에 대해 알아봅니다[Azure 리소스 관리자 템플릿 및 PowerShell을 사용 하 여 리소스를 배포](../azure-resource-manager/resource-group-template-deploy.md) 또는 [Azure 리소스 관리자 템플릿 사용 하 여 리소스를 배포 하 고 Azure 포털 hello](../azure-resource-manager/resource-group-template-deploy-portal.md)합니다.

### <a name="authorize-oauth-connections"></a>OAuth 연결 권한 부여

배포 후 hello 논리 앱 종단 유효한 매개 변수와 함께 작동합니다.
그러나 OAuth 연결 toogenerate 유효한 액세스 토큰이 아직 권한을 부여 해야 합니다.
tooauthorize OAuth 연결 hello 논리 앱을 열고 hello 논리 앱 디자이너에서에서 이러한 연결 권한을 부여 합니다. 또는 자동화 된 배포 스크립트 tooconsent tooeach OAuth 연결을 사용할 수 있습니다.
GitHub에 [LogicAppConnectionAuth](https://github.com/logicappsio/LogicAppConnectionAuth) 프로젝트라는 예시가 있습니다.

<a name="team-services"></a>
## <a name="visual-studio-team-services-release-management"></a>Visual Studio Team Services 릴리스 관리

배포 및 관리 환경에 대 한 일반적인 시나리오에는 toouse 논리 앱 배포 템플릿 사용 하 여 Visual Studio Team Services에서 Release Management와 같은 도구입니다. Visual Studio Team Services에 포함 되어는 [Azure 리소스 그룹 배포](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/DeployAzureResourceGroup) 작업 tooany 빌드 추가할 수 또는 파이프라인을 해제 합니다. Toohave 필요는 [서비스 사용자](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/) 권한 부여 toodeploy, 한 다음 생성할 수 있으며, hello 릴리스 정의 합니다.

1. 릴리스 관리에서 빈 정의를 생성할 수 있도록 **비어 있음**을 선택합니다.

    ![빈 정의 만들기][1]

2. 빌드 프로세스에이 가장 가능성이 높은 포함 하 여 hello 논리 앱 템플릿은 수동으로 또는 hello의 일부로 생성 되는 필요한 모든 리소스를 선택 합니다.
3. **Azure 리소스 그룹 배포** 작업을 추가합니다.
4. 사용 하 여 구성는 [서비스 사용자](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/), hello 템플릿과 템플릿 매개 변수 파일을 참조 하 고 있습니다.
5. 다른 환경, 자동화 된 테스트 또는 필요에 따라 승인자에 대 한 hello 릴리스 프로세스에서 toobuild 단계를 계속 합니다.

<!-- Image References -->
[1]: ./media/logic-apps-create-deploy-template/emptyreleasedefinition.png
