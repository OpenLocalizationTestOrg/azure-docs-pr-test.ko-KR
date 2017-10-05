---
title: "Visual Studio를 사용하여 Azure 앱 서비스에서 웹 앱 문제 해결"
description: "Visual Studio 2013에서 기본 제공되는 원격 디버깅, 추적 및 로깅 도구를 사용하여 Azure 웹 앱 문제를 해결하는 방법에 대해 알아봅니다."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: 
ms.assetid: def8e481-7803-4371-aa55-64025d116c97
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: abfd9a4c1b346377d7f1fc30455a1487b113537d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-a-web-app-in-azure-app-service-using-visual-studio"></a><span data-ttu-id="553b5-103">Visual Studio를 사용하여 Azure 앱 서비스에서 웹 앱 문제 해결</span><span class="sxs-lookup"><span data-stu-id="553b5-103">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="553b5-104">개요</span><span class="sxs-lookup"><span data-stu-id="553b5-104">Overview</span></span>
<span data-ttu-id="553b5-105">이 자습서에서는 원격으로 [디버그 모드](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx)를 실행하거나 응용 프로그램 로그 및 웹 서버 로그를 확인하여 [App Service](http://go.microsoft.com/fwlink/?LinkId=529714)에서 웹앱을 디버그할 수 있는 Visual Studio 도구를 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-105">This tutorial shows how to use Visual Studio tools that help debug a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), by running in [debug mode](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) remotely or by viewing application logs and web server logs.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="553b5-106">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-106">You'll learn:</span></span>

* <span data-ttu-id="553b5-107">Visual Studio에서 사용할 수 있는 Azure 웹 앱 관리 기능</span><span class="sxs-lookup"><span data-stu-id="553b5-107">Which Azure web app management functions are available in Visual Studio.</span></span>
* <span data-ttu-id="553b5-108">Visual Studio 원격 뷰를 사용하여 원격 웹 앱에서 빠르게 변경하는 방법</span><span class="sxs-lookup"><span data-stu-id="553b5-108">How to use Visual Studio remote view to make quick changes in a remote web app.</span></span>
* <span data-ttu-id="553b5-109">웹 응용 및 WebJob에 대한 프로젝트를 Azure에서 실행하는 동안 원격으로 디버그 모드를 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="553b5-109">How to run debug mode remotely while a project is running in Azure, both for a web app and for a WebJob.</span></span>
* <span data-ttu-id="553b5-110">응용 프로그램 추적 로그를 만드는 방법 및 해당 로그가 생성될 때 이를 보는 방법</span><span class="sxs-lookup"><span data-stu-id="553b5-110">How to create application trace logs and view them while the application is creating them.</span></span>
* <span data-ttu-id="553b5-111">자세한 오류 메시지 및 실패한 요청 추적을 포함하여 웹 서버 로그를 보는 방법</span><span class="sxs-lookup"><span data-stu-id="553b5-111">How to view web server logs, including detailed error messages and failed request tracing.</span></span>
* <span data-ttu-id="553b5-112">진단 로그를 Azure 저장소 계정으로 보내고 해당 위치에서 로그를 보는 방법</span><span class="sxs-lookup"><span data-stu-id="553b5-112">How to send diagnostic logs to an Azure Storage account and view them there.</span></span>

<span data-ttu-id="553b5-113">Visual Studio Ultimate가 있으면 디버깅에 [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) 를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-113">If you have Visual Studio Ultimate, you can also use [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) for debugging.</span></span> <span data-ttu-id="553b5-114">IntelliTrace는 이 자습서에서 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-114">IntelliTrace is not covered in this tutorial.</span></span>

## <span data-ttu-id="553b5-115"><a name="prerequisites"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="553b5-115"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="553b5-116">이 자습서에서는 [Azure 및 ASP.NET 시작][GetStarted]에서 설정한 개발 환경, 웹 프로젝트 및 Azure 웹앱을 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-116">This tutorial works with the development environment, web project, and Azure web app that you set up in [Get started with Azure and ASP.NET][GetStarted].</span></span> <span data-ttu-id="553b5-117">WebJobs 섹션의 경우 [Azure WebJobs SDK 시작][GetStartedWJ]에서 만든 응용 프로그램이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-117">For the WebJobs sections, you'll need the application that you create in [Get Started with the Azure WebJobs SDK][GetStartedWJ].</span></span>

<span data-ttu-id="553b5-118">이 자습서에 제시된 코드 샘플은 C# MVC 웹 응용 프로그램용이지만 문제 해결 절차는 Visual Basic 및 Web Forms 응용 프로그램에도 동일하게 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-118">The code samples shown in this tutorial are for a C# MVC web application, but the troubleshooting procedures are the same for Visual Basic and Web Forms applications.</span></span>

<span data-ttu-id="553b5-119">이 자습서는 Visual Studio 2015 또는 2013을 사용하는 경우를 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-119">The tutorial assumes you're using Visual Studio 2015 or 2013.</span></span> <span data-ttu-id="553b5-120">Visual Studio 2013을 사용하는 경우 WebJobs 기능을 사용하려면 [업데이트 4](http://go.microsoft.com/fwlink/?LinkID=510314) 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-120">If you're using Visual Studio 2013, the WebJobs features require [Update 4](http://go.microsoft.com/fwlink/?LinkID=510314) or later.</span></span>

<span data-ttu-id="553b5-121">로그 스트리밍 기능은 .NET Framework 4 이상을 대상으로 하는 응용 프로그램에 대해서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-121">The streaming logs feature only works for applications that target .NET Framework 4 or later.</span></span>

## <span data-ttu-id="553b5-122"><a name="sitemanagement"></a>웹 앱 구성 및 관리</span><span class="sxs-lookup"><span data-stu-id="553b5-122"><a name="sitemanagement"></a>Web app configuration and management</span></span>
<span data-ttu-id="553b5-123">Visual Studio를 사용하면 [Azure 포털](http://go.microsoft.com/fwlink/?LinkId=529715)에서 사용할 수 있는 웹 앱 관리 기능 및 구성 설정의 일부에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-123">Visual Studio provides access to a subset of the web app management functions and configuration settings available in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="553b5-124">이 섹션에서는 **서버 탐색기**를 사용하여 사용할 수 있는 기능에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-124">In this section you'll see what's available by using **Server Explorer**.</span></span> <span data-ttu-id="553b5-125">최신 Azure 통합 기능을 확인하려면 **클라우드 탐색기** 도 사용해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="553b5-125">To see the latest Azure integration features, try out **Cloud Explorer** also.</span></span> <span data-ttu-id="553b5-126">**보기** 메뉴에서 두 창을 모두 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-126">You can open both windows from the **View** menu.</span></span>

1. <span data-ttu-id="553b5-127">Visual Studio에서 Azure에 아직 로그인하지 않았으면 **서버 탐색기**에서 **Azure에 연결** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-127">If you aren't already signed in to Azure in Visual Studio, click the **Connect to Azure** button in **Server Explorer**.</span></span>

    <span data-ttu-id="553b5-128">계정에 액세스할 수 있게 해 주는 또 다른 방법은 관리 인증서를 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-128">An alternative is to install a management certificate that enables access to your account.</span></span> <span data-ttu-id="553b5-129">인증서를 설치하도록 선택한 경우 **서버 탐색기**에서 **Azure** 노드를 마우스 오른쪽 단추로 클릭한 다음 상황에 맞는 메뉴에서 **구독 관리 및 필터링**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-129">If you choose to install a certificate, right-click the **Azure** node in **Server Explorer**, and then click **Manage and Filter Subscriptions** in the context menu.</span></span> <span data-ttu-id="553b5-130">**Azure 구독 관리** 대화 상자에서 **인증서** 탭을 클릭한 후 **가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-130">In the **Manage Azure Subscriptions** dialog box, click the **Certificates** tab, and then click **Import**.</span></span> <span data-ttu-id="553b5-131">지침에 따라 Azure 계정에 대한 구독 파일( *.publishsettings* 파일이라고도 함)을 다운로드하고 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-131">Follow the directions to download and then import a subscription file (also called a *.publishsettings* file) for your Azure account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="553b5-132">구독 파일을 다운로드한 경우 소스 코드 디렉터리의 외부 폴더(예: Downloads 폴더)에 구독 파일을 저장한 다음 가져오기가 완료되면 해당 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-132">If you download a subscription file, save it to a folder outside your source code directories (for example, in the Downloads folder), and then delete it once the import has completed.</span></span> <span data-ttu-id="553b5-133">악의적인 사용자가 구독 파일에 액세스할 경우 Azure 서비스를 편집, 생성 및 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-133">A malicious user who gains access to the subscription file can edit, create, and delete your Azure services.</span></span>
   >
   >

    <span data-ttu-id="553b5-134">Visual Studio에서 Azure 리소스에 연결하는 방법에 대한 자세한 내용은 [계정, 구독 및 관리 역할 관리](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="553b5-134">For more information about connecting to Azure resources from Visual Studio, see [Manage Accounts, Subscriptions, and Administrative Roles](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert).</span></span>
2. <span data-ttu-id="553b5-135">**서버 탐색기**에서 **Azure**를 확장한 후 **App Service**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-135">In **Server Explorer**, expand **Azure** and expand **App Service**.</span></span>
3. <span data-ttu-id="553b5-136">[Azure 및 ASP.NET 시작][GetStarted]에서 만든 웹앱을 리소스 그룹을 확장한 후 웹앱 노드를 마우스 오른쪽 단추로 클릭하고 **설정 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-136">Expand the resource group that includes the web app that you created in [Getting started with Azure and ASP.NET][GetStarted], and then right-click the web app node and click **View Settings**.</span></span>

    ![서버 탐색기에서 설정 보기](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewsettings.png)

    <span data-ttu-id="553b5-138">**Azure 웹 앱** 탭이 나타나면 이 탭에서 Visual Studio에서 사용할 수 있는 웹 앱 관리 및 구성 작업이 무엇인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-138">The **Azure Web App** tab appears, and you can see there the web app management and configuration tasks that are available in Visual Studio.</span></span>

    ![Azure 웹 앱 창](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configtab.png)

    <span data-ttu-id="553b5-140">이 자습서에서는 로깅 및 추적 드롭다운을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-140">In this tutorial you'll be using the logging and tracing drop-downs.</span></span> <span data-ttu-id="553b5-141">원격 디버깅도 사용하지만 이를 사용하도록 설정하는 방법은 다른 방법을 사용하게 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-141">You'll also use remote debugging but you'll use a different method to enable it.</span></span>

    <span data-ttu-id="553b5-142">이 창에 있는 응용 프로그램 설정 및 연결 문자열 상자에 대한 자세한 내용은 [Azure 웹 앱: 응용 프로그램 문자열 및 연결 문자열 작동 방식](http://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="553b5-142">For information about the App Settings and Connection Strings boxes in this window, see [Azure Web Apps: How Application Strings and Connection Strings Work](http://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).</span></span>

    <span data-ttu-id="553b5-143">이 창에서 지원하지 않는 웹앱 관리 작업을 수행하려는 경우 **관리 포털에서 열기** 를 클릭하여 브라우저 창에서 Azure 포털을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-143">If you want to perform a web app management task that can't be done in this window, click **Open in Management Portal** to open a browser window to the Azure portal.</span></span>

## <span data-ttu-id="553b5-144"><a name="remoteview"></a>서버 탐색기에서 웹 앱 파일 액세스</span><span class="sxs-lookup"><span data-stu-id="553b5-144"><a name="remoteview"></a>Access web app files in Server Explorer</span></span>
<span data-ttu-id="553b5-145">일반적으로 Web.config 파일에서 `customErrors` 플래그를 `On` 또는 `RemoteOnly`로 설정한 상태로 웹 프로젝트가 배포되기 때문에 문제가 발생한 경우 유용한 오류 메시지를 받지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-145">You typically deploy a web project with the `customErrors` flag in the Web.config file set to `On` or `RemoteOnly`, which means you don't get a helpful error message when something goes wrong.</span></span> <span data-ttu-id="553b5-146">받을 수 있는 대부분의 오류는 모두 다음 중 하나와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-146">For many errors all you get is a page like one of the following ones.</span></span>

<span data-ttu-id="553b5-147">**'/' 응용 프로그램의 서버 오류:**</span><span class="sxs-lookup"><span data-stu-id="553b5-147">**Server Error in '/' Application:**</span></span>

![도움이 되지 않는 오류 메시지](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror.png)

<span data-ttu-id="553b5-149">**오류가 발생했습니다.**</span><span class="sxs-lookup"><span data-stu-id="553b5-149">**An error occurred:**</span></span>

![도움이 되지 않는 오류 메시지](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror1.png)

<span data-ttu-id="553b5-151">**웹 사이트에서 페이지를 표시할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="553b5-151">**The website cannot display the page**</span></span>

![도움이 되지 않는 오류 메시지](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror2.png)

<span data-ttu-id="553b5-153">오류의 원인을 찾는 가장 쉬운 방법은 주로 자세한 오류 메시지를 사용하도록 설정하는 것입니다. 이전 스크린샷 중 첫 번째 스크린샷에 그 방법이 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-153">Frequently the easiest way to find the cause of the error is to enable detailed error messages, which the first of the preceding screenshots explains how to do.</span></span> <span data-ttu-id="553b5-154">배포된 Web.config 파일의 변경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-154">That requires a change in the deployed Web.config file.</span></span> <span data-ttu-id="553b5-155">프로젝트에서 *Web.config* 파일을 편집한 후 프로젝트를 다시 배포하거나 [Web.config 변환](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations)을 만들고 디버그 빌드를 배포할 수도 있지만 더 빠른 방법이 있습니다. **솔루션 탐색기**에서 *원격 보기* 기능을 사용하면 원격 웹앱의 파일을 직접 보고 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-155">You could edit the *Web.config* file in the project and redeploy the project, or create a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) and deploy a debug build, but there's a quicker way: in **Solution Explorer** you can directly view and edit files in the remote web app by using the *remote view* feature.</span></span>

1. <span data-ttu-id="553b5-156">**서버 탐색기**에서 **Azure**, **App Service**, 웹앱이 있는 리소스 그룹, 웹앱의 노드를 차례로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-156">In **Server Explorer**, expand **Azure**, expand **App Service**, expand the resource group that your web app is located in, and then expand the node for your web app.</span></span>

    <span data-ttu-id="553b5-157">표시되는 노드를 통해 웹 앱의 콘텐츠 파일 및 로그 파일에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-157">You see nodes that give you access to the web app's content files and log files.</span></span>
2. <span data-ttu-id="553b5-158">**파일** 노드를 확장하고 *Web.config* 파일을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-158">Expand the **Files** node, and double-click the *Web.config* file.</span></span>

    ![Web.config 열기](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfig.png)

    <span data-ttu-id="553b5-160">원격 웹앱의 Visual Studio에서 Web.config 파일이 열리고 제목 표시줄의 파일 이름 옆에 [원격]이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-160">Visual Studio opens the Web.config file from the remote web app and shows [Remote] next to the file name in the title bar.</span></span>
3. <span data-ttu-id="553b5-161">`system.web` 요소에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-161">Add the following line to the `system.web` element:</span></span>

    `<customErrors mode="Off"></customErrors>`

    ![Web.config 편집](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfigedit.png)
4. <span data-ttu-id="553b5-163">도움이 되지 않는 오류 메시지가 표시된 브라우저를 새로 고칩니다. 이제 다음 예와 같이 자세한 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-163">Refresh the browser that is showing the unhelpful error message, and now you get a detailed error message, such as the following example:</span></span>

    ![자세한 오류 메시지](./media/web-sites-dotnet-troubleshoot-visual-studio/detailederror.png)

    <span data-ttu-id="553b5-165">(표시된 오류는 빨간색으로 표시된 줄이 *Views\Home\Index.cshtml*에 추가되어 생성됨)</span><span class="sxs-lookup"><span data-stu-id="553b5-165">(The error shown was created by adding the line shown in red to *Views\Home\Index.cshtml*.)</span></span>

<span data-ttu-id="553b5-166">Web.config 파일을 편집하는 방법은 문제를 더 쉽게 해결할 수 있도록 Azure 웹 앱의 파일 읽기/편집 기능을 사용하는 한 가지 예에 지나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-166">Editing the Web.config file is only one example of scenarios in which the ability to read and edit files on your Azure web app make troubleshooting easier.</span></span>

## <span data-ttu-id="553b5-167"><a name="remotedebug"></a>원격 디버깅 웹 앱</span><span class="sxs-lookup"><span data-stu-id="553b5-167"><a name="remotedebug"></a>Remote debugging web apps</span></span>
<span data-ttu-id="553b5-168">자세한 오류 메시지에 충분한 정보가 제공되지 않은 경우 로컬로 오류를 다시 만들 수는 없습니다. 이때 문제를 해결하는 또 다른 방법은 원격으로 디버그 모드에서 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-168">If the detailed error message doesn't provide enough information, and you can't re-create the error locally, another way to troubleshoot is to run in debug mode remotely.</span></span> <span data-ttu-id="553b5-169">중단점을 설정하고 메모리를 직접 조작하며 코드를 단계별로 실행하고 심지어 코드 경로를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-169">You can set breakpoints, manipulate memory directly, step through code, and even change the code path.</span></span>

<span data-ttu-id="553b5-170">원격 디버깅은 Visual Studio의 Express Edition에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-170">Remote debugging does not work in Express editions of Visual Studio.</span></span>

<span data-ttu-id="553b5-171">이 섹션에서는 [Azure 및 ASP.NET 시작][GetStarted]에서 만든 프로젝트를 사용하여 원격으로 디버그하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-171">This section shows how to debug remotely using the project you create in [Getting started with Azure and ASP.NET][GetStarted].</span></span>

1. <span data-ttu-id="553b5-172">[Azure 및 ASP.NET 시작][GetStarted]에서 만든 웹 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-172">Open the web project that you created in [Getting started with Azure and ASP.NET][GetStarted].</span></span>
2. <span data-ttu-id="553b5-173">*Controllers\HomeController.cs*를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-173">Open *Controllers\HomeController.cs*.</span></span>
3. <span data-ttu-id="553b5-174">`About()` 메서드를 삭제하고 그 자리에 다음 코드를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-174">Delete the `About()` method and insert the following code in its place.</span></span>

        public ActionResult About()
        {
            string currentTime = DateTime.Now.ToLongTimeString();
            ViewBag.Message = "The current time is " + currentTime;
            return View();
        }
4. <span data-ttu-id="553b5-175">`ViewBag.Message` 줄에 [중단점을 설정](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-175">[Set a breakpoint](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) on the `ViewBag.Message` line.</span></span>
5. <span data-ttu-id="553b5-176">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-176">In **Solution Explorer**, right-click the project, and click **Publish**.</span></span>
6. <span data-ttu-id="553b5-177">[Azure 및 ASP.NET 시작][GetStarted]에서 사용한 프로필과 동일한 프로필을 **프로필** 드롭다운 목록에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-177">In the **Profile** drop-down list, select the same profile that you used in [Getting started with Azure and ASP.NET][GetStarted].</span></span>
7. <span data-ttu-id="553b5-178">**설정** 탭을 클릭하고 **구성**을 **디버그**로 변경한 후 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-178">Click the **Settings** tab, and change **Configuration** to **Debug**, and then click **Publish**.</span></span>

    ![디버그 모드에서 게시](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-publishdebug.png)
8. <span data-ttu-id="553b5-180">배포를 마치고 브라우저에 웹 앱의 Azure URL이 열리면 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-180">After deployment finishes and your browser opens to the Azure URL of your web app, close the browser.</span></span>
9. <span data-ttu-id="553b5-181">**서버 탐색기**에서 웹앱을 마우스 오른쪽 단추로 클릭한 다음 **디버거 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-181">In **Server Explorer**, right-click your web app, and then click **Attach Debugger**.</span></span>

    ![디버거 연결](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-attachdebugger.png)

    <span data-ttu-id="553b5-183">브라우저에 Azure에서 실행되는 홈 페이지가 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-183">The browser automatically opens to your home page running in Azure.</span></span> <span data-ttu-id="553b5-184">Azure에서 디버깅용 서버를 설정할 때까지 약 20초 정도 기다려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-184">You might have to wait 20 seconds or so while Azure sets up the server for debugging.</span></span> <span data-ttu-id="553b5-185">이 지연은 웹 앱에서 디버그 모드를 처음 실행하는 경우에만 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-185">This delay only happens the first time you run in debug mode on a web app.</span></span> <span data-ttu-id="553b5-186">이후 48시간 내에 디버그를 다시 시작하면 지연이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-186">Subsequent times within the next 48 hours when you start debugging again there won't be a delay.</span></span>

    <span data-ttu-id="553b5-187">**참고:** 디버거를 시작하는 데 문제가 있는 경우 **서버 탐색기** 대신 **클라우드 탐색기**를 사용해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="553b5-187">**Note:** If you have any trouble starting the debugger, try to do it by using **Cloud Explorer** instead of **Server Explorer**.</span></span>
10. <span data-ttu-id="553b5-188">메뉴에서 **정보** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-188">Click **About** in the menu.</span></span>

     <span data-ttu-id="553b5-189">Visual Studio가 중단점에서 중지되고 코드는 로컬 컴퓨터가 아닌 Azure에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-189">Visual Studio stops on the breakpoint, and the code is running in Azure, not on your local computer.</span></span>
11. <span data-ttu-id="553b5-190">`currentTime` 변수를 마우스 포인터로 가리켜 시간 값을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-190">Hover over the `currentTime` variable to see the time value.</span></span>

     ![Azure에서 실행 중인 디버그 모드의 변수 보기](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugviewinwa.png)

     <span data-ttu-id="553b5-192">보이는 시간은 Azure 서버 시간이며 이는 로컬 컴퓨터의 표준 시간대와 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-192">The time you see is the Azure server time, which may be in a different time zone than your local computer.</span></span>
12. <span data-ttu-id="553b5-193">`currentTime` 변수에 "현재 Azure에서 실행 중" 같은 새 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-193">Enter a new value for the `currentTime` variable, such as "Now running in Azure".</span></span>
13. <span data-ttu-id="553b5-194">F5 키를 눌러 계속 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-194">Press F5 to continue running.</span></span>

     <span data-ttu-id="553b5-195">Azure에서 실행되는 정보 페이지에는 currentTime 변수에 입력한 새 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-195">The About page running in Azure displays the new value that you entered into the currentTime variable.</span></span>

     ![새 값이 표시된 정보 페이지](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugchangeinwa.png)

## <span data-ttu-id="553b5-197"><a name="remotedebugwj"></a> 원격 디버깅 WebJob</span><span class="sxs-lookup"><span data-stu-id="553b5-197"><a name="remotedebugwj"></a> Remote debugging WebJobs</span></span>
<span data-ttu-id="553b5-198">이 섹션에서는 [Azure WebJob SDK 시작](websites-dotnet-webjobs-sdk.md)에서 만든 프로젝트 및 웹 앱을 사용하여 원격으로 디버그하는 방법을 보여 줍니다</span><span class="sxs-lookup"><span data-stu-id="553b5-198">This section shows how to debug remotely using the project and web app you create in [Get Started with the Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

<span data-ttu-id="553b5-199">이 섹션에 표시된 기능은 Visual Studio 2013 업데이트 4에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-199">The features shown in this section are available only in Visual Studio 2013 with Update 4 or later.</span></span>

<span data-ttu-id="553b5-200">연속 WebJobs에서 원격 디버깅만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-200">Remote debugging only works with continuous WebJobs.</span></span> <span data-ttu-id="553b5-201">예약 및 주문형 WebJobs은 디버깅을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-201">Scheduled and on-demand WebJobs don't support debugging.</span></span>

1. <span data-ttu-id="553b5-202">[Azure WebJobs SDK 시작][GetStartedWJ]에서 만든 웹 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-202">Open the web project that you created in [Get Started with the Azure WebJobs SDK][GetStartedWJ].</span></span>
2. <span data-ttu-id="553b5-203">ContosoAdsWebJob 프로젝트에서 *Functions.cs*를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-203">In the ContosoAdsWebJob project, open *Functions.cs*.</span></span>
3. <span data-ttu-id="553b5-204">`GnerateThumbnail` 메서드의 첫 번째 문에 [중단점을 설정](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-204">[Set a breakpoint](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) on the first statement in the `GnerateThumbnail` method.</span></span>

    ![중단점 설정](./media/web-sites-dotnet-troubleshoot-visual-studio/wjbreakpoint.png)
4. <span data-ttu-id="553b5-206">**솔루션 탐색기**에서 웹 프로젝트(WebJob 프로젝트가 아님)를 마우스 오른쪽 단추로 클릭하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-206">In **Solution Explorer**, right-click the web project (not the WebJob project), and click **Publish**.</span></span>
5. <span data-ttu-id="553b5-207">**프로필** 드롭다운 목록에서 [Azure WebJobs SDK 시작](websites-dotnet-webjobs-sdk.md)에서 사용한 것과 같은 프로필을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-207">In the **Profile** drop-down list, select the same profile that you used in [Get Started with the Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>
6. <span data-ttu-id="553b5-208">**설정** 탭을 클릭하고 **구성**을 **디버그**로 변경한 후 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-208">Click the **Settings** tab, and change **Configuration** to **Debug**, and then click **Publish**.</span></span>

    <span data-ttu-id="553b5-209">Visual Studio에서 웹 및 WebJob 프로젝트를 배포하며 브라우저에서 웹 앱의 Azure URL이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-209">Visual Studio deploys the web and WebJob projects, and your browser opens to the Azure URL of your web app.</span></span>
7. <span data-ttu-id="553b5-210">**서버 탐색기**에서 **Azure > App Service > 리소스 그룹 > 웹앱 > WebJobs > 연속**을 확장하고 **ContosoAdsWebJob**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-210">In **Server Explorer** expand **Azure > App Service > your resource group > your web app > WebJobs > Continuous**, and then right-click **ContosoAdsWebJob**.</span></span>
8. <span data-ttu-id="553b5-211">**디버거 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-211">Click **Attach Debugger**.</span></span>

    ![디버거 연결](./media/web-sites-dotnet-troubleshoot-visual-studio/wjattach.png)

    <span data-ttu-id="553b5-213">브라우저에 Azure에서 실행되는 홈 페이지가 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-213">The browser automatically opens to your home page running in Azure.</span></span> <span data-ttu-id="553b5-214">Azure에서 디버깅용 서버를 설정할 때까지 약 20초 정도 기다려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-214">You might have to wait 20 seconds or so while Azure sets up the server for debugging.</span></span> <span data-ttu-id="553b5-215">이 지연은 웹 앱에서 디버그 모드를 처음 실행하는 경우에만 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-215">This delay only happens the first time you run in debug mode on a web app.</span></span> <span data-ttu-id="553b5-216">48시간 이내에 수행하는 경우 다음에 디버거를 연결할 때는 지연이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-216">The next time you attach the debugger there won't be a delay, if you do it within 48 hours.</span></span>
9. <span data-ttu-id="553b5-217">Contoso Ads 홈페이지로 열리는 웹 브라우저에서 새 광고를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-217">In the web browser that is opened to the Contoso Ads home page, create a new ad.</span></span>

    <span data-ttu-id="553b5-218">광고를 만들면 큐 메시지가 생성되며, WebJob에서 메시지를 선택하여 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-218">Creating an ad causes a queue message to be created, which will be picked up by the WebJob and processed.</span></span> <span data-ttu-id="553b5-219">WebJobs SDK가 큐 메시지를 처리할 함수를 호출하면 코드가 중단점에 도달합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-219">When the WebJobs SDK calls the function to process the queue message, the code will hit your breakpoint.</span></span>
10. <span data-ttu-id="553b5-220">디버거가 중단점에서 중단되면 프로그램이 클라우드에서 실행되는 동안 변수 값을 검사하고 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-220">When the debugger breaks at your breakpoint, you can examine and change variable values while the program is running the cloud.</span></span> <span data-ttu-id="553b5-221">다음 그림에서 디버거는 GenerateThumbnail 메서드로 전달된 blobInfo 개체의 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-221">In the following illustration the debugger shows the contents of the blobInfo object that was passed to the GenerateThumbnail method.</span></span>

     ![디버거에서 blobInfo 개체](./media/web-sites-dotnet-troubleshoot-visual-studio/blobinfo.png)
11. <span data-ttu-id="553b5-223">F5 키를 눌러 계속 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-223">Press F5 to continue running.</span></span>

     <span data-ttu-id="553b5-224">GenerateThumbnail 메서드가 미리 보기 만들기를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-224">The GenerateThumbnail method finishes creating the thumbnail.</span></span>
12. <span data-ttu-id="553b5-225">브라우저에서 인덱스 페이지를 새로 고치면 미리 보기가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-225">In the browser, refresh the Index page and you see the thumbnail.</span></span>
13. <span data-ttu-id="553b5-226">Visual Studio에서 디버깅을 중지하려면 SHIFT+F5를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-226">In Visual Studio, press SHIFT+F5 to stop debugging.</span></span>
14. <span data-ttu-id="553b5-227">**서버 탐색기**에서 ContosoAdsWebJob 노드를 마우스 오른쪽 단추로 클릭하고 **대시보드 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-227">In **Server Explorer**, right-click the ContosoAdsWebJob node and click **View Dashboard**.</span></span>
15. <span data-ttu-id="553b5-228">Azure 자격 증명을 사용하여 로그인한 다음 WebJob 이름을 클릭하여 WebJob 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-228">Sign in with your Azure credentials, and then click the WebJob name to go to the page for your WebJob.</span></span>

     ![ContosoAdsWebJob 클릭](./media/web-sites-dotnet-troubleshoot-visual-studio/clickcaw.png)

     <span data-ttu-id="553b5-230">대시보드에서 GenerateThumbnail 함수 대시보드가 최근에 실행되었음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-230">The Dashboard shows that the GenerateThumbnail function executed recently.</span></span>

     <span data-ttu-id="553b5-231">(다음에 **대시보드 보기**를 클릭하면 로그인할 필요가 없고 브라우저가 바로 WebJob에 대한 페이지로 이동합니다.)</span><span class="sxs-lookup"><span data-stu-id="553b5-231">(The next time you click **View Dashboard**, you don't have to sign in, and the browser goes directly to the page for your WebJob.)</span></span>
16. <span data-ttu-id="553b5-232">함수 이름을 클릭하여 함수 실행에 대한 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-232">Click the function name to see details about the function execution.</span></span>

     ![함수 정보](./media/web-sites-dotnet-troubleshoot-visual-studio/funcdetails.png)

<span data-ttu-id="553b5-234">함수에서 [로그가 작성](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)되었으면 **ToggleOutput** 을 클릭하여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-234">If your function [wrote logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs), you could click **ToggleOutput** to see them.</span></span>

## <a name="notes-about-remote-debugging"></a><span data-ttu-id="553b5-235">원격 디버깅 관련 참고 사항</span><span class="sxs-lookup"><span data-stu-id="553b5-235">Notes about remote debugging</span></span>
* <span data-ttu-id="553b5-236">프로덕션 사이트에서 디버그 모드로 실행하는 것은 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-236">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="553b5-237">프로덕션 웹 앱이 여러 서버 인스턴스로 확장되지 않은 경우 디버깅으로 인해 웹 서버에서 다른 요청에 응답할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-237">If your production web app is not scaled out to multiple server instances, debugging will prevent the web server from responding to other requests.</span></span> <span data-ttu-id="553b5-238">여러 웹 서버 인스턴스를 배포하여 이들을 디버거에 연결한 경우 디버깅은 임의 인스턴스에서 실행되므로 후속 브라우저 요청이 해당 인스턴스로 이동하도록 보장할 수 있는 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-238">If you do have multiple web server instances, when you attach to the debugger you'll get a random instance, and you have no way to ensure that subsequent browser requests will go to that instance.</span></span> <span data-ttu-id="553b5-239">또한 일반적으로는 프로덕션 사이트에 디버그 빌드를 배포하지 않는데 이는 릴리스 빌드용 컴파일러 최적화로 인해 현재 진행되는 상황이 소스 코드에 자세히 표시되는 것이 불가능하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-239">Also, you typically don't deploy a debug build to production, and compiler optimizations for release builds might make it impossible to show what is happening line by line in your source code.</span></span> <span data-ttu-id="553b5-240">프로덕션 문제를 해결하는 데는 응용 프로그램 추적 및 웹 서버 로그가 최적의 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-240">For troubleshooting production problems, your best resource is application tracing and web server logs.</span></span>
* <span data-ttu-id="553b5-241">원격 디버깅 시 중단점에서 장시간 중지하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-241">Avoid long stops at breakpoints when remote debugging.</span></span> <span data-ttu-id="553b5-242">몇 분 이상 중지된 프로세스는 Azure에서 응답하지 않는 프로세스로 간주되어 종료되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-242">Azure treats a process that is stopped for longer than a few minutes as an unresponsive process, and shuts it down.</span></span>
* <span data-ttu-id="553b5-243">디버그하는 동안 서버는 데이터를 Visual Studio로 보내며, 이로 인해 대역폭 사용 요금에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-243">While you're debugging, the server is sending data to Visual Studio, which could affect bandwidth charges.</span></span> <span data-ttu-id="553b5-244">대역폭 요금에 대한 자세한 내용은 [Azure 가격 책정](https://azure.microsoft.com/pricing/calculator/)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="553b5-244">For information about bandwidth rates, see [Azure Pricing](https://azure.microsoft.com/pricing/calculator/).</span></span>
* <span data-ttu-id="553b5-245">*Web.config* 파일에서 `compilation` 요소의 `debug` 특성이 true로 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-245">Make sure that the `debug` attribute of the `compilation` element in the *Web.config* file is set to true.</span></span> <span data-ttu-id="553b5-246">디버그 빌드 구성을 게시하면 기본적으로 true로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-246">It is set to true by default when you publish a debug build configuration.</span></span>

        <system.web>
          <compilation debug="true" targetFramework="4.5" />
          <httpRuntime targetFramework="4.5" />
        </system.web>
* <span data-ttu-id="553b5-247">디버거에서 디버그하려는 코드가 단계별로 실행되지 않는 경우 "내 코드만" 설정을 변경해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-247">If you find that the debugger won't step into code that you want to debug, you might have to change the Just My Code setting.</span></span>  <span data-ttu-id="553b5-248">자세한 내용은 [단계별 코드 실행을 내 코드만으로 제한](http://msdn.microsoft.com/library/vstudio/y740d9d3.aspx#BKMK_Restrict_stepping_to_Just_My_Code)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="553b5-248">For more information, see [Restrict stepping to Just My Code](http://msdn.microsoft.com/library/vstudio/y740d9d3.aspx#BKMK_Restrict_stepping_to_Just_My_Code).</span></span>
* <span data-ttu-id="553b5-249">원격 디버깅 기능을 사용하도록 설정하면 서버의 타이머가 시작되고 48시간 후 기능이 자동으로 꺼집니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-249">A timer starts on the server when you enable the remote debugging feature, and after 48 hours the feature is automatically turned off.</span></span> <span data-ttu-id="553b5-250">이 48시간 제한은 보안 및 성능상의 이유로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-250">This 48 hour limit is done for security and performance reasons.</span></span> <span data-ttu-id="553b5-251">원하는 횟수만큼 기능을 쉽게 다시 켤 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-251">You can easily turn the feature back on as many times as you like.</span></span> <span data-ttu-id="553b5-252">디버깅을 활발히 사용하지 않는 경우 이를 사용하지 않는 상태로 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-252">We recommend leaving it disabled when you are not actively debugging.</span></span>
* <span data-ttu-id="553b5-253">웹 앱 프로세스(w3wp.exe)뿐만 아니라 모든 프로세스에 디버거를 수동으로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-253">You can manually attach the debugger to any process, not only the web app process (w3wp.exe).</span></span> <span data-ttu-id="553b5-254">Visual Studio에서 디버그 모드를 사용하는 방법에 대한 자세한 내용은 [Visual Studio의 디버깅](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="553b5-254">For more information about how to use debug mode in Visual Studio, see [Debugging in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx).</span></span>

## <span data-ttu-id="553b5-255"><a name="logsoverview"></a>진단 로그 개요</span><span class="sxs-lookup"><span data-stu-id="553b5-255"><a name="logsoverview"></a>Diagnostic logs overview</span></span>
<span data-ttu-id="553b5-256">Azure 웹 앱에서 실행하는 ASP.NET 응용 프로그램은 다음과 같은 종류의 로그를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-256">An ASP.NET application that runs in an Azure web app can create the following kinds of logs:</span></span>

* <span data-ttu-id="553b5-257">**응용 프로그램 추적 로그**</span><span class="sxs-lookup"><span data-stu-id="553b5-257">**Application tracing logs**</span></span><br/>
  <span data-ttu-id="553b5-258">응용 프로그램은 [System.Diagnostics.Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx) 클래스의 메서드를 호출하여 추적 로그를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-258">The application creates these logs by calling methods of the [System.Diagnostics.Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx) class.</span></span>
* <span data-ttu-id="553b5-259">**웹 서버 로그**</span><span class="sxs-lookup"><span data-stu-id="553b5-259">**Web server logs**</span></span><br/>
  <span data-ttu-id="553b5-260">웹 서버는 웹 앱에 대한 모든 HTTP 요청에 대해 로그 항목을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-260">The web server creates a log entry for every HTTP request to the web app.</span></span>
* <span data-ttu-id="553b5-261">**자세한 오류 메시지 로그**</span><span class="sxs-lookup"><span data-stu-id="553b5-261">**Detailed error message logs**</span></span><br/>
  <span data-ttu-id="553b5-262">웹 서버는 실패한 HTTP 요청(상태 코드 400 이상으로 인해 발생한 오류)에 대해 일부 추가 정보가 수록된 HTML 페이지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-262">The web server creates an HTML page with some additional information for failed HTTP requests (those that result in status code 400 or greater).</span></span>
* <span data-ttu-id="553b5-263">**실패한 요청 추적 로그**</span><span class="sxs-lookup"><span data-stu-id="553b5-263">**Failed request tracing logs**</span></span><br/>
  <span data-ttu-id="553b5-264">웹 서버는 실패한 HTTP 요청에 대한 자세한 추적 정보가 수록된 XML 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-264">The web server creates an XML file with detailed tracing information for failed HTTP requests.</span></span> <span data-ttu-id="553b5-265">또한 웹 서버는 브라우저에서 XML 파일 형식으로 지정할 수 있도록 XSL 파일도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-265">The web server also provides an XSL file to format the XML in a browser.</span></span>

<span data-ttu-id="553b5-266">로깅 기능을 사용하면 웹 앱 성능에 영향을 미칠 수 있으므로 Azure에서는 필요에 따라 각 로그 유형을 사용 또는 사용하지 않도록 설정할 수 있는 기능이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-266">Logging affects web app performance, so Azure gives you the ability to enable or disable each type of log as needed.</span></span> <span data-ttu-id="553b5-267">응용 프로그램 로그의 경우 특정 심각도 수준 이상의 로그만 작성되도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-267">For application logs, you can specify that only logs above a certain severity level should be written.</span></span> <span data-ttu-id="553b5-268">새 웹 앱을 만들 때 기본적으로 모든 로깅은 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-268">When you create a new web app, by default all logging is disabled.</span></span>

<span data-ttu-id="553b5-269">로그는 웹 앱의 파일 시스템에 있는 *LogFiles* 폴더의 파일에 기록되며 FTP를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-269">Logs are written to files in a *LogFiles* folder in the file system of your web app and are accessible via FTP.</span></span> <span data-ttu-id="553b5-270">웹 서버 로그 및 응용 프로그램 로그는 또한 Azure 저장소 계정에도 기록될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-270">Web server logs and application logs can also be written to an Azure Storage account.</span></span> <span data-ttu-id="553b5-271">저장소 계정에서는 파일 시스템에서 보존할 수 있는 로그보다 훨씬 많은 볼륨의 로그를 보존할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-271">You can retain a greater volume of logs in a storage account than is possible in the file system.</span></span> <span data-ttu-id="553b5-272">파일 시스템을 사용하는 경우 최대 100MB의 로그로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-272">You're limited to a maximum of 100 megabytes of logs when you use the file system.</span></span> <span data-ttu-id="553b5-273">참고로, 파일 시스템 로그는 단기 보존용입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-273">(File system logs are only for short-term retention.</span></span> <span data-ttu-id="553b5-274">제한값에 도달한 경우 Azure는 새 로그를 위한 공간을 만들기 위해 오래된 로그 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-274">Azure deletes old log files to make room for new ones after the limit is reached.)</span></span>  

## <span data-ttu-id="553b5-275"><a name="apptracelogs"></a>응용 프로그램 추적 로그 만들기 및 보기</span><span class="sxs-lookup"><span data-stu-id="553b5-275"><a name="apptracelogs"></a>Create and view application trace logs</span></span>
<span data-ttu-id="553b5-276">이 섹션에서는 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-276">In this section you'll do the following tasks:</span></span>

* <span data-ttu-id="553b5-277">[Azure 및 ASP.NET 시작][GetStarted]에서 만든 웹 프로젝트에 추적 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-277">Add tracing statements to the web project that you created in [Get started with Azure and ASP.NET][GetStarted].</span></span>
* <span data-ttu-id="553b5-278">프로젝트를 로컬로 실행하는 경우 로그 보기</span><span class="sxs-lookup"><span data-stu-id="553b5-278">View the logs when you run the project locally.</span></span>
* <span data-ttu-id="553b5-279">Azure에서 실행하는 응용 프로그램에서 생성된 로그 보기</span><span class="sxs-lookup"><span data-stu-id="553b5-279">View the logs as they are generated by the application running in Azure.</span></span>

<span data-ttu-id="553b5-280">WebJob에서 응용 프로그램을 만드는 방법에 대한 자세한 내용은 [WebJobs SDK를 사용하여 Azure 큐 저장소 작업을 하는 방법 - 로그를 쓰는 방법](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="553b5-280">For information about how to create application logs in WebJobs, see [How to work with Azure queue storage using the WebJobs SDK - How to write logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs).</span></span> <span data-ttu-id="553b5-281">로그를 보고 Azure에 저장하는 방법을 제어하기 위한 다음 지침은 WebJob에서 만들어진 응용 프로그램 로그에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-281">The following instructions for viewing logs and controlling how they're stored in Azure apply also to application logs created by WebJobs.</span></span>

### <a name="add-tracing-statements-to-the-application"></a><span data-ttu-id="553b5-282">응용 프로그램에 추적 문 추가</span><span class="sxs-lookup"><span data-stu-id="553b5-282">Add tracing statements to the application</span></span>
1. <span data-ttu-id="553b5-283">*Controllers\HomeController.cs*를 열고 `Index`, `About`, `Contact` 메서드를 다음 코드로 바꾸어 `System.Diagnostics`에 대해 `Trace` 문과 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-283">Open *Controllers\HomeController.cs*, and replace the `Index`, `About`, and `Contact` methods with the following code in order to add `Trace` statements and a `using` statement for `System.Diagnostics`:</span></span>

        public ActionResult Index()
        {
            Trace.WriteLine("Entering Index method");
            ViewBag.Message = "Modify this template to jump-start your ASP.NET MVC application.";
            Trace.TraceInformation("Displaying the Index page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Index method");
            return View();
        }

        public ActionResult About()
        {
            Trace.WriteLine("Entering About method");
            ViewBag.Message = "Your app description page.";
            Trace.TraceWarning("Transient error on the About page at " + DateTime.Now.ToShortTimeString());
            Trace.WriteLine("Leaving About method");
            return View();
        }

        public ActionResult Contact()
        {
            Trace.WriteLine("Entering Contact method");
            ViewBag.Message = "Your contact page.";
            Trace.TraceError("Fatal error on the Contact page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Contact method");
            return View();
        }        
2. <span data-ttu-id="553b5-284">파일 맨 위에 `using System.Diagnostics;` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-284">Add a `using System.Diagnostics;` statement to the top of the file.</span></span>

### <a name="view-the-tracing-output-locally"></a><span data-ttu-id="553b5-285">로컬에서 추적 출력 보기</span><span class="sxs-lookup"><span data-stu-id="553b5-285">View the tracing output locally</span></span>
1. <span data-ttu-id="553b5-286">F5 키를 눌러 디버그 모드에서 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-286">Press F5 to run the application in debug mode.</span></span>

    <span data-ttu-id="553b5-287">기본 추적 수신기는 모든 추적 출력을 다른 디버그 출력과 함께 **출력** 창에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-287">The default trace listener writes all trace output to the **Output** window, along with other Debug output.</span></span> <span data-ttu-id="553b5-288">다음 그림에서는 `Index` 메서드에 추가한 trace 문의 출력을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-288">The following illustration shows the output from the trace statements that you added to the `Index` method.</span></span>

    ![디버그 창의 추적](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugtracing.png)

    <span data-ttu-id="553b5-290">다음 단계는 디버그 모드에서 컴파일하지 않고 웹 페이지에서 추적 출력을 보는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-290">The following steps show how to view trace output in a web page, without compiling in debug mode.</span></span>
2. <span data-ttu-id="553b5-291">프로젝트 폴더에 위치한 응용 프로그램 Web.config 파일을 열고 파일 끝에 있는 닫는 `<system.diagnostics>` 요소 바로 앞에 `</configuration>` 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-291">Open the application Web.config file (the one located in the project folder) and add a `<system.diagnostics>` element at the end of the file just before the closing `</configuration>` element:</span></span>

          <system.diagnostics>
            <trace>
              <listeners>
                <add name="WebPageTraceListener"
                    type="System.Web.WebPageTraceListener,
                    System.Web,
                    Version=4.0.0.0,
                    Culture=neutral,
                    PublicKeyToken=b03f5f7f11d50a3a" />
              </listeners>
            </trace>
          </system.diagnostics>

    <span data-ttu-id="553b5-292">`WebPageTraceListener`를 사용하면 `/trace.axd`로 이동하여 추적 출력을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-292">The `WebPageTraceListener` lets you view trace output by browsing to `/trace.axd`.</span></span>
3. <span data-ttu-id="553b5-293">Web.config 파일의 `<system.web>` 아래에 <a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">trace 요소</a>를 다음 예와 같이 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-293">Add a <a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">trace element</a> under `<system.web>` in the Web.config file, such as the following example:</span></span>

        <trace enabled="true" writeToDiagnosticsTrace="true" mostRecent="true" pageOutput="false" />
4. <span data-ttu-id="553b5-294">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-294">Press CTRL+F5 to run the application.</span></span>
5. <span data-ttu-id="553b5-295">브라우저 창의 주소 표시줄에서 *trace.axd*를 URL에 추가한 후 Enter 키를 누릅니다. URL은 http://localhost:53370/trace.axd와 유사해집니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-295">In the address bar of the browser window, add *trace.axd* to the URL, and then press Enter (the URL will be similar to http://localhost:53370/trace.axd).</span></span>
6. <span data-ttu-id="553b5-296">**응용 프로그램 추적** 페이지에서 BrowserLink 줄이 아니라 첫 번째 줄의 **세부 정보 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-296">On the **Application Trace** page, click **View Details** on the first line (not the BrowserLink line).</span></span>

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd1.png)

    <span data-ttu-id="553b5-298">**요청 세부 정보** 페이지가 나타나며, **추적 정보** 섹션에서 `Index` 메서드에 추가한 trace 문의 출력을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-298">The **Request Details** page appears, and in the **Trace Information** section you see the output from the trace statements that you added to the `Index` method.</span></span>

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd2.png)

    <span data-ttu-id="553b5-300">기본적으로 `trace.axd` 는 로컬에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-300">By default, `trace.axd` is only available locally.</span></span> <span data-ttu-id="553b5-301">원격 웹앱에서 사용할 수 있도록 하려면, 다음 예에 표시된 것처럼 *Web.config* 파일의 `trace` 요소에 `localOnly="false"`를 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-301">If you wanted to make it available from a remote web app, you could add `localOnly="false"` to the `trace` element in the *Web.config* file, as shown in the following example:</span></span>

        <trace enabled="true" writeToDiagnosticsTrace="true" localOnly="false" mostRecent="true" pageOutput="false" />

    <span data-ttu-id="553b5-302">하지만 보안상의 이유로 프로덕션 웹 앱에서 `trace.axd`를 사용하도록 설정하는 것은 일반적으로 권장되지 않습니다. 다음 섹션에서는 Azure 웹 앱의 추적 로그를 더 쉽게 읽을 수 있는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-302">However, enabling `trace.axd` in a production web app is generally not recommended for security reasons, and in the following sections you'll see an easier way to read tracing logs in an Azure web app.</span></span>

### <a name="view-the-tracing-output-in-azure"></a><span data-ttu-id="553b5-303">Azure에서 추적 출력 보기</span><span class="sxs-lookup"><span data-stu-id="553b5-303">View the tracing output in Azure</span></span>
1. <span data-ttu-id="553b5-304">**솔루션 탐색기**에서 웹 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-304">In **Solution Explorer**, right-click the web project and click **Publish**.</span></span>
2. <span data-ttu-id="553b5-305">**웹 게시** 대화 상자에서 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-305">In the **Publish Web** dialog box, click **Publish**.</span></span>

    <span data-ttu-id="553b5-306">Visual Studio에서 업데이트가 게시된 후 **연결** 탭의 **대상 URL**의 확인란을 선택 취소하지 않은 경우 브라우저 창이 열리고 사용자의 홈 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-306">After Visual Studio publishes your update, it opens a browser window to your home page (assuming you didn't clear **Destination URL** on the **Connection** tab).</span></span>
3. <span data-ttu-id="553b5-307">**서버 탐색기**에서 웹앱을 마우스 오른쪽 단추로 클릭하고 **스트리밍 로그 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-307">In **Server Explorer**, right-click your web app and select **View Streaming Logs**.</span></span>

    ![상황에 맞는 메뉴의 스트리밍 로그 보기](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewlogsmenu.png)

    <span data-ttu-id="553b5-309">**출력** 창에는 현재 로그 스트리밍 서비스에 연결되어 있음이 표시되고, 로그는 표시되지 않은 상태로 매분마다 알림 줄이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-309">The **Output** window shows that you are connected to the log-streaming service, and adds a notification line each minute that goes by without a log to display.</span></span>

    ![상황에 맞는 메뉴의 스트리밍 로그 보기](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-nologsyet.png)
4. <span data-ttu-id="553b5-311">응용 프로그램 홈 페이지가 표시된 브라우저 창에서 **연락처**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-311">In the browser window that shows your application home page, click **Contact**.</span></span>

    <span data-ttu-id="553b5-312">몇 초 이내에 `Contact` 메서드에 추가한 오류 수준의 추적에 대한 출력이 **출력** 창에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-312">Within a few seconds the output from the error-level trace you added to the `Contact` method appears in the **Output** window.</span></span>

    ![출력 창의 오류 추적](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-errortrace.png)

    <span data-ttu-id="553b5-314">로그 모니터링 서비스를 사용하도록 설정하는 경우 오류 수준의 추적이 기본 설정이므로 Visual Studio에는 오류 수준의 추적만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-314">Visual Studio is only showing error-level traces because that is the default setting when you enable the log monitoring service.</span></span> <span data-ttu-id="553b5-315">새 Azure 웹 앱을 만드는 경우 이전에 사이트 설정 페이지를 열고 확인한 것처럼 모든 로깅은 기본적으로 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-315">When you create a new Azure web app, all logging is disabled by default, as you saw when you opened the settings page earlier:</span></span>

    ![응용 프로그램 로깅 끄기](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-apploggingoff.png)

    <span data-ttu-id="553b5-317">하지만 **스트리밍 로그 보기**를 선택한 경우 Visual Studio는 자동으로 **응용 프로그램 로깅(파일 시스템)**을 **오류**로 변경합니다. 이는 오류 수준의 로그가 보고된다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-317">However, when you selected **View Streaming Logs**, Visual Studio automatically changed **Application Logging(File System)** to **Error**, which means error-level logs get reported.</span></span> <span data-ttu-id="553b5-318">추적 로그를 모두 보려면 이 설정을 **자세한 정보 표시**로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-318">In order to see all of your tracing logs, you can change this setting to **Verbose**.</span></span> <span data-ttu-id="553b5-319">심각도 수준을 오류보다 낮은 수준으로 선택하면 그보다 더 높은 심각도 수준의 모든 로그가 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-319">When you select a severity level lower than error, all logs for higher severity levels are also reported.</span></span> <span data-ttu-id="553b5-320">따라서 자세한 정보 표시를 선택하는 경우 정보, 경고 및 오류 로그도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-320">So when you select verbose, you also see information, warning, and error logs.</span></span>  

1. <span data-ttu-id="553b5-321">**서버 탐색기**에서 웹앱을 마우스 오른쪽 단추로 클릭하고 이전과 마찬가지로 **설정 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-321">In **Server Explorer**, right-click the web app, and then click **View Settings** as you did earlier.</span></span>
2. <span data-ttu-id="553b5-322">**응용 프로그램 로깅(파일 시스템)**을 **자세한 정보 표시**로 변경한 후 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-322">Change **Application Logging (File System)** to **Verbose**, and then click **Save**.</span></span>

    ![추적 수준을 자세한 정보 표시로 설정](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-applogverbose.png)
3. <span data-ttu-id="553b5-324">이제 **연락처** 페이지가 표시되는 브라우저 창에서 **홈**을 클릭하고 **정보**를 클릭한 후 **연락처**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-324">In the browser window that is now showing your **Contact** page, click **Home**, then click **About**, and then click **Contact**.</span></span>

    <span data-ttu-id="553b5-325">몇 초 이내에 **출력** 창에 추적 출력이 모두 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-325">Within a few seconds, the **Output** window shows all of your tracing output.</span></span>

    ![자세한 정보 표시 추적 출력](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-verbosetraces.png)

    <span data-ttu-id="553b5-327">이 섹션에서는 Azure 웹 앱 설정을 사용하여 로깅을 사용 및 사용하지 않도록 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-327">In this section you enabled and disabled logging by using Azure web app settings.</span></span> <span data-ttu-id="553b5-328">또한 Web.config 파일을 수정하여 추적 수신기를 사용 또는 사용하지 않도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-328">You can also enable and disable trace listeners by modifying the Web.config file.</span></span> <span data-ttu-id="553b5-329">하지만 Web.config 파일을 수정하면 앱 도메인이 재순환할 수 있습니다. 반면에 웹 앱 구성을 통해 로깅을 사용하도록 설정하면 재순환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-329">However, modifying the Web.config file causes the app domain to recycle, while enabling logging via the web app configuration doesn't do that.</span></span> <span data-ttu-id="553b5-330">문제를 재현하는 데 오랜 시간이 걸리는 경우 또는 문제가 일시적인 경우 앱 도메인을 재순환하면 문제가 "수정"되고 문제가 다시 발생할 때까지 강제로 대기해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-330">If the problem takes a long time to reproduce, or is intermittent, recycling the app domain might "fix" it and force you to wait until it happens again.</span></span> <span data-ttu-id="553b5-331">Azure에서 진단을 사용하도록 설정하면 이러한 상황이 발생하지 않으므로 오류 정보를 즉시 캡처하기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-331">Enabling diagnostics in Azure doesn't do this, so you can start capturing error information immediately.</span></span>

### <a name="output-window-features"></a><span data-ttu-id="553b5-332">출력 창 기능</span><span class="sxs-lookup"><span data-stu-id="553b5-332">Output window features</span></span>
<span data-ttu-id="553b5-333">**출력** 창의 **Azure 로그** 탭에는 여러 단추와 하나의 입력란이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-333">The **Azure Logs** tab of the **Output** Window has several buttons and a text box:</span></span>

![로그 탭의 단추](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-icons.png)

<span data-ttu-id="553b5-335">이들은 다음 기능을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-335">These perform the following functions:</span></span>

* <span data-ttu-id="553b5-336">**출력** 창의 내용을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-336">Clear the **Output** window.</span></span>
* <span data-ttu-id="553b5-337">자동 줄 바꿈을 사용 또는 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-337">Enable or disable word wrap.</span></span>
* <span data-ttu-id="553b5-338">로그 모니터링을 시작 또는 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-338">Start or stop monitoring logs.</span></span>
* <span data-ttu-id="553b5-339">모니터링할 로그를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-339">Specify which logs to monitor.</span></span>
* <span data-ttu-id="553b5-340">로그를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-340">Download logs.</span></span>
* <span data-ttu-id="553b5-341">검색 문자열 또는 정규식을 기반으로 로그를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-341">Filter logs based on a search string or a regular expression.</span></span>
* <span data-ttu-id="553b5-342">**출력** 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-342">Close the **Output** window.</span></span>

<span data-ttu-id="553b5-343">검색 문자열 또는 정규식을 입력하면 Visual Studio에서 클라이언트 측의 로깅 정보가 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-343">If you enter a search string or regular expression, Visual Studio filters logging information at the client.</span></span> <span data-ttu-id="553b5-344">즉, **Output** 창에 로그가 표시된 후에 조건을 입력할 수 있으며 로그를 다시 생성할 필요 없이 필터링 조건을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-344">That means you can enter the criteria after the logs are displayed in the **Output** window and you can change filtering criteria without having to regenerate the logs.</span></span>

## <span data-ttu-id="553b5-345"><a name="webserverlogs"></a>웹 서버 로그 보기</span><span class="sxs-lookup"><span data-stu-id="553b5-345"><a name="webserverlogs"></a>View web server logs</span></span>
<span data-ttu-id="553b5-346">웹 서버 로그는 웹 앱의 모든 HTTP 작업을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-346">Web server logs record all HTTP activity for the web app.</span></span> <span data-ttu-id="553b5-347">**출력** 창에서 웹 서버 로그를 보려면 웹 앱에서 이를 사용하도록 설정하고 Visual Studio에서 이들의 모니터링을 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-347">In order to see them in the **Output** window you have to enable them for the web app and tell Visual Studio that you want to monitor them.</span></span>

1. <span data-ttu-id="553b5-348">**서버 탐색기**에서 열었던 **Azure Web App 구성** 탭에서 웹 서버 로깅을 **켜기**로 변경하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-348">In the **Azure Web App Configuration** tab that you opened from **Server Explorer**, change Web Server Logging to **On**, and then click **Save**.</span></span>

    ![웹 서버 로깅 사용](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-webserverloggingon.png)
2. <span data-ttu-id="553b5-350">**출력** 창에서 **모니터링할 Azure 로그 지정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-350">In the **Output** Window, click the **Specify which Azure logs to monitor** button.</span></span>

    ![Specify which Azure logs to monitor](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-specifylogs.png)
3. <span data-ttu-id="553b5-352">**Azure 로깅 옵션** 대화 상자에서 **웹 서버 로그**를 선택한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-352">In the **Azure Logging Options** dialog box, select **Web server logs**, and then click **OK**.</span></span>

    ![웹 서버 로그 모니터링](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorwslogson.png)
4. <span data-ttu-id="553b5-354">웹앱이 표시되는 브라우저 창에서 **홈**을 클릭하고 **정보**를 클릭한 후 **연락처**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-354">In the browser window that shows the web app, click **Home**, then click **About**, and then click **Contact**.</span></span>

    <span data-ttu-id="553b5-355">일반적으로 응용 프로그램 로그가 나타나고 다음으로 웹 서버 로그가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-355">The application logs generally appear first, followed by the web server logs.</span></span> <span data-ttu-id="553b5-356">로그가 나타날 때까지 잠시 기다려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-356">You might have to wait a while for the logs to appear.</span></span>

    ![출력 창의 웹 서버 로그](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-wslogs.png)

<span data-ttu-id="553b5-358">기본적으로 Visual Studio를 사용하여 웹 서버 로그를 사용하도록 처음 설정하는 경우 Azure는 로그를 파일 시스템에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-358">By default, when you first enable web server logs by using Visual Studio, Azure writes the logs to the file system.</span></span> <span data-ttu-id="553b5-359">또는 Azure 포털을 사용하여 웹 서버 로그가 저장소 계정의 Blob 컨테이너에 기록되도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-359">As an alternative, you can use the Azure portal to specify that web server logs should be written to a blob container in a storage account.</span></span>

<span data-ttu-id="553b5-360">포털을 사용하여 Azure 저장소 계정에 기록하도록 웹 서버 로깅을 설정한 후 Visual Studio에서 로깅을 사용하지 않도록 설정하는 경우 Visual Studio에서 로깅을 사용하도록 다시 설정하면 저장소 계정 설정이 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-360">If you use the portal to enable web server logging to an Azure storage account, and then disable logging in Visual Studio, when you re-enable logging in Visual Studio your storage account settings are restored.</span></span>

## <span data-ttu-id="553b5-361"><a name="detailederrorlogs"></a>자세한 오류 메시지 로그 보기</span><span class="sxs-lookup"><span data-stu-id="553b5-361"><a name="detailederrorlogs"></a>View detailed error message logs</span></span>
<span data-ttu-id="553b5-362">자세한 오류 로그에서는 오류 응답 코드(400 이상)를 유발한 HTTP 요청과 관련된 일부 추가 정보가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-362">Detailed error logs provide some additional information about HTTP requests that result in error response codes (400 or above).</span></span> <span data-ttu-id="553b5-363">**출력** 창에서 웹 서버 로그를 보려면 웹 앱에서 이를 사용하도록 설정하고, Visual Studio에서 이들의 모니터링을 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-363">In order to see them in the **Output** window, you have to enable them for the web app and tell Visual Studio that you want to monitor them.</span></span>

1. <span data-ttu-id="553b5-364">**서버 탐색기**에서 열었던 **Azure Web App 구성** 탭에서 **자세한 오류 메시지**를 **켜기**로 변경하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-364">In the **Azure Web App Configuration** tab that you opened from **Server Explorer**, change **Detailed Error Messages** to **On**, and then click **Save**.</span></span>

    ![자세한 오류 메시지 사용](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailedlogson.png)
2. <span data-ttu-id="553b5-366">**출력** 창에서 **모니터링할 Azure 로그 지정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-366">In the **Output** Window, click the **Specify which Azure logs to monitor** button.</span></span>
3. <span data-ttu-id="553b5-367">**Azure 로깅 옵션** 대화 상자에서 **모든 로그**를 클릭한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-367">In the **Azure Logging Options** dialog box, click **All logs**, and then click **OK**.</span></span>

    ![모든 로그 모니터링](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorall.png)
4. <span data-ttu-id="553b5-369">404 오류를 유발하도록 브라우저 창의 주소 표시줄에서 추가 문자를 URL에 추가(예: `http://localhost:53370/Home/Contactx`)한 후 Enter를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-369">In the address bar of the browser window, add an extra character to the URL to cause a 404 error (for example, `http://localhost:53370/Home/Contactx`), and press Enter.</span></span>

    <span data-ttu-id="553b5-370">몇 초 후 Visual Studio의 **출력** 창에 자세한 오류 로그가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-370">After several seconds the detailed error log appears in the Visual Studio **Output** window.</span></span>

    ![출력 창의 자세한 오류 로그](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorlog.png)

    <span data-ttu-id="553b5-372">Ctrl 키를 누른 채 링크를 클릭하면 브라우저에 서식이 지정된 로그 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-372">Control+click the link to see the log output formatted in a browser:</span></span>

    ![브라우저 창의 자세한 오류 로그](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorloginbrowser.png)

## <span data-ttu-id="553b5-374"><a name="downloadlogs"></a>파일 시스템 로그 다운로드</span><span class="sxs-lookup"><span data-stu-id="553b5-374"><a name="downloadlogs"></a>Download file system logs</span></span>
<span data-ttu-id="553b5-375">**출력** 창에서 모니터링할 수 있는 모든 로그는 *.zip* 파일로 다운로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-375">Any logs that you can monitor in the **Output** window can also be downloaded as a *.zip* file.</span></span>

1. <span data-ttu-id="553b5-376">**출력** 창에서 **스트리밍 로그 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-376">In the **Output** window, click **Download Streaming Logs**.</span></span>

    ![로그 탭의 단추](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadicon.png)

    <span data-ttu-id="553b5-378">파일 탐색기에서 다운로드한 파일이 선택된 상태로 *Downloads* 폴더가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-378">File Explorer opens to your *Downloads* folder with the downloaded file selected.</span></span>

    ![다운로드한 파일](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadedfile.png)
2. <span data-ttu-id="553b5-380">*.zip* 파일의 압축을 풀면 다음 폴더 구조가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-380">Extract the *.zip* file, and you see the following folder structure:</span></span>

    ![다운로드한 파일](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilefolders.png)

   * <span data-ttu-id="553b5-382">응용 프로그램 추적 로그는 *LogFiles\Application* 폴더에 *.txt* 파일로 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-382">Application tracing logs are in *.txt* files in the *LogFiles\Application* folder.</span></span>
   * <span data-ttu-id="553b5-383">웹 서버 로그는 *LogFiles\http\RawLogs* 폴더에 *.log* 파일로 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-383">Web server logs are in *.log* files in the *LogFiles\http\RawLogs* folder.</span></span> <span data-ttu-id="553b5-384">[Log Parser](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659) 같은 도구를 사용하여 이들 파일을 보고 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-384">You can use a tool such as [Log Parser](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659) to view and manipulate these files.</span></span>
   * <span data-ttu-id="553b5-385">자세한 오류 메시지 로그는 *LogFiles\DetailedErrors* 폴더에 *.html* 파일로 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-385">Detailed error message logs are in *.html* files in the *LogFiles\DetailedErrors* folder.</span></span>

     <span data-ttu-id="553b5-386">참고로, *deployments* 폴더는 소스 제어 게시로 인해 생성되는 것이며 Visual Studio 게시와는 전혀 관계가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-386">(The *deployments* folder is for files created by source control publishing; it doesn't have anything related to Visual Studio publishing.</span></span> <span data-ttu-id="553b5-387">*Git* 폴더는 소스 제어 게시 및 로그 파일 스트리밍 서비스와 관련된 추적 로그용입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-387">The *Git* folder is for traces related to source control publishing and the log file streaming service.)</span></span>  

## <span data-ttu-id="553b5-388"><a name="storagelogs"></a>저장소 로그 보기</span><span class="sxs-lookup"><span data-stu-id="553b5-388"><a name="storagelogs"></a>View storage logs</span></span>
<span data-ttu-id="553b5-389">응용 프로그램 추적 로그를 Azure 저장소 계정으로 보낼 수 있고 이들 로그를 Visual Studio에서 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-389">Application tracing logs can also be sent to an Azure storage account, and you can view them in Visual Studio.</span></span> <span data-ttu-id="553b5-390">그러려면 저장소 계정을 만들고 클래식 포털에서 저장소 로그를 사용하도록 설정한 후 **Azure Web App** 창의 **로그** 탭에서 보면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-390">To do that you'll create a storage account, enable storage logs in the classic portal, and view them in the **Logs** tab of the **Azure Web App** window.</span></span>

<span data-ttu-id="553b5-391">다음 세 대상 모두 또는 일부에 로그를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-391">You can send logs to any or all of three destinations:</span></span>

* <span data-ttu-id="553b5-392">파일 시스템</span><span class="sxs-lookup"><span data-stu-id="553b5-392">The file system.</span></span>
* <span data-ttu-id="553b5-393">저장소 계정 테이블</span><span class="sxs-lookup"><span data-stu-id="553b5-393">Storage account tables.</span></span>
* <span data-ttu-id="553b5-394">저장소 계정 Blob</span><span class="sxs-lookup"><span data-stu-id="553b5-394">Storage account blobs.</span></span>

<span data-ttu-id="553b5-395">각 대상마다 서로 다른 심각도 수준을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-395">You can specify a different severity level for each destination.</span></span>

<span data-ttu-id="553b5-396">테이블을 사용하면 로그 세부 정보를 온라인으로 쉽게 볼 수 있으며 스트리밍도 지원됩니다. 테이블에서 로그를 쿼리할 수 있고 새 로그가 생성될 때 새 로그를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-396">Tables make it easy to view details of logs online, and they support streaming; you can query logs in tables and see new logs as they are being created.</span></span> <span data-ttu-id="553b5-397">Blob을 사용하면 로그를 파일로 쉽게 다운로드할 수 있고, Blob 저장소와의 연동 방식이 인식되는 HDInsight를 사용하여 로그를 분석할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-397">Blobs make it easy to download logs in files and to analyze them using HDInsight, because HDInsight knows how to work with blob storage.</span></span> <span data-ttu-id="553b5-398">자세한 내용은 [데이터 저장소 옵션(Azure에서 실제 클라우드 앱 빌드)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options)에서 **Hadoop 및 MapReduce**를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="553b5-398">For more information, see **Hadoop and MapReduce** in [Data Storage Options (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options).</span></span>

<span data-ttu-id="553b5-399">현재 파일 시스템 로그가 자세한 정보 표시 수준으로 설정되어 있습니다. 다음 단계에서는 정보 수준의 로그가 저장소 계정 테이블로 전송되도록 설정하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-399">You currently have file system logs set to verbose level; the following steps walk you through setting up information level logs to go to storage account tables.</span></span> <span data-ttu-id="553b5-400">정보 수준이란 `Trace.WriteLine`을 호출하여 생성된 로그를 제외하고 `Trace.TraceInformation`, `Trace.TraceWarning` 및 `Trace.TraceError`를 호출하여 생성된 모든 로그가 표시됨을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-400">Information level means all logs created by calling `Trace.TraceInformation`, `Trace.TraceWarning`, and `Trace.TraceError` will be displayed, but not logs created by calling `Trace.WriteLine`.</span></span>

<span data-ttu-id="553b5-401">저장소 계정은 파일 시스템에 비해 더 많은 저장 공간을 제공하고 더 오랫동안 로그를 보존합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-401">Storage accounts offer more storage and longer-lasting retention for logs compared to the file system.</span></span> <span data-ttu-id="553b5-402">응용 프로그램 추적 로그를 저장소로 보내는 또 다른 이점은 파일 시스템 로그에서 얻을 수 없는 각 로그별 일부 추가 정보를 얻을 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-402">Another advantage of sending application tracing logs to storage is that you get some additional information with each log that you don't get from file system logs.</span></span>

1. <span data-ttu-id="553b5-403">Azure 노드 아래에서 **저장소**를 마우스 오른쪽 단추로 클릭하고 **저장소 계정 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-403">Right-click **Storage** under the Azure node, and then click **Create Storage Account**.</span></span>

![저장소 계정 만들기](./media/web-sites-dotnet-troubleshoot-visual-studio/createstor.png)

1. <span data-ttu-id="553b5-405">**저장소 계정 만들기** 대화 상자에서 저장소 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-405">In the **Create Storage Account** dialog, enter a name for the storage account.</span></span>

    <span data-ttu-id="553b5-406">이 이름은 고유해야 합니다(다른 Azure 저장소 계정이 동일한 이름을 사용할 수 없음).</span><span class="sxs-lookup"><span data-stu-id="553b5-406">The name must be must be unique (no other Azure storage account can have the same name).</span></span> <span data-ttu-id="553b5-407">입력한 이름이 이미 사용 중이면 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-407">If the name you enter is already in use you'll get a chance to change it.</span></span>

    <span data-ttu-id="553b5-408">저장소 계정에 액세스하기 위한 URL은 *{name}*.core.windows.net입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-408">The URL to access your storage account will be *{name}*.core.windows.net.</span></span>
2. <span data-ttu-id="553b5-409">**지역 또는 선호도 그룹** 드롭다운 목록을 가장 가까운 지역으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-409">Set the **Region or Affinity Group** drop-down list to the region closest to you.</span></span>

    <span data-ttu-id="553b5-410">이 설정은 저장소 계정을 호스트할 Azure 데이터 센터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-410">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="553b5-411">이 자습서의 경우 어떤 항목을 선택해도 두드러진 차이를 느낄 수 없지만 프로덕션 웹 앱의 경우에는 대기 시간과 데이터 발신 요금을 최소화하기 위해 웹 서버와 저장소 계정을 동일한 지역에 두기 원할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-411">For this tutorial your choice won't make a noticeable difference, but for a production web app you want your web server and your storage account to be in the same region to minimize latency and data egress charges.</span></span> <span data-ttu-id="553b5-412">나중에 만들게 될 웹 앱은 대기 시간을 최소화하기 위해 웹 앱에 액세스하는 브라우저에 가능한 한 가까운 지역에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-412">The web app (which you'll create later) should run in a region as close as possible to the browsers accessing your web app in order to minimize latency.</span></span>
3. <span data-ttu-id="553b5-413">**복제** 드롭다운 목록을 **로컬 중복**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-413">Set the **Replication** drop-down list to **Locally redundant**.</span></span>
   
    <span data-ttu-id="553b5-414">저장소 계정에 대해 지역에서 복제를 사용하는 경우에는 저장된 콘텐츠가 보조 위치에 복제되어 기본 위치에서 주요 재해가 발생하는 경우 보조 데이터 센터로 장애 조치(Failover)할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-414">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover to that location in case of a major disaster in the primary location.</span></span> <span data-ttu-id="553b5-415">지역에서 복제는 추가 비용을 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-415">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="553b5-416">테스트 및 개발 계정의 경우 일반적으로 지역에서 복제 비용을 지불하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-416">For test and development accounts, you generally don't want to pay for geo-replication.</span></span> <span data-ttu-id="553b5-417">자세한 내용은 [저장소 계정 만들기, 관리 또는 삭제](../storage/common/storage-create-storage-account.md)를 참조하세요</span><span class="sxs-lookup"><span data-stu-id="553b5-417">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
4. <span data-ttu-id="553b5-418">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-418">Click **Create**.</span></span>

    ![새 저장소 계정](./media/web-sites-dotnet-troubleshoot-visual-studio/newstorage.png)    
5. <span data-ttu-id="553b5-420">Visual Studio **Azure Web App** 창에서 **로그** 탭을 클릭한 다음 **관리 포털에서 로깅 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-420">In the Visual Studio **Azure Web App** window, click the **Logs** tab, and then click **Configure Logging in Management Portal**.</span></span>

    <!-- todo:screenshot of new portal if the VS page link goes to new portal -->
    ![로깅 구성](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configlogging.png)

    <span data-ttu-id="553b5-422">웹앱의 클래식 포털에서 **구성** 탭이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-422">This opens the **Configure** tab in the classic portal for your web app.</span></span>
6. <span data-ttu-id="553b5-423">클래식 포털의 **구성** 탭에서 응용 프로그램 진단 섹션까지 아래로 스크롤한 후 **응용 프로그램 로깅(Table Storage)**을 **켜기**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-423">In the classic portal's **Configure** tab, scroll down to the application diagnostics section, and then change **Application Logging (Table Storage)** to **On**.</span></span>
7. <span data-ttu-id="553b5-424">**로깅 수준**을 **정보**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-424">Change **Logging Level** to **Information**.</span></span>
8. <span data-ttu-id="553b5-425">**Manage Table Storage**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-425">Click **Manage Table Storage**.</span></span>

    ![Manage Table Storage 클릭](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-stgsettingsmgmtportal.png)

    <span data-ttu-id="553b5-427">둘 이상의 저장소 계정이 있는 경우 **Manage table storage for application diagnostics** 상자에서 사용자의 저장소 계정을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-427">In the **Manage table storage for application diagnostics** box, you can choose your storage account if you have more than one.</span></span> <span data-ttu-id="553b5-428">새 테이블을 만들거나 기존 테이블을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-428">You can create a new table or use an existing one.</span></span>

    ![Manage Table Storage](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-choosestorageacct.png)
9. <span data-ttu-id="553b5-430">**Manage table storage for application diagnostics** 상자에서 확인 표시를 클릭하여 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-430">In the **Manage table storage for application diagnostics** box click the check mark to close the box.</span></span>
10. <span data-ttu-id="553b5-431">클래식 포털의 **구성** 탭에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-431">In the classic portal's **Configure** tab, click **Save**.</span></span>
11. <span data-ttu-id="553b5-432">응용 프로그램 웹앱이 표시되는 브라우저 창에서 **홈**을 클릭하고 **정보**를 클릭한 후 **연락처**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-432">In the browser window that displays the application web app, click **Home**, then click **About**, and then click **Contact**.</span></span>

     <span data-ttu-id="553b5-433">이들 웹 페이지를 탐색하는 동안 생성된 로깅 정보가 저장소 계정에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-433">The logging information produced by browsing these web pages will be written to the storage account.</span></span>
12. <span data-ttu-id="553b5-434">Visual Studio의 **Azure Web App** 창에 있는 **로그** 탭에서 **진단 요약** 아래의 **새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-434">In the **Logs** tab of the **Azure Web App** window in Visual Studio, click **Refresh** under **Diagnostic Summary**.</span></span>

     ![새로 고침 클릭](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-refreshstorage.png)

     <span data-ttu-id="553b5-436">**Diagnostic Summary** 섹션에는 기본적으로 지난 15분간의 로그가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-436">The **Diagnostic Summary** section shows logs for the last 15 minutes by default.</span></span> <span data-ttu-id="553b5-437">더 많은 로그를 표시하도록 기간을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-437">You can change the period to see more logs.</span></span>

     <span data-ttu-id="553b5-438">참고로, "테이블을 찾을 수 없습니다" 오류가 나타나면 **응용 프로그램 로깅(저장소)**을 사용하도록 설정하고 **저장**을 클릭한 후 추적하는 페이지를 탐색했는지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="553b5-438">(If you get a "table not found" error, verify that you browsed to the pages that do the tracing after you enabled **Application Logging (Storage)** and after you clicked **Save**.)</span></span>

     ![저장소 로그](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-storagelogs.png)

     <span data-ttu-id="553b5-440">이 보기에는 파일 시스템 로그에서 얻을 수 없는 각 로그의 **프로세스 ID** 및 **스레드 ID**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-440">Notice that in this view you see **Process ID** and **Thread ID** for each log, which you don't get in the file system logs.</span></span> <span data-ttu-id="553b5-441">Azure 저장소 테이블을 직접 보면 추가 필드를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-441">You can see additional fields by viewing the Azure storage table directly.</span></span>
13. <span data-ttu-id="553b5-442">**View all application logs**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-442">Click **View all application logs**.</span></span>

     <span data-ttu-id="553b5-443">추적 로그 테이블은 Azure 저장소 테이블 뷰어에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-443">The trace log table appears in the Azure storage table viewer.</span></span>

     <span data-ttu-id="553b5-444">참고로, "시퀀스에 요소가 없습니다" 오류가 나타나면 **서버 탐색기**를 열고 **Azure** 노드 아래에서 사용자 저장소 계정의 노드를 확장한 후 **테이블**을 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-444">(If you get a "sequence contains no elements" error, open **Server Explorer**, expand the node for your storage account under the **Azure** node, and then right-click **Tables** and click **Refresh**.)</span></span>

     ![테이블 보기의 저장소 로그](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracelogtableview.png)

     <span data-ttu-id="553b5-446">이 보기에는 다른 보기에서 볼 수 없는 추가 필드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-446">This view shows additional fields you don't see in any other views.</span></span> <span data-ttu-id="553b5-447">이 보기에서는 또한 쿼리를 작성하는 특수 쿼리 작성기 UI를 사용하여 로그를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-447">This view also enables you to filter logs by using special Query Builder UI for constructing a query.</span></span> <span data-ttu-id="553b5-448">자세한 내용은 [서버 탐색기를 사용하여 저장소 리소스 탐색](http://msdn.microsoft.com/library/ff683677.aspx)(영문)에서 "테이블 리소스 사용 - 엔터티 필터링"을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="553b5-448">For more information, see Working with Table Resources - Filtering Entities in [Browsing Storage Resources with Server Explorer](http://msdn.microsoft.com/library/ff683677.aspx).</span></span>
14. <span data-ttu-id="553b5-449">단일 행에 대한 세부 정보를 확인하려면 행의 하나를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-449">To look at the details for a single row, double-click one of the rows.</span></span>

     ![서버 탐색기의 추적 테이블](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracetablerow.png)

## <span data-ttu-id="553b5-451"><a name="failedrequestlogs"></a>실패한 요청 추적 로그 보기</span><span class="sxs-lookup"><span data-stu-id="553b5-451"><a name="failedrequestlogs"></a>View failed request tracing logs</span></span>
<span data-ttu-id="553b5-452">실패한 요청 추적 로그는 URL 다시 쓰기 또는 인증 문제 등이 발생하는 경우 IIS에서 HTTP 요청이 처리되는 방식을 자세히 이해해야 하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-452">Failed request tracing logs are useful when you need to understand the details of how IIS is handling an HTTP request, in scenarios such as URL rewriting or authentication problems.</span></span>

<span data-ttu-id="553b5-453">Azure 웹 앱은 IIS 7.0 이상 버전에서 사용할 수 있는 실패한 요청 추적 기능을 똑같이 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-453">Azure web apps use the same failed request tracing functionality that has been available with IIS 7.0 and later.</span></span> <span data-ttu-id="553b5-454">하지만 기록될 오류를 구성하는 IIS 설정에 대한 액세스 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-454">You don't have access to the IIS settings that configure which errors get logged, however.</span></span> <span data-ttu-id="553b5-455">실패한 요청 추적을 사용하도록 설정하면 모든 오류가 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-455">When you enable failed request tracing, all errors are captured.</span></span>

<span data-ttu-id="553b5-456">Visual Studio를 사용하여 실패한 요청 추적을 사용하도록 설정할 수 있지만 Visual Studio에서 해당 로그를 볼 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-456">You can enable failed request tracing by using Visual Studio, but you can't view them in Visual Studio.</span></span> <span data-ttu-id="553b5-457">이러한 로그는 XML 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-457">These logs are XML files.</span></span> <span data-ttu-id="553b5-458">스트리밍 로그 서비스는 일반 텍스트 모드에서 읽을 수 있는 것으로 간주되는 파일인 *.txt*, *.html*, *.log* 파일만을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-458">The streaming log service only monitors files that are deemed readable in plain text mode:  *.txt*, *.html*, and *.log* files.</span></span>

<span data-ttu-id="553b5-459">실패한 요청 추적 로그는 FTP를 통해 브라우저에서 직접 보거나 로컬에서 FTP 도구를 사용하여 로컬 컴퓨터에 다운로드한 후 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-459">You can view failed request tracing logs in a browser directly via FTP or locally after using an FTP tool to download them to your local computer.</span></span> <span data-ttu-id="553b5-460">이 섹션에서는 브라우저에서 직접 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-460">In this section you'll view them in a browser directly.</span></span>

1. <span data-ttu-id="553b5-461">**서버 탐색기**에서 열었던 **Azure Web App** 창의 **구성** 탭에서 **실패한 요청 추적**을 **켜기**로 변경하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-461">In the **Configuration** tab of the **Azure Web App** window that you opened from **Server Explorer**, change **Failed Request Tracing** to **On**, and then click **Save**.</span></span>

    ![실패한 요청 추적 사용](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequeston.png)
2. <span data-ttu-id="553b5-463">웹 앱이 표시된 브라우저 창의 주소 표시줄에서 추가 문자를 URL에 추가하고 Enter 키를 눌러 404 오류를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-463">In the address bar of the browser window that shows the web app, add an extra character to the URL and click Enter to cause a 404 error.</span></span>

    <span data-ttu-id="553b5-464">그러면 실패한 요청 추적 로그가 만들어집니다. 다은 단계는 로그를 보거나 다운로드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-464">This causes a failed request tracing log to be created, and the following steps show how to view or download the log.</span></span>
3. <span data-ttu-id="553b5-465">Visual Studio의 **Azure Web App** 창에 있는 **구성** 탭에서 **관리 포털에서 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-465">In Visual Studio, in the **Configuration** tab of the **Azure Web App** window, click **Open in Management Portal**.</span></span>
4. <span data-ttu-id="553b5-466">웹앱의 [Azure Portal](https://portal.azure.com) **설정** 블레이드에서 **배포 자격 증명**을 클릭한 다음 새 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-466">In the [Azure Portal](https://portal.azure.com) **Settings** blade for your web app, click **Deployment credentials**, and then enter a new user name and password.</span></span>

    ![새 FTP 사용자 이름 및 암호](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-enterftpcredentials.png)

    <span data-ttu-id="553b5-468">**로그인할 때, 앞에 웹 앱 이름이 있는 상태로 전체 사용자 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-468">**When you log in, you have to use the full user name with the web app name prefixed to it.</span></span> <span data-ttu-id="553b5-469">예를 들어, 사용자 이름으로 "myid"를 입력하고 사이트가 "myexample"인 경우, "myexample\myid"로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-469">For example, if you enter "myid" as a user name and the site is "myexample", you log in as "myexample\myid".</span></span>
5. <span data-ttu-id="553b5-470">새 브라우저 창에서, 사용자 웹앱에 대한 **웹앱** 블레이드의 **FTP 호스트 이름** 또는 **FTPS 호스트 이름** 아래에 표시된 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-470">In a new browser window, go to the URL that is shown under **FTP hostname** or **FTPS hostname** in the **Web App** blade for your web app.</span></span>
6. <span data-ttu-id="553b5-471">이전에 만든 FTP 자격 증명을 사용하여 로그인합니다(사용자 이름 앞에 웹 앱 이름 포함).</span><span class="sxs-lookup"><span data-stu-id="553b5-471">Log in using the FTP credentials that you created earlier (including the web app name prefix for the user name).</span></span>

    <span data-ttu-id="553b5-472">브라우저에 웹 앱의 루트 폴더가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-472">The browser shows the root folder of the web app.</span></span>
7. <span data-ttu-id="553b5-473">*LogFiles* 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-473">Open the *LogFiles* folder.</span></span>

    ![LogFiles 폴더 열기](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilesfolder.png)
8. <span data-ttu-id="553b5-475">이름에 W3SVC와 숫자 값이 있는 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-475">Open the folder that is named W3SVC plus a numeric value.</span></span>

    ![W3SVC 폴더 열기](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfolder.png)

    <span data-ttu-id="553b5-477">폴더에는 실패한 요청 추적을 사용하도록 설정한 후에 기록된 모든 로그가 XML 파일로 포함되어 있습니다. 또한 브라우저에서 XML 형식으로 사용할 수 있는 XSL 파일도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-477">The folder contains XML files for any errors that have been logged after you enabled failed request tracing, and an XSL file that a browser can use to format the XML.</span></span>

    ![W3SVC 폴더](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfoldercontents.png)
9. <span data-ttu-id="553b5-479">추적 정보를 확인하려는 실패한 요청의 XML 파일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-479">Click the XML file for the failed request that you want to see tracing information for.</span></span>

    <span data-ttu-id="553b5-480">다음 그림에는 샘플 오류에 대한 추적 정보의 일부가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-480">The following illustration shows part of the tracing information for a sample error.</span></span>

    ![브라우저의 실패한 요청 추적](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequestinbrowser.png)

## <span data-ttu-id="553b5-482"><a name="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="553b5-482"><a name="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="553b5-483">Visual Studio를 사용하여 Azure 웹 앱에서 생성된 로그를 쉽게 보는 방법을 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-483">You've seen how Visual Studio makes it easy to view logs created by an Azure web app.</span></span> <span data-ttu-id="553b5-484">다음 섹션에서는 관련 항목에 대한 기타 리소스 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-484">The following sections provide links to more resources on related topics:</span></span>

* <span data-ttu-id="553b5-485">Azure 웹 앱 문제 해결</span><span class="sxs-lookup"><span data-stu-id="553b5-485">Azure web app troubleshooting</span></span>
* <span data-ttu-id="553b5-486">Visual Studio의 디버깅</span><span class="sxs-lookup"><span data-stu-id="553b5-486">Debugging in Visual Studio</span></span>
* <span data-ttu-id="553b5-487">Azure의 원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="553b5-487">Remote debugging in Azure</span></span>
* <span data-ttu-id="553b5-488">ASP.NET 응용 프로그램의 추적</span><span class="sxs-lookup"><span data-stu-id="553b5-488">Tracing in ASP.NET applications</span></span>
* <span data-ttu-id="553b5-489">웹 서버 로그 분석</span><span class="sxs-lookup"><span data-stu-id="553b5-489">Analyzing web server logs</span></span>
* <span data-ttu-id="553b5-490">실패한 요청 로그 분석</span><span class="sxs-lookup"><span data-stu-id="553b5-490">Analyzing failed request tracing logs</span></span>
* <span data-ttu-id="553b5-491">클라우드 서비스 디버깅</span><span class="sxs-lookup"><span data-stu-id="553b5-491">Debugging Cloud Services</span></span>

### <a name="azure-web-app-troubleshooting"></a><span data-ttu-id="553b5-492">Azure 웹 앱 문제 해결</span><span class="sxs-lookup"><span data-stu-id="553b5-492">Azure web app troubleshooting</span></span>
<span data-ttu-id="553b5-493">Azure 앱 서비스에서 웹 앱 문제 해결에 대한 자세한 내용은 다음 리소스를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="553b5-493">For more information about troubleshooting web apps in Azure App Service, see the following resources:</span></span>

* [<span data-ttu-id="553b5-494">웹 앱을 모니터링하는 방법</span><span class="sxs-lookup"><span data-stu-id="553b5-494">How to monitor web apps</span></span>](/manage/services/web-sites/how-to-monitor-websites/)
* <span data-ttu-id="553b5-495">[Visual Studio 2013을 사용하여 Azure Web Apps에서 메모리 누수 검사](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx)</span><span class="sxs-lookup"><span data-stu-id="553b5-495">[Investigating Memory Leaks in Azure Web Apps with Visual Studio 2013](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx).</span></span> <span data-ttu-id="553b5-496">관리되는 메모리 문제를 분석하는 데 사용되는 Visual Studio 기능에 대한 Microsoft ALM 블로그 게시물입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-496">Microsoft ALM blog post about Visual Studio features for analyzing managed memory issues.</span></span>
* <span data-ttu-id="553b5-497">[알아 두면 도움이 되는 Azure Web Apps 온라인 도구](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/)</span><span class="sxs-lookup"><span data-stu-id="553b5-497">[Azure web apps online tools you should know about](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/).</span></span> <span data-ttu-id="553b5-498">Amit Apple의 블로그 게시물입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-498">Blog post by Amit Apple.</span></span>

<span data-ttu-id="553b5-499">특정 문제 해결 질문과 관련하여 도움이 필요한 경우 다음 포럼 중 하나에서 게시물을 작성하십시오.</span><span class="sxs-lookup"><span data-stu-id="553b5-499">For help with a specific troubleshooting question, start a thread in one of the following forums:</span></span>

* <span data-ttu-id="553b5-500">[ASP.NET 사이트의 Azure 포럼](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET)(영문)</span><span class="sxs-lookup"><span data-stu-id="553b5-500">[The Azure forum on the ASP.NET site](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET).</span></span>
* <span data-ttu-id="553b5-501">[MSDN의 Azure 포럼](http://social.msdn.microsoft.com/Forums/windowsazure/)(영문)</span><span class="sxs-lookup"><span data-stu-id="553b5-501">[The Azure forum on MSDN](http://social.msdn.microsoft.com/Forums/windowsazure/).</span></span>
* <span data-ttu-id="553b5-502">[StackOverflow.com](http://www.stackoverflow.com)(영문)</span><span class="sxs-lookup"><span data-stu-id="553b5-502">[StackOverflow.com](http://www.stackoverflow.com).</span></span>

### <a name="debugging-in-visual-studio"></a><span data-ttu-id="553b5-503">Visual Studio의 디버깅</span><span class="sxs-lookup"><span data-stu-id="553b5-503">Debugging in Visual Studio</span></span>
<span data-ttu-id="553b5-504">Visual Studio에서 디버그 모드를 사용하는 방법에 대한 자세한 내용은 MSDN 토픽 [Visual Studio의 디버깅](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx)과 [Visual Studio 2010을 사용한 디버깅 팁](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="553b5-504">For more information about how to use debug mode in Visual Studio, see the [Debugging in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx) MSDN topic and [Debugging Tips with Visual Studio 2010](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx).</span></span>

### <a name="remote-debugging-in-azure"></a><span data-ttu-id="553b5-505">Azure의 원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="553b5-505">Remote debugging in Azure</span></span>
<span data-ttu-id="553b5-506">Azure 웹 앱 및 WebJob의 원격 디버깅에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="553b5-506">For more information about remote debugging for Azure web apps and WebJobs, see the following resources:</span></span>

* <span data-ttu-id="553b5-507">[Azure 앱 서비스 웹 앱의 원격 디버깅 소개.](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/)</span><span class="sxs-lookup"><span data-stu-id="553b5-507">[Introduction to Remote Debugging Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/).</span></span>
* [<span data-ttu-id="553b5-508">Azure 앱 서비스 웹 앱의 원격 디버깅 소개 2부 - 원격 디버깅 세부 정보</span><span class="sxs-lookup"><span data-stu-id="553b5-508">Introduction to Remote Debugging Azure App Service Web Apps part 2 - Inside Remote debugging</span></span>](https://azure.microsoft.com/blog/2014/05/07/introduction-to-remote-debugging-azure-web-sites-part-2-inside-remote-debugging/)
* [<span data-ttu-id="553b5-509">Azure 앱 서비스 웹 앱의 원격 디버깅 소개 3부 - 다중 인스턴스 환경 및 GIT</span><span class="sxs-lookup"><span data-stu-id="553b5-509">Introduction to Remote Debugging on Azure App Service Web Apps part 3 - Multi-Instance environment and GIT</span></span>](https://azure.microsoft.com/blog/2014/05/08/introduction-to-remote-debugging-on-azure-web-sites-part-3-multi-instance-environment-and-git/)
* [<span data-ttu-id="553b5-510">Webjob 디버깅(비디오)</span><span class="sxs-lookup"><span data-stu-id="553b5-510">WebJobs Debugging (video)</span></span>](https://www.youtube.com/watch?v=ncQm9q5ZFZs&list=UU_SjTh-ZltPmTYzAybypB-g&index=1)

<span data-ttu-id="553b5-511">웹 앱에 Azure 웹 API 또는 모바일 서비스 백 엔드가 사용되는 경우 이들을 디버그해야 하면 [Visual Studio에서 .NET 백 엔드 디버깅](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="553b5-511">If your web app uses an Azure Web API or Mobile Services back-end and you need to debug that, see [Debugging .NET Backend in Visual Studio](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx).</span></span>

### <a name="tracing-in-aspnet-applications"></a><span data-ttu-id="553b5-512">ASP.NET 응용 프로그램의 추적</span><span class="sxs-lookup"><span data-stu-id="553b5-512">Tracing in ASP.NET applications</span></span>
<span data-ttu-id="553b5-513">현재 인터넷에서 ASP.NET 추적과 관련하여 완벽한 최신 소개 정보를 제공하는 곳이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-513">There are no thorough and up-to-date introductions to ASP.NET tracing available on the Internet.</span></span> <span data-ttu-id="553b5-514">최상의 방법은 MVC가 아직 출시되지 않은 시점에 Web Forms용으로 작성된 기존 소개 자료를 먼저 참조한 후, 특정 문제에 주력하는 최신 블로그 게시물의 정보로 보충하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-514">The best you can do is get started with old introductory materials written for Web Forms because MVC didn't exist yet, and supplement that with newer blog posts that focus on specific issues.</span></span> <span data-ttu-id="553b5-515">시작하기에 유용한 리소스 위치는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-515">Some good places to start are the following resources:</span></span>

* <span data-ttu-id="553b5-516">[모니터링 및 원격 분석(Azure에서 실제 클라우드 앱 빌드)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry)</span><span class="sxs-lookup"><span data-stu-id="553b5-516">[Monitoring and Telemetry (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry).</span></span><br>
  <span data-ttu-id="553b5-517">Azure 클라우드 응용 프로그램에서 추적을 권장하는 전자책의 한 챕터</span><span class="sxs-lookup"><span data-stu-id="553b5-517">E-book chapter with recommendations for tracing in Azure cloud applications.</span></span>
* [<span data-ttu-id="553b5-518">ASP.NET 추적</span><span class="sxs-lookup"><span data-stu-id="553b5-518">ASP.NET Tracing</span></span>](http://msdn.microsoft.com/library/ms972204.aspx)<br/>
  <span data-ttu-id="553b5-519">오래된 자료이지만 추적의 기초를 소개하는 여전히 유용한 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-519">Old but still a good resource for a basic introduction to the subject.</span></span>
* [<span data-ttu-id="553b5-520">추적 수신기</span><span class="sxs-lookup"><span data-stu-id="553b5-520">Trace Listeners</span></span>](http://msdn.microsoft.com/library/4y5y10s7.aspx)<br/>
  <span data-ttu-id="553b5-521">추적 수신기에 대한 정보를 제공하지만 [WebPageTraceListener](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx)를 언급하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-521">Information about trace listeners but doesn't mention the [WebPageTraceListener](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx).</span></span>
* [<span data-ttu-id="553b5-522">연습: ASP.NET 추적을 System.Diagnostics 추적과 통합</span><span class="sxs-lookup"><span data-stu-id="553b5-522">Walkthrough: Integrating ASP.NET Tracing with System.Diagnostics Tracing</span></span>](http://msdn.microsoft.com/library/b0ectfxd.aspx)<br/>
  <span data-ttu-id="553b5-523">이 자료도 오래되었지만 소개 자료에서 다루지 않은 일부 추가 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-523">This too is old, but includes some additional information that the introductory article doesn't cover.</span></span>
* [<span data-ttu-id="553b5-524">ASP.NET MVC Razor 뷰에서 추적</span><span class="sxs-lookup"><span data-stu-id="553b5-524">Tracing in ASP.NET MVC Razor Views</span></span>](http://blogs.msdn.com/b/webdev/archive/2013/07/16/tracing-in-asp-net-mvc-razor-views.aspx)<br/>
  <span data-ttu-id="553b5-525">Razor 뷰의 추적 정보와 더불어, MVC 응용 프로그램의 처리되지 않은 모든 예외를 기록할 수 있도록 오류 필터를 만드는 방법을 설명하는 게시물입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-525">Besides tracing in Razor views, the post also explains how to create an error filter in order to log all unhandled exceptions in an MVC application.</span></span> <span data-ttu-id="553b5-526">Web Forms 응용 프로그램의 처리되지 않은 모든 예외를 기록하는 방법에 대한 자세한 내용은 MSDN의 [오류 처리기의 전체 예제](http://msdn.microsoft.com/library/bb397417.aspx) 에서 Global.asax를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="553b5-526">For information about how to log all unhandled exceptions in a Web Forms application, see the Global.asax example in [Complete Example for Error Handlers](http://msdn.microsoft.com/library/bb397417.aspx) on MSDN.</span></span> <span data-ttu-id="553b5-527">MVC 또는 Web Forms 중 하나에서 특정 예외를 기록하되 기본 프레임워크 처리 방식은 그대로 적용하려면 다음 예와 같이 해당 오류를 catch한 후 다시 throw하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-527">In either MVC or Web Forms, if you want to log certain exceptions but let the default framework handling take effect for them, you can catch and rethrow as in the following example:</span></span>

        try
        {
           // Your code that might cause an exception to be thrown.
        }
        catch (Exception ex)
        {
            Trace.TraceError("Exception: " + ex.ToString());
            throw;
        }
* [<span data-ttu-id="553b5-528">Azure 명령줄에서 진단 추적 로깅 스트리밍(Glimpse 포함)</span><span class="sxs-lookup"><span data-stu-id="553b5-528">Streaming Diagnostics Trace Logging from the Azure Command Line (plus Glimpse!)</span></span>](http://www.hanselman.com/blog/StreamingDiagnosticsTraceLoggingFromTheAzureCommandLinePlusGlimpse.aspx)<br/>
  <span data-ttu-id="553b5-529">이 자습서에서 설명한 Visual Studio 관련 작업을 명령줄로 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-529">How to use the command line to do what this tutorial shows how to do in Visual Studio.</span></span> <span data-ttu-id="553b5-530">[Glimpse](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) 는 ASP.NET 응용 프로그램을 디버그하는 데 사용하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-530">[Glimpse](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) is a tool for debugging ASP.NET applications.</span></span>
* <span data-ttu-id="553b5-531">[David Ebbo와 함께 하는 Web Apps 로깅 및 진단](/documentation/videos/azure-web-site-logging-and-diagnostics/) 및 [David Ebbo와 함께 하는 Web Apps에서 로그 스트리밍](/documentation/videos/log-streaming-with-azure-web-sites/)</span><span class="sxs-lookup"><span data-stu-id="553b5-531">[Using Web Apps Logging and Diagnostics - with David Ebbo](/documentation/videos/azure-web-site-logging-and-diagnostics/) and [Streaming Logs from Web Apps - with David Ebbo](/documentation/videos/log-streaming-with-azure-web-sites/)</span></span><br>
  <span data-ttu-id="553b5-532">은 Scott Hanselman과 David Ebbo가 제작한 비디오입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-532">Videos by Scott Hanselman and David Ebbo.</span></span>

<span data-ttu-id="553b5-533">오류 로깅과 관련하여, 사용자 자신의 추적 코드를 기록하는 또 다른 방법은 [ELMAH](http://nuget.org/packages/elmah/)같은 오픈 소스 로깅 프레임워크를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-533">For error logging, an alternative to writing your own tracing code is to use an open-source logging framework such as [ELMAH](http://nuget.org/packages/elmah/).</span></span> <span data-ttu-id="553b5-534">자세한 내용은 [Scott Hanselman의 ELMAH 관련 블로그 게시물](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)(영문)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="553b5-534">For more information, see [Scott Hanselman's blog posts about ELMAH](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx).</span></span>

<span data-ttu-id="553b5-535">또한 Azure에서 로그를 스트리밍하려면 ASP.NET 또는 System.Diagnostics 추적 기능을 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-535">Also, note that you don't have to use ASP.NET or System.Diagnostics tracing if you want to get streaming logs from Azure.</span></span> <span data-ttu-id="553b5-536">Azure 웹앱 스트리밍 로그 서비스는 *LogFiles* 폴더에 위치한 *.txt*, *.html* 또는 *.log* 파일을 스트리밍합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-536">The Azure web app streaming log service will stream any *.txt*, *.html*, or *.log* file that it finds in the *LogFiles* folder.</span></span> <span data-ttu-id="553b5-537">따라서 웹 앱의 파일 시스템에 기록하는 사용자 자신의 로깅 시스템을 만들 수 있습니다. 그러면 파일이 자동으로 스트리밍되어 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-537">Therefore, you could create your own logging system that writes to the file system of the web app, and your file will be automatically streamed and downloaded.</span></span> <span data-ttu-id="553b5-538">그러려면 *d:\home\logfiles* 폴더에 파일을 만드는 응용 프로그램 코드만 작성하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-538">All you have to do is write application code that creates files in the *d:\home\logfiles* folder.</span></span>

### <a name="analyzing-web-server-logs"></a><span data-ttu-id="553b5-539">웹 서버 로그 분석</span><span class="sxs-lookup"><span data-stu-id="553b5-539">Analyzing web server logs</span></span>
<span data-ttu-id="553b5-540">웹 서버 로그 분석에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="553b5-540">For more information about analyzing web server logs, see the following resources:</span></span>

* [<span data-ttu-id="553b5-541">LogParser</span><span class="sxs-lookup"><span data-stu-id="553b5-541">LogParser</span></span>](http://www.microsoft.com/download/details.aspx?id=24659)<br/>
  <span data-ttu-id="553b5-542">웹 서버 로그(*.log* 파일)의 데이터를 보는 데 사용하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-542">A tool for viewing data in web server logs (*.log* files).</span></span>
* [<span data-ttu-id="553b5-543">LogParser를 사용하여 IIS 성능 문제 또는 응용 프로그램 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="553b5-543">Troubleshooting IIS Performance Issues or Application Errors using LogParser </span></span>](http://www.iis.net/learn/troubleshoot/performance-issues/troubleshooting-iis-performance-issues-or-application-errors-using-logparser)<br/>
  <span data-ttu-id="553b5-544">웹 서버 로그를 분석하는 데 사용할 수 있는 로그 파서 도구를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-544">An introduction to the Log Parser tool that you can use to analyze web server logs.</span></span>
* [<span data-ttu-id="553b5-545">Robert McMurray의 LogParser 사용 관련 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="553b5-545">Blog posts by Robert McMurray on using LogParser</span></span>](http://blogs.msdn.com/b/robert_mcmurray/archive/tags/logparser/)<br/>
* [<span data-ttu-id="553b5-546">IIS 7.0, IIS 7.5 및 IIS 8.0의 HTTP 상태 코드</span><span class="sxs-lookup"><span data-stu-id="553b5-546">The HTTP status code in IIS 7.0, IIS 7.5, and IIS 8.0</span></span>](http://support.microsoft.com/kb/943891)

### <a name="analyzing-failed-request-tracing-logs"></a><span data-ttu-id="553b5-547">실패한 요청 로그 분석</span><span class="sxs-lookup"><span data-stu-id="553b5-547">Analyzing failed request tracing logs</span></span>
<span data-ttu-id="553b5-548">Microsoft TechNet 웹 사이트에 포함된 [실패한 요청 추적 사용](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing) (영문) 섹션은 이러한 로그 사용 방법을 이해하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-548">The Microsoft TechNet website includes a [Using Failed Request Tracing](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing) section which may be helpful for understanding how to use these logs.</span></span> <span data-ttu-id="553b5-549">하지만 이 설명서에서는 IIS에서 실패한 요청 추적을 구성하는 방법을 중점적으로 다루며, 이는 Azure 웹 앱에서 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="553b5-549">However, this documentation focuses mainly on configuring failed request tracing in IIS, which you can't do in Azure Web Apps.</span></span>

[GetStarted]: app-service-web-get-started-dotnet.md
[GetStartedWJ]: websites-dotnet-webjobs-sdk.md
