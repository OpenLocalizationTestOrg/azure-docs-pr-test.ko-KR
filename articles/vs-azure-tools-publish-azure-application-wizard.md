---
title: "Visual Studio 게시 Azure 응용 프로그램 마법사 aaaUsing hello | Microsoft Docs"
description: "Tooconfigure hello Visual Studio Azure 응용 프로그램 게시 마법사에서에서 다양 한 설정을 hello 하는 방법에 대해 알아봅니다"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d8f1ac9-e439-47e0-a183-0642c4ea1920
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3f0b580d0054cc246372597660d8ae317d9b8686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-visual-studio-publish-azure-application-wizard"></a><span data-ttu-id="b9f60-103">Hello Visual Studio Azure 응용 프로그램 게시 마법사를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b9f60-103">Using hello Visual Studio Publish Azure Application Wizard</span></span>
<span data-ttu-id="b9f60-104">Visual Studio에서 웹 응용 프로그램을 개발한 후 hello를 사용 하 여 해당 응용 프로그램 tooan Azure 클라우드 서비스를 게시할 수 있습니다 **Azure 응용 프로그램 게시** 마법사.</span><span class="sxs-lookup"><span data-stu-id="b9f60-104">After you develop a web application in Visual Studio, you can publish that application tooan Azure cloud service by using hello **Publish Azure Application** wizard.</span></span> 

> [!NOTE]
> <span data-ttu-id="b9f60-105">이 항목은 서비스 toocloud 하지 tooweb 사이트 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-105">This topic is about deploying toocloud services, not tooweb sites.</span></span> <span data-ttu-id="b9f60-106">Tooweb 사이트를 배포 하는 방법에 대 한 정보를 참조 하십시오. [어떻게 tooDeploy Azure 웹 사이트](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-106">For information about deploying tooweb sites, see [How tooDeploy an Azure Web Site](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false).</span></span>
> 
> 

## <a name="accessing-hello-publish-azure-application-wizard"></a><span data-ttu-id="b9f60-107">Hello Azure 응용 프로그램 게시 마법사에 액세스</span><span class="sxs-lookup"><span data-stu-id="b9f60-107">Accessing hello Publish Azure Application wizard</span></span>

<span data-ttu-id="b9f60-108">Visual Studio 프로젝트의 hello 형식에 따라 두 가지 방법으로 hello Azure 응용 프로그램 게시 마법사를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-108">You can access hello Publish Azure Application wizard in two ways depending on hello type of Visual Studio project you have.</span></span>

<span data-ttu-id="b9f60-109">**Azure 클라우드 서비스 프로젝트가 있는 경우:**</span><span class="sxs-lookup"><span data-stu-id="b9f60-109">**If you have an Azure cloud service project:**</span></span>

1. <span data-ttu-id="b9f60-110">Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="b9f60-111">**솔루션 탐색기**, hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고, hello 상황에 맞는 메뉴에서 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Publish**.</span></span>

<span data-ttu-id="b9f60-112">**Azure에서 사용되지 않는 웹 응용 프로그램 프로젝트가 있는 경우:**</span><span class="sxs-lookup"><span data-stu-id="b9f60-112">**If you have a web application project that is not enabled for Azure:**</span></span>

1. <span data-ttu-id="b9f60-113">Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-113">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="b9f60-114">**솔루션 탐색기**, hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고, hello 상황에 맞는 메뉴에서 선택 **변환** > **tooAzure 클라우드 서비스 프로젝트를 변환**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-114">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Convert** > **Convert tooAzure Cloud Service Project**.</span></span> 

1. <span data-ttu-id="b9f60-115">**솔루션 탐색기**, hello 새로 만든 Azure 프로젝트를 마우스 오른쪽 단추로 클릭 하 고, hello 상황에 맞는 메뉴에서 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-115">In **Solution Explorer**, right-click hello newly created Azure project, and, from hello context menu, select **Publish**.</span></span>

## <a name="sign-in-page"></a><span data-ttu-id="b9f60-116">로그인 페이지</span><span class="sxs-lookup"><span data-stu-id="b9f60-116">Sign-in page</span></span>

![로그인 페이지](./media/vs-azure-tools-publish-azure-application-wizard/sign-in.png)

<span data-ttu-id="b9f60-118">**계정** -계정을 선택 하거나 선택 **계정 추가** hello 계정 드롭다운 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-118">**Account** - Select an account or select **Add an account** in hello account dropdown list.</span></span>

<span data-ttu-id="b9f60-119">**구독 선택** -배포에 대 한 구독 toouse hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-119">**Choose your subscription** - Choose hello subscription toouse for your deployment.</span></span>
   
## <a name="settings-page---common-settings-tab"></a><span data-ttu-id="b9f60-120">설정 페이지 - 일반 설정 탭</span><span class="sxs-lookup"><span data-stu-id="b9f60-120">Settings page - Common Settings tab</span></span>   

![일반 설정](./media/vs-azure-tools-publish-azure-application-wizard/settings-common-settings.png)

<span data-ttu-id="b9f60-122">**클라우드 서비스** -hello 드롭다운을 선택 하 여 하거나 기존 클라우드 서비스 또는 선택  **&lt;새로 만들기 >**, 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-122">**Cloud service** - Using hello dropdown, either select an existing cloud service, or select **&lt;Create New>**, and create a cloud service.</span></span> <span data-ttu-id="b9f60-123">hello 데이터 센터는 각 클라우드 서비스에 대 한 괄호 안에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-123">hello data center displays in parentheses for each cloud service.</span></span> <span data-ttu-id="b9f60-124">데이터 센터 위치 hello hello 클라우드 서비스 수에 대 한 hello 동일 hello 저장소 계정 (고급 설정)에 대 한 데이터 센터 위치 hello로 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-124">It is recommended that hello data center location for hello cloud service be hello same as hello data center location for hello storage account (Advanced Settings).</span></span>  

<span data-ttu-id="b9f60-125">**환경** - **프로덕션** 또는 **스테이징** 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-125">**Environment** - Select either **Production** or **Staging**.</span></span> <span data-ttu-id="b9f60-126">테스트 환경에서 스테이징 환경 toodeploy 하려는 경우 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-126">Choose hello staging environment if you want toodeploy your application in a test environment.</span></span> 

<span data-ttu-id="b9f60-127">**빌드 구성** - **디버그** 또는 **릴리스** 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-127">**Build configuration** - Select either **Debug** or **Release**.</span></span>

<span data-ttu-id="b9f60-128">**서비스 구성** - **클라우드** 또는 **로컬** 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-128">**Service configuration** - Select either **Cloud** or **Local**.</span></span>
   
<span data-ttu-id="b9f60-129">**모든 역할에 대 한 원격 데스크톱 사용** -toobe 수 tooremotely 하려는 경우이 옵션의 선택을 toohello 서비스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-129">**Enable Remote Desktop for all roles** - Check this option if you want toobe able tooremotely connect toohello service.</span></span> <span data-ttu-id="b9f60-130">이 옵션은 주로 문제 해결을 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-130">This option is primarily used for troubleshooting.</span></span> <span data-ttu-id="b9f60-131">이 확인란을 선택 하면 hello **원격 데스크톱 구성** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-131">When you select this check box, hello **Remote Desktop Configuration** dialog box appears.</span></span> <span data-ttu-id="b9f60-132">Hello 선택 **설정을** 링크 toochange hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-132">Choose hello **Settings** link toochange hello configuration.</span></span>
   
<span data-ttu-id="b9f60-133">**모든 웹 역할에 대해 웹 배포 사용** -이 옵션을 hello 서비스에 대 한 tooenable 웹 배포를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-133">**Enable Web Deploy for all web roles** - Check this option, tooenable web deployment for hello service.</span></span> <span data-ttu-id="b9f60-134">Hello를 선택 해야 **모든 역할에 원격 데스크톱 사용** 이 기능은 toouse 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-134">You must select hello **Enable Remote Desktop for all roles** option toouse this feature.</span></span> <span data-ttu-id="b9f60-135">자세한 내용은 [[Visual Studio를 사용하여 Azure 클라우드 서비스 게시](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9f60-135">For more information, see [[Publishing a Azure cloud service using Visual Studio](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx).</span></span> 

## <a name="settings-page---advanced-settings-tab"></a><span data-ttu-id="b9f60-136">설정 페이지 - 고급 설정 탭</span><span class="sxs-lookup"><span data-stu-id="b9f60-136">Settings page - Advanced Settings tab</span></span>

![고급 설정](./media/vs-azure-tools-publish-azure-application-wizard/settings-advanced-settings.png)

<span data-ttu-id="b9f60-138">**배포 레이블** -hello 기본 이름을 그대로 적용 하거나 사용자가 선택 하는 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-138">**Deployment label** - Either accept hello default name, or enter a name of your choosing.</span></span> <span data-ttu-id="b9f60-139">tooappend hello 날짜 toohello 배포 레이블, leave hello 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-139">tooappend hello date toohello deployment label, leave hello check box selected.</span></span> 
   
<span data-ttu-id="b9f60-140">**저장소 계정** -선택이 배포에 대 한 저장소 계정 toouse hello * *&lt;새로 만들기 > toocreate 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-140">**Storage account** - Select hello storage account toouse for this deployment, **&lt;Create New> toocreate a storage account.</span></span> <span data-ttu-id="b9f60-141">hello 데이터 센터는 각 저장소 계정에 대 한 괄호 안에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-141">hello data center displays in parentheses for each storage account.</span></span> <span data-ttu-id="b9f60-142">데이터 센터 위치 hello hello 저장소 계정 수에 대 한 hello 동일 hello 클라우드 서비스 (일반 설정)에 대 한 데이터 센터 위치 hello로 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-142">It is recommended that hello data center location for hello storage account be hello same as hello data center location for hello cloud service (Common Settings).</span></span>  
   
<span data-ttu-id="b9f60-143">Azure 저장소 계정 hello hello 응용 프로그램 배포에 대 한 hello 패키지를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-143">hello Azure storage account stores hello package for hello application deployment.</span></span> <span data-ttu-id="b9f60-144">Hello 응용 프로그램 배포 된 후 hello 패키지가 hello 저장소 계정에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-144">After hello application is deployed, hello package is removed from hello storage account.</span></span>

<span data-ttu-id="b9f60-145">**실패 시 배포 삭제** -게시 하는 동안 오류가 발생 하는 경우 삭제 되는이 옵션 toohave hello 배포를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-145">**Delete deployment on failure** - Select this option toohave hello deployment deleted if any errors are encountered during publishing.</span></span> <span data-ttu-id="b9f60-146">이 선택 취소 해야 클라우드 서비스에 대 한 toomaintain 일정 한 가상 IP 주소를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-146">This should be unchecked if you want toomaintain a constant virtual IP address for your cloud service.</span></span>

<span data-ttu-id="b9f60-147">**배포 업데이트** -toodeploy 구성 요소에만 업데이트 하려는 경우이 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-147">**Deployment update** - Select this option if you want toodeploy only updated components.</span></span> <span data-ttu-id="b9f60-148">이 유형의 배포는 전체 배포보다 빠를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-148">This type of deployment can be faster than a full deployment.</span></span> <span data-ttu-id="b9f60-149">클라우드 서비스에 대 한 toomaintain 일정 한 가상 IP 주소를 사용 하려는 경우이 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-149">This should be checked if you want toomaintain a constant virtual IP address for your cloud service.</span></span> 

<span data-ttu-id="b9f60-150">**배포 업데이트-설정** -이 대화 상자를 사용 toofurther hello 역할 toobe 업데이트 하려는 방식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-150">**Deployment update - settings** - This dialog is used toofurther specify how you want hello roles toobe updated.</span></span> <span data-ttu-id="b9f60-151">선택 하면 **증분 업데이트**, 해당 hello 응용 프로그램은 항상 사용할 수 있도록 응용 프로그램의 각 인스턴스는 서로 하나씩 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-151">If you choose **Incremental update**, each instance of your application is updated one after another, so that hello application is always available.</span></span> <span data-ttu-id="b9f60-152">선택 하면 **동시 업데이트**, hello에 응용 프로그램의 모든 인스턴스가 업데이트 됩니다 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-152">If you choose **Simultaneous update**, all instances of your application are updated at hello same time.</span></span> <span data-ttu-id="b9f60-153">동시 업데이트는 속도가 더 있지만 hello 업데이트 과정 인해 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-153">Simultaneous updating is faster, but your service might not be available during hello update process.</span></span> 

![배포 설정](./media/vs-azure-tools-publish-azure-application-wizard/deployment-settings.png)

<span data-ttu-id="b9f60-155">**IntelliTrace를 활성화** -tooenable IntelliTrace 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-155">**Enable IntelliTrace** - Specify if you want tooenable IntelliTrace.</span></span> <span data-ttu-id="b9f60-156">IntelliTrace를 사용하여 Azure에서 실행할 때 역할 인스턴스에 대한 광범위한 정보를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-156">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="b9f60-157">IntelliTrace 로그 toostep hello Azure에서 실행 중인 경우에 따라 toofind hello 원인을 해야 할 경우 Visual Studio에서 코드를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-157">If you need toofind hello cause of a problem, you can use hello IntelliTrace logs toostep through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="b9f60-158">IntelliTrace 사용에 대한 자세한 내용은 [IntelliTrace 및 Visual Studio를 사용하여 게시된 Azure 클라우드 서비스 디버깅](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9f60-158">For more information about using IntelliTrace, see [Debugging a published Azure cloud service with Visual Studio and IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md).</span></span> 

<span data-ttu-id="b9f60-159">**프로 파일링 사용** -tooenable 성능 프로 파일링 하려는 경우를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-159">**Enable profiling** - Specify if you want tooenable performance profiling.</span></span> <span data-ttu-id="b9f60-160">Visual Studio 프로파일러 hello tooget을 hello 클라우드 서비스가 실행 되는 어떻게 계산 측면을 자세히 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-160">hello Visual Studio profiler enables you tooget an in-depth analysis of hello computational aspects of how your cloud service runs.</span></span> <span data-ttu-id="b9f60-161">Hello Visual Studio 프로파일러를 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [Azure 클라우드 서비스의 hello 성능을 테스트](./vs-azure-tools-performance-profiling-cloud-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-161">For more information on using hello Visual Studio profiler, see [Test hello performance of an Azure cloud service](./vs-azure-tools-performance-profiling-cloud-services.md).</span></span>

<span data-ttu-id="b9f60-162">**모든 역할에 원격 디버거 사용** -tooenable 원격 디버깅 하려는 경우를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-162">**Enable Remote Debugger for all roles** - Specify if you want tooenable remote debugging.</span></span> <span data-ttu-id="b9f60-163">Visual Studio를 사용하여 클라우드 서비스를 디버그하는 방법에 대한 자세한 내용은 [Visual Studio에서 Azure 클라우드 서비스 또는 가상 컴퓨터 디버깅](./vs-azure-tools-debug-cloud-services-virtual-machines.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9f60-163">For more information on debugging cloud services using Visual Studio, see [Debugging an Azure cloud service or virtual machine in Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md).</span></span>

## <a name="diagnostics-settings-page"></a><span data-ttu-id="b9f60-164">진단 설정 페이지</span><span class="sxs-lookup"><span data-stu-id="b9f60-164">Diagnostics Settings page</span></span>

![진단 설정](./media/vs-azure-tools-publish-azure-application-wizard/diagnostic-settings.png)

<span data-ttu-id="b9f60-166">진단을 사용 tootroubleshoot Azure 클라우드 서비스 (또는 Azure 가상 컴퓨터) 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-166">Diagnostics enables you tootroubleshoot an Azure cloud service (or Azure virtual machine).</span></span> <span data-ttu-id="b9f60-167">진단에 대한 자세한 내용은 [Azure 클라우드 서비스 및 가상 컴퓨터에서 진단 구성](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9f60-167">For information about diagnostics, see [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span> <span data-ttu-id="b9f60-168">Application Insights에 대한 자세한 내용은 [Application Insights란?](./application-insights/app-insights-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9f60-168">For information about Application Insights, see [What is Application Insights?](./application-insights/app-insights-overview.md).</span></span>

## <a name="summary-page"></a><span data-ttu-id="b9f60-169">요약 페이지</span><span class="sxs-lookup"><span data-stu-id="b9f60-169">Summary page</span></span>

![요약](./media/vs-azure-tools-publish-azure-application-wizard/summary.png)

<span data-ttu-id="b9f60-171">**Profile을 대상** -하고자 하는 hello 설정에서 toocreate 게시 프로필을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-171">**Target profile** - You can choose toocreate a publishing profile from hello settings that you have chosen.</span></span> <span data-ttu-id="b9f60-172">예를 들어, 테스트 환경에 대한 하나의 프로필을 만들고 프로덕션용으로 다른 하나를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-172">For example, you might create one profile for a test environment and another for production.</span></span> <span data-ttu-id="b9f60-173">toosave이 프로필을 선택 hello **저장** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-173">toosave this profile, choose hello **Save** icon.</span></span> <span data-ttu-id="b9f60-174">hello 마법사 hello 프로필을 만들고 hello Visual Studio 프로젝트에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-174">hello wizard creates hello profile and saves it in hello Visual Studio project.</span></span> <span data-ttu-id="b9f60-175">toomodify hello 프로필 이름에 열기 hello **profile을 대상** 목록에서 선택한 후 **< 관리... >**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-175">toomodify hello profile name, open hello **Target profile** list, and then choose **<Manage…>**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b9f60-176">hello 게시 프로필이 나타나고 Visual Studio의 솔루션 탐색기에서 및 hello 프로필 설정이 확장명이.azurePubxml tooa 파일에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-176">hello publishing profile appears in Solution Explorer in Visual Studio, and hello profile settings are written tooa file with an .azurePubxml extension.</span></span> <span data-ttu-id="b9f60-177">설정은 XML 태그의 특성으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-177">Settings are saved as attributes of XML tags.</span></span>
   > 
   > 

## <a name="publishing-your-application"></a><span data-ttu-id="b9f60-178">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="b9f60-178">Publishing your application</span></span>

<span data-ttu-id="b9f60-179">프로젝트의 배포에 대 한 모든 hello 설정을 구성 하 고 나면 선택 **게시** hello hello 대화 상자 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-179">Once you configure all hello settings for your project's deployment, select **Publish** at hello bottom of hello dialog.</span></span> <span data-ttu-id="b9f60-180">Hello에 hello 프로세스 상태를 모니터링할 수 **출력** Visual Studio의 창.</span><span class="sxs-lookup"><span data-stu-id="b9f60-180">You can monitor hello process status in hello **Output** window in Visual Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9f60-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b9f60-181">Next steps</span></span>
- [<span data-ttu-id="b9f60-182">마이그레이션 및 웹 응용 프로그램 tooan Visual Studio에서 Azure 클라우드 서비스 게시</span><span class="sxs-lookup"><span data-stu-id="b9f60-182">Migrate and publish a Web Application tooan Azure cloud service from Visual Studio</span></span>](./vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)
- [<span data-ttu-id="b9f60-183">방법: Visual Studio toopublish toouse Azure 클라우드 서비스에 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="b9f60-183">Learn how toouse Visual Studio toopublish an Azure cloud service</span></span>](./vs-azure-tools-publishing-a-cloud-service.md)
- [<span data-ttu-id="b9f60-184">IntelliTrace 및 Visual Studio를 사용하여 게시된 Azure 클라우드 서비스 디버깅</span><span class="sxs-lookup"><span data-stu-id="b9f60-184">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)
- [<span data-ttu-id="b9f60-185">Azure 클라우드 서비스의 hello 성능을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f60-185">Test hello performance of an Azure cloud service</span></span>](./vs-azure-tools-performance-profiling-cloud-services.md)
- <span data-ttu-id="b9f60-186">[Azure 클라우드 서비스 및 가상 컴퓨터에서 진단 구성](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="b9f60-186">[Configuring Diagnostics for Azure Cloud Services and Virtual Machines](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span> 
- [<span data-ttu-id="b9f60-187">Application Insights란?</span><span class="sxs-lookup"><span data-stu-id="b9f60-187">What is Application Insights?</span></span>](./application-insights/app-insights-overview.md)