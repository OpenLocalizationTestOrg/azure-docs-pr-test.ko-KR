---
title: "Visual Studio Azure 응용 프로그램 게시 마법사 사용 | Microsoft Docs"
description: "Visual Studio Azure 응용 프로그램 게시 마법사에서 다양한 설정을 구성하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 25b3ca9af2639860d9cfcb1492aef745fb47beb9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-visual-studio-publish-azure-application-wizard"></a><span data-ttu-id="74e2c-103">Visual Studio Azure 응용 프로그램 게시 마법사 사용</span><span class="sxs-lookup"><span data-stu-id="74e2c-103">Using the Visual Studio Publish Azure Application Wizard</span></span>
<span data-ttu-id="74e2c-104">Visual Studio에서 웹 응용 프로그램을 개발한 후 **Azure 응용 프로그램 게시** 마법사를 사용하여 해당 응용 프로그램을 Azure 클라우드 서비스에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-104">After you develop a web application in Visual Studio, you can publish that application to an Azure cloud service by using the **Publish Azure Application** wizard.</span></span> 

> [!NOTE]
> <span data-ttu-id="74e2c-105">이 토픽은 웹 사이트가 아닌 클라우드 서비스에 배포에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-105">This topic is about deploying to cloud services, not to web sites.</span></span> <span data-ttu-id="74e2c-106">웹 사이트에 배포에 대한 자세한 내용은 [Azure 웹 사이트에 배포하는 방법](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74e2c-106">For information about deploying to web sites, see [How to Deploy an Azure Web Site](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false).</span></span>
> 
> 

## <a name="accessing-the-publish-azure-application-wizard"></a><span data-ttu-id="74e2c-107">Azure 응용 프로그램 게시 마법사 액세스</span><span class="sxs-lookup"><span data-stu-id="74e2c-107">Accessing the Publish Azure Application wizard</span></span>

<span data-ttu-id="74e2c-108">사용하는 Visual Studio 프로젝트 형식에 따라 다음 두 가지 방법으로 Azure 응용 프로그램 게시 마법사에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-108">You can access the Publish Azure Application wizard in two ways depending on the type of Visual Studio project you have.</span></span>

<span data-ttu-id="74e2c-109">**Azure 클라우드 서비스 프로젝트가 있는 경우:**</span><span class="sxs-lookup"><span data-stu-id="74e2c-109">**If you have an Azure cloud service project:**</span></span>

1. <span data-ttu-id="74e2c-110">Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="74e2c-111">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고, 상황에 맞는 메뉴에서 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-111">In **Solution Explorer**, right-click the project, and, from the context menu, select **Publish**.</span></span>

<span data-ttu-id="74e2c-112">**Azure에서 사용되지 않는 웹 응용 프로그램 프로젝트가 있는 경우:**</span><span class="sxs-lookup"><span data-stu-id="74e2c-112">**If you have a web application project that is not enabled for Azure:**</span></span>

1. <span data-ttu-id="74e2c-113">Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-113">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="74e2c-114">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고, 상황에 맞는 메뉴에서 **변환** > **Azure 클라우드 서비스 프로젝트로 변환**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-114">In **Solution Explorer**, right-click the project, and, from the context menu, select **Convert** > **Convert to Azure Cloud Service Project**.</span></span> 

1. <span data-ttu-id="74e2c-115">**솔루션 탐색기**에서 새로 만든 Azure 프로젝트를 마우스 오른쪽 단추로 클릭하고, 상황에 맞는 메뉴에서 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-115">In **Solution Explorer**, right-click the newly created Azure project, and, from the context menu, select **Publish**.</span></span>

## <a name="sign-in-page"></a><span data-ttu-id="74e2c-116">로그인 페이지</span><span class="sxs-lookup"><span data-stu-id="74e2c-116">Sign-in page</span></span>

![로그인 페이지](./media/vs-azure-tools-publish-azure-application-wizard/sign-in.png)

<span data-ttu-id="74e2c-118">**계정** - 계정을 선택하거나 계정 드롭다운 목록에서 **계정 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-118">**Account** - Select an account or select **Add an account** in the account dropdown list.</span></span>

<span data-ttu-id="74e2c-119">**구독 선택** - 배포에 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-119">**Choose your subscription** - Choose the subscription to use for your deployment.</span></span>
   
## <a name="settings-page---common-settings-tab"></a><span data-ttu-id="74e2c-120">설정 페이지 - 일반 설정 탭</span><span class="sxs-lookup"><span data-stu-id="74e2c-120">Settings page - Common Settings tab</span></span>   

![일반 설정](./media/vs-azure-tools-publish-azure-application-wizard/settings-common-settings.png)

<span data-ttu-id="74e2c-122">**클라우드 서비스** - 드롭다운을 사용하여 기존 클라우드 서비스를 선택하거나 **&lt;새로 만들기>**를 선택하고 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-122">**Cloud service** - Using the dropdown, either select an existing cloud service, or select **&lt;Create New>**, and create a cloud service.</span></span> <span data-ttu-id="74e2c-123">데이터 센터가 각 클라우드 서비스에 대한 괄호 안에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-123">The data center displays in parentheses for each cloud service.</span></span> <span data-ttu-id="74e2c-124">클라우드 서비스의 데이터 센터 위치는 저장소 계정의 데이터 센터 위치와 동일하게 설정(고급 설정)하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-124">It is recommended that the data center location for the cloud service be the same as the data center location for the storage account (Advanced Settings).</span></span>  

<span data-ttu-id="74e2c-125">**환경** - **프로덕션** 또는 **스테이징** 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-125">**Environment** - Select either **Production** or **Staging**.</span></span> <span data-ttu-id="74e2c-126">테스트 환경에 응용 프로그램을 배포하려면 스테이징 환경을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-126">Choose the staging environment if you want to deploy your application in a test environment.</span></span> 

<span data-ttu-id="74e2c-127">**빌드 구성** - **디버그** 또는 **릴리스** 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-127">**Build configuration** - Select either **Debug** or **Release**.</span></span>

<span data-ttu-id="74e2c-128">**서비스 구성** - **클라우드** 또는 **로컬** 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-128">**Service configuration** - Select either **Cloud** or **Local**.</span></span>
   
<span data-ttu-id="74e2c-129">**모든 역할에 대해 원격 데스크톱 사용** - 원격으로 서비스에 연결하려면 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-129">**Enable Remote Desktop for all roles** - Check this option if you want to be able to remotely connect to the service.</span></span> <span data-ttu-id="74e2c-130">이 옵션은 주로 문제 해결을 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-130">This option is primarily used for troubleshooting.</span></span> <span data-ttu-id="74e2c-131">이 확인란을 선택하는 경우 **원격 데스크톱 구성** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-131">When you select this check box, the **Remote Desktop Configuration** dialog box appears.</span></span> <span data-ttu-id="74e2c-132">구성을 변경하려면 **설정** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-132">Choose the **Settings** link to change the configuration.</span></span>
   
<span data-ttu-id="74e2c-133">**모든 웹 역할에 대해 웹 배포 사용** - 서비스에 웹 배포를 사용하도록 설정하려면 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-133">**Enable Web Deploy for all web roles** - Check this option, to enable web deployment for the service.</span></span> <span data-ttu-id="74e2c-134">이 기능을 사용하려면 **모든 역할에 대해 원격 데스크톱 사용** 옵션을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-134">You must select the **Enable Remote Desktop for all roles** option to use this feature.</span></span> <span data-ttu-id="74e2c-135">자세한 내용은 [[Visual Studio를 사용하여 Azure 클라우드 서비스 게시](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74e2c-135">For more information, see [[Publishing a Azure cloud service using Visual Studio](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx).</span></span> 

## <a name="settings-page---advanced-settings-tab"></a><span data-ttu-id="74e2c-136">설정 페이지 - 고급 설정 탭</span><span class="sxs-lookup"><span data-stu-id="74e2c-136">Settings page - Advanced Settings tab</span></span>

![고급 설정](./media/vs-azure-tools-publish-azure-application-wizard/settings-advanced-settings.png)

<span data-ttu-id="74e2c-138">**배포 레이블** - 기본 이름을 그대로 사용하거나 선택한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-138">**Deployment label** - Either accept the default name, or enter a name of your choosing.</span></span> <span data-ttu-id="74e2c-139">배포 레이블에 날짜를 추가하려면 확인란을 선택한 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-139">To append the date to the deployment label, leave the check box selected.</span></span> 
   
<span data-ttu-id="74e2c-140">**저장소 계정** - 이 배포에 사용할 저장소 계정을 선택하거나 ** &lt;새로 만들기>를 사용하여 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-140">**Storage account** - Select the storage account to use for this deployment, **&lt;Create New> to create a storage account.</span></span> <span data-ttu-id="74e2c-141">데이터 센터가 각 저장소 계정에 대한 괄호 안에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-141">The data center displays in parentheses for each storage account.</span></span> <span data-ttu-id="74e2c-142">저장소 계정의 데이터 센터 위치는 클라우드 서비스의 데이터 센터 위치와 동일하게 설정(일반 설정)하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-142">It is recommended that the data center location for the storage account be the same as the data center location for the cloud service (Common Settings).</span></span>  
   
<span data-ttu-id="74e2c-143">Azure 저장소 계정은 응용 프로그램 배포용 패키지를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-143">The Azure storage account stores the package for the application deployment.</span></span> <span data-ttu-id="74e2c-144">응용 프로그램이 배포된 후 패키지는 저장소 계정에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-144">After the application is deployed, the package is removed from the storage account.</span></span>

<span data-ttu-id="74e2c-145">**실패 시 배포 삭제** - 게시 중에 오류가 발생한 배포를 삭제하려면 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-145">**Delete deployment on failure** - Select this option to have the deployment deleted if any errors are encountered during publishing.</span></span> <span data-ttu-id="74e2c-146">클라우드 서비스의 상수 가상 IP 주소를 유지하려면 이 옵션을 선택 취소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-146">This should be unchecked if you want to maintain a constant virtual IP address for your cloud service.</span></span>

<span data-ttu-id="74e2c-147">**배포 업데이트** - 업데이트된 구성 요소만 배포하려면 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-147">**Deployment update** - Select this option if you want to deploy only updated components.</span></span> <span data-ttu-id="74e2c-148">이 유형의 배포는 전체 배포보다 빠를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-148">This type of deployment can be faster than a full deployment.</span></span> <span data-ttu-id="74e2c-149">클라우드 서비스의 상수 가상 IP 주소를 유지하려면 이 옵션을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-149">This should be checked if you want to maintain a constant virtual IP address for your cloud service.</span></span> 

<span data-ttu-id="74e2c-150">**배포 업데이트 - 설정** - 이 대화 상자는 역할을 업데이트하는 방법을 자세히 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-150">**Deployment update - settings** - This dialog is used to further specify how you want the roles to be updated.</span></span> <span data-ttu-id="74e2c-151">**증분 업데이트**를 선택하면 응용 프로그램의 각 인스턴스가 하나씩 차례로 업데이트되므로 해당 응용 프로그램을 항상 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-151">If you choose **Incremental update**, each instance of your application is updated one after another, so that the application is always available.</span></span> <span data-ttu-id="74e2c-152">**동시 업데이트**를 선택하면 응용 프로그램의 모든 인스턴스가 동시에 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-152">If you choose **Simultaneous update**, all instances of your application are updated at the same time.</span></span> <span data-ttu-id="74e2c-153">동시 업데이트는 신속하게 진행되지만 업데이트 과정 중에 서비스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-153">Simultaneous updating is faster, but your service might not be available during the update process.</span></span> 

![배포 설정](./media/vs-azure-tools-publish-azure-application-wizard/deployment-settings.png)

<span data-ttu-id="74e2c-155">**IntelliTrace 사용** - IntelliTrace를 사용하도록 설정할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-155">**Enable IntelliTrace** - Specify if you want to enable IntelliTrace.</span></span> <span data-ttu-id="74e2c-156">IntelliTrace를 사용하여 Azure에서 실행할 때 역할 인스턴스에 대한 광범위한 정보를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-156">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="74e2c-157">문제의 원인을 찾아야 하는 경우 Azure에서 실행 중인 것처럼 Visual Studio에서 코드를 단계별로 거쳐 IntelliTrace 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-157">If you need to find the cause of a problem, you can use the IntelliTrace logs to step through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="74e2c-158">IntelliTrace 사용에 대한 자세한 내용은 [IntelliTrace 및 Visual Studio를 사용하여 게시된 Azure 클라우드 서비스 디버깅](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74e2c-158">For more information about using IntelliTrace, see [Debugging a published Azure cloud service with Visual Studio and IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md).</span></span> 

<span data-ttu-id="74e2c-159">**프로파일링 사용** - 성능 프로파일링을 사용하도록 설정할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-159">**Enable profiling** - Specify if you want to enable performance profiling.</span></span> <span data-ttu-id="74e2c-160">Visual Studio 프로파일러를 사용하면 클라우드 서비스가 실행되는 방식의 계산 측면을 자세히 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-160">The Visual Studio profiler enables you to get an in-depth analysis of the computational aspects of how your cloud service runs.</span></span> <span data-ttu-id="74e2c-161">Visual Studio 프로파일러 사용에 대한 자세한 내용은 [Azure 클라우드 서비스의 성능 테스트](./vs-azure-tools-performance-profiling-cloud-services.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74e2c-161">For more information on using the Visual Studio profiler, see [Test the performance of an Azure cloud service](./vs-azure-tools-performance-profiling-cloud-services.md).</span></span>

<span data-ttu-id="74e2c-162">**모든 역할에 대해 원격 디버거 사용** - 원격 디버깅을 사용하도록 설정할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-162">**Enable Remote Debugger for all roles** - Specify if you want to enable remote debugging.</span></span> <span data-ttu-id="74e2c-163">Visual Studio를 사용하여 클라우드 서비스를 디버그하는 방법에 대한 자세한 내용은 [Visual Studio에서 Azure 클라우드 서비스 또는 가상 컴퓨터 디버깅](./vs-azure-tools-debug-cloud-services-virtual-machines.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74e2c-163">For more information on debugging cloud services using Visual Studio, see [Debugging an Azure cloud service or virtual machine in Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md).</span></span>

## <a name="diagnostics-settings-page"></a><span data-ttu-id="74e2c-164">진단 설정 페이지</span><span class="sxs-lookup"><span data-stu-id="74e2c-164">Diagnostics Settings page</span></span>

![진단 설정](./media/vs-azure-tools-publish-azure-application-wizard/diagnostic-settings.png)

<span data-ttu-id="74e2c-166">진단을 통해 Azure 클라우드 서비스(또는 Azure 가상 컴퓨터)의 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-166">Diagnostics enables you to troubleshoot an Azure cloud service (or Azure virtual machine).</span></span> <span data-ttu-id="74e2c-167">진단에 대한 자세한 내용은 [Azure 클라우드 서비스 및 가상 컴퓨터에서 진단 구성](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74e2c-167">For information about diagnostics, see [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span> <span data-ttu-id="74e2c-168">Application Insights에 대한 자세한 내용은 [Application Insights란?](./application-insights/app-insights-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74e2c-168">For information about Application Insights, see [What is Application Insights?](./application-insights/app-insights-overview.md).</span></span>

## <a name="summary-page"></a><span data-ttu-id="74e2c-169">요약 페이지</span><span class="sxs-lookup"><span data-stu-id="74e2c-169">Summary page</span></span>

![요약](./media/vs-azure-tools-publish-azure-application-wizard/summary.png)

<span data-ttu-id="74e2c-171">**대상 프로필** - 선택한 설정에서 게시 프로필을 만들도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-171">**Target profile** - You can choose to create a publishing profile from the settings that you have chosen.</span></span> <span data-ttu-id="74e2c-172">예를 들어, 테스트 환경에 대한 하나의 프로필을 만들고 프로덕션용으로 다른 하나를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-172">For example, you might create one profile for a test environment and another for production.</span></span> <span data-ttu-id="74e2c-173">이 프로필을 저장하려면 **저장** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-173">To save this profile, choose the **Save** icon.</span></span> <span data-ttu-id="74e2c-174">마법사는 프로필을 만들고 Visual Studio 프로젝트에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-174">The wizard creates the profile and saves it in the Visual Studio project.</span></span> <span data-ttu-id="74e2c-175">프로필 이름을 수정하려면 **대상 프로필** 목록을 연 다음 **<관리...>**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-175">To modify the profile name, open the **Target profile** list, and then choose **<Manage…>**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="74e2c-176">게시 프로필은 Visual Studio의 솔루션 탐색기에 나타나며 프로필 설정은 확장명이 .azurePubxml인 파일로 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-176">The publishing profile appears in Solution Explorer in Visual Studio, and the profile settings are written to a file with an .azurePubxml extension.</span></span> <span data-ttu-id="74e2c-177">설정은 XML 태그의 특성으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-177">Settings are saved as attributes of XML tags.</span></span>
   > 
   > 

## <a name="publishing-your-application"></a><span data-ttu-id="74e2c-178">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="74e2c-178">Publishing your application</span></span>

<span data-ttu-id="74e2c-179">프로젝트 배포에 대한 설정을 모두 구성했으면 대화 상자의 아래쪽에서 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-179">Once you configure all the settings for your project's deployment, select **Publish** at the bottom of the dialog.</span></span> <span data-ttu-id="74e2c-180">Visual Studio의 **출력** 창에서 프로세스 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74e2c-180">You can monitor the process status in the **Output** window in Visual Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74e2c-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="74e2c-181">Next steps</span></span>
- [<span data-ttu-id="74e2c-182">Visual Studio에서 Azure 클라우드 서비스로 웹 응용 프로그램 마이그레이션 및 게시</span><span class="sxs-lookup"><span data-stu-id="74e2c-182">Migrate and publish a Web Application to an Azure cloud service from Visual Studio</span></span>](./vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)
- [<span data-ttu-id="74e2c-183">Visual Studio를 사용하여 Azure 클라우드 서비스 게시</span><span class="sxs-lookup"><span data-stu-id="74e2c-183">Learn how to use Visual Studio to publish an Azure cloud service</span></span>](./vs-azure-tools-publishing-a-cloud-service.md)
- [<span data-ttu-id="74e2c-184">IntelliTrace 및 Visual Studio를 사용하여 게시된 Azure 클라우드 서비스 디버깅</span><span class="sxs-lookup"><span data-stu-id="74e2c-184">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)
- [<span data-ttu-id="74e2c-185">Azure 클라우드 서비스의 성능 테스트</span><span class="sxs-lookup"><span data-stu-id="74e2c-185">Test the performance of an Azure cloud service</span></span>](./vs-azure-tools-performance-profiling-cloud-services.md)
- <span data-ttu-id="74e2c-186">[Azure 클라우드 서비스 및 가상 컴퓨터에서 진단 구성](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="74e2c-186">[Configuring Diagnostics for Azure Cloud Services and Virtual Machines](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span> 
- [<span data-ttu-id="74e2c-187">Application Insights란?</span><span class="sxs-lookup"><span data-stu-id="74e2c-187">What is Application Insights?</span></span>](./application-insights/app-insights-overview.md)