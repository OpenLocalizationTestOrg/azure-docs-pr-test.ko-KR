---
title: "Visual Studio를 사용 하 여 Azure 앱 서비스의 웹 앱 aaaTroubleshoot"
description: "어떻게 tootroubleshoot 원격 디버깅을 사용 하 여 Azure 웹 앱, 추적, 로깅 도구 및 tooVisual Studio 2013에에서는 기본 제공에 대해 알아봅니다."
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
ms.openlocfilehash: 8e3a8a58293f2ebcdc131fbf2534f8ff99b26730
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-web-app-in-azure-app-service-using-visual-studio"></a><span data-ttu-id="2b4ee-103">Visual Studio를 사용하여 Azure 앱 서비스에서 웹 앱 문제 해결</span><span class="sxs-lookup"><span data-stu-id="2b4ee-103">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="2b4ee-104">개요</span><span class="sxs-lookup"><span data-stu-id="2b4ee-104">Overview</span></span>
<span data-ttu-id="2b4ee-105">이 자습서는 데 도움이 되는 toouse Visual Studio 도구에 웹 응용 프로그램을 디버깅 하는 방법을 보여 줍니다. [앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714),를 실행 하 여 [디버그 모드](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) 원격으로 또는 응용 프로그램 로그와 웹 서버 로그를 확인 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-105">This tutorial shows how toouse Visual Studio tools that help debug a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), by running in [debug mode](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) remotely or by viewing application logs and web server logs.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="2b4ee-106">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-106">You'll learn:</span></span>

* <span data-ttu-id="2b4ee-107">Visual Studio에서 사용할 수 있는 Azure 웹 앱 관리 기능</span><span class="sxs-lookup"><span data-stu-id="2b4ee-107">Which Azure web app management functions are available in Visual Studio.</span></span>
* <span data-ttu-id="2b4ee-108">어떻게 toouse Visual Studio 원격 원격 웹 앱에서 toomake 빠른 변경 내용을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-108">How toouse Visual Studio remote view toomake quick changes in a remote web app.</span></span>
* <span data-ttu-id="2b4ee-109">어떻게 toorun 디버그 모드는 프로젝트 하는 동안 원격으로와 같은 웹 작업이 모두 웹 응용 프로그램에 대 한 Azure에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-109">How toorun debug mode remotely while a project is running in Azure, both for a web app and for a WebJob.</span></span>
* <span data-ttu-id="2b4ee-110">어떻게 toocreate 응용 프로그램 추적 로그 하 고 보는 동안 hello 응용 프로그램을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-110">How toocreate application trace logs and view them while hello application is creating them.</span></span>
* <span data-ttu-id="2b4ee-111">어떻게 tooview 웹 서버 로그를 포함 하 여 자세한 오류 메시지 및 실패 한 요청 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-111">How tooview web server logs, including detailed error messages and failed request tracing.</span></span>
* <span data-ttu-id="2b4ee-112">어떻게 toosend 진단 tooan Azure 저장소 계정 로그 하 고 보는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-112">How toosend diagnostic logs tooan Azure Storage account and view them there.</span></span>

<span data-ttu-id="2b4ee-113">Visual Studio Ultimate가 있으면 디버깅에 [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) 를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-113">If you have Visual Studio Ultimate, you can also use [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) for debugging.</span></span> <span data-ttu-id="2b4ee-114">IntelliTrace는 이 자습서에서 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-114">IntelliTrace is not covered in this tutorial.</span></span>

## <span data-ttu-id="2b4ee-115"><a name="prerequisites"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="2b4ee-115"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="2b4ee-116">이 자습서는 hello 개발 환경, 웹 프로젝트 및 Azure 웹 앱에서 설정한 [Azure 및 ASP.NET 시작][GetStarted]합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-116">This tutorial works with hello development environment, web project, and Azure web app that you set up in [Get started with Azure and ASP.NET][GetStarted].</span></span> <span data-ttu-id="2b4ee-117">Hello WebJobs 섹션에 대 한 hello 응용 프로그램에서 만드는 해야 [hello Azure WebJobs SDK 시작][GetStartedWJ]합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-117">For hello WebJobs sections, you'll need hello application that you create in [Get Started with hello Azure WebJobs SDK][GetStartedWJ].</span></span>

<span data-ttu-id="2b4ee-118">이 자습서에 표시 된 예제는 C# MVC 웹 응용 프로그램에 대 한 있지만 문제 해결 절차 hello hello 코드는 Visual Basic 및 Web Forms 응용 프로그램에 대 한 동일한 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-118">hello code samples shown in this tutorial are for a C# MVC web application, but hello troubleshooting procedures are hello same for Visual Basic and Web Forms applications.</span></span>

<span data-ttu-id="2b4ee-119">hello 자습서에서는 Visual Studio 2015 또는 2013을 사용 하는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-119">hello tutorial assumes you're using Visual Studio 2015 or 2013.</span></span> <span data-ttu-id="2b4ee-120">Visual Studio 2013을 사용 하는 경우에 hello WebJobs 기능 필요 [업데이트 4](http://go.microsoft.com/fwlink/?LinkID=510314) 이상.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-120">If you're using Visual Studio 2013, hello WebJobs features require [Update 4](http://go.microsoft.com/fwlink/?LinkID=510314) or later.</span></span>

<span data-ttu-id="2b4ee-121">hello 스트리밍 로그 기능에 대 한.NET Framework 4 이상을 대상으로 하는 응용 프로그램 에서만 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-121">hello streaming logs feature only works for applications that target .NET Framework 4 or later.</span></span>

## <span data-ttu-id="2b4ee-122"><a name="sitemanagement"></a>웹 앱 구성 및 관리</span><span class="sxs-lookup"><span data-stu-id="2b4ee-122"><a name="sitemanagement"></a>Web app configuration and management</span></span>
<span data-ttu-id="2b4ee-123">Visual Studio는 hello 웹 응용 프로그램 관리 기능 및 hello에서 사용할 수 있는 구성 설정의 액세스 tooa 하위 집합을 제공 [Azure 포털](http://go.microsoft.com/fwlink/?LinkId=529715)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-123">Visual Studio provides access tooa subset of hello web app management functions and configuration settings available in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="2b4ee-124">이 섹션에서는 **서버 탐색기**를 사용하여 사용할 수 있는 기능에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-124">In this section you'll see what's available by using **Server Explorer**.</span></span> <span data-ttu-id="2b4ee-125">toosee hello 최신 Azure 통합 기능을 사용해 **클라우드 탐색기** 도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-125">toosee hello latest Azure integration features, try out **Cloud Explorer** also.</span></span> <span data-ttu-id="2b4ee-126">Windows hello에서 열 수 **보기** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-126">You can open both windows from hello **View** menu.</span></span>

1. <span data-ttu-id="2b4ee-127">Visual Studio에서 tooAzure에 로그인 하지 않은 경우 클릭 hello **tooAzure 연결** 단추 **서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-127">If you aren't already signed in tooAzure in Visual Studio, click hello **Connect tooAzure** button in **Server Explorer**.</span></span>

    <span data-ttu-id="2b4ee-128">Tooinstall 액세스 tooyour 계정을 사용 하도록 설정 하는 관리 인증서 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-128">An alternative is tooinstall a management certificate that enables access tooyour account.</span></span> <span data-ttu-id="2b4ee-129">Tooinstall 인증서를 선택 하면 hello 마우스 오른쪽 단추로 클릭 **Azure** 노드에서 **서버 탐색기**, 클릭 하 고 **구독 관리 및 필터링** hello 상황에 맞는 메뉴에서입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-129">If you choose tooinstall a certificate, right-click hello **Azure** node in **Server Explorer**, and then click **Manage and Filter Subscriptions** in hello context menu.</span></span> <span data-ttu-id="2b4ee-130">Hello에 **Azure 구독 관리** 대화 상자를 클릭 hello **인증서** 탭을 클릭 한 다음 **가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-130">In hello **Manage Azure Subscriptions** dialog box, click hello **Certificates** tab, and then click **Import**.</span></span> <span data-ttu-id="2b4ee-131">Hello directions toodownload 따르고 다음 구독 파일을 가져옵니다 (라고도 *.publishsettings* 파일) 하 여 Azure 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-131">Follow hello directions toodownload and then import a subscription file (also called a *.publishsettings* file) for your Azure account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2b4ee-132">구독 파일을 다운로드 하는 경우 소스 코드 디렉터리 외부 (예를 들어 hello 다운로드 폴더), tooa 폴더를 저장 하 고 hello 가져오기가 완료 되 면 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-132">If you download a subscription file, save it tooa folder outside your source code directories (for example, in hello Downloads folder), and then delete it once hello import has completed.</span></span> <span data-ttu-id="2b4ee-133">Access toohello 구독 파일을 얻은 악의적인 사용자는 수 편집 만들고 Azure 서비스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-133">A malicious user who gains access toohello subscription file can edit, create, and delete your Azure services.</span></span>
   >
   >

    <span data-ttu-id="2b4ee-134">Visual Studio에서 tooAzure 리소스를 연결 하는 방법에 대 한 자세한 내용은 참조 [계정 관리, 구독 및 관리 역할](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-134">For more information about connecting tooAzure resources from Visual Studio, see [Manage Accounts, Subscriptions, and Administrative Roles](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert).</span></span>
2. <span data-ttu-id="2b4ee-135">**서버 탐색기**에서 **Azure**를 확장한 후 **App Service**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-135">In **Server Explorer**, expand **Azure** and expand **App Service**.</span></span>
3. <span data-ttu-id="2b4ee-136">만든 hello 웹 앱을 포함 하는 hello 리소스 그룹을 확장 [Azure 및 ASP.NET 시작][GetStarted], hello 웹 응용 프로그램 노드를 마우스 오른쪽 단추로 클릭 한 다음 고를 클릭 **설정보기**.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-136">Expand hello resource group that includes hello web app that you created in [Getting started with Azure and ASP.NET][GetStarted], and then right-click hello web app node and click **View Settings**.</span></span>

    ![서버 탐색기에서 설정 보기](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewsettings.png)

    <span data-ttu-id="2b4ee-138">hello **Azure 웹 앱** 탭에 표시 되 고 있는 웹 응용 프로그램 관리 및 구성 작업 Visual Studio에서 사용할 수 있는 hello를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-138">hello **Azure Web App** tab appears, and you can see there hello web app management and configuration tasks that are available in Visual Studio.</span></span>

    ![Azure 웹 앱 창](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configtab.png)

    <span data-ttu-id="2b4ee-140">이 자습서에서는 있습니다 사용할 예정 hello 로깅 및 추적 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-140">In this tutorial you'll be using hello logging and tracing drop-downs.</span></span> <span data-ttu-id="2b4ee-141">또한 원격 디버깅을 사용 하지만 다른 방법을 tooenable 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-141">You'll also use remote debugging but you'll use a different method tooenable it.</span></span>

    <span data-ttu-id="2b4ee-142">이 창에 hello 앱 설정 및 연결 문자열 상자에 대 한 정보를 참조 하십시오. [Azure 웹 앱: 방법: 응용 프로그램 문자열 및 연결 문자열 작업](http://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-142">For information about hello App Settings and Connection Strings boxes in this window, see [Azure Web Apps: How Application Strings and Connection Strings Work](http://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).</span></span>

    <span data-ttu-id="2b4ee-143">이 창에서 수행할 수 없는 웹 응용 프로그램 관리 작업을 tooperform 클릭 **관리 포털에서 열기** tooopen 브라우저 창 toohello Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-143">If you want tooperform a web app management task that can't be done in this window, click **Open in Management Portal** tooopen a browser window toohello Azure portal.</span></span>

## <span data-ttu-id="2b4ee-144"><a name="remoteview"></a>서버 탐색기에서 웹 앱 파일 액세스</span><span class="sxs-lookup"><span data-stu-id="2b4ee-144"><a name="remoteview"></a>Access web app files in Server Explorer</span></span>
<span data-ttu-id="2b4ee-145">일반적으로 hello로 웹 프로젝트를 배포 하면 `customErrors` hello Web.config 파일 집합에에서 플래그가 지정 너무`On` 또는 `RemoteOnly`, 의미 하는 경우 다른 유용한 오류 메시지를 가져오지 않음 문제가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-145">You typically deploy a web project with hello `customErrors` flag in hello Web.config file set too`On` or `RemoteOnly`, which means you don't get a helpful error message when something goes wrong.</span></span> <span data-ttu-id="2b4ee-146">많은 오류에 대 한 모든 얻게는 hello는 스토리를 다음 중 하 나와 비슷한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-146">For many errors all you get is a page like one of hello following ones.</span></span>

<span data-ttu-id="2b4ee-147">**'/' 응용 프로그램의 서버 오류:**</span><span class="sxs-lookup"><span data-stu-id="2b4ee-147">**Server Error in '/' Application:**</span></span>

![도움이 되지 않는 오류 메시지](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror.png)

<span data-ttu-id="2b4ee-149">**오류가 발생했습니다.**</span><span class="sxs-lookup"><span data-stu-id="2b4ee-149">**An error occurred:**</span></span>

![도움이 되지 않는 오류 메시지](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror1.png)

<span data-ttu-id="2b4ee-151">**hello 웹 사이트 hello 페이지를 표시할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="2b4ee-151">**hello website cannot display hello page**</span></span>

![도움이 되지 않는 오류 메시지](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror2.png)

<span data-ttu-id="2b4ee-153">자주 hello 가장 쉬운 방법은 toofind hello hello 오류는 발생 tooenable hello 스크린 샷을 앞의 첫 번째 hello 되는 자세한 오류 메시지에 설명 방법을 toodo 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-153">Frequently hello easiest way toofind hello cause of hello error is tooenable detailed error messages, which hello first of hello preceding screenshots explains how toodo.</span></span> <span data-ttu-id="2b4ee-154">변경 hello에 배포 된 Web.config 파일을 필요로 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-154">That requires a change in hello deployed Web.config file.</span></span> <span data-ttu-id="2b4ee-155">Hello를 편집할 수 *Web.config* hello 프로젝트와 재배포 hello 프로젝트에서 파일을 만들거나 한 [f i g 변환](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) 및 디버그 빌드를 배포 하지만 더 빠른 방법:에서 **솔루션 탐색기** 직접 보고 하 고 hello를 사용 하 여 hello 원격 웹 앱에서 파일을 편집할 수 *원격 뷰* 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-155">You could edit hello *Web.config* file in hello project and redeploy hello project, or create a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) and deploy a debug build, but there's a quicker way: in **Solution Explorer** you can directly view and edit files in hello remote web app by using hello *remote view* feature.</span></span>

1. <span data-ttu-id="2b4ee-156">**서버 탐색기**를 확장 하 고 **Azure**를 확장 하 고 **앱 서비스**, 웹 앱에 있는 hello 리소스 그룹을 확장 한 다음 웹 앱에 대 한 hello 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-156">In **Server Explorer**, expand **Azure**, expand **App Service**, expand hello resource group that your web app is located in, and then expand hello node for your web app.</span></span>

    <span data-ttu-id="2b4ee-157">액세스 toohello 웹 앱의 콘텐츠 파일 및 로그 파일을 제공 하는 노드를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-157">You see nodes that give you access toohello web app's content files and log files.</span></span>
2. <span data-ttu-id="2b4ee-158">Hello 확장 **파일** 노드를 hello를 두 번 클릭 하 고 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-158">Expand hello **Files** node, and double-click hello *Web.config* file.</span></span>

    ![Web.config 열기](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfig.png)

    <span data-ttu-id="2b4ee-160">Visual Studio hello 원격 웹 앱에서 hello Web.config 파일이 열리고 hello 제목 표시줄에 다음 [원격] toohello 파일 이름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-160">Visual Studio opens hello Web.config file from hello remote web app and shows [Remote] next toohello file name in hello title bar.</span></span>
3. <span data-ttu-id="2b4ee-161">다음 줄 toohello hello 추가 `system.web` 요소:</span><span class="sxs-lookup"><span data-stu-id="2b4ee-161">Add hello following line toohello `system.web` element:</span></span>

    `<customErrors mode="Off"></customErrors>`

    ![Web.config 편집](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfigedit.png)
4. <span data-ttu-id="2b4ee-163">Hello 도움이 되지 않는 오류 메시지를 표시 하는 hello 브라우저 새로 고치고 이제 다음 예제는 hello 같은 자세한 오류 메시지를 받을:</span><span class="sxs-lookup"><span data-stu-id="2b4ee-163">Refresh hello browser that is showing hello unhelpful error message, and now you get a detailed error message, such as hello following example:</span></span>

    ![자세한 오류 메시지](./media/web-sites-dotnet-troubleshoot-visual-studio/detailederror.png)

    <span data-ttu-id="2b4ee-165">(표시 하는 hello 오류가 너무 빨간색으로 표시 된 hello 줄을 추가 하 여 만들어진*Views\Home\Index.cshtml*.)</span><span class="sxs-lookup"><span data-stu-id="2b4ee-165">(hello error shown was created by adding hello line shown in red too*Views\Home\Index.cshtml*.)</span></span>

<span data-ttu-id="2b4ee-166">편집 hello Web.config 파일은 하나의 예는 hello 기능에 Azure 웹 앱에 tooread 및 편집 파일 확인 문제 해결에 도움이 되는 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-166">Editing hello Web.config file is only one example of scenarios in which hello ability tooread and edit files on your Azure web app make troubleshooting easier.</span></span>

## <span data-ttu-id="2b4ee-167"><a name="remotedebug"></a>원격 디버깅 웹 앱</span><span class="sxs-lookup"><span data-stu-id="2b4ee-167"><a name="remotedebug"></a>Remote debugging web apps</span></span>
<span data-ttu-id="2b4ee-168">Hello 자세한 오류 메시지는 정보를 충분히 제공 하지 않는 경우 hello 오류 로컬로 다시 만들 수 없습니다 또 다른 방법은 tootroubleshoot는 toorun 디버그 모드에서 원격으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-168">If hello detailed error message doesn't provide enough information, and you can't re-create hello error locally, another way tootroubleshoot is toorun in debug mode remotely.</span></span> <span data-ttu-id="2b4ee-169">중단점을 설정할 메모리를 직접 조작 및 코드를 단계적 hello 코드 경로 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-169">You can set breakpoints, manipulate memory directly, step through code, and even change hello code path.</span></span>

<span data-ttu-id="2b4ee-170">원격 디버깅은 Visual Studio의 Express Edition에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-170">Remote debugging does not work in Express editions of Visual Studio.</span></span>

<span data-ttu-id="2b4ee-171">이 섹션에서는 hello를 사용 하 여 원격 toodebug 어떻게 프로젝트에서 만드는 [Azure 및 ASP.NET 시작][GetStarted]합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-171">This section shows how toodebug remotely using hello project you create in [Getting started with Azure and ASP.NET][GetStarted].</span></span>

1. <span data-ttu-id="2b4ee-172">만든 웹 프로젝트를 열고 hello [Azure 및 ASP.NET 시작][GetStarted]합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-172">Open hello web project that you created in [Getting started with Azure and ASP.NET][GetStarted].</span></span>
2. <span data-ttu-id="2b4ee-173">*Controllers\HomeController.cs*를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-173">Open *Controllers\HomeController.cs*.</span></span>
3. <span data-ttu-id="2b4ee-174">Hello 삭제 `About()` 메서드 및 삽입 hello 다음 해당 위치에 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-174">Delete hello `About()` method and insert hello following code in its place.</span></span>

        public ActionResult About()
        {
            string currentTime = DateTime.Now.ToLongTimeString();
            ViewBag.Message = "hello current time is " + currentTime;
            return View();
        }
4. <span data-ttu-id="2b4ee-175">[중단점을 설정](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) hello에 `ViewBag.Message` 선입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-175">[Set a breakpoint](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) on hello `ViewBag.Message` line.</span></span>
5. <span data-ttu-id="2b4ee-176">**솔루션 탐색기**hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-176">In **Solution Explorer**, right-click hello project, and click **Publish**.</span></span>
6. <span data-ttu-id="2b4ee-177">Hello에 **프로필** 동일 하면에 사용 된 프로필 드롭 다운 목록, 선택 hello [Azure 및 ASP.NET 시작][GetStarted]합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-177">In hello **Profile** drop-down list, select hello same profile that you used in [Getting started with Azure and ASP.NET][GetStarted].</span></span>
7. <span data-ttu-id="2b4ee-178">Hello 클릭 **설정** 를 탭 하 고 변경 **구성** 너무**디버그**, 클릭 하 고 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-178">Click hello **Settings** tab, and change **Configuration** too**Debug**, and then click **Publish**.</span></span>

    ![디버그 모드에서 게시](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-publishdebug.png)
8. <span data-ttu-id="2b4ee-180">배포 후 완료 되 고 브라우저가 toohello 닫기 hello 브라우저 웹 응용 프로그램의 Azure URL을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-180">After deployment finishes and your browser opens toohello Azure URL of your web app, close hello browser.</span></span>
9. <span data-ttu-id="2b4ee-181">**서버 탐색기**에서 웹앱을 마우스 오른쪽 단추로 클릭한 다음 **디버거 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-181">In **Server Explorer**, right-click your web app, and then click **Attach Debugger**.</span></span>

    ![디버거 연결](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-attachdebugger.png)

    <span data-ttu-id="2b4ee-183">hello 브라우저는 자동으로 Azure에서 실행 중인 tooyour 홈 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-183">hello browser automatically opens tooyour home page running in Azure.</span></span> <span data-ttu-id="2b4ee-184">수 toowait 20 초 했거나 하므로 하는 동안 Azure 디버깅에 대 한 hello 서버를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-184">You might have toowait 20 seconds or so while Azure sets up hello server for debugging.</span></span> <span data-ttu-id="2b4ee-185">이 지연은만 hello 웹 응용 프로그램에서 디버그 모드에서 실행 되는 처음으로 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-185">This delay only happens hello first time you run in debug mode on a web app.</span></span> <span data-ttu-id="2b4ee-186">디버깅 다시 시작 하면 다음 48 시간 hello 내에서 이후 시간 지연 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-186">Subsequent times within hello next 48 hours when you start debugging again there won't be a delay.</span></span>

    <span data-ttu-id="2b4ee-187">**참고:** hello 디버거를 시작 하는 데 문제가 있는 경우 시도 toodo 사용 하 여 **클라우드 탐색기** 대신 **서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-187">**Note:** If you have any trouble starting hello debugger, try toodo it by using **Cloud Explorer** instead of **Server Explorer**.</span></span>
10. <span data-ttu-id="2b4ee-188">클릭 **에 대 한** hello 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-188">Click **About** in hello menu.</span></span>

     <span data-ttu-id="2b4ee-189">Visual Studio hello 중단점에서 중지 하 고 hello 코드가 로컬 컴퓨터에 없는 Azure에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-189">Visual Studio stops on hello breakpoint, and hello code is running in Azure, not on your local computer.</span></span>
11. <span data-ttu-id="2b4ee-190">Hello 위로 마우스를 가져가고 `currentTime` 변수 toosee hello 시간 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-190">Hover over hello `currentTime` variable toosee hello time value.</span></span>

     ![Azure에서 실행 중인 디버그 모드의 변수 보기](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugviewinwa.png)

     <span data-ttu-id="2b4ee-192">hello 표시 시간은 로컬 컴퓨터에는 다른 표준 시간대에 있을 수 있는 hello Azure 서버 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-192">hello time you see is hello Azure server time, which may be in a different time zone than your local computer.</span></span>
12. <span data-ttu-id="2b4ee-193">Hello에 대 한 새 값을 입력 `currentTime` "이제 Azure에서 실행 중인"와 같은 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-193">Enter a new value for hello `currentTime` variable, such as "Now running in Azure".</span></span>
13. <span data-ttu-id="2b4ee-194">F5 toocontinue 실행 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-194">Press F5 toocontinue running.</span></span>

     <span data-ttu-id="2b4ee-195">Azure에서 실행 되는 페이지에 대 한 hello hello hello currentTime 변수에 입력 한 새 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-195">hello About page running in Azure displays hello new value that you entered into hello currentTime variable.</span></span>

     ![새 값이 표시된 정보 페이지](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugchangeinwa.png)

## <span data-ttu-id="2b4ee-197"><a name="remotedebugwj"></a> 원격 디버깅 WebJob</span><span class="sxs-lookup"><span data-stu-id="2b4ee-197"><a name="remotedebugwj"></a> Remote debugging WebJobs</span></span>
<span data-ttu-id="2b4ee-198">이 섹션에서는 hello 프로젝트와 웹 응용 프로그램을 사용 하 여 원격 toodebug를 만드는 방법에 [hello Azure WebJobs SDK 시작](websites-dotnet-webjobs-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-198">This section shows how toodebug remotely using hello project and web app you create in [Get Started with hello Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

<span data-ttu-id="2b4ee-199">이 섹션에 표시 된 hello 기능은 Visual Studio 2013 업데이트 4 이상에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-199">hello features shown in this section are available only in Visual Studio 2013 with Update 4 or later.</span></span>

<span data-ttu-id="2b4ee-200">연속 WebJobs에서 원격 디버깅만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-200">Remote debugging only works with continuous WebJobs.</span></span> <span data-ttu-id="2b4ee-201">예약 및 주문형 WebJobs은 디버깅을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-201">Scheduled and on-demand WebJobs don't support debugging.</span></span>

1. <span data-ttu-id="2b4ee-202">만든 웹 프로젝트를 열고 hello [hello Azure WebJobs SDK 시작][GetStartedWJ]합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-202">Open hello web project that you created in [Get Started with hello Azure WebJobs SDK][GetStartedWJ].</span></span>
2. <span data-ttu-id="2b4ee-203">Hello ContosoAdsWebJob 프로젝트를 열고 *Functions.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-203">In hello ContosoAdsWebJob project, open *Functions.cs*.</span></span>
3. <span data-ttu-id="2b4ee-204">[중단점을 설정](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) hello의 첫 번째 문에서 hello `GnerateThumbnail` 메서드.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-204">[Set a breakpoint](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) on hello first statement in hello `GnerateThumbnail` method.</span></span>

    ![중단점 설정](./media/web-sites-dotnet-troubleshoot-visual-studio/wjbreakpoint.png)
4. <span data-ttu-id="2b4ee-206">**솔루션 탐색기**hello 웹 프로젝트 (하지 hello WebJob 프로젝트의 경우)를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-206">In **Solution Explorer**, right-click hello web project (not hello WebJob project), and click **Publish**.</span></span>
5. <span data-ttu-id="2b4ee-207">Hello에 **프로필** 동일 하면에 사용 된 프로필 드롭 다운 목록, 선택 hello [hello Azure WebJobs SDK 시작](websites-dotnet-webjobs-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-207">In hello **Profile** drop-down list, select hello same profile that you used in [Get Started with hello Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>
6. <span data-ttu-id="2b4ee-208">Hello 클릭 **설정** 를 탭 하 고 변경 **구성** 너무**디버그**, 클릭 하 고 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-208">Click hello **Settings** tab, and change **Configuration** too**Debug**, and then click **Publish**.</span></span>

    <span data-ttu-id="2b4ee-209">Visual Studio hello 웹 및 WebJob 프로젝트를 배포 하 고 브라우저 웹 응용 프로그램의 Azure URL toohello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-209">Visual Studio deploys hello web and WebJob projects, and your browser opens toohello Azure URL of your web app.</span></span>
7. <span data-ttu-id="2b4ee-210">**서버 탐색기**에서 **Azure > App Service > 리소스 그룹 > 웹앱 > WebJobs > 연속**을 확장하고 **ContosoAdsWebJob**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-210">In **Server Explorer** expand **Azure > App Service > your resource group > your web app > WebJobs > Continuous**, and then right-click **ContosoAdsWebJob**.</span></span>
8. <span data-ttu-id="2b4ee-211">**디버거 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-211">Click **Attach Debugger**.</span></span>

    ![디버거 연결](./media/web-sites-dotnet-troubleshoot-visual-studio/wjattach.png)

    <span data-ttu-id="2b4ee-213">hello 브라우저는 자동으로 Azure에서 실행 중인 tooyour 홈 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-213">hello browser automatically opens tooyour home page running in Azure.</span></span> <span data-ttu-id="2b4ee-214">수 toowait 20 초 했거나 하므로 하는 동안 Azure 디버깅에 대 한 hello 서버를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-214">You might have toowait 20 seconds or so while Azure sets up hello server for debugging.</span></span> <span data-ttu-id="2b4ee-215">이 지연은만 hello 웹 응용 프로그램에서 디버그 모드에서 실행 되는 처음으로 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-215">This delay only happens hello first time you run in debug mode on a web app.</span></span> <span data-ttu-id="2b4ee-216">hello 있는 hello 디버거를 연결 하는 다음 번 됩니다는 지연을 48 시간 이내에 수행 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-216">hello next time you attach hello debugger there won't be a delay, if you do it within 48 hours.</span></span>
9. <span data-ttu-id="2b4ee-217">열린된 toohello Contoso 광고 홈 페이지는 hello 웹 브라우저에서 새 ad를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-217">In hello web browser that is opened toohello Contoso Ads home page, create a new ad.</span></span>

    <span data-ttu-id="2b4ee-218">광고를 만들면는 큐 메시지 toobe 만들어지면 WebJob hello에 의해 선택 되 고 처리 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-218">Creating an ad causes a queue message toobe created, which will be picked up by hello WebJob and processed.</span></span> <span data-ttu-id="2b4ee-219">WebJobs SDK hello hello 함수 tooprocess hello 큐 메시지를 호출 하면 hello 코드 중단점이 적중 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-219">When hello WebJobs SDK calls hello function tooprocess hello queue message, hello code will hit your breakpoint.</span></span>
10. <span data-ttu-id="2b4ee-220">Hello 디버거는 중단점에서 중단을 검토 하 고 hello 프로그램 hello 클라우드 실행 되는 동안 변수 값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-220">When hello debugger breaks at your breakpoint, you can examine and change variable values while hello program is running hello cloud.</span></span> <span data-ttu-id="2b4ee-221">Hello 다음 그림 hello 디버거 toohello GenerateThumbnail 메서드에 전달 된 hello blobInfo 개체의 hello 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-221">In hello following illustration hello debugger shows hello contents of hello blobInfo object that was passed toohello GenerateThumbnail method.</span></span>

     ![디버거에서 blobInfo 개체](./media/web-sites-dotnet-troubleshoot-visual-studio/blobinfo.png)
11. <span data-ttu-id="2b4ee-223">F5 toocontinue 실행 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-223">Press F5 toocontinue running.</span></span>

     <span data-ttu-id="2b4ee-224">hello GenerateThumbnail 메서드 hello 축소판 그림을 만들기를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-224">hello GenerateThumbnail method finishes creating hello thumbnail.</span></span>
12. <span data-ttu-id="2b4ee-225">Hello 브라우저를 새로 고침 hello 인덱스 페이지의 hello 축소판 그림을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-225">In hello browser, refresh hello Index page and you see hello thumbnail.</span></span>
13. <span data-ttu-id="2b4ee-226">Visual Studio에서 toostop 디버깅 SHIFT + f 5를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-226">In Visual Studio, press SHIFT+F5 toostop debugging.</span></span>
14. <span data-ttu-id="2b4ee-227">**서버 탐색기**hello ContosoAdsWebJob 노드를 마우스 오른쪽 단추로 클릭 하 고 클릭 **View 대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-227">In **Server Explorer**, right-click hello ContosoAdsWebJob node and click **View Dashboard**.</span></span>
15. <span data-ttu-id="2b4ee-228">Azure 자격 증명으로 로그인 하 고에 대 한 WebJob hello WebJob 이름 toogo toohello 페이지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-228">Sign in with your Azure credentials, and then click hello WebJob name toogo toohello page for your WebJob.</span></span>

     ![ContosoAdsWebJob 클릭](./media/web-sites-dotnet-troubleshoot-visual-studio/clickcaw.png)

     <span data-ttu-id="2b4ee-230">hello 대시보드 해당 hello 최근에 실행 GenerateThumbnail 함수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-230">hello Dashboard shows that hello GenerateThumbnail function executed recently.</span></span>

     <span data-ttu-id="2b4ee-231">(다음 클릭할 때 hello **View 대시보드**,에서는 toosign 없는 나타나고 hello 브라우저 직접 toohello 페이지에 대 한 WebJob.)</span><span class="sxs-lookup"><span data-stu-id="2b4ee-231">(hello next time you click **View Dashboard**, you don't have toosign in, and hello browser goes directly toohello page for your WebJob.)</span></span>
16. <span data-ttu-id="2b4ee-232">Hello 함수 이름 toosee hello 함수를 실행 하는 방법에 대 한 정보를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-232">Click hello function name toosee details about hello function execution.</span></span>

     ![함수 정보](./media/web-sites-dotnet-troubleshoot-visual-studio/funcdetails.png)

<span data-ttu-id="2b4ee-234">경우 함수 [로그 작성](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs), 누르면 **ToggleOutput** toosee 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-234">If your function [wrote logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs), you could click **ToggleOutput** toosee them.</span></span>

## <a name="notes-about-remote-debugging"></a><span data-ttu-id="2b4ee-235">원격 디버깅 관련 참고 사항</span><span class="sxs-lookup"><span data-stu-id="2b4ee-235">Notes about remote debugging</span></span>
* <span data-ttu-id="2b4ee-236">프로덕션 사이트에서 디버그 모드로 실행하는 것은 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-236">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="2b4ee-237">Toomultiple 서버 인스턴스는 프로덕션 웹 앱 확장 되지 않습니다, 하는 경우 디버깅 tooother 요청 응답에서 웹 서버 hello 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-237">If your production web app is not scaled out toomultiple server instances, debugging will prevent hello web server from responding tooother requests.</span></span> <span data-ttu-id="2b4ee-238">이렇게 하면 여러 웹 서버 인스턴스를 얻을 수 있습니다 및 임의 인스턴스를 toohello 디버거를 연결 하는 경우가 없는 방식으로 tooensure 해당 후속 브라우저 요청은 toothat 인스턴스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-238">If you do have multiple web server instances, when you attach toohello debugger you'll get a random instance, and you have no way tooensure that subsequent browser requests will go toothat instance.</span></span> <span data-ttu-id="2b4ee-239">또한 일반적으로 디버그 빌드 tooproduction를 배포 하지 않으려는 릴리스 빌드에 대 한 컴파일러 최적화 수 일어나는 불가능 한 tooshow 여 한 줄씩 소스 코드에서.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-239">Also, you typically don't deploy a debug build tooproduction, and compiler optimizations for release builds might make it impossible tooshow what is happening line by line in your source code.</span></span> <span data-ttu-id="2b4ee-240">프로덕션 문제를 해결하는 데는 응용 프로그램 추적 및 웹 서버 로그가 최적의 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-240">For troubleshooting production problems, your best resource is application tracing and web server logs.</span></span>
* <span data-ttu-id="2b4ee-241">원격 디버깅 시 중단점에서 장시간 중지하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-241">Avoid long stops at breakpoints when remote debugging.</span></span> <span data-ttu-id="2b4ee-242">몇 분 이상 중지된 프로세스는 Azure에서 응답하지 않는 프로세스로 간주되어 종료되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-242">Azure treats a process that is stopped for longer than a few minutes as an unresponsive process, and shuts it down.</span></span>
* <span data-ttu-id="2b4ee-243">디버그 하는 동안 hello 서버 데이터 tooVisual 대역폭 요금에 영향을 줄 수 있는 Studio 보내는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-243">While you're debugging, hello server is sending data tooVisual Studio, which could affect bandwidth charges.</span></span> <span data-ttu-id="2b4ee-244">대역폭 요금에 대한 자세한 내용은 [Azure 가격 책정](https://azure.microsoft.com/pricing/calculator/)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-244">For information about bandwidth rates, see [Azure Pricing](https://azure.microsoft.com/pricing/calculator/).</span></span>
* <span data-ttu-id="2b4ee-245">해당 hello 있는지 확인 `debug` hello 특성 `compilation` hello 요소 *Web.config* 파일 tootrue 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-245">Make sure that hello `debug` attribute of hello `compilation` element in hello *Web.config* file is set tootrue.</span></span> <span data-ttu-id="2b4ee-246">디버그 빌드 구성을 게시할 때 tootrue 기본적으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-246">It is set tootrue by default when you publish a debug build configuration.</span></span>

        <system.web>
          <compilation debug="true" targetFramework="4.5" />
          <httpRuntime targetFramework="4.5" />
        </system.web>
* <span data-ttu-id="2b4ee-247">해당 hello 디버거 않습니다 toodebug 원하는 코드를 한 단계씩를 찾을 경우 toochange hello 내 코드만 설정을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-247">If you find that hello debugger won't step into code that you want toodebug, you might have toochange hello Just My Code setting.</span></span>  <span data-ttu-id="2b4ee-248">자세한 내용은 참조 [내 코드만 단계별 실행 tooJust 제한](http://msdn.microsoft.com/library/vstudio/y740d9d3.aspx#BKMK_Restrict_stepping_to_Just_My_Code)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-248">For more information, see [Restrict stepping tooJust My Code](http://msdn.microsoft.com/library/vstudio/y740d9d3.aspx#BKMK_Restrict_stepping_to_Just_My_Code).</span></span>
* <span data-ttu-id="2b4ee-249">Hello 원격 디버깅 기능을 사용 하도록 설정 하 고 48 시간 후 hello 기능은 자동으로 해제 되어 hello 서버에서 타이머를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-249">A timer starts on hello server when you enable hello remote debugging feature, and after 48 hours hello feature is automatically turned off.</span></span> <span data-ttu-id="2b4ee-250">이 48시간 제한은 보안 및 성능상의 이유로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-250">This 48 hour limit is done for security and performance reasons.</span></span> <span data-ttu-id="2b4ee-251">원하는 횟수 만큼 다시에 hello 기능을 쉽게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-251">You can easily turn hello feature back on as many times as you like.</span></span> <span data-ttu-id="2b4ee-252">디버깅을 활발히 사용하지 않는 경우 이를 사용하지 않는 상태로 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-252">We recommend leaving it disabled when you are not actively debugging.</span></span>
* <span data-ttu-id="2b4ee-253">Hello 디버거 tooany 프로세스 뿐만 아니라 hello 웹 응용 프로그램 프로세스 (w3wp.exe)를 수동으로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-253">You can manually attach hello debugger tooany process, not only hello web app process (w3wp.exe).</span></span> <span data-ttu-id="2b4ee-254">Toouse 모드 Visual Studio에서 디버깅 하는 방법에 대 한 자세한 내용은 참조 [Visual Studio의 디버깅](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-254">For more information about how toouse debug mode in Visual Studio, see [Debugging in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx).</span></span>

## <span data-ttu-id="2b4ee-255"><a name="logsoverview"></a>진단 로그 개요</span><span class="sxs-lookup"><span data-stu-id="2b4ee-255"><a name="logsoverview"></a>Diagnostic logs overview</span></span>
<span data-ttu-id="2b4ee-256">Azure 웹 앱에서 실행 되는 ASP.NET 응용 프로그램 종류의 로그를 다음 hello를 만들 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="2b4ee-256">An ASP.NET application that runs in an Azure web app can create hello following kinds of logs:</span></span>

* <span data-ttu-id="2b4ee-257">**응용 프로그램 추적 로그**</span><span class="sxs-lookup"><span data-stu-id="2b4ee-257">**Application tracing logs**</span></span><br/>
  <span data-ttu-id="2b4ee-258">hello 응용 프로그램이 로그가 만들어집니다 hello의 메서드를 호출 하 여 [System.Diagnostics.Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-258">hello application creates these logs by calling methods of hello [System.Diagnostics.Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx) class.</span></span>
* <span data-ttu-id="2b4ee-259">**웹 서버 로그**</span><span class="sxs-lookup"><span data-stu-id="2b4ee-259">**Web server logs**</span></span><br/>
  <span data-ttu-id="2b4ee-260">hello 웹 서버는 모든 HTTP 요청 toohello 웹 앱에 대 한 로그 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-260">hello web server creates a log entry for every HTTP request toohello web app.</span></span>
* <span data-ttu-id="2b4ee-261">**자세한 오류 메시지 로그**</span><span class="sxs-lookup"><span data-stu-id="2b4ee-261">**Detailed error message logs**</span></span><br/>
  <span data-ttu-id="2b4ee-262">hello 웹 서버 (상태 코드가 400 이상 하) 실패 한 HTTP 요청에 대 한 몇 가지 추가 정보가 있는 HTML 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-262">hello web server creates an HTML page with some additional information for failed HTTP requests (those that result in status code 400 or greater).</span></span>
* <span data-ttu-id="2b4ee-263">**실패한 요청 추적 로그**</span><span class="sxs-lookup"><span data-stu-id="2b4ee-263">**Failed request tracing logs**</span></span><br/>
  <span data-ttu-id="2b4ee-264">hello 웹 서버는 실패 한 HTTP 요청에 대 한 자세한 추적 정보를 XML 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-264">hello web server creates an XML file with detailed tracing information for failed HTTP requests.</span></span> <span data-ttu-id="2b4ee-265">hello 웹 서버는 XSL 파일 tooformat hello XML 브라우저에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-265">hello web server also provides an XSL file tooformat hello XML in a browser.</span></span>

<span data-ttu-id="2b4ee-266">Azure를 사용 하면 되므로 웹 앱 성능에 영향을, 로깅 기능 tooenable hello 또는 필요에 따라 각 유형의 로그를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-266">Logging affects web app performance, so Azure gives you hello ability tooenable or disable each type of log as needed.</span></span> <span data-ttu-id="2b4ee-267">응용 프로그램 로그의 경우 특정 심각도 수준 이상의 로그만 작성되도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-267">For application logs, you can specify that only logs above a certain severity level should be written.</span></span> <span data-ttu-id="2b4ee-268">새 웹 앱을 만들 때 기본적으로 모든 로깅은 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-268">When you create a new web app, by default all logging is disabled.</span></span>

<span data-ttu-id="2b4ee-269">로그가 기록 toofiles는 *로그 파일이* 웹 응용 프로그램 및 FTP를 통해 액세스할 수는 hello 파일 시스템의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-269">Logs are written toofiles in a *LogFiles* folder in hello file system of your web app and are accessible via FTP.</span></span> <span data-ttu-id="2b4ee-270">웹 서버 로그 및 응용 프로그램 로그를 기록할 수도 tooan Azure 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-270">Web server logs and application logs can also be written tooan Azure Storage account.</span></span> <span data-ttu-id="2b4ee-271">큰 양의 hello 파일 시스템에 가능한 것 보다는 저장소 계정에 로그를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-271">You can retain a greater volume of logs in a storage account than is possible in hello file system.</span></span> <span data-ttu-id="2b4ee-272">Hello 파일 시스템을 사용 하는 경우 100 메가바이트 로그의 최대 제한 tooa 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-272">You're limited tooa maximum of 100 megabytes of logs when you use hello file system.</span></span> <span data-ttu-id="2b4ee-273">참고로, 파일 시스템 로그는 단기 보존용입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-273">(File system logs are only for short-term retention.</span></span> <span data-ttu-id="2b4ee-274">Azure에 사용할 새 이전 로그 파일 toomake 공간 후 삭제 hello 제한에 도달 합니다.)</span><span class="sxs-lookup"><span data-stu-id="2b4ee-274">Azure deletes old log files toomake room for new ones after hello limit is reached.)</span></span>  

## <span data-ttu-id="2b4ee-275"><a name="apptracelogs"></a>응용 프로그램 추적 로그 만들기 및 보기</span><span class="sxs-lookup"><span data-stu-id="2b4ee-275"><a name="apptracelogs"></a>Create and view application trace logs</span></span>
<span data-ttu-id="2b4ee-276">작업이 섹션에서는 다음 작업 hello:</span><span class="sxs-lookup"><span data-stu-id="2b4ee-276">In this section you'll do hello following tasks:</span></span>

* <span data-ttu-id="2b4ee-277">추적 문이 toohello 웹 프로젝트에서 만든 추가 [Azure 및 ASP.NET 시작][GetStarted]합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-277">Add tracing statements toohello web project that you created in [Get started with Azure and ASP.NET][GetStarted].</span></span>
* <span data-ttu-id="2b4ee-278">Hello 프로젝트를 로컬로 실행할 때 hello 로그를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-278">View hello logs when you run hello project locally.</span></span>
* <span data-ttu-id="2b4ee-279">Azure에서 실행 되는 hello 응용 프로그램에 의해 생성 될 때 hello 로그를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-279">View hello logs as they are generated by hello application running in Azure.</span></span>

<span data-ttu-id="2b4ee-280">WebJobs에 toocreate 응용 프로그램을 기록 하는 방법에 대 한 정보를 참조 하십시오. [방법을 사용 하 여 Azure 큐 저장소와 toowork hello WebJobs SDK-toowrite 기록 하는 방법을](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-280">For information about how toocreate application logs in WebJobs, see [How toowork with Azure queue storage using hello WebJobs SDK - How toowrite logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs).</span></span> <span data-ttu-id="2b4ee-281">hello 로그를 확인 하 고 Azure에 저장 하는 방법을 제어 하기 위한 다음 지침도 적용 WebJobs에서 만들어진 tooapplication 로그 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-281">hello following instructions for viewing logs and controlling how they're stored in Azure apply also tooapplication logs created by WebJobs.</span></span>

### <a name="add-tracing-statements-toohello-application"></a><span data-ttu-id="2b4ee-282">추적 문이 toohello 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="2b4ee-282">Add tracing statements toohello application</span></span>
1. <span data-ttu-id="2b4ee-283">열기 *Controllers\HomeController.cs*, 대체 hello 및 `Index`, `About`, 및 `Contact` tooadd 순서에에서 따라 hello 사용 하 여 메서드 코드 `Trace` 문 및 `using` 문 에 대 한 `System.Diagnostics`:</span><span class="sxs-lookup"><span data-stu-id="2b4ee-283">Open *Controllers\HomeController.cs*, and replace hello `Index`, `About`, and `Contact` methods with hello following code in order tooadd `Trace` statements and a `using` statement for `System.Diagnostics`:</span></span>

        public ActionResult Index()
        {
            Trace.WriteLine("Entering Index method");
            ViewBag.Message = "Modify this template toojump-start your ASP.NET MVC application.";
            Trace.TraceInformation("Displaying hello Index page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Index method");
            return View();
        }

        public ActionResult About()
        {
            Trace.WriteLine("Entering About method");
            ViewBag.Message = "Your app description page.";
            Trace.TraceWarning("Transient error on hello About page at " + DateTime.Now.ToShortTimeString());
            Trace.WriteLine("Leaving About method");
            return View();
        }

        public ActionResult Contact()
        {
            Trace.WriteLine("Entering Contact method");
            ViewBag.Message = "Your contact page.";
            Trace.TraceError("Fatal error on hello Contact page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Contact method");
            return View();
        }        
2. <span data-ttu-id="2b4ee-284">추가 `using System.Diagnostics;` hello 파일의 문 toohello 맨 위로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-284">Add a `using System.Diagnostics;` statement toohello top of hello file.</span></span>

### <a name="view-hello-tracing-output-locally"></a><span data-ttu-id="2b4ee-285">로컬에서 출력 보기 hello 추적</span><span class="sxs-lookup"><span data-stu-id="2b4ee-285">View hello tracing output locally</span></span>
1. <span data-ttu-id="2b4ee-286">F5 toorun hello 응용 프로그램 키를 눌러 디버그 모드에서.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-286">Press F5 toorun hello application in debug mode.</span></span>

    <span data-ttu-id="2b4ee-287">hello 기본 추적 수신기 작성 모든 추적 출력 toohello **출력** 함께 다른 디버그 출력 창.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-287">hello default trace listener writes all trace output toohello **Output** window, along with other Debug output.</span></span> <span data-ttu-id="2b4ee-288">hello 다음 그림과 hello hello 출력 toohello 추가한 추적 문을 `Index` 메서드.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-288">hello following illustration shows hello output from hello trace statements that you added toohello `Index` method.</span></span>

    ![디버그 창의 추적](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugtracing.png)

    <span data-ttu-id="2b4ee-290">단계를 수행 하는 hello tooview 추적 웹 페이지에서 디버그 모드에서 컴파일하면 하지 않고 출력 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-290">hello following steps show how tooview trace output in a web page, without compiling in debug mode.</span></span>
2. <span data-ttu-id="2b4ee-291">Hello 응용 프로그램 Web.config 파일 (hello hello 프로젝트 폴더에 있는 하나)를 열고 추가 된 `<system.diagnostics>` hello hello 닫기 바로 전에 hello 파일 끝에 요소 `</configuration>` 요소:</span><span class="sxs-lookup"><span data-stu-id="2b4ee-291">Open hello application Web.config file (hello one located in hello project folder) and add a `<system.diagnostics>` element at hello end of hello file just before hello closing `</configuration>` element:</span></span>

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

    <span data-ttu-id="2b4ee-292">hello `WebPageTraceListener` 너무 이동 하 여 추적 출력을 볼 수 있으며`/trace.axd`합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-292">hello `WebPageTraceListener` lets you view trace output by browsing too`/trace.axd`.</span></span>
3. <span data-ttu-id="2b4ee-293">추가 <a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">trace 요소</a> 아래 `<system.web>` hello 다음 예제 처럼 hello Web.config 파일에서:</span><span class="sxs-lookup"><span data-stu-id="2b4ee-293">Add a <a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">trace element</a> under `<system.web>` in hello Web.config file, such as hello following example:</span></span>

        <trace enabled="true" writeToDiagnosticsTrace="true" mostRecent="true" pageOutput="false" />
4. <span data-ttu-id="2b4ee-294">CTRL + f 5 toorun hello 응용 프로그램 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-294">Press CTRL+F5 toorun hello application.</span></span>
5. <span data-ttu-id="2b4ee-295">Hello hello 브라우저 창의 주소 표시줄에 추가 *trace.axd* toohello URL 입력 (hello URL이 비슷한 toohttp://localhost:53370/trace.axd 수 없음).</span><span class="sxs-lookup"><span data-stu-id="2b4ee-295">In hello address bar of hello browser window, add *trace.axd* toohello URL, and then press Enter (hello URL will be similar toohttp://localhost:53370/trace.axd).</span></span>
6. <span data-ttu-id="2b4ee-296">Hello에 **응용 프로그램 추적** 페이지 **세부 정보 보기** hello 첫 번째 줄 (하지 hello BrowserLink 선)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-296">On hello **Application Trace** page, click **View Details** on hello first line (not hello BrowserLink line).</span></span>

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd1.png)

    <span data-ttu-id="2b4ee-298">hello **요청 세부 사항** 페이지가 표시 되 면 및 hello **추적 정보** toohello 추가한 hello trace 문의 출력 hello 섹션 `Index` 메서드.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-298">hello **Request Details** page appears, and in hello **Trace Information** section you see hello output from hello trace statements that you added toohello `Index` method.</span></span>

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd2.png)

    <span data-ttu-id="2b4ee-300">기본적으로 `trace.axd` 는 로컬에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-300">By default, `trace.axd` is only available locally.</span></span> <span data-ttu-id="2b4ee-301">Toomake 하려는 경우 원격 웹 앱에서 사용할 수 있는 것을 추가할 수 있습니다 `localOnly="false"` toohello `trace` hello 요소 *Web.config* hello 다음 예제와 같이 파일:</span><span class="sxs-lookup"><span data-stu-id="2b4ee-301">If you wanted toomake it available from a remote web app, you could add `localOnly="false"` toohello `trace` element in hello *Web.config* file, as shown in hello following example:</span></span>

        <trace enabled="true" writeToDiagnosticsTrace="true" localOnly="false" mostRecent="true" pageOutput="false" />

    <span data-ttu-id="2b4ee-302">그러나 사용 `trace.axd` 프로덕션에서 웹 앱은 일반적으로 권장 되지 보안상의 이유로 및 hello 다음 섹션에에서는 추적 로그는 Azure 웹 앱에는 쉽게 방법은 tooread 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-302">However, enabling `trace.axd` in a production web app is generally not recommended for security reasons, and in hello following sections you'll see an easier way tooread tracing logs in an Azure web app.</span></span>

### <a name="view-hello-tracing-output-in-azure"></a><span data-ttu-id="2b4ee-303">Azure의 hello 추적 출력을 보려면</span><span class="sxs-lookup"><span data-stu-id="2b4ee-303">View hello tracing output in Azure</span></span>
1. <span data-ttu-id="2b4ee-304">**솔루션 탐색기**hello 웹 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-304">In **Solution Explorer**, right-click hello web project and click **Publish**.</span></span>
2. <span data-ttu-id="2b4ee-305">Hello에 **웹 게시** 대화 상자를 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-305">In hello **Publish Web** dialog box, click **Publish**.</span></span>

    <span data-ttu-id="2b4ee-306">브라우저 창 tooyour 홈 페이지를 열고 Visual Studio가 업데이트를 게시 한 후 (선택 취소 하지 않은 것으로 가정 **대상 URL** hello에 **연결** 탭).</span><span class="sxs-lookup"><span data-stu-id="2b4ee-306">After Visual Studio publishes your update, it opens a browser window tooyour home page (assuming you didn't clear **Destination URL** on hello **Connection** tab).</span></span>
3. <span data-ttu-id="2b4ee-307">**서버 탐색기**에서 웹앱을 마우스 오른쪽 단추로 클릭하고 **스트리밍 로그 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-307">In **Server Explorer**, right-click your web app and select **View Streaming Logs**.</span></span>

    ![상황에 맞는 메뉴의 스트리밍 로그 보기](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewlogsmenu.png)

    <span data-ttu-id="2b4ee-309">hello **출력** 창에 표시에 있는 연결 된 toohello 로그 스트리밍 서비스를 마우스 선을 추가 하는 알림 로그 toodisplay 없이 이동 하는 분 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-309">hello **Output** window shows that you are connected toohello log-streaming service, and adds a notification line each minute that goes by without a log toodisplay.</span></span>

    ![상황에 맞는 메뉴의 스트리밍 로그 보기](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-nologsyet.png)
4. <span data-ttu-id="2b4ee-311">응용 프로그램 홈 페이지를 보여 주는 hello 브라우저 창에서 클릭 **연락처**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-311">In hello browser window that shows your application home page, click **Contact**.</span></span>

    <span data-ttu-id="2b4ee-312">추가한 toohello hello 오류 수준 추적에서 출력 하는 몇 초 hello 내 `Contact` 메서드가 hello에 표시 되는 **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-312">Within a few seconds hello output from hello error-level trace you added toohello `Contact` method appears in hello **Output** window.</span></span>

    ![출력 창의 오류 추적](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-errortrace.png)

    <span data-ttu-id="2b4ee-314">Visual Studio hello 로그 서비스 모니터링을 사용 하도록 설정 하면 hello 기본 설정 이기 때문에 오류 수준 추적을 데이터만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-314">Visual Studio is only showing error-level traces because that is hello default setting when you enable hello log monitoring service.</span></span> <span data-ttu-id="2b4ee-315">새 Azure 웹 앱을 만들 때 이전 hello 설정 페이지를 열어 본 것 처럼 모든 로깅은 기본적으로 비활성화 되어:</span><span class="sxs-lookup"><span data-stu-id="2b4ee-315">When you create a new Azure web app, all logging is disabled by default, as you saw when you opened hello settings page earlier:</span></span>

    ![응용 프로그램 로깅 끄기](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-apploggingoff.png)

    <span data-ttu-id="2b4ee-317">그러나 선택한 경우 **스트리밍 로그 보기**, 자동으로 변경 하는 Visual Studio **응용 프로그램 Logging(File System)** 너무**오류**, 즉, 오류 수준 로그 보고 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-317">However, when you selected **View Streaming Logs**, Visual Studio automatically changed **Application Logging(File System)** too**Error**, which means error-level logs get reported.</span></span> <span data-ttu-id="2b4ee-318">모든 추적 로그 toosee 순서, 너무이 설정을 변경할 수 있습니다**Verbose**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-318">In order toosee all of your tracing logs, you can change this setting too**Verbose**.</span></span> <span data-ttu-id="2b4ee-319">심각도 수준을 오류보다 낮은 수준으로 선택하면 그보다 더 높은 심각도 수준의 모든 로그가 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-319">When you select a severity level lower than error, all logs for higher severity levels are also reported.</span></span> <span data-ttu-id="2b4ee-320">따라서 자세한 정보 표시를 선택하는 경우 정보, 경고 및 오류 로그도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-320">So when you select verbose, you also see information, warning, and error logs.</span></span>  

1. <span data-ttu-id="2b4ee-321">**서버 탐색기**hello 웹 응용 프로그램을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **설정 보기** 앞에서 수행한 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-321">In **Server Explorer**, right-click hello web app, and then click **View Settings** as you did earlier.</span></span>
2. <span data-ttu-id="2b4ee-322">변경 **응용 프로그램 로깅 (파일 시스템)** 너무**Verbose**, 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-322">Change **Application Logging (File System)** too**Verbose**, and then click **Save**.</span></span>

    ![추적 수준 tooVerbose 설정](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-applogverbose.png)
3. <span data-ttu-id="2b4ee-324">이제을 표시 하는 hello 브라우저 창에서 프로그램 **연락처** 페이지 **홈**, 클릭 **에 대 한**, 클릭 하 고 **연락처**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-324">In hello browser window that is now showing your **Contact** page, click **Home**, then click **About**, and then click **Contact**.</span></span>

    <span data-ttu-id="2b4ee-325">몇 초 안에 hello **출력** 창 모든 추적 출력을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-325">Within a few seconds, hello **Output** window shows all of your tracing output.</span></span>

    ![자세한 정보 표시 추적 출력](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-verbosetraces.png)

    <span data-ttu-id="2b4ee-327">이 섹션에서는 Azure 웹 앱 설정을 사용하여 로깅을 사용 및 사용하지 않도록 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-327">In this section you enabled and disabled logging by using Azure web app settings.</span></span> <span data-ttu-id="2b4ee-328">사용 하도록 설정 하 고 hello Web.config 파일을 수정 하 여 추적 수신기를 사용 하지 않도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-328">You can also enable and disable trace listeners by modifying hello Web.config file.</span></span> <span data-ttu-id="2b4ee-329">그러나, hello Web.config 파일을 수정 하는 수행 하지 않는 hello 웹 응용 프로그램 구성을 통해 로깅을 사용 하는 동안 hello 응용 프로그램 도메인 toorecycle를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-329">However, modifying hello Web.config file causes hello app domain toorecycle, while enabling logging via hello web app configuration doesn't do that.</span></span> <span data-ttu-id="2b4ee-330">Hello 문제는 시간이 오래 tooreproduce 또는 간헐적으로 발생 하는 경우 "수정" 및 toowait 강제로 다시 발생 하면 될 때까지 수 hello 응용 프로그램 도메인을 재활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-330">If hello problem takes a long time tooreproduce, or is intermittent, recycling hello app domain might "fix" it and force you toowait until it happens again.</span></span> <span data-ttu-id="2b4ee-331">Azure에서 진단을 사용하도록 설정하면 이러한 상황이 발생하지 않으므로 오류 정보를 즉시 캡처하기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-331">Enabling diagnostics in Azure doesn't do this, so you can start capturing error information immediately.</span></span>

### <a name="output-window-features"></a><span data-ttu-id="2b4ee-332">출력 창 기능</span><span class="sxs-lookup"><span data-stu-id="2b4ee-332">Output window features</span></span>
<span data-ttu-id="2b4ee-333">hello **Azure 로그** hello 탭 **출력** 창에 여러 단추와 텍스트 상자:</span><span class="sxs-lookup"><span data-stu-id="2b4ee-333">hello **Azure Logs** tab of hello **Output** Window has several buttons and a text box:</span></span>

![로그 탭의 단추](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-icons.png)

<span data-ttu-id="2b4ee-335">이러한 함수를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-335">These perform hello following functions:</span></span>

* <span data-ttu-id="2b4ee-336">지우기 hello **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-336">Clear hello **Output** window.</span></span>
* <span data-ttu-id="2b4ee-337">자동 줄 바꿈을 사용 또는 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-337">Enable or disable word wrap.</span></span>
* <span data-ttu-id="2b4ee-338">로그 모니터링을 시작 또는 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-338">Start or stop monitoring logs.</span></span>
* <span data-ttu-id="2b4ee-339">지정 합니다. toomonitor를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-339">Specify which logs toomonitor.</span></span>
* <span data-ttu-id="2b4ee-340">로그를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-340">Download logs.</span></span>
* <span data-ttu-id="2b4ee-341">검색 문자열 또는 정규식을 기반으로 로그를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-341">Filter logs based on a search string or a regular expression.</span></span>
* <span data-ttu-id="2b4ee-342">닫기 hello **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-342">Close hello **Output** window.</span></span>

<span data-ttu-id="2b4ee-343">검색 문자열 또는 정규식을 입력 하면 Visual Studio hello 클라이언트에서 로깅 정보를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-343">If you enter a search string or regular expression, Visual Studio filters logging information at hello client.</span></span> <span data-ttu-id="2b4ee-344">즉, hello 로그 hello에 표시 된 후 hello 조건을 입력할 수 있습니다 **출력** 창과 있습니다 tooregenerate hello 로그 필요 없이 필터링 조건을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-344">That means you can enter hello criteria after hello logs are displayed in hello **Output** window and you can change filtering criteria without having tooregenerate hello logs.</span></span>

## <span data-ttu-id="2b4ee-345"><a name="webserverlogs"></a>웹 서버 로그 보기</span><span class="sxs-lookup"><span data-stu-id="2b4ee-345"><a name="webserverlogs"></a>View web server logs</span></span>
<span data-ttu-id="2b4ee-346">웹 서버 로그 hello 웹 앱에 대 한 모든 HTTP 작업을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-346">Web server logs record all HTTP activity for hello web app.</span></span> <span data-ttu-id="2b4ee-347">순서 toosee에 hello에서 해당 **출력** tooenable hello에 대 한 웹 앱 및 Visual Studio에 지시할 toomonitor 원하는 있는 창에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-347">In order toosee them in hello **Output** window you have tooenable them for hello web app and tell Visual Studio that you want toomonitor them.</span></span>

1. <span data-ttu-id="2b4ee-348">Hello에 **Azure 웹 앱 구성** 탭에서 연 **서버 탐색기**, 웹 서버 로깅도 변경**에**, 클릭 하 고 **저장**.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-348">In hello **Azure Web App Configuration** tab that you opened from **Server Explorer**, change Web Server Logging too**On**, and then click **Save**.</span></span>

    ![웹 서버 로깅 사용](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-webserverloggingon.png)
2. <span data-ttu-id="2b4ee-350">Hello에 **출력** 창의 hello 클릭 **는 Azure 로그 toomonitor 지정** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-350">In hello **Output** Window, click hello **Specify which Azure logs toomonitor** button.</span></span>

    ![Azure 로그 toomonitor 지정](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-specifylogs.png)
3. <span data-ttu-id="2b4ee-352">Hello에 **Azure 로깅 옵션** 대화 상자에서 **웹 서버 로그**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-352">In hello **Azure Logging Options** dialog box, select **Web server logs**, and then click **OK**.</span></span>

    ![웹 서버 로그 모니터링](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorwslogson.png)
4. <span data-ttu-id="2b4ee-354">Hello 웹 응용 프로그램을 보여 주는 hello 브라우저 창에서 클릭 **홈**, 클릭 **에 대 한**, 클릭 하 고 **연락처**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-354">In hello browser window that shows hello web app, click **Home**, then click **About**, and then click **Contact**.</span></span>

    <span data-ttu-id="2b4ee-355">hello 응용 프로그램 로그는 일반적으로 표시, 첫 번째 hello 웹 서버 로그가 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-355">hello application logs generally appear first, followed by hello web server logs.</span></span> <span data-ttu-id="2b4ee-356">Toowait 해야할 hello에 대 한 시간이 tooappear를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-356">You might have toowait a while for hello logs tooappear.</span></span>

    ![출력 창의 웹 서버 로그](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-wslogs.png)

<span data-ttu-id="2b4ee-358">기본적으로 Visual Studio를 사용 하 여 웹 서버 로그를 처음 사용 하는 경우 Azure hello 로그 toohello 파일 시스템을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-358">By default, when you first enable web server logs by using Visual Studio, Azure writes hello logs toohello file system.</span></span> <span data-ttu-id="2b4ee-359">사용 하 여 hello Azure 서버 로그를 웹 포털 toospecify 쓸지 tooa blob 컨테이너는 저장소 계정에 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-359">As an alternative, you can use hello Azure portal toospecify that web server logs should be written tooa blob container in a storage account.</span></span>

<span data-ttu-id="2b4ee-360">Hello 포털 tooenable 웹 서버 로깅 tooan Azure 저장소 계정을 사용 하 고 다음 Visual Studio에서 로깅을 다시 사용 하는 경우 Visual Studio에서 로깅을 사용 하지 않도록 설정 하는 경우 저장소 계정 설정은 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-360">If you use hello portal tooenable web server logging tooan Azure storage account, and then disable logging in Visual Studio, when you re-enable logging in Visual Studio your storage account settings are restored.</span></span>

## <span data-ttu-id="2b4ee-361"><a name="detailederrorlogs"></a>자세한 오류 메시지 로그 보기</span><span class="sxs-lookup"><span data-stu-id="2b4ee-361"><a name="detailederrorlogs"></a>View detailed error message logs</span></span>
<span data-ttu-id="2b4ee-362">자세한 오류 로그에서는 오류 응답 코드(400 이상)를 유발한 HTTP 요청과 관련된 일부 추가 정보가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-362">Detailed error logs provide some additional information about HTTP requests that result in error response codes (400 or above).</span></span> <span data-ttu-id="2b4ee-363">순서 toosee에 hello에서 해당 **출력** tooenable hello에 대 한 웹 앱 및 Visual Studio에 지시할 toomonitor 원하는 있는 창에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-363">In order toosee them in hello **Output** window, you have tooenable them for hello web app and tell Visual Studio that you want toomonitor them.</span></span>

1. <span data-ttu-id="2b4ee-364">Hello에 **Azure 웹 앱 구성** 탭에서 연 **서버 탐색기**, 변경 **자세한 오류 메시지** 너무**에**, 및 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-364">In hello **Azure Web App Configuration** tab that you opened from **Server Explorer**, change **Detailed Error Messages** too**On**, and then click **Save**.</span></span>

    ![자세한 오류 메시지 사용](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailedlogson.png)
2. <span data-ttu-id="2b4ee-366">Hello에 **출력** 창의 hello 클릭 **는 Azure 로그 toomonitor 지정** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-366">In hello **Output** Window, click hello **Specify which Azure logs toomonitor** button.</span></span>
3. <span data-ttu-id="2b4ee-367">Hello에 **Azure 로깅 옵션** 대화 상자를 클릭 **모든 로그**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-367">In hello **Azure Logging Options** dialog box, click **All logs**, and then click **OK**.</span></span>

    ![모든 로그 모니터링](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorall.png)
4. <span data-ttu-id="2b4ee-369">Hello hello 브라우저 창의 주소 표시줄에 추가할 추가 문자가 toohello URL toocause 404 오류 (예를 들어 `http://localhost:53370/Home/Contactx`), Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-369">In hello address bar of hello browser window, add an extra character toohello URL toocause a 404 error (for example, `http://localhost:53370/Home/Contactx`), and press Enter.</span></span>

    <span data-ttu-id="2b4ee-370">몇 초 정도 hello 자세한 오류 로그에도 Visual Studio hello 나타납니다 **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-370">After several seconds hello detailed error log appears in hello Visual Studio **Output** window.</span></span>

    ![출력 창의 자세한 오류 로그](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorlog.png)

    <span data-ttu-id="2b4ee-372">제어 + 브라우저로 서식이 지정 된 hello 링크 toosee hello 로그 출력을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-372">Control+click hello link toosee hello log output formatted in a browser:</span></span>

    ![브라우저 창의 자세한 오류 로그](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorloginbrowser.png)

## <span data-ttu-id="2b4ee-374"><a name="downloadlogs"></a>파일 시스템 로그 다운로드</span><span class="sxs-lookup"><span data-stu-id="2b4ee-374"><a name="downloadlogs"></a>Download file system logs</span></span>
<span data-ttu-id="2b4ee-375">Hello에서 모니터링할 수 있는 모든 로그 **출력** 창으로 다운로드할 수도 있습니다는 *.zip* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-375">Any logs that you can monitor in hello **Output** window can also be downloaded as a *.zip* file.</span></span>

1. <span data-ttu-id="2b4ee-376">Hello에 **출력** 창 클릭 **스트리밍 로그 다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-376">In hello **Output** window, click **Download Streaming Logs**.</span></span>

    ![로그 탭의 단추](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadicon.png)

    <span data-ttu-id="2b4ee-378">파일 탐색기가 열리면 tooyour *다운로드* hello로 폴더 선택한 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-378">File Explorer opens tooyour *Downloads* folder with hello downloaded file selected.</span></span>

    ![다운로드한 파일](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadedfile.png)
2. <span data-ttu-id="2b4ee-380">Hello 추출 *.zip* 파일, 표시 폴더 구조를 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="2b4ee-380">Extract hello *.zip* file, and you see hello following folder structure:</span></span>

    ![다운로드한 파일](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilefolders.png)

   * <span data-ttu-id="2b4ee-382">응용 프로그램 추적 로그에는 *.txt* hello에 대 한 파일 *LogFiles\Application* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-382">Application tracing logs are in *.txt* files in hello *LogFiles\Application* folder.</span></span>
   * <span data-ttu-id="2b4ee-383">웹 서버 로그에는 *.log* hello에 대 한 파일 *LogFiles\http\RawLogs* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-383">Web server logs are in *.log* files in hello *LogFiles\http\RawLogs* folder.</span></span> <span data-ttu-id="2b4ee-384">와 같은 도구를 사용할 수 [로그 구문 분석기](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659) tooview 및 이러한 파일을 조작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-384">You can use a tool such as [Log Parser](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659) tooview and manipulate these files.</span></span>
   * <span data-ttu-id="2b4ee-385">자세한 오류 메시지 로그에는 *.html* hello에 대 한 파일 *LogFiles\DetailedErrors* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-385">Detailed error message logs are in *.html* files in hello *LogFiles\DetailedErrors* folder.</span></span>

     <span data-ttu-id="2b4ee-386">(hello *배포* 폴더 게시; 소스 제어에서 만든 파일에는 모두 관련된 tooVisual Studio 게시 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-386">(hello *deployments* folder is for files created by source control publishing; it doesn't have anything related tooVisual Studio publishing.</span></span> <span data-ttu-id="2b4ee-387">hello *Git* 추적 관련된 toosource 제어 게시 및 hello 로그 파일 스트리밍 서비스에 대 한 폴더는입니다.)</span><span class="sxs-lookup"><span data-stu-id="2b4ee-387">hello *Git* folder is for traces related toosource control publishing and hello log file streaming service.)</span></span>  

## <span data-ttu-id="2b4ee-388"><a name="storagelogs"></a>저장소 로그 보기</span><span class="sxs-lookup"><span data-stu-id="2b4ee-388"><a name="storagelogs"></a>View storage logs</span></span>
<span data-ttu-id="2b4ee-389">응용 프로그램 추적 로그를 보낼 수 있습니다 tooan Azure 저장소 계정 및 Visual Studio에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-389">Application tracing logs can also be sent tooan Azure storage account, and you can view them in Visual Studio.</span></span> <span data-ttu-id="2b4ee-390">toodo 합니다 저장소 계정 만들기, hello 클래식 포털의 저장소 로그를 사용 하도록 설정 하는 hello에서 볼 **로그** hello 탭 **Azure 웹 앱** 창.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-390">toodo that you'll create a storage account, enable storage logs in hello classic portal, and view them in hello **Logs** tab of hello **Azure Web App** window.</span></span>

<span data-ttu-id="2b4ee-391">3 가지 대상의 전체 또는 로그 tooany를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-391">You can send logs tooany or all of three destinations:</span></span>

* <span data-ttu-id="2b4ee-392">hello 파일 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-392">hello file system.</span></span>
* <span data-ttu-id="2b4ee-393">저장소 계정 테이블</span><span class="sxs-lookup"><span data-stu-id="2b4ee-393">Storage account tables.</span></span>
* <span data-ttu-id="2b4ee-394">저장소 계정 Blob</span><span class="sxs-lookup"><span data-stu-id="2b4ee-394">Storage account blobs.</span></span>

<span data-ttu-id="2b4ee-395">각 대상마다 서로 다른 심각도 수준을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-395">You can specify a different severity level for each destination.</span></span>

<span data-ttu-id="2b4ee-396">테이블의 로그를 온라인으로 쉽게 tooview 세부 정보 지정 하 고 스트리밍; 지원 테이블에 있는 로그를 쿼리할 수 있으며 생성 될 때 새 로그를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-396">Tables make it easy tooview details of logs online, and they support streaming; you can query logs in tables and see new logs as they are being created.</span></span> <span data-ttu-id="2b4ee-397">Blob 쉽게 toodownload 로그에서 만들 파일 및 tooanalyze HDInsight 알기 때문에 HDInsight를 통해 어떻게 toowork blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-397">Blobs make it easy toodownload logs in files and tooanalyze them using HDInsight, because HDInsight knows how toowork with blob storage.</span></span> <span data-ttu-id="2b4ee-398">자세한 내용은 [데이터 저장소 옵션(Azure에서 실제 클라우드 앱 빌드)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options)에서 **Hadoop 및 MapReduce**를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-398">For more information, see **Hadoop and MapReduce** in [Data Storage Options (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options).</span></span>

<span data-ttu-id="2b4ee-399">현재 파일 시스템 로그 집합 tooverbose 수준;가 hello 다음 단계에 관한 정보 수준의 로그 toogo toostorage 계정 테이블을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-399">You currently have file system logs set tooverbose level; hello following steps walk you through setting up information level logs toogo toostorage account tables.</span></span> <span data-ttu-id="2b4ee-400">정보 수준이란 `Trace.WriteLine`을 호출하여 생성된 로그를 제외하고 `Trace.TraceInformation`, `Trace.TraceWarning` 및 `Trace.TraceError`를 호출하여 생성된 모든 로그가 표시됨을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-400">Information level means all logs created by calling `Trace.TraceInformation`, `Trace.TraceWarning`, and `Trace.TraceError` will be displayed, but not logs created by calling `Trace.WriteLine`.</span></span>

<span data-ttu-id="2b4ee-401">저장소 계정을 더 많은 디스크 공간과 로그에 대 한 오래 보존 비교 toohello 파일 시스템을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-401">Storage accounts offer more storage and longer-lasting retention for logs compared toohello file system.</span></span> <span data-ttu-id="2b4ee-402">추적 로그 toostorage 보내는 응용 프로그램의 또 다른 이점은 적용 되는 파일 시스템 로그에서 볼 수 없는 각 로그에 몇 가지 추가 정보를 가져올 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-402">Another advantage of sending application tracing logs toostorage is that you get some additional information with each log that you don't get from file system logs.</span></span>

1. <span data-ttu-id="2b4ee-403">마우스 오른쪽 단추로 클릭 **저장소** 아래에서 Azure 노드를 hello 및 클릭 **저장소 계정 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-403">Right-click **Storage** under hello Azure node, and then click **Create Storage Account**.</span></span>

![저장소 계정 만들기](./media/web-sites-dotnet-troubleshoot-visual-studio/createstor.png)

1. <span data-ttu-id="2b4ee-405">Hello에 **저장소 계정 만들기** 대화 상자에서 hello 저장소 계정의 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-405">In hello **Create Storage Account** dialog, enter a name for hello storage account.</span></span>

    <span data-ttu-id="2b4ee-406">hello 이름은 고유 해야 합니다 (다른 Azure 저장소 계정이 없으면 hello 점이 동일한 이름).</span><span class="sxs-lookup"><span data-stu-id="2b4ee-406">hello name must be must be unique (no other Azure storage account can have hello same name).</span></span> <span data-ttu-id="2b4ee-407">입력 한 hello 이름이 이미 사용 중이면 얻게 됩니다 기회 toochange 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-407">If hello name you enter is already in use you'll get a chance toochange it.</span></span>

    <span data-ttu-id="2b4ee-408">저장소 계정 수 URL tooaccess hello *{name}*. core.windows.net 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-408">hello URL tooaccess your storage account will be *{name}*.core.windows.net.</span></span>
2. <span data-ttu-id="2b4ee-409">집합 hello **지역 또는 선호도 그룹** 드롭 다운 목록 toohello 영역에 대 한 가장 가까운 tooyou 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-409">Set hello **Region or Affinity Group** drop-down list toohello region closest tooyou.</span></span>

    <span data-ttu-id="2b4ee-410">이 설정은 저장소 계정을 호스트할 Azure 데이터 센터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-410">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="2b4ee-411">이 자습서에 대 한 사용자가 선택한 눈에 띄는 차이점이 확인 되지 않습니다 되지만 웹 서버 및 사용자 저장소 계정 toobe hello에 원하는 프로덕션 웹 앱에 대 한 동일한 지역 toominimize 대기 시간 및 데이터 요금을 송신 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-411">For this tutorial your choice won't make a noticeable difference, but for a production web app you want your web server and your storage account toobe in hello same region toominimize latency and data egress charges.</span></span> <span data-ttu-id="2b4ee-412">hello 웹 앱 (나중에 만들) 순서 toominimize 대기 시간에 웹 앱에 액세스 가능한 toohello 브라우저와 가까운 지역에서 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-412">hello web app (which you'll create later) should run in a region as close as possible toohello browsers accessing your web app in order toominimize latency.</span></span>
3. <span data-ttu-id="2b4ee-413">집합 hello **복제** 드롭 다운 목록 너무**로컬 중복**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-413">Set hello **Replication** drop-down list too**Locally redundant**.</span></span>
   
    <span data-ttu-id="2b4ee-414">저장소 계정에 대 한 지리적 복제를 사용 하는 경우 저장 된 hello 콘텐츠 hello 기본 위치에서 중요 재해가 발생 한 경우 복제 된 tooa 보조 데이터 센터 tooenable 장애 조치 toothat 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-414">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover toothat location in case of a major disaster in hello primary location.</span></span> <span data-ttu-id="2b4ee-415">지역에서 복제는 추가 비용을 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-415">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="2b4ee-416">테스트 및 개발 계정에 대 한 일반적으로 원하지 toopay 지리적 복제에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-416">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="2b4ee-417">자세한 내용은 [저장소 계정 만들기, 관리 또는 삭제](../storage/common/storage-create-storage-account.md)를 참조하세요</span><span class="sxs-lookup"><span data-stu-id="2b4ee-417">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
4. <span data-ttu-id="2b4ee-418">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-418">Click **Create**.</span></span>

    ![새 저장소 계정](./media/web-sites-dotnet-troubleshoot-visual-studio/newstorage.png)    
5. <span data-ttu-id="2b4ee-420">Hello Visual Studio에서에서 **Azure 웹 앱** 창의 hello 클릭 **로그** 탭을 클릭 한 다음 **관리 포털에서 로깅 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-420">In hello Visual Studio **Azure Web App** window, click hello **Logs** tab, and then click **Configure Logging in Management Portal**.</span></span>

    <!-- todo:screenshot of new portal if hello VS page link goes toonew portal -->
    ![로깅 구성](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configlogging.png)

    <span data-ttu-id="2b4ee-422">Hello 열립니다 **구성** 웹 앱에 대 한 hello 클래식 포털의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-422">This opens hello **Configure** tab in hello classic portal for your web app.</span></span>
6. <span data-ttu-id="2b4ee-423">Hello 클래식 포털에서 **구성** 탭을 toohello 응용 프로그램 진단 섹션에서 아래로 스크롤하여 한 다음 변경 **응용 프로그램 로깅 (테이블 저장소)** 너무**에**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-423">In hello classic portal's **Configure** tab, scroll down toohello application diagnostics section, and then change **Application Logging (Table Storage)** too**On**.</span></span>
7. <span data-ttu-id="2b4ee-424">변경 **로깅 수준** 너무**정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-424">Change **Logging Level** too**Information**.</span></span>
8. <span data-ttu-id="2b4ee-425">**Manage Table Storage**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-425">Click **Manage Table Storage**.</span></span>

    ![Manage Table Storage 클릭](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-stgsettingsmgmtportal.png)

    <span data-ttu-id="2b4ee-427">Hello에 **응용 프로그램 진단 위한 테이블 저장소 관리** 상자 여러 개 있는 경우 저장소 계정의 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-427">In hello **Manage table storage for application diagnostics** box, you can choose your storage account if you have more than one.</span></span> <span data-ttu-id="2b4ee-428">새 테이블을 만들거나 기존 테이블을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-428">You can create a new table or use an existing one.</span></span>

    ![Manage Table Storage](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-choosestorageacct.png)
9. <span data-ttu-id="2b4ee-430">Hello에 **응용 프로그램 진단 위한 테이블 저장소 관리** 상자 hello 확인 표시가 tooclose hello 상자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-430">In hello **Manage table storage for application diagnostics** box click hello check mark tooclose hello box.</span></span>
10. <span data-ttu-id="2b4ee-431">Hello 클래식 포털에서 **구성** 탭을 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-431">In hello classic portal's **Configure** tab, click **Save**.</span></span>
11. <span data-ttu-id="2b4ee-432">Hello 응용 프로그램 웹 응용 프로그램을 표시 하는 hello 브라우저 창에서 클릭 **홈**, 클릭 **에 대 한**, 클릭 하 고 **연락처**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-432">In hello browser window that displays hello application web app, click **Home**, then click **About**, and then click **Contact**.</span></span>

     <span data-ttu-id="2b4ee-433">이러한 웹 페이지를 탐색 하 여 생성 한 hello 로깅 정보 toohello 저장소 계정을 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-433">hello logging information produced by browsing these web pages will be written toohello storage account.</span></span>
12. <span data-ttu-id="2b4ee-434">Hello에 **로그** hello 탭 **Azure 웹 앱** Visual Studio에서 창을 클릭 **새로 고침** 아래 **진단 요약**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-434">In hello **Logs** tab of hello **Azure Web App** window in Visual Studio, click **Refresh** under **Diagnostic Summary**.</span></span>

     ![새로 고침 클릭](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-refreshstorage.png)

     <span data-ttu-id="2b4ee-436">hello **진단 요약** 섹션 hello에 대 한 로그 지난 15 분 동안 기본적으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-436">hello **Diagnostic Summary** section shows logs for hello last 15 minutes by default.</span></span> <span data-ttu-id="2b4ee-437">더 많은 로그 hello 기간 toosee를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-437">You can change hello period toosee more logs.</span></span>

     <span data-ttu-id="2b4ee-438">("테이블을 찾을 수 없습니다" 오류가 발생할 경우 확인 사용 하도록 설정한 후에 추적 hello 않는 toohello 페이지를 검색할 **응용 프로그램 로깅 (저장소)** 클릭 한 후 **저장**.)</span><span class="sxs-lookup"><span data-stu-id="2b4ee-438">(If you get a "table not found" error, verify that you browsed toohello pages that do hello tracing after you enabled **Application Logging (Storage)** and after you clicked **Save**.)</span></span>

     ![저장소 로그](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-storagelogs.png)

     <span data-ttu-id="2b4ee-440">이 보기는 통지 참조 **프로세스 ID** 및 **스레드 ID** hello 파일 시스템 로그에서 얻지 못할 각 로그에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-440">Notice that in this view you see **Process ID** and **Thread ID** for each log, which you don't get in hello file system logs.</span></span> <span data-ttu-id="2b4ee-441">Hello Azure 저장소 테이블을 직접 확인 하 여 추가 필드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-441">You can see additional fields by viewing hello Azure storage table directly.</span></span>
13. <span data-ttu-id="2b4ee-442">**View all application logs**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-442">Click **View all application logs**.</span></span>

     <span data-ttu-id="2b4ee-443">hello 추적 로그 테이블 hello Azure 저장소 테이블 뷰어에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-443">hello trace log table appears in hello Azure storage table viewer.</span></span>

     <span data-ttu-id="2b4ee-444">("시퀀스에 요소가" 오류가 발생할 경우 열 **서버 탐색기**, hello에서 저장소 계정에 대 한 hello 노드를 확장 **Azure** 노드를 마우스 오른쪽 단추로 **테이블**클릭 **새로 고침**.)</span><span class="sxs-lookup"><span data-stu-id="2b4ee-444">(If you get a "sequence contains no elements" error, open **Server Explorer**, expand hello node for your storage account under hello **Azure** node, and then right-click **Tables** and click **Refresh**.)</span></span>

     ![테이블 보기의 저장소 로그](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracelogtableview.png)

     <span data-ttu-id="2b4ee-446">이 보기에는 다른 보기에서 볼 수 없는 추가 필드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-446">This view shows additional fields you don't see in any other views.</span></span> <span data-ttu-id="2b4ee-447">이 보기 사용 수도 toofilter 로그 쿼리를 생성 하기 위한 특수 쿼리 작성기 UI를 사용 하 여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-447">This view also enables you toofilter logs by using special Query Builder UI for constructing a query.</span></span> <span data-ttu-id="2b4ee-448">자세한 내용은 [서버 탐색기를 사용하여 저장소 리소스 탐색](http://msdn.microsoft.com/library/ff683677.aspx)(영문)에서 "테이블 리소스 사용 - 엔터티 필터링"을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-448">For more information, see Working with Table Resources - Filtering Entities in [Browsing Storage Resources with Server Explorer](http://msdn.microsoft.com/library/ff683677.aspx).</span></span>
14. <span data-ttu-id="2b4ee-449">단일 행에 대 한 hello 세부 정보를 toolook hello 행 중 하나를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-449">toolook at hello details for a single row, double-click one of hello rows.</span></span>

     ![서버 탐색기의 추적 테이블](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracetablerow.png)

## <span data-ttu-id="2b4ee-451"><a name="failedrequestlogs"></a>실패한 요청 추적 로그 보기</span><span class="sxs-lookup"><span data-stu-id="2b4ee-451"><a name="failedrequestlogs"></a>View failed request tracing logs</span></span>
<span data-ttu-id="2b4ee-452">실패 한 요청 추적 로그는 IIS URL 재작성 또는 인증 문제를 비롯 한 경우에는 HTTP 요청을 처리 하는 방법의 toounderstand hello 세부 정보를 할 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-452">Failed request tracing logs are useful when you need toounderstand hello details of how IIS is handling an HTTP request, in scenarios such as URL rewriting or authentication problems.</span></span>

<span data-ttu-id="2b4ee-453">Azure 웹 앱 사용 하 여 hello 동일 하지 못했습니다가 IIS 7.0과 함께 사용할 수 있는 이상용 되어 추적 기능을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-453">Azure web apps use hello same failed request tracing functionality that has been available with IIS 7.0 and later.</span></span> <span data-ttu-id="2b4ee-454">그러나 액세스 toohello 기록할 오류를 구성 하는 IIS 설정을 기록, 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-454">You don't have access toohello IIS settings that configure which errors get logged, however.</span></span> <span data-ttu-id="2b4ee-455">실패한 요청 추적을 사용하도록 설정하면 모든 오류가 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-455">When you enable failed request tracing, all errors are captured.</span></span>

<span data-ttu-id="2b4ee-456">Visual Studio를 사용하여 실패한 요청 추적을 사용하도록 설정할 수 있지만 Visual Studio에서 해당 로그를 볼 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-456">You can enable failed request tracing by using Visual Studio, but you can't view them in Visual Studio.</span></span> <span data-ttu-id="2b4ee-457">이러한 로그는 XML 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-457">These logs are XML files.</span></span> <span data-ttu-id="2b4ee-458">일반 텍스트 모드에서 읽을 수 있는 것으로 간주 되는 파일을 모니터링 하는 스트리밍 로그 서비스에만 hello: *.txt*, *.html*, 및 *.log* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-458">hello streaming log service only monitors files that are deemed readable in plain text mode:  *.txt*, *.html*, and *.log* files.</span></span>

<span data-ttu-id="2b4ee-459">FTP를 통해 직접 또는 FTP 도구 toodownload를 사용 하 여 후 로컬로 브라우저에서 실패 한 요청 추적 로그를 볼 수 있습니다 이러한 tooyour 로컬 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-459">You can view failed request tracing logs in a browser directly via FTP or locally after using an FTP tool toodownload them tooyour local computer.</span></span> <span data-ttu-id="2b4ee-460">이 섹션에서는 브라우저에서 직접 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-460">In this section you'll view them in a browser directly.</span></span>

1. <span data-ttu-id="2b4ee-461">Hello에 **구성** hello 탭 **Azure 웹 앱** 에서 열린 창 **서버 탐색기**, 변경 **실패 한 요청 추적**너무**에**, 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-461">In hello **Configuration** tab of hello **Azure Web App** window that you opened from **Server Explorer**, change **Failed Request Tracing** too**On**, and then click **Save**.</span></span>

    ![실패한 요청 추적 사용](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequeston.png)
2. <span data-ttu-id="2b4ee-463">Hello 웹 응용 프로그램을 보여 주는 hello 브라우저 창의 주소 표시줄 hello 추가 문자가 toohello URL을 추가 하 고 Enter toocause 404 오류를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-463">In hello address bar of hello browser window that shows hello web app, add an extra character toohello URL and click Enter toocause a 404 error.</span></span>

    <span data-ttu-id="2b4ee-464">이 인해 생성 하는 실패 한 요청 추적 로그 toobe와 hello 다음 단계 표시 방법을 tooview 또는 다운로드 hello 로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-464">This causes a failed request tracing log toobe created, and hello following steps show how tooview or download hello log.</span></span>
3. <span data-ttu-id="2b4ee-465">Hello에 Visual Studio에서 **구성** hello 탭 **Azure 웹 앱** 창 클릭 **관리 포털에서 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-465">In Visual Studio, in hello **Configuration** tab of hello **Azure Web App** window, click **Open in Management Portal**.</span></span>
4. <span data-ttu-id="2b4ee-466">Hello에 [Azure 포털](https://portal.azure.com) **설정** 블레이드 웹 앱에 대 한 클릭 **배포 자격 증명**, 새 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-466">In hello [Azure Portal](https://portal.azure.com) **Settings** blade for your web app, click **Deployment credentials**, and then enter a new user name and password.</span></span>

    ![새 FTP 사용자 이름 및 암호](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-enterftpcredentials.png)

    <span data-ttu-id="2b4ee-468">* * 로그인 할 때 toouse hello 전체 사용자 이름을 hello 웹 응용 프로그램 이름 tooit 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-468">**When you log in, you have toouse hello full user name with hello web app name prefixed tooit.</span></span> <span data-ttu-id="2b4ee-469">예를 들어, 사용자 이름으로 "myid"를 입력 하는 경우 hello 사이트는 "myexample"로 로그인 "myexample\myid"입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-469">For example, if you enter "myid" as a user name and hello site is "myexample", you log in as "myexample\myid".</span></span>
5. <span data-ttu-id="2b4ee-470">새 브라우저 창에서 아래 표시 된 toohello URL로 이동 **FTP 호스트 이름** 또는 **FTPS 호스트 이름** hello에 **웹 응용 프로그램** 블레이드 웹 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-470">In a new browser window, go toohello URL that is shown under **FTP hostname** or **FTPS hostname** in hello **Web App** blade for your web app.</span></span>
6. <span data-ttu-id="2b4ee-471">이전 버전 (포함 hello 웹 응용 프로그램 이름에 대 한 접두사 hello 사용자 이름) 만든 hello FTP 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-471">Log in using hello FTP credentials that you created earlier (including hello web app name prefix for hello user name).</span></span>

    <span data-ttu-id="2b4ee-472">hello 브라우저 hello 웹 앱의 hello 루트 폴더를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-472">hello browser shows hello root folder of hello web app.</span></span>
7. <span data-ttu-id="2b4ee-473">열기 hello *LogFiles* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-473">Open hello *LogFiles* folder.</span></span>

    ![LogFiles 폴더 열기](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilesfolder.png)
8. <span data-ttu-id="2b4ee-475">W3SVC를 더한 숫자 값을 명명 된 hello 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-475">Open hello folder that is named W3SVC plus a numeric value.</span></span>

    ![W3SVC 폴더 열기](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfolder.png)

    <span data-ttu-id="2b4ee-477">실패 한 요청 추적을 설정한 후 기록 된 모든 오류에 대 한 XML 파일과 브라우저 tooformat hello XML을 사용할 수 있는 XSL 파일 hello 폴더에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-477">hello folder contains XML files for any errors that have been logged after you enabled failed request tracing, and an XSL file that a browser can use tooformat hello XML.</span></span>

    ![W3SVC 폴더](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfoldercontents.png)
9. <span data-ttu-id="2b4ee-479">에 대 한 추적 정보를 toosee hello 실패 한 요청에 대 한 hello XML 파일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-479">Click hello XML file for hello failed request that you want toosee tracing information for.</span></span>

    <span data-ttu-id="2b4ee-480">hello 다음은 샘플 오류에 대 한 hello 추적 정보의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-480">hello following illustration shows part of hello tracing information for a sample error.</span></span>

    ![브라우저의 실패한 요청 추적](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequestinbrowser.png)

## <span data-ttu-id="2b4ee-482"><a name="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="2b4ee-482"><a name="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="2b4ee-483">어떻게 Visual Studio에서는 쉽게 tooview를 살펴 보았으며 Azure 웹 앱에서 만든 로그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-483">You've seen how Visual Studio makes it easy tooview logs created by an Azure web app.</span></span> <span data-ttu-id="2b4ee-484">hello 다음 섹션에서는 링크 toomore 리소스에 관련된 항목:</span><span class="sxs-lookup"><span data-stu-id="2b4ee-484">hello following sections provide links toomore resources on related topics:</span></span>

* <span data-ttu-id="2b4ee-485">Azure 웹 앱 문제 해결</span><span class="sxs-lookup"><span data-stu-id="2b4ee-485">Azure web app troubleshooting</span></span>
* <span data-ttu-id="2b4ee-486">Visual Studio의 디버깅</span><span class="sxs-lookup"><span data-stu-id="2b4ee-486">Debugging in Visual Studio</span></span>
* <span data-ttu-id="2b4ee-487">Azure의 원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="2b4ee-487">Remote debugging in Azure</span></span>
* <span data-ttu-id="2b4ee-488">ASP.NET 응용 프로그램의 추적</span><span class="sxs-lookup"><span data-stu-id="2b4ee-488">Tracing in ASP.NET applications</span></span>
* <span data-ttu-id="2b4ee-489">웹 서버 로그 분석</span><span class="sxs-lookup"><span data-stu-id="2b4ee-489">Analyzing web server logs</span></span>
* <span data-ttu-id="2b4ee-490">실패한 요청 로그 분석</span><span class="sxs-lookup"><span data-stu-id="2b4ee-490">Analyzing failed request tracing logs</span></span>
* <span data-ttu-id="2b4ee-491">클라우드 서비스 디버깅</span><span class="sxs-lookup"><span data-stu-id="2b4ee-491">Debugging Cloud Services</span></span>

### <a name="azure-web-app-troubleshooting"></a><span data-ttu-id="2b4ee-492">Azure 웹 앱 문제 해결</span><span class="sxs-lookup"><span data-stu-id="2b4ee-492">Azure web app troubleshooting</span></span>
<span data-ttu-id="2b4ee-493">Azure 앱 서비스의 웹 응용 프로그램 문제를 해결 하는 방법에 대 한 자세한 내용은 hello 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-493">For more information about troubleshooting web apps in Azure App Service, see hello following resources:</span></span>

* [<span data-ttu-id="2b4ee-494">어떻게 toomonitor 웹 앱</span><span class="sxs-lookup"><span data-stu-id="2b4ee-494">How toomonitor web apps</span></span>](/manage/services/web-sites/how-to-monitor-websites/)
* <span data-ttu-id="2b4ee-495">[Visual Studio 2013을 사용하여 Azure Web Apps에서 메모리 누수 검사](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx)</span><span class="sxs-lookup"><span data-stu-id="2b4ee-495">[Investigating Memory Leaks in Azure Web Apps with Visual Studio 2013](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx).</span></span> <span data-ttu-id="2b4ee-496">관리되는 메모리 문제를 분석하는 데 사용되는 Visual Studio 기능에 대한 Microsoft ALM 블로그 게시물입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-496">Microsoft ALM blog post about Visual Studio features for analyzing managed memory issues.</span></span>
* <span data-ttu-id="2b4ee-497">[알아 두면 도움이 되는 Azure Web Apps 온라인 도구](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/)</span><span class="sxs-lookup"><span data-stu-id="2b4ee-497">[Azure web apps online tools you should know about](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/).</span></span> <span data-ttu-id="2b4ee-498">Amit Apple의 블로그 게시물입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-498">Blog post by Amit Apple.</span></span>

<span data-ttu-id="2b4ee-499">에 대 한 특정 문제 해결 질문 도움말, hello 다음 포럼 중 하나에서 스레드를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-499">For help with a specific troubleshooting question, start a thread in one of hello following forums:</span></span>

* <span data-ttu-id="2b4ee-500">[hello ASP.NET 사이트의 Azure 포럼 hello](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-500">[hello Azure forum on hello ASP.NET site](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET).</span></span>
* <span data-ttu-id="2b4ee-501">[MSDN의 Azure 포럼 hello](http://social.msdn.microsoft.com/Forums/windowsazure/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-501">[hello Azure forum on MSDN](http://social.msdn.microsoft.com/Forums/windowsazure/).</span></span>
* <span data-ttu-id="2b4ee-502">[StackOverflow.com](http://www.stackoverflow.com)(영문)</span><span class="sxs-lookup"><span data-stu-id="2b4ee-502">[StackOverflow.com](http://www.stackoverflow.com).</span></span>

### <a name="debugging-in-visual-studio"></a><span data-ttu-id="2b4ee-503">Visual Studio의 디버깅</span><span class="sxs-lookup"><span data-stu-id="2b4ee-503">Debugging in Visual Studio</span></span>
<span data-ttu-id="2b4ee-504">Toouse 모드 Visual Studio에서 디버깅 하는 방법에 대 한 자세한 내용은 참조 hello [Visual Studio의 디버깅](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx) MSDN 항목 및 [Visual Studio 2010과 디버그 팁](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-504">For more information about how toouse debug mode in Visual Studio, see hello [Debugging in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx) MSDN topic and [Debugging Tips with Visual Studio 2010](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx).</span></span>

### <a name="remote-debugging-in-azure"></a><span data-ttu-id="2b4ee-505">Azure의 원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="2b4ee-505">Remote debugging in Azure</span></span>
<span data-ttu-id="2b4ee-506">Azure 웹 앱 및 WebJobs 원격 디버깅에 대 한 자세한 내용은 hello 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-506">For more information about remote debugging for Azure web apps and WebJobs, see hello following resources:</span></span>

* <span data-ttu-id="2b4ee-507">[소개 tooRemote 디버깅 Azure 앱 서비스 웹 앱](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-507">[Introduction tooRemote Debugging Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/).</span></span>
* [<span data-ttu-id="2b4ee-508">Azure 앱 서비스 웹 앱 디버깅 파트 2-내 원격 디버깅 소개 tooRemote</span><span class="sxs-lookup"><span data-stu-id="2b4ee-508">Introduction tooRemote Debugging Azure App Service Web Apps part 2 - Inside Remote debugging</span></span>](https://azure.microsoft.com/blog/2014/05/07/introduction-to-remote-debugging-azure-web-sites-part-2-inside-remote-debugging/)
* [<span data-ttu-id="2b4ee-509">소개 tooRemote Azure 앱 서비스 웹 앱 파트 3-다중 인스턴스 환경 및 GIT에 디버깅</span><span class="sxs-lookup"><span data-stu-id="2b4ee-509">Introduction tooRemote Debugging on Azure App Service Web Apps part 3 - Multi-Instance environment and GIT</span></span>](https://azure.microsoft.com/blog/2014/05/08/introduction-to-remote-debugging-on-azure-web-sites-part-3-multi-instance-environment-and-git/)
* [<span data-ttu-id="2b4ee-510">Webjob 디버깅(비디오)</span><span class="sxs-lookup"><span data-stu-id="2b4ee-510">WebJobs Debugging (video)</span></span>](https://www.youtube.com/watch?v=ncQm9q5ZFZs&list=UU_SjTh-ZltPmTYzAybypB-g&index=1)

<span data-ttu-id="2b4ee-511">웹 앱에는 Azure 웹 API 또는 모바일 서비스 백 엔드에서 사용 하 여 toodebug 참조 하는 경우 [Visual Studio에서.NET 백 엔드 디버깅](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-511">If your web app uses an Azure Web API or Mobile Services back-end and you need toodebug that, see [Debugging .NET Backend in Visual Studio](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx).</span></span>

### <a name="tracing-in-aspnet-applications"></a><span data-ttu-id="2b4ee-512">ASP.NET 응용 프로그램의 추적</span><span class="sxs-lookup"><span data-stu-id="2b4ee-512">Tracing in ASP.NET applications</span></span>
<span data-ttu-id="2b4ee-513">없는 철저 하 고 최신 소개 tooASP.NET 추적 hello 인터넷에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-513">There are no thorough and up-to-date introductions tooASP.NET tracing available on hello Internet.</span></span> <span data-ttu-id="2b4ee-514">hello 최상의 할 수 있는 Web Forms MVC 아직 존재 하지 않은 및 최신 블로그도 보완 하는 때문에 집중 된에 대 한 게시물 특정 문제 용으로 작성 된 이전 소개 자료는 시작 하세요.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-514">hello best you can do is get started with old introductory materials written for Web Forms because MVC didn't exist yet, and supplement that with newer blog posts that focus on specific issues.</span></span> <span data-ttu-id="2b4ee-515">일부 장황한 toostart hello 다음 리소스는.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-515">Some good places toostart are hello following resources:</span></span>

* <span data-ttu-id="2b4ee-516">[모니터링 및 원격 분석(Azure에서 실제 클라우드 앱 빌드)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry)</span><span class="sxs-lookup"><span data-stu-id="2b4ee-516">[Monitoring and Telemetry (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry).</span></span><br>
  <span data-ttu-id="2b4ee-517">Azure 클라우드 응용 프로그램에서 추적을 권장하는 전자책의 한 챕터</span><span class="sxs-lookup"><span data-stu-id="2b4ee-517">E-book chapter with recommendations for tracing in Azure cloud applications.</span></span>
* [<span data-ttu-id="2b4ee-518">ASP.NET 추적</span><span class="sxs-lookup"><span data-stu-id="2b4ee-518">ASP.NET Tracing</span></span>](http://msdn.microsoft.com/library/ms972204.aspx)<br/>
  <span data-ttu-id="2b4ee-519">이전 하지만 여전히 좋은 리소스의 기본 사항을 소개 toohello 주체입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-519">Old but still a good resource for a basic introduction toohello subject.</span></span>
* [<span data-ttu-id="2b4ee-520">추적 수신기</span><span class="sxs-lookup"><span data-stu-id="2b4ee-520">Trace Listeners</span></span>](http://msdn.microsoft.com/library/4y5y10s7.aspx)<br/>
  <span data-ttu-id="2b4ee-521">추적 수신기에 대 한 정보 hello를 언급 하지 않는 있지만 [WebPageTraceListener](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-521">Information about trace listeners but doesn't mention hello [WebPageTraceListener](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx).</span></span>
* [<span data-ttu-id="2b4ee-522">연습: ASP.NET 추적을 System.Diagnostics 추적과 통합</span><span class="sxs-lookup"><span data-stu-id="2b4ee-522">Walkthrough: Integrating ASP.NET Tracing with System.Diagnostics Tracing</span></span>](http://msdn.microsoft.com/library/b0ectfxd.aspx)<br/>
  <span data-ttu-id="2b4ee-523">이 너무 오래 되 면 하지만 몇 가지 추가 정보를 포함 합니다. 해당 hello 소개 문서 처리 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-523">This too is old, but includes some additional information that hello introductory article doesn't cover.</span></span>
* [<span data-ttu-id="2b4ee-524">ASP.NET MVC Razor 뷰에서 추적</span><span class="sxs-lookup"><span data-stu-id="2b4ee-524">Tracing in ASP.NET MVC Razor Views</span></span>](http://blogs.msdn.com/b/webdev/archive/2013/07/16/tracing-in-asp-net-mvc-razor-views.aspx)<br/>
  <span data-ttu-id="2b4ee-525">Razor 뷰에 사용 되는 추적 외에도 hello post toocreate 오류가 필터링 하는 방법을 순서 toolog에 MVC 응용 프로그램에서 처리 되지 않은 모든 예외도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-525">Besides tracing in Razor views, hello post also explains how toocreate an error filter in order toolog all unhandled exceptions in an MVC application.</span></span> <span data-ttu-id="2b4ee-526">모든 toolog 처리 되지 않은 대 한 정보에 대 한 hello Global.asax 예제를 참조 하는 Web Forms 응용 프로그램에서 예외 [오류 처리기에 대 한 전체 예제](http://msdn.microsoft.com/library/bb397417.aspx) msdn 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-526">For information about how toolog all unhandled exceptions in a Web Forms application, see hello Global.asax example in [Complete Example for Error Handlers](http://msdn.microsoft.com/library/bb397417.aspx) on MSDN.</span></span> <span data-ttu-id="2b4ee-527">MVC 또는 Web Forms toolog 특정 예외가 하지만 고객을 위해 적용을 처리 하는 hello 기본 프레임 워크를 사용 하는 경우 catch 하 고 수 hello 다음 예제와 같이 다시 throw:</span><span class="sxs-lookup"><span data-stu-id="2b4ee-527">In either MVC or Web Forms, if you want toolog certain exceptions but let hello default framework handling take effect for them, you can catch and rethrow as in hello following example:</span></span>

        try
        {
           // Your code that might cause an exception toobe thrown.
        }
        catch (Exception ex)
        {
            Trace.TraceError("Exception: " + ex.ToString());
            throw;
        }
* [<span data-ttu-id="2b4ee-528">Hello Azure 명령줄에서에서 진단 추적 로그 (및 Glimpse!) 스트리밍</span><span class="sxs-lookup"><span data-stu-id="2b4ee-528">Streaming Diagnostics Trace Logging from hello Azure Command Line (plus Glimpse!)</span></span>](http://www.hanselman.com/blog/StreamingDiagnosticsTraceLoggingFromTheAzureCommandLinePlusGlimpse.aspx)<br/>
  <span data-ttu-id="2b4ee-529">어떻게 toouse hello 명령줄 toodo이 자습서에서는 어떤 방법을 Visual Studio에서 toodo 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-529">How toouse hello command line toodo what this tutorial shows how toodo in Visual Studio.</span></span> <span data-ttu-id="2b4ee-530">[Glimpse](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) 는 ASP.NET 응용 프로그램을 디버그하는 데 사용하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-530">[Glimpse](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) is a tool for debugging ASP.NET applications.</span></span>
* <span data-ttu-id="2b4ee-531">[David Ebbo와 함께 하는 Web Apps 로깅 및 진단](/documentation/videos/azure-web-site-logging-and-diagnostics/) 및 [David Ebbo와 함께 하는 Web Apps에서 로그 스트리밍](/documentation/videos/log-streaming-with-azure-web-sites/)</span><span class="sxs-lookup"><span data-stu-id="2b4ee-531">[Using Web Apps Logging and Diagnostics - with David Ebbo](/documentation/videos/azure-web-site-logging-and-diagnostics/) and [Streaming Logs from Web Apps - with David Ebbo](/documentation/videos/log-streaming-with-azure-web-sites/)</span></span><br>
  <span data-ttu-id="2b4ee-532">은 Scott Hanselman과 David Ebbo가 제작한 비디오입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-532">Videos by Scott Hanselman and David Ebbo.</span></span>

<span data-ttu-id="2b4ee-533">오류 로깅에 대 한 대체 toowriting 추적 하는 코드는 오픈 소스 toouse 로깅 프레임 워크와 같은 [ELMAH](http://nuget.org/packages/elmah/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-533">For error logging, an alternative toowriting your own tracing code is toouse an open-source logging framework such as [ELMAH](http://nuget.org/packages/elmah/).</span></span> <span data-ttu-id="2b4ee-534">자세한 내용은 [Scott Hanselman의 ELMAH 관련 블로그 게시물](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)(영문)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-534">For more information, see [Scott Hanselman's blog posts about ELMAH](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx).</span></span>

<span data-ttu-id="2b4ee-535">또한 ASP.NET toouse 없는 또는 System.Diagnostics 추적 tooget 스트리밍 하려는 경우 Azure에서 로그의 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-535">Also, note that you don't have toouse ASP.NET or System.Diagnostics tracing if you want tooget streaming logs from Azure.</span></span> <span data-ttu-id="2b4ee-536">hello Azure 웹 앱 로그 서비스 스트리밍 스트리밍되지 모든 *.txt*, *.html*, 또는 *.log* hello에서 찾은 파일 *LogFiles* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-536">hello Azure web app streaming log service will stream any *.txt*, *.html*, or *.log* file that it finds in hello *LogFiles* folder.</span></span> <span data-ttu-id="2b4ee-537">따라서 hello 웹 응용 프로그램의 toohello 파일 시스템을 작성 하는 로깅 시스템을 만들 수 있습니다 및 파일에 자동으로 스트리밍 되며 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-537">Therefore, you could create your own logging system that writes toohello file system of hello web app, and your file will be automatically streamed and downloaded.</span></span> <span data-ttu-id="2b4ee-538">Toodo 됩니다 hello에서 파일을 작성 하는 응용 프로그램 코드를 작성 *d:\home\logfiles* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-538">All you have toodo is write application code that creates files in hello *d:\home\logfiles* folder.</span></span>

### <a name="analyzing-web-server-logs"></a><span data-ttu-id="2b4ee-539">웹 서버 로그 분석</span><span class="sxs-lookup"><span data-stu-id="2b4ee-539">Analyzing web server logs</span></span>
<span data-ttu-id="2b4ee-540">웹 서버 로그를 분석 하는 방법에 대 한 자세한 내용은 hello 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-540">For more information about analyzing web server logs, see hello following resources:</span></span>

* [<span data-ttu-id="2b4ee-541">LogParser</span><span class="sxs-lookup"><span data-stu-id="2b4ee-541">LogParser</span></span>](http://www.microsoft.com/download/details.aspx?id=24659)<br/>
  <span data-ttu-id="2b4ee-542">웹 서버 로그(*.log* 파일)의 데이터를 보는 데 사용하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-542">A tool for viewing data in web server logs (*.log* files).</span></span>
* [<span data-ttu-id="2b4ee-543">LogParser를 사용하여 IIS 성능 문제 또는 응용 프로그램 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="2b4ee-543">Troubleshooting IIS Performance Issues or Application Errors using LogParser </span></span>](http://www.iis.net/learn/troubleshoot/performance-issues/troubleshooting-iis-performance-issues-or-application-errors-using-logparser)<br/>
  <span data-ttu-id="2b4ee-544">Tooanalyze 웹 서버를 사용할 수 있는 소개 toohello 로그 구문 분석기 도구를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-544">An introduction toohello Log Parser tool that you can use tooanalyze web server logs.</span></span>
* [<span data-ttu-id="2b4ee-545">Robert McMurray의 LogParser 사용 관련 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="2b4ee-545">Blog posts by Robert McMurray on using LogParser</span></span>](http://blogs.msdn.com/b/robert_mcmurray/archive/tags/logparser/)<br/>
* [<span data-ttu-id="2b4ee-546">hello IIS 7.0, IIS 7.5 및 IIS 8.0의 HTTP 상태 코드</span><span class="sxs-lookup"><span data-stu-id="2b4ee-546">hello HTTP status code in IIS 7.0, IIS 7.5, and IIS 8.0</span></span>](http://support.microsoft.com/kb/943891)

### <a name="analyzing-failed-request-tracing-logs"></a><span data-ttu-id="2b4ee-547">실패한 요청 로그 분석</span><span class="sxs-lookup"><span data-stu-id="2b4ee-547">Analyzing failed request tracing logs</span></span>
<span data-ttu-id="2b4ee-548">hello Microsoft TechNet 웹 사이트를 포함 한 [를 사용 하 여 실패 한 요청 추적](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing) 섹션 이해 하는 데 도움이 될 수 있습니다 어떻게 toouse 이러한 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-548">hello Microsoft TechNet website includes a [Using Failed Request Tracing](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing) section which may be helpful for understanding how toouse these logs.</span></span> <span data-ttu-id="2b4ee-549">하지만 이 설명서에서는 IIS에서 실패한 요청 추적을 구성하는 방법을 중점적으로 다루며, 이는 Azure 웹 앱에서 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4ee-549">However, this documentation focuses mainly on configuring failed request tracing in IIS, which you can't do in Azure Web Apps.</span></span>

[GetStarted]: app-service-web-get-started-dotnet.md
[GetStartedWJ]: websites-dotnet-webjobs-sdk.md
