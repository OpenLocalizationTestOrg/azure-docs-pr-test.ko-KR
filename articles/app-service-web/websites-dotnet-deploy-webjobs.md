---
title: "Visual Studio를 사용 하 여 WebJobs aaaDeploy"
description: "자세한 내용은 방법 toodeploy Azure WebJobs tooAzure Visual Studio를 사용 하 여 앱 서비스 웹 앱입니다."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 5fc5d9562e8836348f5ab6844fb6c23ff40a321c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a>Visual Studio를 사용하여 WebJob 배포
## <a name="overview"></a>개요
이 항목에서는 방법을 toouse Visual Studio toodeploy 콘솔 응용 프로그램 프로젝트의 웹 앱 tooa 설명 [앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) 로 [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226)합니다. 사용 하 여 WebJobs toodeploy hello 하는 방법에 대 한 내용은 [Azure 포털](https://portal.azure.com), 참조 [여를 실행 하는 백그라운드 작업](web-sites-create-web-jobs.md)합니다.

Visual Studio는 WebJob 지원 콘솔 응용 프로그램 프로젝트를 배포할 때 다음 두 가지 작업을 수행합니다.

* 복사본 런타임 파일 toohello hello 웹 응용 프로그램에서 적절 한 폴더 (*App_Data/작업/연속* 연속 WebJobs에 대 한 *App_Data/작업/트리거된* 예약 된 백업과 주문형으로 WebJobs에 대 한).
* 설정 [Azure Scheduler 작업](#scheduler) WebJobs는 예약 된 toorun에서 특정 시간에 대 한 합니다. (연속 WebJob에는 필요하지 않습니다.)

Webjob 사용 프로젝트에 다음 항목이 추가 된 tooit hello:

* hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet 패키지 합니다.
* 배포 및 스케줄러 설정을 포함하는 [webjob-publish-settings.json](#publishsettings) 파일 

![Tooa 콘솔 응용 프로그램 tooenable 배포는 WebJob으로 추가 되는 내용을 보여 주는 다이어그램](./media/websites-dotnet-deploy-webjobs/convert.png)

이러한 항목 tooan 기존 콘솔 응용 프로그램 프로젝트를 추가 하거나 템플릿 toocreate 새 WebJobs 사용 콘솔 응용 프로그램 프로젝트를 사용할 수 있습니다. 

Hello 웹 프로젝트를 배포할 때마다 자동으로 배포 되도록 tooa 웹 프로젝트에 연결 또는 자체적으로 WebJob으로 프로젝트를 배포할 수 있습니다. toolink 프로젝트 Visual Studio에서 hello WebJobs 사용이 가능한 프로젝트의 hello 이름을 포함 한 [webjobs list.json](#webjobslist) hello 웹 프로젝트의 파일입니다.

![WebJob 프로젝트 tooweb 프로젝트 연결을 보여 주는 다이어그램](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a>필수 조건
Hello Azure SDK for.NET 설치 WebJobs 배포 기능이 Visual Studio에서 제공 됩니다.

* [.NET용 Azure SDK(Visual Studio)](https://azure.microsoft.com/downloads/)

## <a id="convert"></a>기존 콘솔 응용 프로그램 프로젝트에 WebJob 배포 사용
다음 두 가지 옵션을 사용할 수 있습니다.

* [웹 프로젝트를 사용하여 자동 배포 사용](#convertlink).
  
    기존 콘솔 응용 프로그램 프로젝트가 웹 프로젝트를 배포할 때 WebJob으로 자동 배포되도록 구성합니다. Toorun hello에서 WebJob을 원하는 경우이 옵션을 사용 하 여 hello를 실행 하면 동일한 웹 응용 프로그램 관련 웹 응용 프로그램입니다.
* [웹 프로젝트를 제외하고 배포](#convertnolink).
  
    없는 링크 tooa 웹 프로젝트와 같은 웹 작업이 기존 콘솔 응용 프로그램 프로젝트 toodeploy 자체적으로 구성 합니다. 원하는 웹 응용 프로그램에서 WebJob toorun 자체적으로 hello 웹 앱에서 실행 되는 웹 응용 프로그램이 없는 경우이 옵션을 사용 합니다. 이 toodo를 할 수 있습니다에 주문 toobe 수 tooscale 웹 응용 프로그램 리소스와 독립적으로 WebJob 리소스입니다.

### <a id="convertlink"></a> 웹 프로젝트와 함께 자동 WebJob 배포 사용
1. hello 웹 프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기**, 클릭 하 고 **추가** > **기존 프로젝트를 Azure WebJob으로**합니다.
   
    ![Existing Project as Azure WebJob(기존 프로젝트를 Azure WebJob으로)](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    hello [추가 Azure WebJob](#configure) 대화 상자가 나타납니다.
2. Hello에 **프로젝트 이름을** 드롭다운 목록에서, 한 WebJob으로 콘솔 응용 프로그램 프로젝트 tooadd hello 선택 합니다.
   
    ![Add Azure WebJob(Azure WebJob 추가) 대화 상자에서 프로젝트 선택](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. 전체 hello [Azure WebJob 추가](#configure) 대화 상자를 닫고 클릭 **확인**합니다. 

### <a id="convertnolink"></a> 웹 프로젝트를 제외한 WebJob 배포 사용
1. 마우스 오른쪽 단추로 클릭 hello 콘솔 응용 프로그램 프로젝트 **솔루션 탐색기**, 클릭 하 고 **Azure WebJob으로 게시...** . 
   
    ![Publish as Azure WebJob(Azure WebJob으로 게시)](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    hello [Azure WebJob 추가](#configure) hello에서 선택한 hello 프로젝트와 함께 대화 상자가 나타나면 **프로젝트 이름을** 상자입니다.
2. 전체 hello [Azure WebJob 추가](#configure) 대화 상자를 닫은 다음 **확인**합니다.
   
   hello **웹 게시** 마법사가 나타납니다.  원하지 않는 toopublish 즉시, hello 마법사를 닫습니다. 너무 않을 때 입력 한 hello 설정에 대 한 저장 됩니다[hello 프로젝트 배포](#deploy)합니다.

## <a id="create"></a>새 WebJob 지원 프로젝트 만들기
새 WebJobs 사용이 가능한 프로젝트 toocreate에 설명 된 대로 hello 콘솔 응용 프로그램 프로젝트 템플릿과 enable WebJobs 배포를 사용할 수 있습니다 [이전 섹션 hello](#convert)합니다. 대신 hello WebJobs 새 프로젝트 템플릿을 사용할 수 있습니다.

* [독립 WebJob 위한 hello WebJobs 새 프로젝트 템플릿을 사용합니다](#createnolink)
  
    프로젝트를 만들고 toodeploy 단독으로으로 구성할 수 없는 링크 tooa 웹 프로젝트와 함께 WebJob을 합니다. 원하는 웹 응용 프로그램에서 WebJob toorun 자체적으로 hello 웹 앱에서 실행 되는 웹 응용 프로그램이 없는 경우이 옵션을 사용 합니다. 이 toodo를 할 수 있습니다에 주문 toobe 수 tooscale 웹 응용 프로그램 리소스와 독립적으로 WebJob 리소스입니다.
* [WebJob tooa 연결 된 웹 프로젝트에 대 한 hello WebJobs 새 프로젝트 템플릿을 사용 하 여](#createlink)
  
    동일한 솔루션을 배포 하는 hello에는 웹 프로젝트 WebJob으로 자동으로 구성 된 toodeploy 하는 프로젝트를 만듭니다. Toorun hello에서 WebJob을 원하는 경우이 옵션을 사용 하 여 hello를 실행 하면 동일한 웹 응용 프로그램 관련 웹 응용 프로그램입니다.

> [!NOTE]
> hello WebJobs 새 프로젝트 템플릿을 자동으로 NuGet 패키지를 설치 하 고 코드에서 포함 *Program.cs* hello에 대 한 [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs)합니다. Toouse hello WebJobs SDK를 사용 하지 않으려는 경우 제거 하거나 변경 hello `host.RunAndBlock` 문에서 *Program.cs*합니다.
> 
> 

### <a id="createnolink"></a>독립 WebJob 위한 hello WebJobs 새 프로젝트 템플릿을 사용합니다
1. 클릭 **파일** > **새 프로젝트**, 한 다음 hello **새 프로젝트** 대화 상자 클릭 **클라우드**  >   **Azure WebJob (.NET Framework)**합니다.
   
    ![WebJob 템플릿을 표시하는 새 프로젝트 대화 상자](./media/websites-dotnet-deploy-webjobs/np.png)
2. 앞에서 살펴본 hello 지시에 따라 너무[독립 Webjob 프로젝트는 콘솔 응용 프로그램 프로젝트를 hello 확인](#convertnolink)합니다.

### <a id="createlink"></a>WebJob tooa 연결 된 웹 프로젝트에 대 한 hello WebJobs 새 프로젝트 템플릿을 사용 하 여
1. hello 웹 프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기**, 클릭 하 고 **추가** > **새 Azure WebJob 프로젝트**합니다.
   
    ![New Azure WebJob Project(새 Azure WebJob 프로젝트) 메뉴 항목](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    hello [추가 Azure WebJob](#configure) 대화 상자가 나타납니다.
2. 전체 hello [Azure WebJob 추가](#configure) 대화 상자를 닫은 다음 **확인**합니다.

## <a id="configure"></a>hello Azure WebJob 추가 대화 상자
hello **추가 Azure WebJob** 대화 상자를 사용 하면 hello WebJob 이름을 입력 하 고 모드 설정에 대 한 WebJob 실행 합니다. 

![Add Azure WebJob(Azure WebJob 추가) 대화 상자](./media/websites-dotnet-deploy-webjobs/aaw2.png)

이 대화 상자에 hello 필드 toofields hello에는 해당 **새 작업** hello Azure 포털의 대화 상자. 자세한 내용은 [WebJobs를 사용하여 백그라운드 작업 실행](web-sites-create-web-jobs.md)을 참조하세요.

> [!NOTE]
> * 명령줄 배포에 대한 자세한 내용은 [Azure WebJob의 명령줄 또는 지속적인 전송 사용](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/)을 참조하세요.
> * WebJob을 배포 하 고 싶은 toochange hello 유형 WebJob 및 재배포 하는 경우 toodelete hello webjobs 게시 settings.json 파일이 필요 합니다. 이렇게 하면 Visual Studio hello 유형의 WebJob 변경할 수 있도록 hello 다시 게시 옵션을 표시 합니다.
> * WebJob을 배포 하 고 나중에 변경 하는 경우 실행된 모드에서 연속 toonon 연속 hello 또는 그 반대로 만들어지고 새 WebJob Azure에서 다시 배포할 때 합니다. 다른 일정 설정을 변경 하면 이지만 leave 실행 모드 hello 동일 하거나 예약 및 요청 시 사이 전환 하 여 Visual Studio 업데이트 기존 작업 hello 되지 않고 새로 만드십시오.
> 
> 

## <a id="publishsettings"></a>webjob-publish-settings.json
Visual Studio 설치 hello WebJobs 배포에 대 한 콘솔 응용 프로그램을 구성 하면 [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet 패키지 및 일정에 대 한 정보는 저장소는 *webjob 게시 settings.json*  hello 프로젝트 파일에에서 *속성* hello Webjob 프로젝트의 폴더입니다. 다음은 이 파일의 예입니다.

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

이 파일을 직접 편집할 수도 있고 Visual Studio에 제공되는 IntelliSense를 사용할 수도 있습니다. hello 파일 스키마에 저장 된 [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) 있습니다 볼 수 있습니다.  

## <a id="webjobslist"></a>webjobs-list.json
Visual Studio에서 hello Webjob 프로젝트의 hello 이름을 저장 WebJobs 사용이 가능한 프로젝트 tooa 웹 프로젝트를 링크할 때는 *webjobs list.json* hello 웹 프로젝트의 파일에에서 *속성* 폴더입니다. hello 목록 hello 다음 예제와 같이 여러 웹 작업 프로젝트에 포함 될 수 있습니다.

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

이 파일을 직접 편집할 수도 있고 Visual Studio에 제공되는 IntelliSense를 사용할 수도 있습니다. hello 파일 스키마에 저장 된 [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) 있습니다 볼 수 있습니다.

## <a id="deploy"></a>WebJob 프로젝트 배포
Hello 웹 프로젝트와 tooa 웹 프로젝트를 연결 된 웹 작업 프로젝트를 자동으로 배포 합니다. 웹 프로젝트 배포에 대 한 정보를 참조 하십시오. [어떻게 toodeploy tooWeb 앱](web-sites-deploy.md)합니다.

toodeploy 자체적으로 WebJobs 프로젝트에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 클릭 **Azure WebJob으로 게시 중...** . 

![Publish as Azure WebJob(Azure WebJob으로 게시)](./media/websites-dotnet-deploy-webjobs/paw.png)

독립 WebJob을에 대 한 동일한 hello **웹 게시** 웹 프로젝트에 표시 되지만 설정 사용할 수 있는 toochange 더 적게 사용 되는 마법사입니다.

## <a id="nextsteps"></a>다음 단계
이 문서에 설명 된 방법 Visual Studio를 사용 하 여 WebJobs toodeploy 합니다. Toodeploy Azure WebJobs 확인 하려면 어떻게 해야 하는 방법에 대 한 자세한 내용은 [Azure WebJobs-권장 리소스-배포](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying)합니다.

