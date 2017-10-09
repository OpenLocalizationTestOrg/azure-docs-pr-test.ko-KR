---
title: "aaaCreate, 빌드 및 Visual Studio-Azure 논리 앱에서에서 논리 앱 배포 | Microsoft Docs"
description: "Azure Logic Apps를 디자인, 빌드 및 배포할 수 있도록 Visual Studio 프로젝트를 만듭니다."
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 5154cb05f9a48e9f0f2381a6953947217f7bb114
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a>Visual Studio에서 Azure Logic Apps 디자인, 빌드 및 배포

하지만 hello [Azure 포털](https://portal.azure.com/) toocreate 수 있는 좋은 방법 제공 Azure 논리 앱을 관리 하 고, 설계, 구축 및 논리 앱 배포에 대 한 Visual Studio를 사용할 수 있습니다. Visual Studio hello 논리가 응용 프로그램 디자이너와 같은 풍부한 도구 있습니다 toocreate 논리 앱, 배포 및 자동화 템플릿 구성 하며 tooany 환경을 배포 합니다. 

자세한 내용은 Azure 논리 앱 시작 tooget [어떻게 toocreate hello Azure 포털에서에서 첫 번째 논리 앱](logic-apps-create-a-logic-app.md)합니다.

## <a name="installation-steps"></a>설치 단계

tooinstall 및 Visual Studio tools for Azure 논리 앱 구성, 다음이 단계를 수행 합니다.

### <a name="prerequisites"></a>필수 조건

* [Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) 또는 Visual Studio 2015
* [최신 Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 이상)
* [Azure PowerShell](https://github.com/Azure/azure-powershell#installation)
* 액세스 toohello 웹 hello 포함 된 디자이너를 사용 하는 경우

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a>Azure Logic Apps용 Visual Studio 도구 설치

Hello 필수 구성 요소를 설치한 후:

1. Visual Studio를 엽니다. Hello에 **도구** 메뉴 선택 **확장명 및 업데이트**합니다.
2. Hello 확장 **온라인** 범주 온라인을 검색할 수 있도록 합니다.
3. **Visual Studio용 Azure Logic Apps 도구**를 찾을 때까지 **Logic Apps**을 찾아보거나 검색합니다.
4. toodownload 및 설치 hello 확장 클릭 **다운로드**합니다.
5. 설치 후 Visual Studio를 다시 시작합니다.

> [!NOTE]
> 다운로드할 수 있습니다 [Visual Studio 2017 용 Azure 논리 앱 도구](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) 및 hello [Visual Studio 2015 용 Azure 논리 앱 도구](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) hello Visual Studio 마켓플레이스에서 직접 합니다.

설치를 완료 한 후 논리 앱 디자이너로 hello Azure 리소스 그룹 프로젝트를 사용할 수 있습니다.

## <a name="create-your-project"></a>프로젝트 만들기

1. Hello에 **파일** 메뉴 너무 이동**새로**를 선택 하 고 **프로젝트**합니다. 또는 tooadd 너무 솔루션을 이동 기존 프로그램 프로젝트 tooan**추가**를 선택 하 고 **새 프로젝트**합니다.

    ![파일 메뉴](./media/logic-apps-deploy-from-vs/filemenu.png)

2. Hello에 **새 프로젝트** 창 찾기 **클라우드**를 선택 하 고 **Azure 리소스 그룹**합니다. 프로젝트 이름을 지정하고 **확인**을 클릭합니다.

    ![새 프로젝트 추가](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. 선택 hello **논리 앱** toouse 사용자를 위해 빈 논리 앱 배포 템플릿을 만드는 있는 템플릿을 사용 합니다. 템플릿을 선택한 후에 **확인**을 클릭합니다.

    ![Logic App 템플릿 선택](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    이제 논리 앱 프로젝트 tooyour 솔루션을 추가 했습니다. 
    배포 파일은 hello 솔루션 탐색기에에서 표시 됩니다.

    ![배포 파일](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a>Logic App Designer에서 논리 앱 만들기

논리 앱을 포함 하는 Azure 리소스 그룹 프로젝트를 사용 하는 경우 워크플로 toocreate Visual Studio에서에서 논리 응용 프로그램 디자이너 hello 열 수 있습니다. 

> [!NOTE]
> hello 디자이너에서 사용 가능한 속성 및 데이터에 대 한 커넥터를 너무 쿼리 하는 인터넷에 연결 합니다. 예를 들어 hello Dynamics CRM Online 커넥터를 사용 하는 경우 hello 디자이너 CRM 인스턴스 tooshow 사용할 수 있는 사용자 지정 및 기본 속성을 쿼리 합니다.

1. `<template>.json` 파일을 마우스 오른쪽 단추로 클릭하고 **Logic App Designer로 열기**를 선택합니다. (`Ctrl+L`)

2. Azure 구독, 리소스 그룹 및 배포 템플릿의 위치를 선택합니다.

    > [!NOTE]
    > 논리 앱을 디자인하면 디자인하는 동안 속성을 쿼리하는 API 연결 리소스가 만들어집니다. Visual Studio 디자인 타임 동안 선택한 리소스 그룹 toocreate 해당 연결을 사용 합니다. tooview 하거나 모든 API 연결 변경, toohello Azure 포털을 이동 하 고 찾아보기 **API 연결**합니다.

    ![구독 선택기](./media/logic-apps-deploy-from-vs/designer_picker.png)

    hello 디자이너 hello 정의 사용 하 여 hello에 `<template>.json` 렌더링에 대 한 파일입니다.

4. 논리 앱을 만들고 디자인합니다. 배포 템플릿에는 변경 내용이 업데이트됩니다.

    ![Visual Studio의 Logic App Designer](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

Visual Studio 추가 `Microsoft.Web/connections` 리소스 너무 리소스 파일 모든 연결에 대해 논리 앱 toofunction를 프로비저닝해야 합니다. 이러한 연결 속성을 배포할 때 설정 및 배포한 후 관리할 수 **API 연결** hello Azure 포털의에서.

### <a name="switch-toojson-code-view"></a>스위치 tooJSON 코드 보기

tooshow hello 선택 hello 논리가 응용 프로그램에 대 한 JSON 표현 **코드 보기** hello hello 디자이너 맨 아래에 탭 합니다.

tooswitch JSON toohello 전체 리소스를 다시 마우스 오른쪽 단추로 hello `<template>.json` 파일을 찾아 선택 **열려**합니다.

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a>종속 리소스 tooVisual Studio 배포 템플릿에 대 한 참조를 추가 합니다.

논리 앱 tooreference 종속 리소스를 원하는 경우 사용할 수 있습니다 [Azure 리소스 관리자 템플릿 함수](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) 논리 앱 배포 템플릿에 합니다. 예를 들어 논리 앱 tooreference 논리 앱 함께 toodeploy 되도록 Azure 기능 또는 통합 계정 좋습니다. 배포 템플릿에 hello 논리가 응용 프로그램 디자이너 하므로 toouse 매개 변수가 올바르게 렌더링 하는 방법에 대 한 다음이 지침을 따릅니다. 

이러한 종류의 트리거 및 작업에서 논리 앱 매개 변수를 사용할 수 있습니다.

*   하위 워크플로
*   함수 앱
*   APIM 호출
*   API 연결 런타임 URL
*   API 연결 경로

parameters, variables, resourceId, concat 등과 같은 템플릿 함수를 사용할 수 있습니다. 예를 들어 다음과 같습니다 어떻게 hello Azure 함수 리소스 ID를 바꿀 수 있습니다.

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

그리고 매개 변수를 사용하는 위치는 다음과 같습니다.

```
"MyFunction": {
    "type": "Function",
    "inputs": {
        "body":{},
        "function":{
            "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```
또 다른 예로 서비스 버스 전송 메시지 작업 hello 매개 변수화 할 수 있습니다.

```
"Send_message": {
    "type": "ApiConnection",
        "inputs": {
            "host": {
                "connection": {
                    "name": "@parameters('$connections')['servicebus']['connectionId']"
                }
            },
            "method": "post",
            "path": "[concat('/@{encodeURIComponent(''', parameters('queueuname'), ''')}/messages')]",
            "body": {
                "ContentData": "@{base64(triggerBody())}"
            },
            "queries": {
                "systemProperties": "None"
            }
        },
        "runAfter": {}
    }
```
> [!NOTE] 
> host.runtimeUrl은 선택 사항이며 있는 경우 템플릿에서 제거할 수 있습니다.
> 


> [!NOTE] 
> 논리 응용 프로그램 디자이너 toowork hello에 대 한 매개 변수를 사용할 때 제공 해야 기본 값 예:
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a>논리 앱 저장

toosave에서 언제 든 지 논리 앱 이동 너무**파일** > **저장**합니다. (`Ctrl+S`) 

Hello Visual Studio에에서 나타나는 경우 논리 앱에 응용 프로그램을 저장 하면 모든 오류가 **출력** 창.

## <a name="deploy-your-logic-app-from-visual-studio"></a>Visual Studio에서 논리 앱 배포

앱을 구성한 후에 몇 단계 만에 Visual Studio에서 직접 배포할 수 있습니다. 

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 이동 너무**배포** > **새 배포...**

    ![새 배포](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. 메시지가 나타나면 tooyour Azure 구독에에서 로그인 합니다. 

3. 이제 저장할 toodeploy 논리 앱 hello 리소스 그룹에 대 한 hello 세부 정보를 선택 해야 합니다. 완료되면 **배포**를 선택합니다.

    > [!NOTE]
    > Hello 올바른 템플릿과 hello 리소스 그룹에 대 한 매개 변수 파일을 선택 하 고 있는지 확인 합니다. 예를 들어 toodeploy tooa 프로덕션 환경 hello 프로덕션 매개 변수 파일을 선택 합니다.

    ![Tooresource 그룹 배포](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    hello에 hello 배포 상태가 표시 **출력** 창. 
    Tooselect 해야할 **Azure 프로 비전** hello에 **에서 출력 보기** 목록입니다.

    ![배포 상태 출력](./media/logic-apps-deploy-from-vs/output.png)

이후 hello, 논리 앱의 소스 제어에서 편집한 Visual Studio toodeploy 새 버전을 사용 합니다.

> [!NOTE]
> 직접 hello Azure 포털에서에서 hello 정의 변경 하면 다음에 Visual Studio에서 배포할 때 이러한 변경 내용은 덮어씁니다. 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a>논리 앱 tooan 기존 리소스 그룹 프로젝트를 추가 합니다.

기존 리소스 그룹 프로젝트를 사용 하도록 설정한 경우에 hello JSON 개요 창에서 논리 앱 toothat 프로젝트를 추가할 수 있습니다. 또한 이전에 만든 hello 응용 프로그램과 함께 다른 논리 앱을 추가할 수 있습니다.

1. 열기 hello `<template>.json` 파일입니다.

2. JSON 개요 창의 tooopen hello 너무 이동**보기** > **다른 창** > **JSON 개요**합니다.

3. tooadd 리소스 toohello 템플릿 파일을 클릭 하 여 **리소스 추가** hello hello JSON 개요 창의 위쪽에 있습니다. Hello JSON 개요 창에서 마우스 오른쪽 단추로 클릭 하거나 **리소스**를 선택 하 고 **새 리소스 추가**합니다.

    ![JSON 개요 창](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. Hello에 **리소스 추가** 찾기 및 선택 대화 상자, **논리 앱**합니다. 논리 앱의 이름을 지정하고 **추가**를 선택합니다.

    ![리소스 추가](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a>다음 단계

* [Visual Studio 클라우드 탐색기를 사용하여 Logic Apps 관리](logic-apps-manage-from-vs.md)
* [일반적인 예제 및 시나리오 보기](logic-apps-examples-and-scenarios.md)
* [Azure 논리 앱 tooautomate 비즈니스에서 처리 하는 방법에 대해 알아봅니다](http://channel9.msdn.com/Events/Build/2016/T694)
* [자세한 내용은 방법 toointegrate Azure 논리 앱 시스템](http://channel9.msdn.com/Events/Build/2016/P462)
