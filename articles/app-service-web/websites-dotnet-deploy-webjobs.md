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
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="21b79-103">Visual Studio를 사용하여 WebJob 배포</span><span class="sxs-lookup"><span data-stu-id="21b79-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="21b79-104">개요</span><span class="sxs-lookup"><span data-stu-id="21b79-104">Overview</span></span>
<span data-ttu-id="21b79-105">이 항목에서는 방법을 toouse Visual Studio toodeploy 콘솔 응용 프로그램 프로젝트의 웹 앱 tooa 설명 [앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) 로 [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226)합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-105">This topic explains how toouse Visual Studio toodeploy a Console Application project tooa web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="21b79-106">사용 하 여 WebJobs toodeploy hello 하는 방법에 대 한 내용은 [Azure 포털](https://portal.azure.com), 참조 [여를 실행 하는 백그라운드 작업](web-sites-create-web-jobs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-106">For information about how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="21b79-107">Visual Studio는 WebJob 지원 콘솔 응용 프로그램 프로젝트를 배포할 때 다음 두 가지 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="21b79-108">복사본 런타임 파일 toohello hello 웹 응용 프로그램에서 적절 한 폴더 (*App_Data/작업/연속* 연속 WebJobs에 대 한 *App_Data/작업/트리거된* 예약 된 백업과 주문형으로 WebJobs에 대 한).</span><span class="sxs-lookup"><span data-stu-id="21b79-108">Copies runtime files toohello appropriate folder in hello web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="21b79-109">설정 [Azure Scheduler 작업](#scheduler) WebJobs는 예약 된 toorun에서 특정 시간에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled toorun at particular times.</span></span> <span data-ttu-id="21b79-110">(연속 WebJob에는 필요하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="21b79-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="21b79-111">Webjob 사용 프로젝트에 다음 항목이 추가 된 tooit hello:</span><span class="sxs-lookup"><span data-stu-id="21b79-111">A WebJobs-enabled project has hello following items added tooit:</span></span>

* <span data-ttu-id="21b79-112">hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-112">hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="21b79-113">배포 및 스케줄러 설정을 포함하는 [webjob-publish-settings.json](#publishsettings) 파일</span><span class="sxs-lookup"><span data-stu-id="21b79-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Tooa 콘솔 응용 프로그램 tooenable 배포는 WebJob으로 추가 되는 내용을 보여 주는 다이어그램](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="21b79-115">이러한 항목 tooan 기존 콘솔 응용 프로그램 프로젝트를 추가 하거나 템플릿 toocreate 새 WebJobs 사용 콘솔 응용 프로그램 프로젝트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-115">You can add these items tooan existing Console Application project or use a template toocreate a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="21b79-116">Hello 웹 프로젝트를 배포할 때마다 자동으로 배포 되도록 tooa 웹 프로젝트에 연결 또는 자체적으로 WebJob으로 프로젝트를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-116">You can deploy a project as a WebJob by itself, or link it tooa web project so that it automatically deploys whenever you deploy hello web project.</span></span> <span data-ttu-id="21b79-117">toolink 프로젝트 Visual Studio에서 hello WebJobs 사용이 가능한 프로젝트의 hello 이름을 포함 한 [webjobs list.json](#webjobslist) hello 웹 프로젝트의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-117">toolink projects, Visual Studio includes hello name of hello WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in hello web project.</span></span>

![WebJob 프로젝트 tooweb 프로젝트 연결을 보여 주는 다이어그램](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="21b79-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="21b79-119">Prerequisites</span></span>
<span data-ttu-id="21b79-120">Hello Azure SDK for.NET 설치 WebJobs 배포 기능이 Visual Studio에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-120">WebJobs deployment features are available in Visual Studio when you install hello Azure SDK for .NET:</span></span>

* <span data-ttu-id="21b79-121">[.NET용 Azure SDK(Visual Studio)](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="21b79-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="21b79-122"><a id="convert"></a>기존 콘솔 응용 프로그램 프로젝트에 WebJob 배포 사용</span><span class="sxs-lookup"><span data-stu-id="21b79-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="21b79-123">다음 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-123">You have two options:</span></span>

* <span data-ttu-id="21b79-124">[웹 프로젝트를 사용하여 자동 배포 사용](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="21b79-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="21b79-125">기존 콘솔 응용 프로그램 프로젝트가 웹 프로젝트를 배포할 때 WebJob으로 자동 배포되도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="21b79-126">Toorun hello에서 WebJob을 원하는 경우이 옵션을 사용 하 여 hello를 실행 하면 동일한 웹 응용 프로그램 관련 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-126">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>
* <span data-ttu-id="21b79-127">[웹 프로젝트를 제외하고 배포](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="21b79-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="21b79-128">없는 링크 tooa 웹 프로젝트와 같은 웹 작업이 기존 콘솔 응용 프로그램 프로젝트 toodeploy 자체적으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-128">Configure an existing Console Application project toodeploy as a WebJob by itself, with no link tooa web project.</span></span> <span data-ttu-id="21b79-129">원하는 웹 응용 프로그램에서 WebJob toorun 자체적으로 hello 웹 앱에서 실행 되는 웹 응용 프로그램이 없는 경우이 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-129">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="21b79-130">이 toodo를 할 수 있습니다에 주문 toobe 수 tooscale 웹 응용 프로그램 리소스와 독립적으로 WebJob 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-130">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="21b79-131"><a id="convertlink"></a> 웹 프로젝트와 함께 자동 WebJob 배포 사용</span><span class="sxs-lookup"><span data-stu-id="21b79-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="21b79-132">hello 웹 프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기**, 클릭 하 고 **추가** > **기존 프로젝트를 Azure WebJob으로**합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-132">Right-click hello web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Existing Project as Azure WebJob(기존 프로젝트를 Azure WebJob으로)](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="21b79-134">hello [추가 Azure WebJob](#configure) 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-134">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="21b79-135">Hello에 **프로젝트 이름을** 드롭다운 목록에서, 한 WebJob으로 콘솔 응용 프로그램 프로젝트 tooadd hello 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-135">In hello **Project name** drop-down list, select hello Console Application project tooadd as a WebJob.</span></span>
   
    ![Add Azure WebJob(Azure WebJob 추가) 대화 상자에서 프로젝트 선택](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="21b79-137">전체 hello [Azure WebJob 추가](#configure) 대화 상자를 닫고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-137">Complete hello [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="21b79-138"><a id="convertnolink"></a> 웹 프로젝트를 제외한 WebJob 배포 사용</span><span class="sxs-lookup"><span data-stu-id="21b79-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="21b79-139">마우스 오른쪽 단추로 클릭 hello 콘솔 응용 프로그램 프로젝트 **솔루션 탐색기**, 클릭 하 고 **Azure WebJob으로 게시...** .</span><span class="sxs-lookup"><span data-stu-id="21b79-139">Right-click hello Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Publish as Azure WebJob(Azure WebJob으로 게시)](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="21b79-141">hello [Azure WebJob 추가](#configure) hello에서 선택한 hello 프로젝트와 함께 대화 상자가 나타나면 **프로젝트 이름을** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-141">hello [Add Azure WebJob](#configure) dialog box appears, with hello project selected in hello **Project name** box.</span></span>
2. <span data-ttu-id="21b79-142">전체 hello [Azure WebJob 추가](#configure) 대화 상자를 닫은 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-142">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="21b79-143">hello **웹 게시** 마법사가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-143">hello **Publish Web** wizard appears.</span></span>  <span data-ttu-id="21b79-144">원하지 않는 toopublish 즉시, hello 마법사를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-144">If you do not want toopublish immediately, close hello wizard.</span></span> <span data-ttu-id="21b79-145">너무 않을 때 입력 한 hello 설정에 대 한 저장 됩니다[hello 프로젝트 배포](#deploy)합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-145">hello settings that you've entered are saved for when you do want too[deploy hello project](#deploy).</span></span>

## <span data-ttu-id="21b79-146"><a id="create"></a>새 WebJob 지원 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="21b79-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="21b79-147">새 WebJobs 사용이 가능한 프로젝트 toocreate에 설명 된 대로 hello 콘솔 응용 프로그램 프로젝트 템플릿과 enable WebJobs 배포를 사용할 수 있습니다 [이전 섹션 hello](#convert)합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-147">toocreate a new WebJobs-enabled project, you can use hello Console Application project template and enable WebJobs deployment as explained in [hello previous section](#convert).</span></span> <span data-ttu-id="21b79-148">대신 hello WebJobs 새 프로젝트 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-148">As an alternative, you can use hello WebJobs new-project template:</span></span>

* [<span data-ttu-id="21b79-149">독립 WebJob 위한 hello WebJobs 새 프로젝트 템플릿을 사용합니다</span><span class="sxs-lookup"><span data-stu-id="21b79-149">Use hello WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="21b79-150">프로젝트를 만들고 toodeploy 단독으로으로 구성할 수 없는 링크 tooa 웹 프로젝트와 함께 WebJob을 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-150">Create a project and configure it toodeploy by itself as a WebJob, with no link tooa web project.</span></span> <span data-ttu-id="21b79-151">원하는 웹 응용 프로그램에서 WebJob toorun 자체적으로 hello 웹 앱에서 실행 되는 웹 응용 프로그램이 없는 경우이 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-151">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="21b79-152">이 toodo를 할 수 있습니다에 주문 toobe 수 tooscale 웹 응용 프로그램 리소스와 독립적으로 WebJob 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-152">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="21b79-153">WebJob tooa 연결 된 웹 프로젝트에 대 한 hello WebJobs 새 프로젝트 템플릿을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="21b79-153">Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>](#createlink)
  
    <span data-ttu-id="21b79-154">동일한 솔루션을 배포 하는 hello에는 웹 프로젝트 WebJob으로 자동으로 구성 된 toodeploy 하는 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-154">Create a project that is configured toodeploy automatically as a WebJob when a web project in hello same solution is deployed.</span></span> <span data-ttu-id="21b79-155">Toorun hello에서 WebJob을 원하는 경우이 옵션을 사용 하 여 hello를 실행 하면 동일한 웹 응용 프로그램 관련 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-155">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="21b79-156">hello WebJobs 새 프로젝트 템플릿을 자동으로 NuGet 패키지를 설치 하 고 코드에서 포함 *Program.cs* hello에 대 한 [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs)합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-156">hello WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for hello [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="21b79-157">Toouse hello WebJobs SDK를 사용 하지 않으려는 경우 제거 하거나 변경 hello `host.RunAndBlock` 문에서 *Program.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-157">If you don't want toouse hello WebJobs SDK, remove or change hello `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="21b79-158"><a id="createnolink"></a>독립 WebJob 위한 hello WebJobs 새 프로젝트 템플릿을 사용합니다</span><span class="sxs-lookup"><span data-stu-id="21b79-158"><a id="createnolink"></a> Use hello WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="21b79-159">클릭 **파일** > **새 프로젝트**, 한 다음 hello **새 프로젝트** 대화 상자 클릭 **클라우드**  >   **Azure WebJob (.NET Framework)**합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-159">Click **File** > **New Project**, and then in hello **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![WebJob 템플릿을 표시하는 새 프로젝트 대화 상자](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="21b79-161">앞에서 살펴본 hello 지시에 따라 너무[독립 Webjob 프로젝트는 콘솔 응용 프로그램 프로젝트를 hello 확인](#convertnolink)합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-161">Follow hello directions shown earlier too[make hello Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="21b79-162"><a id="createlink"></a>WebJob tooa 연결 된 웹 프로젝트에 대 한 hello WebJobs 새 프로젝트 템플릿을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="21b79-162"><a id="createlink"></a> Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>
1. <span data-ttu-id="21b79-163">hello 웹 프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기**, 클릭 하 고 **추가** > **새 Azure WebJob 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-163">Right-click hello web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![New Azure WebJob Project(새 Azure WebJob 프로젝트) 메뉴 항목](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="21b79-165">hello [추가 Azure WebJob](#configure) 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-165">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="21b79-166">전체 hello [Azure WebJob 추가](#configure) 대화 상자를 닫은 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-166">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="21b79-167"><a id="configure"></a>hello Azure WebJob 추가 대화 상자</span><span class="sxs-lookup"><span data-stu-id="21b79-167"><a id="configure"></a>hello Add Azure WebJob dialog</span></span>
<span data-ttu-id="21b79-168">hello **추가 Azure WebJob** 대화 상자를 사용 하면 hello WebJob 이름을 입력 하 고 모드 설정에 대 한 WebJob 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-168">hello **Add Azure WebJob** dialog lets you enter hello WebJob name and run mode setting for your WebJob.</span></span> 

![Add Azure WebJob(Azure WebJob 추가) 대화 상자](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="21b79-170">이 대화 상자에 hello 필드 toofields hello에는 해당 **새 작업** hello Azure 포털의 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="21b79-170">hello fields in this dialog correspond toofields on hello **New Job** dialog of hello Azure Portal.</span></span> <span data-ttu-id="21b79-171">자세한 내용은 [WebJobs를 사용하여 백그라운드 작업 실행](web-sites-create-web-jobs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21b79-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="21b79-172">명령줄 배포에 대한 자세한 내용은 [Azure WebJob의 명령줄 또는 지속적인 전송 사용](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21b79-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="21b79-173">WebJob을 배포 하 고 싶은 toochange hello 유형 WebJob 및 재배포 하는 경우 toodelete hello webjobs 게시 settings.json 파일이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-173">If you deploy a WebJob and then decide you want toochange hello type of WebJob and redeploy, you'll need toodelete hello webjobs-publish-settings.json file.</span></span> <span data-ttu-id="21b79-174">이렇게 하면 Visual Studio hello 유형의 WebJob 변경할 수 있도록 hello 다시 게시 옵션을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-174">This will make Visual Studio show hello publishing options again, so you can change hello type of WebJob.</span></span>
> * <span data-ttu-id="21b79-175">WebJob을 배포 하 고 나중에 변경 하는 경우 실행된 모드에서 연속 toonon 연속 hello 또는 그 반대로 만들어지고 새 WebJob Azure에서 다시 배포할 때 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-175">If you deploy a WebJob and later change hello run mode from continuous toonon-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="21b79-176">다른 일정 설정을 변경 하면 이지만 leave 실행 모드 hello 동일 하거나 예약 및 요청 시 사이 전환 하 여 Visual Studio 업데이트 기존 작업 hello 되지 않고 새로 만드십시오.</span><span class="sxs-lookup"><span data-stu-id="21b79-176">If you change other scheduling settings but leave run mode hello same or switch between Scheduled and On Demand, Visual Studio updates hello existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="21b79-177"><a id="publishsettings"></a>webjob-publish-settings.json</span><span class="sxs-lookup"><span data-stu-id="21b79-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="21b79-178">Visual Studio 설치 hello WebJobs 배포에 대 한 콘솔 응용 프로그램을 구성 하면 [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet 패키지 및 일정에 대 한 정보는 저장소는 *webjob 게시 settings.json*  hello 프로젝트 파일에에서 *속성* hello Webjob 프로젝트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in hello project *Properties* folder of hello WebJobs project.</span></span> <span data-ttu-id="21b79-179">다음은 이 파일의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="21b79-180">이 파일을 직접 편집할 수도 있고 Visual Studio에 제공되는 IntelliSense를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="21b79-181">hello 파일 스키마에 저장 된 [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) 있습니다 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-181">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="21b79-182"><a id="webjobslist"></a>webjobs-list.json</span><span class="sxs-lookup"><span data-stu-id="21b79-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="21b79-183">Visual Studio에서 hello Webjob 프로젝트의 hello 이름을 저장 WebJobs 사용이 가능한 프로젝트 tooa 웹 프로젝트를 링크할 때는 *webjobs list.json* hello 웹 프로젝트의 파일에에서 *속성* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-183">When you link a WebJobs-enabled project tooa web project, Visual Studio stores hello name of hello WebJobs project in a *webjobs-list.json* file in hello web project's *Properties* folder.</span></span> <span data-ttu-id="21b79-184">hello 목록 hello 다음 예제와 같이 여러 웹 작업 프로젝트에 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-184">hello list might contain multiple WebJobs projects, as shown in hello following example:</span></span>

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

<span data-ttu-id="21b79-185">이 파일을 직접 편집할 수도 있고 Visual Studio에 제공되는 IntelliSense를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="21b79-186">hello 파일 스키마에 저장 된 [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) 있습니다 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-186">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="21b79-187"><a id="deploy"></a>WebJob 프로젝트 배포</span><span class="sxs-lookup"><span data-stu-id="21b79-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="21b79-188">Hello 웹 프로젝트와 tooa 웹 프로젝트를 연결 된 웹 작업 프로젝트를 자동으로 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-188">A WebJobs project that you have linked tooa web project deploys automatically with hello web project.</span></span> <span data-ttu-id="21b79-189">웹 프로젝트 배포에 대 한 정보를 참조 하십시오. [어떻게 toodeploy tooWeb 앱](web-sites-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-189">For information about web project deployment, see [How toodeploy tooWeb Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="21b79-190">toodeploy 자체적으로 WebJobs 프로젝트에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 클릭 **Azure WebJob으로 게시 중...** .</span><span class="sxs-lookup"><span data-stu-id="21b79-190">toodeploy a WebJobs project by itself, right-click hello project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Publish as Azure WebJob(Azure WebJob으로 게시)](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="21b79-192">독립 WebJob을에 대 한 동일한 hello **웹 게시** 웹 프로젝트에 표시 되지만 설정 사용할 수 있는 toochange 더 적게 사용 되는 마법사입니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-192">For an independent WebJob, hello same **Publish Web** wizard that is used for web projects appears, but with fewer settings available toochange.</span></span>

## <span data-ttu-id="21b79-193"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="21b79-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="21b79-194">이 문서에 설명 된 방법 Visual Studio를 사용 하 여 WebJobs toodeploy 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-194">This article has explained how toodeploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="21b79-195">Toodeploy Azure WebJobs 확인 하려면 어떻게 해야 하는 방법에 대 한 자세한 내용은 [Azure WebJobs-권장 리소스-배포](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying)합니다.</span><span class="sxs-lookup"><span data-stu-id="21b79-195">For more information about how toodeploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

