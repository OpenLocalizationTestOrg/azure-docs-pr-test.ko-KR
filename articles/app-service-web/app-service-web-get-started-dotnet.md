---
title: "aaaCreate ASP.NET 웹 앱에 Azure | Microsoft Docs"
description: "어떻게 hello 기본 ASP.NET 배포 하 여 Azure 앱 서비스에서 웹 앱 toorun 웹 앱에 알아봅니다."
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eec916b3c32b6c8b68083177938c5c822a9782b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a>Azure에서 ASP.NET 웹앱 만들기

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.  이 퀵 스타트의 표시 방법을 toodeploy 첫 번째 ASP.NET 웹 응용 프로그램 tooAzure 웹 앱입니다. 완료되면 배포된 웹 응용 프로그램으로 App Service 계획 및 Azure 웹앱으로 구성된 리소스 그룹을 갖습니다.

작업에서이 퀵 스타트의 hello 비디오 toosee를 감시 하 고 다음 따라 hello 직접 toopublish 첫.NET 응용 프로그램에서 단계 Azure입니다.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a>필수 조건

toocomplete이이 자습서:

* 설치 [Visual Studio 2017](https://www.visualstudio.com/downloads/) 워크 로드를 수행 하는 hello로:
    - **ASP.NET 및 웹 배포**
    - **Azure 개발**

    ![ASP.NET 및 웹 개발 및 Azure 개발(웹 & 클라우드에서)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a>ASP.NET 웹앱 만들기

Visual Studio에서 **파일 > 새로 만들기 > 프로젝트**를 선택하여 프로젝트를 만듭니다. 

Hello에 **새 프로젝트** 대화 상자에서 **Visual C# > 웹 > ASP.NET 웹 응용 프로그램 (.NET Framework)**합니다.

Hello 응용 프로그램 이름을 _myFirstAzureWebApp_를 선택한 후 **확인**합니다.
   
![새 프로젝트 대화 상자](./media/app-service-web-get-started-dotnet/new-project.png)

모든 종류의 ASP.NET 웹 응용 프로그램 tooAzure 배포할 수 있습니다. 이 빠른 시작에 대 한 선택 hello **MVC** 템플릿을 인증 너무 설정 되어 있는지 확인 하 고**인증 안 함**합니다.
      
**확인**을 선택합니다.

![새 ASP.NET 프로젝트 대화 상자](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

Hello 메뉴에서 선택 **디버그 > 디버깅 하지 않고 시작** toorun hello 웹 앱을 로컬로 합니다.

![로컬에서 앱 실행](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-tooazure"></a>TooAzure 게시

Hello에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello **myFirstAzureWebApp** 프로젝트를 마우스 선택 **게시**합니다.

![솔루션 탐색기에서 게시](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

**Microsoft Azure App Service**를 선택했는지 확인하고 **게시**를 선택합니다.

![프로젝트 개요 페이지에서 게시](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

Hello 열립니다 **응용 프로그램 서비스 만들기** 대화 상자를 사용 하면 Azure에서 모든 hello 필요한 Azure 리소스 toorun hello ASP.NET 웹 앱을 만들 수 있습니다.

## <a name="sign-in-tooazure"></a>TooAzure에 로그인

Hello에 **응용 프로그램 서비스 만들기** 대화 상자에서 **계정 추가**, tooyour Azure 구독에에서 로그인 합니다. 이미 등록 했으므로, 구독 hello 드롭다운에서 원하는 선택 hello 계정 hello 포함.

> [!NOTE]
> 이미 로그인한 경우 **만들기**를 선택하지 마십시오.
>
>
   
![TooAzure에 로그인](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a>리소스 그룹 만들기

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

다음 너무**리소스 그룹**선택, **새로**합니다.

Hello 리소스 그룹 이름 **myResourceGroup** 선택 **확인**합니다.

## <a name="create-an-app-service-plan"></a>App Service 계획 만들기

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

다음 너무**앱 서비스 계획**선택, **새로**합니다. 

Hello에 **앱 서비스 계획 구성** 대화 상자에서 다음에 나오는 hello 스크린 샷 hello 테이블에서 사용 하 여 hello 설정 합니다.

![App Service 계획 만들기](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| 설정 | 제안 값 | 설명 |
|-|-|-|
|App Service 계획| myAppServicePlan | Hello 앱 서비스 계획의 이름입니다. |
| 위치 | 서유럽 | hello 데이터 센터 hello 웹 응용 프로그램이 호스팅된 곳입니다. |
| 크기 | 무료 | [가격 책정 계층](https://azure.microsoft.com/pricing/details/app-service/)은 호스팅 기능을 결정합니다. |

**확인**을 선택합니다.

## <a name="create-and-publish-hello-web-app"></a>만들기 및 hello 웹 응용 프로그램 게시

**웹 앱 이름은**, 고유한 응용 프로그램 이름 입력 (유효한 문자는 `a-z`, `0-9`, 및 `-`), 하거나 자동으로 생성 한 고유 이름 hello 적용 합니다. hello 웹 앱의 hello URL은 `http://<app_name>.azurewebsites.net`여기서 `<app_name>` 웹 응용 프로그램 이름입니다.

선택 **만들기** toostart hello Azure 리소스를 작성 합니다.

![웹앱 이름 구성](./media/app-service-web-get-started-dotnet/web-app-name.png)

Hello 마법사가 완료 되 면 hello ASP.NET 웹 응용 프로그램 tooAzure 게시 하 고 실행 하는 경우 hello hello 기본 브라우저에서 응용 프로그램입니다.

![Azure에서 게시된 ASP.NET 웹앱](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

hello에 지정 된 hello 웹 앱 이름은 [만들기 및 게시 단계](#create-and-publish-the-web-app) hello 형태로 표시 URL 접두사 hello로 사용 되 `http://<app_name>.azurewebsites.net`합니다.

축하합니다. ASP.NET 웹앱이 Azure App Service에서 실시간으로 실행 중입니다.

## <a name="update-hello-app-and-redeploy"></a>Hello 앱 업데이트 및 다시 배포

Hello에서 **솔루션 탐색기**개방형 _Views\Home\Index.cshtml_합니다.

Hello `<div class="jumbotron">` HTML hello 맨 위 근처에 태그 및 코드 다음 hello hello 전체 요소를 바꿉니다.

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how toodeploy a .NET app tooAzure App Service.</p>
</div>
```

tooredeploy tooAzure를 마우스 오른쪽 단추로 클릭 hello **myFirstAzureWebApp** 프로젝트에서 **솔루션 탐색기** 선택 **게시**합니다.

Hello 게시 페이지, 선택 **게시**합니다.

게시에는 다음이 완료 되 면 Visual Studio hello 웹 앱의 브라우저 toohello URL을 시작 합니다.

![Azure에서 업데이트된 ASP.NET 웹앱](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-hello-azure-web-app"></a>Hello Azure 웹 앱 관리

Toohello 이동 <a href="https://portal.azure.com" target="_blank">Azure 포털</a> toomanage hello 웹 앱입니다.

Hello 왼쪽된 메뉴에서 선택 **응용 프로그램 서비스**, Azure 웹 앱의 hello 이름을 선택 합니다.

![포털 탐색 tooAzure 웹 응용 프로그램](./media/app-service-web-get-started-dotnet/access-portal.png)

웹앱의 개요 페이지가 표시됩니다. 여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다. 

![Azure Portal의 App Service 블레이드](./media/app-service-web-get-started-dotnet/web-app-blade.png)

왼쪽된 메뉴 hello 응용 프로그램을 구성 하는 서로 다른 페이지를 제공 합니다. 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [SQL Database를 사용하는 ASP.NET](app-service-web-tutorial-dotnet-sqldatabase.md)
