---
title: "Azure Active Directory 인증을 사용 하는 기간 업무 Azure 앱 aaaCreate | Microsoft Docs"
description: "자세한 내용은 방법 toocreate는 ASP.NET MVC의 업무 앱에 Azure 앱 서비스를 인증 하는 Azure Active Directory와"
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a><span data-ttu-id="5ebae-103">Azure Active Directory 인증을 사용하여 LOB(기간 업무) Azure 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="5ebae-103">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>
<span data-ttu-id="5ebae-104">표시 하는이 문서에는.NET의 업무 toocreate 앱 [Azure 앱 서비스 웹 앱](http://go.microsoft.com/fwlink/?LinkId=529714) hello를 사용 하 여 [인증 / 권한 부여](../app-service/app-service-authentication-overview.md) 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-104">This article shows you how toocreate a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using hello [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span></span> <span data-ttu-id="5ebae-105">또한 표시 방법을 toouse hello [Azure Active Directory 그래프 API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery 디렉터리 데이터 hello 응용 프로그램에 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-105">It also shows how toouse hello [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery directory data in hello application.</span></span>

<span data-ttu-id="5ebae-106">hello Azure Active Directory 테 넌 트를 사용 하면 Azure 전용 디렉터리가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-106">hello Azure Active Directory tenant that you use can be an Azure-only directory.</span></span> <span data-ttu-id="5ebae-107">수 또는 [온-프레미스 Active Directory와 동기화](../active-directory/active-directory-aadconnect.md) toocreate은 온-프레미스 및 원격 작업자에 대 한 single sign on 환경 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-107">Or, it can be [synced with your on-premises Active Directory](../active-directory/active-directory-aadconnect.md) toocreate a single sign-on experience for workers that are on-premises and remote.</span></span> <span data-ttu-id="5ebae-108">이 문서에서는 Azure 계정에 대 한 hello 기본 디렉터리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-108">This article uses hello default directory for your Azure account.</span></span>

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="5ebae-109">빌드할 내용</span><span class="sxs-lookup"><span data-stu-id="5ebae-109">What you will build</span></span>
<span data-ttu-id="5ebae-110">추적으로 작업 항목 같은 기능 hello로 앱 서비스 웹 응용 프로그램에서 간단한 기간 업무 만들기-읽기-업데이트-삭제 (CRUD) 응용 프로그램 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with hello following features:</span></span>

* <span data-ttu-id="5ebae-111">Azure Active Directory에 대해 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="5ebae-111">Authenticates users against Azure Active Directory</span></span>
* <span data-ttu-id="5ebae-112">[Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span><span class="sxs-lookup"><span data-stu-id="5ebae-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span></span>
* <span data-ttu-id="5ebae-113">사용 하 여 ASP.NET MVC hello *인증 안 함* 서식 파일</span><span class="sxs-lookup"><span data-stu-id="5ebae-113">Use hello ASP.NET MVC *No Authentication* template</span></span>

<span data-ttu-id="5ebae-114">Azure에서 LOB(기간 업무) 앱에 대한 RBAC(역할 기반 액세스 제어)가 필요한 경우 [다음 단계](#next)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ebae-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span></span>

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="5ebae-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="5ebae-115">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="5ebae-116">이 자습서 toocomplete 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="5ebae-116">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="5ebae-117">다양한 그룹의 사용자가 포함된 Azure Active Directory 테넌트</span><span class="sxs-lookup"><span data-stu-id="5ebae-117">An Azure Active Directory tenant with users in various groups</span></span>
* <span data-ttu-id="5ebae-118">Hello Azure Active Directory 테 넌 트에 사용 권한 toocreate 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="5ebae-118">Permissions toocreate applications on hello Azure Active Directory tenant</span></span>
* <span data-ttu-id="5ebae-119">Visual Studio 2013 업데이트 4 이상</span><span class="sxs-lookup"><span data-stu-id="5ebae-119">Visual Studio 2013 Update 4 or later</span></span>
* [<span data-ttu-id="5ebae-120">Azure SDK 2.8.1 이상</span><span class="sxs-lookup"><span data-stu-id="5ebae-120">Azure SDK 2.8.1 or later</span></span>](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a><span data-ttu-id="5ebae-121">만들기 및 웹 응용 프로그램 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="5ebae-121">Create and deploy a web app tooAzure</span></span>
1. <span data-ttu-id="5ebae-122">Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-122">From Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="5ebae-123">**ASP.NET 웹 응용 프로그램**을 선택하고 프로젝트의 이름을 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span></span>
3. <span data-ttu-id="5ebae-124">선택 hello **MVC** 서식 파일을 다음 hello 인증도 변경**인증 안 함**합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-124">Select hello **MVC** template, then change hello authentication too**No Authentication**.</span></span> <span data-ttu-id="5ebae-125">확인 **호스트 클라우드 hello에** 을 선택 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-125">Make sure **Host in hello Cloud** is selected and click **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. <span data-ttu-id="5ebae-126">Hello에 **응용 프로그램 서비스 만들기** 대화 상자에서 클릭 **계정 추가** (차례로 **계정 추가** hello 드롭다운에서) toolog tooyour Azure 계정에에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-126">In hello **Create App Service** dialog, click **Add an account** (and then **Add an account** in hello dropdown) toolog in tooyour Azure account.</span></span>
5. <span data-ttu-id="5ebae-127">로그인하면 웹앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-127">Once logged in configure your web app.</span></span> <span data-ttu-id="5ebae-128">각각 hello를 클릭 하 여 리소스 그룹 및 새 앱 서비스 계획 만들기 **새로** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-128">Create a resource group and a new App Service plan by clicking hello respective **New** button.</span></span> <span data-ttu-id="5ebae-129">클릭 **추가 Azure 서비스 탐색** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-129">Click **Explore additional Azure services** toocontinue.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. <span data-ttu-id="5ebae-130">Hello에 **서비스** 탭을 클릭  **+**  tooadd 앱에 대 한 SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-130">In hello **Services** tab, click **+** tooadd a SQL Database for your app.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. <span data-ttu-id="5ebae-131">**SQL 데이터베이스를 구성**, 클릭 **새로** toocreate SQL Server 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="5ebae-131">In **Configure SQL Database**, click **New** toocreate a SQL Server instance.</span></span>
8. <span data-ttu-id="5ebae-132">**SQL Server 구성**에서 SQL Server 인스턴스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-132">In **Configure SQL Server**, configure your SQL Server instance.</span></span> <span data-ttu-id="5ebae-133">클릭 **확인**, **확인**, 및 **만들기** tookick Azure의 hello 응용 프로그램 생성을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-133">Then, click **OK**, **OK**, and **Create** tookick off hello app creation in Azure.</span></span>
9. <span data-ttu-id="5ebae-134">**Azure 앱 서비스 활동**, hello 앱 작성이 완료 되 면 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-134">In **Azure App Service Activity**, you can see when hello app creation is finished.</span></span> <span data-ttu-id="5ebae-135">클릭  **게시 &lt;* appname*> toothis 웹 응용 프로그램 지금 * *를 클릭 한 다음 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-135">Click **Publish &lt;*appname*> toothis Web App now**, then click **Publish**.</span></span> 
   
    <span data-ttu-id="5ebae-136">Visual Studio 완료 되 면 hello 열립니다 hello 브라우저에서 앱을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-136">Once Visual Studio finishes, it opens hello publish app in hello browser.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a><span data-ttu-id="5ebae-137">인증 및 디렉터리 액세스 구성</span><span class="sxs-lookup"><span data-stu-id="5ebae-137">Configure authentication and directory access</span></span>
1. <span data-ttu-id="5ebae-138">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5ebae-139">Hello 왼쪽된 메뉴에서 클릭 **응용 프로그램 서비스** > **&lt;*appname*> * * > **인증 / 권한 부여**.</span><span class="sxs-lookup"><span data-stu-id="5ebae-139">From hello left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. <span data-ttu-id="5ebae-140">**켜기** > **Azure Active Directory** > **Express** > **확인**을 클릭하여 Azure Active Directory 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. <span data-ttu-id="5ebae-141">클릭 **저장** hello 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-141">Click **Save** in hello command bar.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    <span data-ttu-id="5ebae-142">Hello 인증 설정을 저장 했습니다., 탐색 tooyour 앱 hello 브라우저에 다시 시도해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="5ebae-142">Once hello authentication settings are saved successfully, try navigating tooyour app again in hello browser.</span></span> <span data-ttu-id="5ebae-143">기본 설정을 hello 전체 응용 프로그램에서 인증을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-143">Your default settings enforce authentication on hello whole app.</span></span> <span data-ttu-id="5ebae-144">로그인 하지 않은 이미를 모르는 경우 리디렉션된 tooa 로그인 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-144">If you aren't already logged in, you are redirected tooa login screen.</span></span> <span data-ttu-id="5ebae-145">로그인하면 HTTPS에서 보호하는 앱을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-145">Once logged in, you see your app secured by HTTPS.</span></span> <span data-ttu-id="5ebae-146">다음으로, tooenable toodirectory 데이터에 액세스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-146">Next, you need tooenable access toodirectory data.</span></span> 
5. <span data-ttu-id="5ebae-147">Toohello 이동 [클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-147">Navigate toohello [classic portal](https://manage.windowsazure.com).</span></span>
6. <span data-ttu-id="5ebae-148">Hello 왼쪽된 메뉴에서 클릭 **Active Directory** > **기본 디렉터리** > **응용 프로그램**  >   **&lt;* appname*> * *입니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-148">From hello left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    <span data-ttu-id="5ebae-149">앱 서비스 있습니다 tooenable hello 권한 부여에 대해 생성 hello Azure Active Directory 응용 프로그램 / 인증 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-149">This is hello Azure Active Directory application that App Service created for you tooenable hello Authorization / Authentication feature.</span></span>
7. <span data-ttu-id="5ebae-150">클릭 **사용자** 및 **그룹** toomake hello 디렉터리에서 일부 사용자 및 그룹 갖도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-150">Click **Users** and **Groups** toomake sure that you have some users and groups in hello directory.</span></span> <span data-ttu-id="5ebae-151">그렇지 않은 경우 몇 가지 테스트 사용자 및 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-151">If not, create a few test users and groups.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. <span data-ttu-id="5ebae-152">클릭 **구성** tooconfigure이 응용이 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-152">Click **Configure** tooconfigure this application.</span></span>
9. <span data-ttu-id="5ebae-153">Toohello 아래로 스크롤하여 **키** 섹션 및 기간을 선택 하 여 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-153">Scroll down toohello **Keys** section and add a key by selecting a duration.</span></span> <span data-ttu-id="5ebae-154">그런 다음 **위임된 사용 권한**을 클릭하고 **디렉터리 데이터 읽기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-154">Then, click **Delegated Permissions** and select **Read directory data**.</span></span> 
   <span data-ttu-id="5ebae-155">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-155">Click **Save**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. <span data-ttu-id="5ebae-156">설정이 저장 되 면 toohello 위로 다시 스크롤하고 **키** 섹션 및 hello 클릭 **복사** 단추 toocopy hello 클라이언트 키입니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-156">Once your settings are saved, scroll back up toohello **Keys** section and click hello **Copy** button toocopy hello client key.</span></span> 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="5ebae-157">이 페이지에서 이제 이동 하는 경우이 클라이언트 키를 다시 적이 수 tooaccess 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-157">If you navigate away from this page now, you won't be able tooaccess this client key ever again.</span></span>
    > 
    > 
11. <span data-ttu-id="5ebae-158">다음으로, 해야 tooconfigure 웹 앱이이 키와 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-158">Next, you need tooconfigure your web app with this key.</span></span> <span data-ttu-id="5ebae-159">Toohello 로그인 [Azure 리소스 탐색기](https://resources.azure.com) Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="5ebae-159">Log in toohello [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span></span>
12. <span data-ttu-id="5ebae-160">Hello hello 페이지의 위쪽에 클릭 **읽기/쓰기** hello Azure 리소스 탐색기의에서 toomake 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-160">At hello top of hello page, click **Read/Write** toomake changes in hello Azure Resource Explorer.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. <span data-ttu-id="5ebae-161">구독에 있는 앱에 대 한 인증 설정을 hello 찾기 >  **&lt;* subscriptionname*> * * > **resourceGroups**  >   **&lt;* resourcegroupname*> * * > **공급자** > **Microsoft.Web**  >  **사이트** > **&lt;*appname*> * * > **config**  >  **authsettings**합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-161">Find hello authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span></span>
14. <span data-ttu-id="5ebae-162">**편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-162">Click **Edit**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. <span data-ttu-id="5ebae-163">Hello 편집 창, 설정 hello `clientSecret` 및 `additionalLoginParams` 다음과 같이 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-163">In hello editing pane, set hello `clientSecret` and `additionalLoginParams` properties as follows.</span></span>
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. <span data-ttu-id="5ebae-164">클릭 **배치** 에 hello 상위 toosubmit 변경 내용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-164">Click **Put** at hello top toosubmit your changes.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. <span data-ttu-id="5ebae-165">권한이 없으면 hello tooaccess hello Azure Active Directory 그래프 API 토큰, 방금로 tootest 이제  **https://&lt;*appname*>에서.azurewebsites.net/.auth/me** 프로그램 브라우저.</span><span class="sxs-lookup"><span data-stu-id="5ebae-165">Now, tootest if you have hello authorization token tooaccess hello Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span></span> <span data-ttu-id="5ebae-166">Hello 올바르게 모든 작업을 구성 하는 경우 나타납니다 `access_token` hello JSON 응답의에서 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-166">If you configured everything correctly, you should see hello `access_token` property in hello JSON response.</span></span>
    
    <span data-ttu-id="5ebae-167">hello `~/.auth/me` 서비스 인증 앱에서 관리 하는 URL 경로 / 권한 부여 toogive 모든 hello 정보 관련 tooyour 인증 된 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-167">hello `~/.auth/me` URL path is managed by App Service Authentication / Authorization toogive you all hello information related tooyour authenticated session.</span></span> <span data-ttu-id="5ebae-168">자세한 내용은 [Azure App Service에서 인증 및 권한 부여](../app-service/app-service-authentication-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ebae-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="5ebae-169">hello `access_token` 기간이 만료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-169">hello `access_token` has an expiration period.</span></span> <span data-ttu-id="5ebae-170">그러나 App Service 인증/권한 부여는 `~/.auth/refresh`를 사용하여 토큰 새로 고침 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span></span> <span data-ttu-id="5ebae-171">방법에 대 한 자세한 내용은 toouse, 참조 [응용 프로그램 서비스 토큰 저장소](https://cgillum.tech/2016/03/07/app-service-token-store/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-171">For more information on how toouse it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span></span>
    > 
    > 

<span data-ttu-id="5ebae-172">다음으로, 디렉터리 데이터에 유용한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-172">Next, you will do something useful with directory data.</span></span>

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a><span data-ttu-id="5ebae-173">기간 업무 기능 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="5ebae-173">Add line-of-business functionality tooyour app</span></span>
<span data-ttu-id="5ebae-174">이제 간단한 CRUD 작업 항목 추적기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-174">Now, you create a simple CRUD work items tracker.</span></span>  

1. <span data-ttu-id="5ebae-175">Hello ~\Models 폴더 WorkItem.cs, 클래스 파일을 만들 및 바꾸기 `public class WorkItem {...}` 코드 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="5ebae-175">In hello ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with hello following code:</span></span>
   
     <span data-ttu-id="5ebae-176">using System.ComponentModel.DataAnnotations;</span><span class="sxs-lookup"><span data-stu-id="5ebae-176">using System.ComponentModel.DataAnnotations;</span></span>
   
     <span data-ttu-id="5ebae-177">public class WorkItem   {</span><span class="sxs-lookup"><span data-stu-id="5ebae-177">public class WorkItem   {</span></span>
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     <span data-ttu-id="5ebae-178">}</span><span class="sxs-lookup"><span data-stu-id="5ebae-178">}</span></span>
   
     <span data-ttu-id="5ebae-179">public enum WorkItemStatus   {</span><span class="sxs-lookup"><span data-stu-id="5ebae-179">public enum WorkItemStatus   {</span></span>
   
         Open,
         Investigating,
         Resolved,
         Closed
     <span data-ttu-id="5ebae-180">}</span><span class="sxs-lookup"><span data-stu-id="5ebae-180">}</span></span>
2. <span data-ttu-id="5ebae-181">Visual Studio에서 새 모델 액세스할 수 있는 toohello 스 캐 폴딩 논리 hello 프로젝트 toomake를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="5ebae-181">Build hello project toomake your new model accessible toohello scaffolding logic in Visual Studio.</span></span>
3. <span data-ttu-id="5ebae-182">새 스 캐 폴드 항목을 추가 `WorkItemsController` toohello ~\Controllers 폴더 (마우스 오른쪽 단추로 클릭 **컨트롤러**, 너무 가리킨**추가**를 선택 하 고 **새 스 캐 폴드 항목**).</span><span class="sxs-lookup"><span data-stu-id="5ebae-182">Add a new scaffolded item `WorkItemsController` toohello ~\Controllers folder (right-click **Controllers**, point too**Add**, and select **New scaffolded item**).</span></span> 
4. <span data-ttu-id="5ebae-183">**뷰가 포함된 MVC 5 컨트롤러, Entity Framework 사용**을 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span></span>
5. <span data-ttu-id="5ebae-184">선택 hello 만든 모델을를 차례로 클릭 합니다.  **+**  차례로 **추가** tooadd 데이터 컨텍스트를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-184">Select hello model that you created, then click **+** and then **Add** tooadd a data context, and then click **Add**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. <span data-ttu-id="5ebae-185">(자동으로 스 캐 폴드 항목) ~\Views\WorkItems\Create.cshtml hello를 찾습니다 `Html.BeginForm` 도우미 메서드 hello 다음 표시 된 변경 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find hello `Html.BeginForm` helper method and make hello following highlighted changes:</span></span>  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   <span data-ttu-id="5ebae-186">`token` 및 `tenant` hello에서 사용 `AadPicker` 개체 toomake Azure Active Directory Graph API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-186">Note that `token` and `tenant` are used by hello `AadPicker` object toomake Azure Active Directory Graph API calls.</span></span> <span data-ttu-id="5ebae-187">나중에 `AadPicker` 를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-187">You'll add `AadPicker` later.</span></span>     
   
   > [!NOTE]
   > <span data-ttu-id="5ebae-188">와 마찬가지로 얻을 수 있습니다 `token` 및 `tenant` 와 hello 클라이언트 쪽에서 `~/.auth/me`했지만 해당 추가 서버 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-188">You can just as well get `token` and `tenant` from hello client side with `~/.auth/me`, but that would be an additional server call.</span></span> <span data-ttu-id="5ebae-189">예:</span><span class="sxs-lookup"><span data-stu-id="5ebae-189">For example:</span></span>
   > 
   > <span data-ttu-id="5ebae-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span><span class="sxs-lookup"><span data-stu-id="5ebae-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span></span>
   > 
   > 
7. <span data-ttu-id="5ebae-191">동일 하 게 hello 변경 된 ~ \Views\WorkItems\Edit.cshtml 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-191">Make hello same changes with ~\Views\WorkItems\Edit.cshtml.</span></span>
8. <span data-ttu-id="5ebae-192">hello `AadPicker` tooadd tooyour 프로젝트 해야 하는 개체가 스크립트에 정의 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-192">hello `AadPicker` object is defined in a script that you need tooadd tooyour project.</span></span> <span data-ttu-id="5ebae-193">Hello ~\Scripts 폴더를 마우스 오른쪽 단추로 클릭, 너무 가리킨**추가**를 클릭 하 고 **JavaScript 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-193">Right-click hello ~\Scripts folder, point too**Add**, and click **JavaScript file**.</span></span> <span data-ttu-id="5ebae-194">형식 `AadPickerLibrary` hello 파일 이름 및 클릭에 대 한 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-194">Type `AadPickerLibrary` for hello filename and click **OK**.</span></span>
9. <span data-ttu-id="5ebae-195">Hello 콘텐츠를 복사할 [여기](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) 에 ~ \Scripts\AadPickerLibrary.js 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-195">Copy hello content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span></span>
   
   <span data-ttu-id="5ebae-196">Hello 스크립트에 hello `AadPicker` 호출 개체 [Azure Active Directory 그래프 API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch hello 입력과 일치 있는 사용자 및 그룹에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-196">In hello script, hello `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch for users and groups that match hello input.</span></span>  
10. <span data-ttu-id="5ebae-197">또한 사용 하 여 hello ~\Scripts\AadPickerLibrary.js [jQuery UI 자동 완성 위젯](https://jqueryui.com/autocomplete/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-197">~\Scripts\AadPickerLibrary.js also uses hello [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span></span> <span data-ttu-id="5ebae-198">따라서 tooadd jQuery UI tooyour 프로젝트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-198">So you need tooadd jQuery UI tooyour project.</span></span> <span data-ttu-id="5ebae-199">프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-199">Right-click your project in and click **Manage NuGet Packages**.</span></span>
11. <span data-ttu-id="5ebae-200">NuGet 패키지 관리자 hello에서 찾아보기를 클릭 형식 **jquery ui** 검색 표시줄을 hello와 클릭 **jQuery.UI.Combined**합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-200">In hello NuGet Package Manager, click Browse, type **jquery-ui** in hello search bar, and click **jQuery.UI.Combined**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. <span data-ttu-id="5ebae-201">Hello 오른쪽 창에서 클릭 **설치**, 클릭 **확인** tooproceed 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-201">In hello right pane, click **Install**, then click **OK** tooproceed.</span></span>
13. <span data-ttu-id="5ebae-202">~\App_Start\BundleConfig.cs 열고 hello 다음 표시 된 변경 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-202">Open ~\App_Start\BundleConfig.cs and make hello following highlighted changes:</span></span>  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    <span data-ttu-id="5ebae-203">더 많은 성능이 뛰어난 방법으로 toomanage JavaScript 및 CSS 파일 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-203">There are more performant ways toomanage JavaScript and CSS files in your app.</span></span> <span data-ttu-id="5ebae-204">그러나 편의상 방금 갈 때 toopiggyback hello 번들으로 모든 보기를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-204">However, for simplicity you're just going toopiggyback on hello bundles that are loaded with every view.</span></span>
14. <span data-ttu-id="5ebae-205">마지막으로, ~, \Global.asax hello 다음 hello에 대 한 코드 줄을 추가 `Application_Start()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="5ebae-205">Finally, in ~\Global.asax, add hello following line of code in hello `Application_Start()` method.</span></span> <span data-ttu-id="5ebae-206">`Ctrl`+`.`각 명명 해상도에 오류가 너무 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-206">`Ctrl`+`.` on each naming resolution error too fix it.</span></span>
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > <span data-ttu-id="5ebae-207">Hello 기본 MVC 템플릿의 사용 하기 때문에이 코드 줄을 해야 <code>[ValidateAntiForgeryToken]</code> hello 작업 중 일부에 장식입니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-207">You need this line of code because hello default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of hello actions.</span></span> <span data-ttu-id="5ebae-208">설명 된 toohello 동작 인해 [Brock Allen](https://twitter.com/BrockLAllen) 에서 [MVC 4, AntiForgeryToken 및 클레임](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) 때문에 HTTP POST 위조 방지 토큰 유효성 검사를 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-208">Due toohello behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span></span>
    > 
    > * <span data-ttu-id="5ebae-209">Azure Active Directory hello 위조 방지 토큰에 의해 기본적으로 필요한 hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider를 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-209">Azure Active Directory does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by hello anti-forgery token.</span></span>
    > * <span data-ttu-id="5ebae-210">Azure Active Directory 동기화 및 AD FS 디렉터리 이면, 기본적으로 AD FS hello 신뢰 보내지 않습니다 hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider 클레임, AD FS toosend를 수동으로 구성할 수 있지만 이 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-210">If Azure Active Directory is directory synced with AD FS, hello AD FS trust by default does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS toosend this claim.</span></span>
    > 
    > <span data-ttu-id="5ebae-211">`ClaimTypes.NameIdentifies`hello 클레임을 지정 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, Azure Active Directory에서 제공 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-211">`ClaimTypes.NameIdentifies` specifies hello claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span></span>  
    > 
    > 
15. <span data-ttu-id="5ebae-212">이제 변경 내용을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-212">Now, publish your changes.</span></span> <span data-ttu-id="5ebae-213">프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-213">Right-click your project and click **Publish**.</span></span>
16. <span data-ttu-id="5ebae-214">클릭 **설정**없는지 확인 한 연결 문자열 tooyour SQL 데이터베이스, 선택, **데이터베이스 업데이트** toomake 스키마 변경 내용을 모델에 대 한 hello 및 클릭 **게시** .</span><span class="sxs-lookup"><span data-stu-id="5ebae-214">Click **Settings**, make sure there is a connection string tooyour SQL Database, select **Update Database** toomake hello schema changes for your model, and click **Publish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. <span data-ttu-id="5ebae-215">Hello 브라우저에서 탐색 toohttps: / /&lt;*appname*>.azurewebsites.net/workitems 누른 **새로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-215">In hello browser, navigate toohttps://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span></span>
18. <span data-ttu-id="5ebae-216">Hello에 클릭 **AssignedToName** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-216">Click in hello **AssignedToName** box.</span></span> <span data-ttu-id="5ebae-217">드롭다운에서 Azure Active Directory 테넌트의 사용자 및 그룹이 이제 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span></span> <span data-ttu-id="5ebae-218">Toofilter를 입력할 수도 있고 hello를 사용 하 여 `Up` 또는 `Down` 키 또는 tooselect hello 사용자 또는 그룹을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-218">You can type toofilter, or use hello `Up` or `Down` key or click tooselect hello user or group.</span></span> 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. <span data-ttu-id="5ebae-219">클릭 **만들기** toosave hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-219">Click **Create** toosave hello changes.</span></span> <span data-ttu-id="5ebae-220">클릭 **편집** hello 만든 작업 항목 tooobserve hello 동작이 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-220">Then, click **Edit** on hello created work item tooobserve hello same behavior.</span></span>

<span data-ttu-id="5ebae-221">축하합니다. 이제 디렉터리 액세스 권한으로 Azure에서 LOB(기간 업무) 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span></span> <span data-ttu-id="5ebae-222">더 많은 hello Graph API로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-222">There's a lot more you can do with hello Graph API.</span></span> <span data-ttu-id="5ebae-223">[Azure AD Graph API 참조](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ebae-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span>

<a name="next"></a>

## <a name="next-step"></a><span data-ttu-id="5ebae-224">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ebae-224">Next Step</span></span>
<span data-ttu-id="5ebae-225">Azure에서 기간 업무 앱에 대 한 역할 기반 액세스 제어 (RBAC) 해야 할 경우 참조 [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) hello Azure Active Directory 팀에서 샘플에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from hello Azure Active Directory team.</span></span> <span data-ttu-id="5ebae-226">그 표시 하는 Azure Active Directory 응용 프로그램에 대 한 tooenable 역할 hello로 사용자에 게 권한을 부여 하 고 `[Authorize]` 장식 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-226">It shows you how tooenable roles for your Azure Active Directory application, and then authorize users with hello `[Authorize]` decoration.</span></span>

<span data-ttu-id="5ebae-227">기간 업무 앱 tooon 온-프레미스 데이터에 액세스 해야 하는 경우 참조 [액세스 온-프레미스 하이브리드 연결을 사용 하 여 Azure 앱 서비스의 리소스](web-sites-hybrid-connection-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ebae-227">If your line-of-business app needs access tooon-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="5ebae-228">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5ebae-228">Further resources</span></span>
* [<span data-ttu-id="5ebae-229">Azure 앱 서비스의 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="5ebae-229">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)
* [<span data-ttu-id="5ebae-230">Azure 앱에서 온-프레미스 Active Directory를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="5ebae-230">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="5ebae-231">AD FS 인증을 사용하여 Azure에서 LOB(기간 업무) 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="5ebae-231">Create a line-of-business app in Azure with AD FS authentication</span></span>](web-sites-dotnet-lob-application-adfs.md)
* [<span data-ttu-id="5ebae-232">앱 서비스 인증 및 hello Azure AD Graph API</span><span class="sxs-lookup"><span data-stu-id="5ebae-232">App Service Auth and hello Azure AD Graph API</span></span>](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [<span data-ttu-id="5ebae-233">Microsoft Azure Active Directory 샘플 및 설명서</span><span class="sxs-lookup"><span data-stu-id="5ebae-233">Microsoft Azure Active Directory Samples and Documentation</span></span>](https://github.com/AzureADSamples)
* [<span data-ttu-id="5ebae-234">Azure Active Directory 지원 토큰 및 클레임 유형</span><span class="sxs-lookup"><span data-stu-id="5ebae-234">Azure Active Directory Supported Token and Claim Types</span></span>](http://msdn.microsoft.com/library/azure/dn195587.aspx)
