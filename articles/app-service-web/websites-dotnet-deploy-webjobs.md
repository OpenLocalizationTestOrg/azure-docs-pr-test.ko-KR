---
title: "Visual Studio를 사용하여 WebJob 배포"
description: "Visual Studio를 사용하여 Azure 앱 서비스에 Azure WebJob를 배포하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 5b0808afdadcf4d86a9a2d07ee6fc63b80b22993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="9cb9c-103">Visual Studio를 사용하여 WebJob 배포</span><span class="sxs-lookup"><span data-stu-id="9cb9c-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="9cb9c-104">개요</span><span class="sxs-lookup"><span data-stu-id="9cb9c-104">Overview</span></span>
<span data-ttu-id="9cb9c-105">이 항목에서는 Visual Studio를 사용하여 콘솔 응용 프로그램 프로젝트를 [App Service](http://go.microsoft.com/fwlink/?LinkId=529714)의 웹앱에 [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226)으로 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-105">This topic explains how to use Visual Studio to deploy a Console Application project to a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="9cb9c-106">[Azure Portal](https://portal.azure.com)을 사용하여 WebJob을 배포하는 방법에 대한 내용은 [Webjob으로 백그라운드 작업 실행](web-sites-create-web-jobs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-106">For information about how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="9cb9c-107">Visual Studio는 WebJob 지원 콘솔 응용 프로그램 프로젝트를 배포할 때 다음 두 가지 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="9cb9c-108">웹 앱의 해당 폴더에 런타임 파일을 복사합니다(연속 WebJob의 경우 *App_Data/jobs/continuous*, 예약된 주문형 WebJob의 경우 *App_Data/jobs/triggered*).</span><span class="sxs-lookup"><span data-stu-id="9cb9c-108">Copies runtime files to the appropriate folder in the web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="9cb9c-109">특정 시간에 실행되도록 예약된 WebJob에 대해 [Azure 스케줄러 작업](#scheduler) 을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled to run at particular times.</span></span> <span data-ttu-id="9cb9c-110">(연속 WebJob에는 필요하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="9cb9c-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="9cb9c-111">WebJob 지원 프로젝트에는 다음 항목이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-111">A WebJobs-enabled project has the following items added to it:</span></span>

* <span data-ttu-id="9cb9c-112">[Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="9cb9c-112">The [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="9cb9c-113">배포 및 스케줄러 설정을 포함하는 [webjob-publish-settings.json](#publishsettings) 파일</span><span class="sxs-lookup"><span data-stu-id="9cb9c-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![배포를 WebJob으로 설정하기 위해 콘솔 앱에 추가되는 내용을 보여 주는 다이어그램](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="9cb9c-115">이러한 항목을 기존 콘솔 응용 프로그램 프로젝트에 추가하거나 템플릿을 사용하여 새 WebJob 지원 콘솔 응용 프로그램 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-115">You can add these items to an existing Console Application project or use a template to create a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="9cb9c-116">프로젝트를 WebJob 자체로 배포하거나 웹 프로젝트를 배포할 때마다 자동으로 배포되도록 웹 프로젝트에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-116">You can deploy a project as a WebJob by itself, or link it to a web project so that it automatically deploys whenever you deploy the web project.</span></span> <span data-ttu-id="9cb9c-117">프로젝트를 연결할 수 있게 Visual Studio는 웹 프로젝트의 [webjobs-list.json](#webjobslist) 파일에 WebJob 지원 프로젝트의 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-117">To link projects, Visual Studio includes the name of the WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in the web project.</span></span>

![웹 프로젝트에 연결된 WebJob 프로젝트를 보여 주는 다이어그램](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="9cb9c-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9cb9c-119">Prerequisites</span></span>
<span data-ttu-id="9cb9c-120">WebJobs 배포 기능은 .NET용 Azure SDK를 설치할 때 Visual Studio에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-120">WebJobs deployment features are available in Visual Studio when you install the Azure SDK for .NET:</span></span>

* <span data-ttu-id="9cb9c-121">[.NET용 Azure SDK(Visual Studio)](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="9cb9c-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="9cb9c-122"><a id="convert"></a>기존 콘솔 응용 프로그램 프로젝트에 WebJob 배포 사용</span><span class="sxs-lookup"><span data-stu-id="9cb9c-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="9cb9c-123">다음 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-123">You have two options:</span></span>

* <span data-ttu-id="9cb9c-124">[웹 프로젝트를 사용하여 자동 배포 사용](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="9cb9c-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="9cb9c-125">기존 콘솔 응용 프로그램 프로젝트가 웹 프로젝트를 배포할 때 WebJob으로 자동 배포되도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="9cb9c-126">관련 웹 응용 프로그램을 실행하는 동일한 웹 앱에서 WebJob을 실행하려는 경우에 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-126">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>
* <span data-ttu-id="9cb9c-127">[웹 프로젝트를 제외하고 배포](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="9cb9c-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="9cb9c-128">기존 콘솔 응용 프로그램 프로젝트가 웹 프로젝트에 연결되지 않고 WebJob 자체로 배포되도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-128">Configure an existing Console Application project to deploy as a WebJob by itself, with no link to a web project.</span></span> <span data-ttu-id="9cb9c-129">웹 앱에서 웹 응용 프로그램은 실행하지 않고 WebJob만 실행하려는 경우에 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-129">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="9cb9c-130">웹 응용 프로그램 리소스와는 별도로 WebJob 리소스를 확장하기 위해서도 이러한 방식을 원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-130">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="9cb9c-131"><a id="convertlink"></a> 웹 프로젝트와 함께 자동 WebJob 배포 사용</span><span class="sxs-lookup"><span data-stu-id="9cb9c-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="9cb9c-132">**솔루션 탐색기**에서 웹 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **Existing Project as Azure WebJob(기존 프로젝트를 Azure WebJob으로)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-132">Right-click the web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Existing Project as Azure WebJob(기존 프로젝트를 Azure WebJob으로)](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="9cb9c-134">[Add Azure WebJob(Azure WebJob 추가)](#configure) 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-134">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="9cb9c-135">**프로젝트 이름** 드롭다운 목록에서 WebJob으로 추가할 콘솔 응용 프로그램 프로젝트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-135">In the **Project name** drop-down list, select the Console Application project to add as a WebJob.</span></span>
   
    ![Add Azure WebJob(Azure WebJob 추가) 대화 상자에서 프로젝트 선택](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="9cb9c-137">[Add Azure WebJob(Azure WebJob 추가)](#configure) 대화 상자를 완료하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-137">Complete the [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="9cb9c-138"><a id="convertnolink"></a> 웹 프로젝트를 제외한 WebJob 배포 사용</span><span class="sxs-lookup"><span data-stu-id="9cb9c-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="9cb9c-139">**솔루션 탐색기**에서 콘솔 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **Azure WebJob 게시...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-139">Right-click the Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Publish as Azure WebJob(Azure WebJob으로 게시)](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="9cb9c-141">[프로젝트 이름](#configure) 상자에서 프로젝트가 선택된 상태로 **Add Azure WebJob(Azure WebJob 추가)** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-141">The [Add Azure WebJob](#configure) dialog box appears, with the project selected in the **Project name** box.</span></span>
2. <span data-ttu-id="9cb9c-142">[Add Azure WebJob(Azure WebJob 추가)](#configure) 대화 상자를 완료하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-142">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="9cb9c-143">**웹 게시** 마법사가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-143">The **Publish Web** wizard appears.</span></span>  <span data-ttu-id="9cb9c-144">바로 게시하지 않으려면 마법사를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-144">If you do not want to publish immediately, close the wizard.</span></span> <span data-ttu-id="9cb9c-145">입력한 설정은 [프로젝트를 배포](#deploy)할 때 사용할 수 있게 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-145">The settings that you've entered are saved for when you do want to [deploy the project](#deploy).</span></span>

## <span data-ttu-id="9cb9c-146"><a id="create"></a>새 WebJob 지원 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="9cb9c-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="9cb9c-147">새 WebJob 지원 프로젝트를 만들려면 [이전 섹션](#convert)에 설명된 대로 콘솔 응용 프로그램 프로젝트 템플릿을 사용하고 WebJob 배포를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-147">To create a new WebJobs-enabled project, you can use the Console Application project template and enable WebJobs deployment as explained in [the previous section](#convert).</span></span> <span data-ttu-id="9cb9c-148">또는 WebJob new-project 템플릿을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-148">As an alternative, you can use the WebJobs new-project template:</span></span>

* [<span data-ttu-id="9cb9c-149">독립 WebJob을 위해 WebJob new-project 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="9cb9c-149">Use the WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="9cb9c-150">프로젝트를 만든 다음 웹 프로젝트에 연결되지 않고 WebJob 자체로 배포되도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-150">Create a project and configure it to deploy by itself as a WebJob, with no link to a web project.</span></span> <span data-ttu-id="9cb9c-151">웹 앱에서 웹 응용 프로그램은 실행하지 않고 WebJob만 실행하려는 경우에 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-151">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="9cb9c-152">웹 응용 프로그램 리소스와는 별도로 WebJob 리소스를 확장하기 위해서도 이러한 방식을 원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-152">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="9cb9c-153">웹 프로젝트에 연결된 WebJob을 위해 WebJob new-project 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="9cb9c-153">Use the WebJobs new-project template for a WebJob linked to a web project</span></span>](#createlink)
  
    <span data-ttu-id="9cb9c-154">동일한 솔루션의 웹 프로젝트가 배포될 때 자동으로 WebJob으로 배포되도록 구성된 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-154">Create a project that is configured to deploy automatically as a WebJob when a web project in the same solution is deployed.</span></span> <span data-ttu-id="9cb9c-155">관련 웹 응용 프로그램을 실행하는 동일한 웹 앱에서 WebJob을 실행하려는 경우에 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-155">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="9cb9c-156">WebJobs new-project 새 프로젝트 템플릿은 NuGet 패키지를 자동으로 설치하고 *WebJobs SDK* 에 대한 [Program.cs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs)에 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-156">The WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for the [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="9cb9c-157">WebJobs SDK를 사용하지 않으려면 *Program.cs*에서 `host.RunAndBlock` 문을 제거하거나 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-157">If you don't want to use the WebJobs SDK, remove or change the `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="9cb9c-158"><a id="createnolink"></a> 독립 WebJob을 위해 WebJob new-project 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="9cb9c-158"><a id="createnolink"></a> Use the WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="9cb9c-159">**파일** > **새 프로젝트**를 클릭한 다음 **새 프로젝트** 대화 상자에서 **클라우드** > **Azure WebJob(.NET Framework)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-159">Click **File** > **New Project**, and then in the **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![WebJob 템플릿을 표시하는 새 프로젝트 대화 상자](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="9cb9c-161">앞에 표시된 지침에 따라 [콘솔 응용 프로그램 프로젝트를 독립 WebJob 프로젝트로 만듭니다](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="9cb9c-161">Follow the directions shown earlier to [make the Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="9cb9c-162"><a id="createlink"></a> 웹 프로젝트에 연결된 WebJob을 위해 WebJob new-project 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="9cb9c-162"><a id="createlink"></a> Use the WebJobs new-project template for a WebJob linked to a web project</span></span>
1. <span data-ttu-id="9cb9c-163">**솔루션 탐색기**에서 웹 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **New Azure WebJob Project(새 Azure WebJob 프로젝트)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-163">Right-click the web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![New Azure WebJob Project(새 Azure WebJob 프로젝트) 메뉴 항목](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="9cb9c-165">[Add Azure WebJob(Azure WebJob 추가)](#configure) 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-165">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="9cb9c-166">[Add Azure WebJob(Azure WebJob 추가)](#configure) 대화 상자를 완료하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-166">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="9cb9c-167"><a id="configure"></a>Azure WebJob 추가 대화 상자</span><span class="sxs-lookup"><span data-stu-id="9cb9c-167"><a id="configure"></a>The Add Azure WebJob dialog</span></span>
<span data-ttu-id="9cb9c-168">**Azure WebJob 추가** 대화 상자에서 WebJob 이름을 입력하고 WebJob에 대한 모드 설정을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-168">The **Add Azure WebJob** dialog lets you enter the WebJob name and run mode setting for your WebJob.</span></span> 

![Add Azure WebJob(Azure WebJob 추가) 대화 상자](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="9cb9c-170">이 대화 상자의 필드는 Azure 포털의 **새 작업** 대화 상자에 있는 필드에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-170">The fields in this dialog correspond to fields on the **New Job** dialog of the Azure Portal.</span></span> <span data-ttu-id="9cb9c-171">자세한 내용은 [WebJobs를 사용하여 백그라운드 작업 실행](web-sites-create-web-jobs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="9cb9c-172">명령줄 배포에 대한 자세한 내용은 [Azure WebJob의 명령줄 또는 지속적인 전송 사용](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="9cb9c-173">WebJob을 배포한 다음 WebJob의 유형을 변경하고 재배포하는 경우, webjobs-publish-settings.json 파일을 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-173">If you deploy a WebJob and then decide you want to change the type of WebJob and redeploy, you'll need to delete the webjobs-publish-settings.json file.</span></span> <span data-ttu-id="9cb9c-174">이렇게 하면 Visual Studio가 게시 옵션을 다시 표시하므로, 웹 작업의 유형을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-174">This will make Visual Studio show the publishing options again, so you can change the type of WebJob.</span></span>
> * <span data-ttu-id="9cb9c-175">WebJob을 배포하고 나중에 실행 모드를 연속에서 비연속으로 또는 그 반대로 변경하면 Visual Studio는 사용자가 WebJob을 다시 배포할 때 Azure에서 새 WebJob을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-175">If you deploy a WebJob and later change the run mode from continuous to non-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="9cb9c-176">다른 일정 설정을 변경하고 실행 모드를 그대로 두거나 예약형 및 주문형 간을 전환하면 Visual Studio는 새 작업을 만들지 않고 기존 작업을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-176">If you change other scheduling settings but leave run mode the same or switch between Scheduled and On Demand, Visual Studio updates the existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="9cb9c-177"><a id="publishsettings"></a>webjob-publish-settings.json</span><span class="sxs-lookup"><span data-stu-id="9cb9c-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="9cb9c-178">WebJob 배포를 위해 콘솔 응용 프로그램을 구성하는 경우, Visual Studio는 [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet 패키지를 설치하고 WebJob 프로젝트의 프로젝트 *Properties* 폴더에 있는 *webjob-publish-settings.json* 파일에 일정 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs the [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in the project *Properties* folder of the WebJobs project.</span></span> <span data-ttu-id="9cb9c-179">다음은 이 파일의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="9cb9c-180">이 파일을 직접 편집할 수도 있고 Visual Studio에 제공되는 IntelliSense를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="9cb9c-181">파일 스키마는 [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) 에 저장되며 이 위치에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-181">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="9cb9c-182"><a id="webjobslist"></a>webjobs-list.json</span><span class="sxs-lookup"><span data-stu-id="9cb9c-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="9cb9c-183">WebJob 지원 프로젝트를 웹 프로젝트에 연결하면 Visual Studio는 WebJob 프로젝트의 이름을 웹 프로젝트의 *Properties* 폴더에 있는 *webjobs-list.json* 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-183">When you link a WebJobs-enabled project to a web project, Visual Studio stores the name of the WebJobs project in a *webjobs-list.json* file in the web project's *Properties* folder.</span></span> <span data-ttu-id="9cb9c-184">이 목록에는 다음 예와 같은 여러 WebJob 프로젝트가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-184">The list might contain multiple WebJobs projects, as shown in the following example:</span></span>

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

<span data-ttu-id="9cb9c-185">이 파일을 직접 편집할 수도 있고 Visual Studio에 제공되는 IntelliSense를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="9cb9c-186">파일 스키마는 [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) 에 저장되며 이 위치에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-186">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="9cb9c-187"><a id="deploy"></a>WebJob 프로젝트 배포</span><span class="sxs-lookup"><span data-stu-id="9cb9c-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="9cb9c-188">웹 프로젝트에 연결한 WebJob 프로젝트는 웹 프로젝트와 함께 자동으로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-188">A WebJobs project that you have linked to a web project deploys automatically with the web project.</span></span> <span data-ttu-id="9cb9c-189">웹 프로젝트 배포에 대한 자세한 내용은 [웹 앱에 배포하는 방법](web-sites-deploy.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-189">For information about web project deployment, see [How to deploy to Web Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="9cb9c-190">WebJob 프로젝트 자체적으로 배포하려면 **솔루션 탐색기**에서 이 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Azure WebJob 게시...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-190">To deploy a WebJobs project by itself, right-click the project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Publish as Azure WebJob(Azure WebJob으로 게시)](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="9cb9c-192">독립 WebJob의 경우 웹 프로젝트에 사용되는 것과 동일한 **웹 게시** 마법사가 나타나지만 변경할 수 있는 설정은 더 적습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-192">For an independent WebJob, the same **Publish Web** wizard that is used for web projects appears, but with fewer settings available to change.</span></span>

## <span data-ttu-id="9cb9c-193"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="9cb9c-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="9cb9c-194">이 문서는 Visual Studio를 사용하여 WebJobs를 배포하는 방법을 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-194">This article has explained how to deploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="9cb9c-195">Azure WebJobs를 배포하는 방법은 [Azure WebJobs - 권장 리소스 - 배포](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cb9c-195">For more information about how to deploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

