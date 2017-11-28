---
title: "aaaAccess 온-프레미스 하이브리드 연결을 사용 하 여 Azure 앱 서비스의 리소스"
description: "Azure 앱 서비스의 웹 앱과 정적 TCP 포트를 사용하는 온-프레미스 리소스 간의 연결 만들기"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: de7c57b94f4bd6250a93757817178e8455daae4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a><span data-ttu-id="537cf-103">Azure 앱 서비스에서 하이브리드 연결을 사용하여 온-프레미스 리소스에 액세스</span><span class="sxs-lookup"><span data-stu-id="537cf-103">Access on-premises resources using hybrid connections in Azure App Service</span></span>
<span data-ttu-id="537cf-104">SQL Server, MySQL, HTTP 웹 Api 및 대부분의 사용자 지정 웹 서비스와 같은 정적 TCP 포트를 사용 하는 Azure 앱 서비스 앱 tooany 온-프레미스 리소스를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-104">You can connect an Azure App Service app tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="537cf-105">이 문서에서는 어떻게 toocreate 응용 프로그램 서비스와 온-프레미스 SQL Server 데이터베이스 간의 하이브리드 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-105">This article shows you how toocreate a hybrid connection between App Service and an on-premises SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="537cf-106">hello 하이브리드 연결 기능은의 hello 웹 응용 프로그램 부분은 hello에만 사용할 수 있는 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-106">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="537cf-107">BizTalk 서비스의 연결 toocreate 참조 [하이브리드 연결](http://go.microsoft.com/fwlink/p/?LinkID=397274)합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-107">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span> 
> 
> <span data-ttu-id="537cf-108">이 콘텐츠에 Azure 앱 서비스에서 tooMobile 앱도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-108">This content also applies tooMobile Apps in Azure App Service.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="537cf-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="537cf-109">Prerequisites</span></span>
* <span data-ttu-id="537cf-110">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="537cf-110">An Azure subscription.</span></span> <span data-ttu-id="537cf-111">무료 구독에 대해서는 [Azure 1개월 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="537cf-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
  
    <span data-ttu-id="537cf-112">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-112">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="537cf-113">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-113">No credit cards required; no commitments.</span></span>
* <span data-ttu-id="537cf-114">toouse 온-프레미스 SQL Server 또는 SQL Server Express 데이터베이스 하이브리드 연결 된 TCP/IP toobe 고정 포트에서 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-114">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="537cf-115">SQL Server의 기본 인스턴스는 고정 포트 1433을 사용하므로 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span></span> <span data-ttu-id="537cf-116">설치 및 하이브리드 연결 사용 하기 위해 SQL Server Express를 구성에 대 한 자세한 내용은 참조 하십시오. [연결 tooan 온-프레미스 SQL Server 하이브리드 연결을 사용 하 여 Azure 웹 사이트에서](http://go.microsoft.com/fwlink/?LinkID=397979)합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span>
* <span data-ttu-id="537cf-117">에이 문서의 뒷부분에 설명 하는 hello 온-프레미스 하이브리드 연결 관리자 에이전트를 설치 하는 hello 컴퓨터:</span><span class="sxs-lookup"><span data-stu-id="537cf-117">hello computer on which you install hello on-premises Hybrid Connection Manager agent described later in this article:</span></span>
  
  * <span data-ttu-id="537cf-118">포트 5671 통해 수 tooconnect tooAzure 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-118">Must be able tooconnect tooAzure over port 5671</span></span>
  * <span data-ttu-id="537cf-119">수 tooreach hello 있어야 *hostname*:*portnumber* 온-프레미스 리소스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-119">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span> 

> [!NOTE]
> <span data-ttu-id="537cf-120">이 문서의 단계 hello hello 브라우저 hello 온-프레미스 하이브리드 연결 에이전트를 호스트 하는 hello 컴퓨터에서 사용 하는 것을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-120">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="537cf-121">Hello Azure 포털에서에서 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="537cf-121">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="537cf-122">이미 만든 웹 응용 프로그램 또는 모바일 앱 백 엔드에서 hello이이 자습서에 대 한 toouse 되도록 하는 Azure 포털에서 있습니다 건너뛰어 너무[하이브리드 연결을 만들고 BizTalk 서비스](#CreateHC) 하 고 여기에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-122">If you have already created a web app or Mobile App backend in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span></span>
> 
> 

1. <span data-ttu-id="537cf-123">Hello의 왼쪽된 위 모서리 hello에에서 [Azure 포털](https://portal.azure.com), 클릭 **새로** > **웹 + 모바일** > **웹 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-123">In hello upper left corner of hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span></span>
   
    ![새 웹 앱][NewWebsite]
2. <span data-ttu-id="537cf-125">Hello에 **웹 앱** 블레이드에서 URL을 입력 하 고 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-125">On hello **Web app** blade, provide a URL and click **Create**.</span></span> 
   
    ![웹 사이트 이름][WebsiteCreationBlade]
3. <span data-ttu-id="537cf-127">몇 분 후 hello 웹 응용 프로그램이 만들어지고 해당 웹 앱 블레이드 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-127">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="537cf-128">hello 블레이드는 사이트를 관리할 수 있는 수직으로 스크롤 가능한 한 대시보드입니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-128">hello blade is a vertically scrollable dashboard that lets you manage your site.</span></span>
   
    ![실행 중인 웹 사이트][WebSiteRunningBlade]
4. <span data-ttu-id="537cf-130">tooverify hello 사이트는 라이브, hello를 클릭할 수 있는 **찾아보기** 아이콘 toodisplay hello 기본 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-130">tooverify hello site is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>
   
    ![웹 앱 찾아보기 toosee를 클릭 합니다.][Browse]
   
    ![기본 웹 앱 페이지][DefaultWebSitePage]

<span data-ttu-id="537cf-133">다음으로 hello 웹 앱에 대 한 BizTalk 서비스 및 하이브리드 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-133">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="537cf-134">하이브리드 연결 및 BizTalk 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="537cf-134">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="537cf-135">웹앱 블레이드에서 **모든 설정** > **네트워킹** > **하이브리드 연결 끝점 구성**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![하이브리드 연결][CreateHCHCIcon]
2. <span data-ttu-id="537cf-137">Hello 하이브리드 연결 블레이드에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-137">On hello Hybrid connections blade, click **Add**.</span></span>
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. <span data-ttu-id="537cf-138">hello **하이브리드 연결을 추가할** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-138">hello **Add a hybrid connection** blade opens.</span></span>  <span data-ttu-id="537cf-139">첫 번째 하이브리드 연결 이므로, hello **새 하이브리드 연결** 옵션은 미리 선택 하 고 hello **하이브리드 연결** 블레이드에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-139">Since this is your first hybrid connection, hello **New hybrid connection** option is preselected, and hello **Create hybrid connection** blade opens for you.</span></span>
   
    ![하이브리드 연결 만들기][TwinCreateHCBlades]
   
    <span data-ttu-id="537cf-141">Hello에 **만들기 하이브리드 연결 블레이드**:</span><span class="sxs-lookup"><span data-stu-id="537cf-141">On hello **Create hybrid connection blade**:</span></span>
   
   * <span data-ttu-id="537cf-142">에 대 한 **이름**, hello 연결에 대 한 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-142">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="537cf-143">에 대 한 **Hostname**, 리소스를 호스트 하는 hello 온-프레미스 컴퓨터의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-143">For **Hostname**, enter hello name of hello on-premises computer that hosts your resource.</span></span>
   * <span data-ttu-id="537cf-144">에 대 한 **포트**, 온-프레미스 리소스 (SQL Server 기본 인스턴스의 경우 1433)를 사용 하는 hello 포트 번호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-144">For **Port**, enter hello port number that your on-premises resource uses (1433 for a SQL Server default instance).</span></span>
   * <span data-ttu-id="537cf-145">**Biz Talk 서비스**</span><span class="sxs-lookup"><span data-stu-id="537cf-145">Click **Biz Talk Service**</span></span>
4. <span data-ttu-id="537cf-146">hello **BizTalk 서비스 만들기** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-146">hello **Create BizTalk Service** blade opens.</span></span> <span data-ttu-id="537cf-147">BizTalk 서비스를 hello에 대 한 이름을 입력 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-147">Enter a name for hello BizTalk service, and then click **OK**.</span></span>
   
    ![BizTalk 서비스 만들기][CreateHCCreateBTS]
   
    <span data-ttu-id="537cf-149">hello **BizTalk 서비스 만들기** 블레이드를 닫고 toohello 반환될지 **하이브리드 연결** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-149">hello **Create BizTalk Service** blade closes and you are returned toohello **Create hybrid connection** blade.</span></span>
5. <span data-ttu-id="537cf-150">Hello 만들기 하이브리드 연결 블레이드에서 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-150">On hello Create hybrid connection blade, click **OK**.</span></span> 
   
    ![확인 클릭][CreateBTScomplete]
6. <span data-ttu-id="537cf-152">Hello 프로세스가 완료 되 면 hello 포털의에서 알림 영역 hello hello 연결이 성공적으로 생성 된 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-152">When hello process completes, hello notifications area in hello Portal informs you that hello connection has been successfully created.</span></span>
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in hello dogfood portal. I switch toohello classic portal
    (full portal) and created hello BizTalk service but it doesn't seem toolet you connnect them - When you finish the
    Create hybrid conn step, you get hello following error
    Failed toocreate hybrid connection RelecIoudHC. hello 
    resource type could not be found in hello namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    hello error indicates it couldn't find hello type, not hello instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. <span data-ttu-id="537cf-153">Hello 웹 앱의 블레이드에서 hello **하이브리드 연결** 아이콘은 이제 1 하이브리드 연결을 이미 만들었다고 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-153">On hello web app's blade, hello **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span></span>
   
    ![1개의 하이브리드 연결 생성됨][CreateHCOneConnectionCreated]

<span data-ttu-id="537cf-155">이 시점에서 hello 클라우드 하이브리드 연결 인프라의 중요 한 부분을 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-155">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="537cf-156">이제 해당하는 온-프레미스 부분을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-156">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="537cf-157">Hello 온-프레미스 하이브리드 연결 관리자 toocomplete hello 연결 설치</span><span class="sxs-lookup"><span data-stu-id="537cf-157">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
1. <span data-ttu-id="537cf-158">Hello 웹 앱 블레이드 클릭 **모든 설정을** > **네트워킹** > **하이브리드 연결 끝점 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-158">On hello web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span> 
   
    ![하이브리드 연결 아이콘][HCIcon]
2. <span data-ttu-id="537cf-160">Hello에 **하이브리드 연결** 블레이드, hello **상태** hello에 대 한 열 최근에 추가 하 고 끝점 **연결 되어 있지 않은**합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-160">On hello **Hybrid connections** blade, hello **Status** column for hello recently added endpoint shows **Not connected**.</span></span> <span data-ttu-id="537cf-161">Hello 연결 tooconfigure 클릭 것입니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-161">Click hello connection tooconfigure it.</span></span>
   
    ![연결되지 않음][NotConnected]
   
    <span data-ttu-id="537cf-163">hello 하이브리드 연결 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-163">hello Hybrid connection blade opens.</span></span>
   
    ![NotConnectedBlade][NotConnectedBlade]
3. <span data-ttu-id="537cf-165">Hello 블레이드에서 클릭 **수신기 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-165">On hello blade, click **Listener Setup**.</span></span>
   
    ![수신기 설정 클릭][ClickListenerSetup]
4. <span data-ttu-id="537cf-167">hello **하이브리드 연결 속성** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-167">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="537cf-168">아래 **온-프레미스 하이브리드 연결 관리자**, 선택 **tooinstall 여기를 클릭**합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-168">Under **On-premises Hybrid Connection Manager**, choose **Click here tooinstall**.</span></span>
   
    ![Tooinstall 여기를 클릭합니다][ClickToInstallHCM]
5. <span data-ttu-id="537cf-170">Hello 응용 프로그램 실행 보안 경고 대화 상자에서 선택 **실행** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-170">In hello Application Run security warning dialog, choose **Run** toocontinue.</span></span>
   
    ![실행 toocontinue 선택][ApplicationRunWarning]
6. <span data-ttu-id="537cf-172">Hello에 **사용자 계정 컨트롤** 대화 상자에서 선택 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-172">In hello **User Account Control** dialog, choose **Yes**.</span></span>
   
   ![예 선택][UAC]
7. <span data-ttu-id="537cf-174">hello 하이브리드 연결 관리자 다운로드 되어 자동으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-174">hello Hybrid Connection Manager is downloaded and installed for you.</span></span> 
   
    ![설치][HCMInstalling]
8. <span data-ttu-id="537cf-176">Hello 설치 완료 되 면 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-176">When hello install completes, click **Close**.</span></span>
   
    ![닫기 클릭][HCMInstallComplete]
   
    <span data-ttu-id="537cf-178">Hello에 **하이브리드 연결** 블레이드, hello **상태** 열 이제 표시 **연결 됨**합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-178">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![연결됨 상태][HCStatusConnected]

<span data-ttu-id="537cf-180">이제 hello 하이브리드 연결 인프라에 완료 되 면이 사용 하는 하이브리드 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-180">Now that hello hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span></span> 

> [!NOTE]
> <span data-ttu-id="537cf-181">hello 다음 섹션에서는 방법을 보여 줍니다 toouse 하이브리드 모바일 앱.NET 백 엔드 프로젝트와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-181">hello following sections show you how toouse a hybrid connection with a Mobile Apps .NET backend project.</span></span>
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a><span data-ttu-id="537cf-182">Hello 모바일 앱을.NET 백 엔드 프로젝트 tooconnect toohello SQL Server 데이터베이스 구성</span><span class="sxs-lookup"><span data-stu-id="537cf-182">Configure hello Mobile App .NET backend project tooconnect toohello SQL Server database</span></span>
<span data-ttu-id="537cf-183">앱 서비스에서 모바일 앱 .NET 백 엔드 프로젝트는 추가 모바일 앱 SDK가 설치되고 초기화된 ASP.NET 웹앱입니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span></span> <span data-ttu-id="537cf-184">toouse 해야 웹 응용 프로그램을 모바일 앱 백 엔드를 [다운로드 하 고 hello 모바일 앱을.NET 백 엔드 SDK 초기화](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk)합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-184">toouse your web app as a Mobile Apps backend, you must [download and initialize hello Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span></span>  

<span data-ttu-id="537cf-185">모바일 앱에 대 한도 hello 온-프레미스 데이터베이스에 대 한 연결 문자열 toodefine 필요 하 고 hello 백 엔드 toouse이이 연결을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-185">For Mobile Apps, you also need toodefine a connection string for hello on-premises database and modify hello backend toouse this connection.</span></span> 

1. <span data-ttu-id="537cf-186">모바일 앱을.NET 백 엔드에 대 한 Web.config 파일을 열고 hello Visual Studio의 솔루션 탐색기에서 찾을 hello **connectionStrings** 섹션에서 어떤 지점 toohello 온-프레미스 SQL, hello 다음과 같은 새 SqlClient 항목 추가 서버 데이터베이스:</span><span class="sxs-lookup"><span data-stu-id="537cf-186">In Solution Explorer in Visual Studio, open hello Web.config file for your Mobile App .NET backend, locate hello **connectionStrings** section, add a new SqlClient entry like hello following, which points toohello on-premises SQL Server database:</span></span>
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    <span data-ttu-id="537cf-187">Tooreplace 기억 `<**secure_password**>` hello 암호에 대해 생성 된이 문자열의 *HybridConnectionLogin*합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-187">Remember tooreplace `<**secure_password**>` in this string with hello password you created for  *HybridConnectionLogin*.</span></span>
2. <span data-ttu-id="537cf-188">클릭 **저장** Visual Studio toosave hello Web.config 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-188">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="537cf-189">이 연결 설정은 hello 로컬 컴퓨터에서 실행할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-189">This connection setting is used when running on hello local computer.</span></span> <span data-ttu-id="537cf-190">Azure에서 실행 하는 경우이 설정은 hello 포털에 정의 된 hello 연결 설정으로 재정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-190">When running in Azure, this setting is overriden by hello connection setting defined in hello portal.</span></span>
   > 
   > 
3. <span data-ttu-id="537cf-191">Hello 확장 **모델** 폴더 및 끝나는 열기 hello 데이터 모델 파일을 *Context.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-191">Expand hello **Models** folder and open hello data model file, which ends in *Context.cs*.</span></span>
4. <span data-ttu-id="537cf-192">Hello 수정 **DbContext** 인스턴스 생성자 toopass hello 값 `OnPremisesDBConnection` toohello 기본 **DbContext** 생성자, 다음 코드 조각 비슷한 toohello:</span><span class="sxs-lookup"><span data-stu-id="537cf-192">Modify hello **DbContext** instance constructor toopass hello value `OnPremisesDBConnection` toohello base **DbContext** constructor, similar toohello following snippet:</span></span>
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    <span data-ttu-id="537cf-193">hello 서비스 hello 새 연결 toohello SQL Server 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-193">hello service will now use hello new connection toohello SQL Server database.</span></span>

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a><span data-ttu-id="537cf-194">Hello 모바일 앱 백 엔드 toouse hello 온-프레미스 연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="537cf-194">Update hello Mobile App backend toouse hello on-premises connection string</span></span>
<span data-ttu-id="537cf-195">다음으로, Azure에서 사용할 수 있도록이 새 연결 문자열에 대 한 tooadd 앱 설정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-195">Next, you need tooadd an app setting for this new connection string so that it can be used from Azure.</span></span>  

1. <span data-ttu-id="537cf-196">Hello에 다시 [Azure 포털](https://portal.azure.com) hello 웹 앱 백 엔드 코드에서 모바일 앱에 대 한 클릭 **모든 설정을**, 다음 **응용 프로그램 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-196">Back in hello [Azure portal](https://portal.azure.com) in hello web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span></span>
2. <span data-ttu-id="537cf-197">Hello에 **웹 앱 설정** 블레이드에서 너무 아래로 스크롤하여**연결 문자열** 는 새로 추가 **SQL Server** 라는 연결 문자열 `OnPremisesDBConnection` 같은값으로`Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span><span class="sxs-lookup"><span data-stu-id="537cf-197">In hello **Web app settings** blade, scroll down too**Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span></span>
   
    <span data-ttu-id="537cf-198">대체 `<**secure_password**>` hello 온-프레미스 데이터베이스에 대 한 보안 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-198">Replace `<**secure_password**>` with hello secure password for your on-premises database.</span></span>
   
    ![온-프레미스 데이터베이스에 대한 연결 문자열](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. <span data-ttu-id="537cf-200">키를 눌러 **저장** 방금 만든 toosave hello 하이브리드 연결 및 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-200">Press **Save** toosave hello hybrid connection and connection string you just created.</span></span>

<span data-ttu-id="537cf-201">이 시점에서 hello 서버 프로젝트를 다시 게시 하 고 기존 모바일 앱 클라이언트에 hello 새 연결을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-201">At this point you can republish hello server project and test hello new connection with your existing Mobile Apps clients.</span></span> <span data-ttu-id="537cf-202">데이터에서 읽이 되며 hello 하이브리드 연결을 사용 하 여 toohello 온-프레미스 데이터베이스를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-202">Data will be read from and written toohello on-premises database using hello hybrid connection.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="537cf-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="537cf-203">Next Steps</span></span>
* <span data-ttu-id="537cf-204">하이브리드 연결을 사용 하 여 ASP.NET 웹 응용 프로그램을 만드는 방법에 대 한 정보를 참조 하십시오. [연결 tooan 온-프레미스 SQL Server 하이브리드 연결을 사용 하 여 Azure 웹 사이트에서](http://go.microsoft.com/fwlink/?LinkID=397979)합니다.</span><span class="sxs-lookup"><span data-stu-id="537cf-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span> 

### <a name="additional-resources"></a><span data-ttu-id="537cf-205">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="537cf-205">Additional Resources</span></span>
[<span data-ttu-id="537cf-206">하이브리드 연결 개요</span><span class="sxs-lookup"><span data-stu-id="537cf-206">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="537cf-207">Josh Twist가 소개하는 하이브리드 연결(채널 9 비디오)(영문)</span><span class="sxs-lookup"><span data-stu-id="537cf-207">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="537cf-208">하이브리드 연결 웹 사이트</span><span class="sxs-lookup"><span data-stu-id="537cf-208">Hybrid Connections web site</span></span>](https://azure.microsoft.com/services/biztalk-services/)

[<span data-ttu-id="537cf-209">BizTalk 서비스: 대시보드, 모니터, 확장, 구성 및 하이브리드 연결 탭</span><span class="sxs-lookup"><span data-stu-id="537cf-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="537cf-210">원활한 응용 프로그램 이식성으로 실시간 하이브리드 연결 클라우드 구축(채널 9 비디오)(영문)</span><span class="sxs-lookup"><span data-stu-id="537cf-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="537cf-211">연결 tooan 온-프레미스 하이브리드 연결 (Channel 9 비디오)를 사용 하 여 Azure 모바일 서비스에서 SQL Server</span><span class="sxs-lookup"><span data-stu-id="537cf-211">Connect tooan on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a><span data-ttu-id="537cf-212">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="537cf-212">What's changed</span></span>
* <span data-ttu-id="537cf-213">웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="537cf-213">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[New]:./media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
