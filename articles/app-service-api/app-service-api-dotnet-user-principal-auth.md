---
title: "Azure App Service의 API 앱에 대한 사용자 인증 | Microsoft Docs"
description: "인증된 사용자에게만 액세스를 허용하여 Azure 앱 서비스에서 API 앱을 보호하는 방법을 알아봅니다."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 3896760d-46ff-4b67-b98a-edd233f24758
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: a5b713f3a60b3886d813438496d704f464d914e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a><span data-ttu-id="c80b1-103">Azure 앱 서비스의 API 앱에 대한 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="c80b1-103">User authentication for API Apps in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="c80b1-104">개요</span><span class="sxs-lookup"><span data-stu-id="c80b1-104">Overview</span></span>
<span data-ttu-id="c80b1-105">이 문서는 인증된 사용자만 호출할 수 있도록 Azure API 앱을 보호하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-105">This article shows how to protect an Azure API app so that only authenticated users can call it.</span></span> <span data-ttu-id="c80b1-106">문서는 [Azure 앱 서비스 인증 개요](../app-service/app-service-authentication-overview.md)를 읽었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-106">The article assumes that you have read the [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span>

<span data-ttu-id="c80b1-107">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-107">You'll learn:</span></span>

* <span data-ttu-id="c80b1-108">인증 공급자 구성 방법 및 Azure AD(Azure Active Directory)에 대한 세부 정보</span><span class="sxs-lookup"><span data-stu-id="c80b1-108">How to configure an authentication provider, with details for Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="c80b1-109">[JavaScript용 ADAL(Active Directory 인증 라이브러리)](https://github.com/AzureAD/azure-activedirectory-library-for-js)을 사용하여 보호되는 API 앱 사용 방법</span><span class="sxs-lookup"><span data-stu-id="c80b1-109">How to consume a protected API app by using the [Active Directory Authentication Library (ADAL) for JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js).</span></span>

<span data-ttu-id="c80b1-110">이 문서에는 두 섹션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-110">The article contains two sections:</span></span>

* <span data-ttu-id="c80b1-111">[Azure 앱 서비스에서 사용자 인증을 구성하는 방법](#authconfig) 섹션은 모든 API 앱에 사용자 인증을 구성하는 방법을 일반적으로 설명하며 .NET, Node.js 및 Java 등, 앱 서비스에서 지원하는 모든 프레임워크에 동일하게 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-111">The [How to configure user authentication in Azure App Service](#authconfig) section explains in general how to configure user authentication for any API app and applies equally to all frameworks supported by App Service, including .NET, Node.js, and Java.</span></span>
* <span data-ttu-id="c80b1-112">[.NET API 앱 자습서 계속](#tutorialstart) 섹션으로 시작하는 이 문서는 사용자 인증에 Azure Active Directory를 사용할 수 있도록 .NET 백 엔드 및 AngularJS 프런트 엔드로 응용 프로그램 예제를 구성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-112">Starting with the [Continuing the .NET API Apps tutorials](#tutorialstart) section, the article guides you through configuring a sample application with a .NET back end and an AngularJS front end so that it uses Azure Active Directory for user authentication.</span></span> 

## <span data-ttu-id="c80b1-113"><a id="authconfig"></a> Azure 앱 서비스의 사용자 인증 구성 방법</span><span class="sxs-lookup"><span data-stu-id="c80b1-113"><a id="authconfig"></a> How to configure user authentication in Azure App Service</span></span>
<span data-ttu-id="c80b1-114">이 섹션에서는 모든 API 앱에 적용되는 일반적인 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-114">This section provides general instructions that apply to any API app.</span></span> <span data-ttu-id="c80b1-115">수행 목록 .NET 샘플 응용 프로그램에 특정한 단계는 [.NET 시작 자습서 계속](#tutorialstart)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-115">For steps specific to the To Do List .NET sample application, go to [Continuing the .NET getting-started tutorials](#tutorialstart).</span></span>

1. <span data-ttu-id="c80b1-116">[Azure 포털](https://portal.azure.com/)에서 보호할 API 앱의 **설정** 블레이드로 이동하고 **기능** 섹션을 찾은 후 **인증/권한 부여**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-116">In the [Azure portal](https://portal.azure.com/), navigate to the **Settings** blade of the API app that you want to protect, find the **Features** section, and then click **Authentication/ Authorization**.</span></span>
   
    ![Azure 포털 인증/권한 부여](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. <span data-ttu-id="c80b1-118">**인증/권한 부여** 블레이드에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-118">In the **Authentication / Authorization** blade, click **On**.</span></span>
3. <span data-ttu-id="c80b1-119">**요청이 인증되지 않은 경우에 수행할 동작** 드롭다운 목록에서 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-119">Select one of the options from the **Action to take when request is not authenticated** drop-down list.</span></span>
   
   * <span data-ttu-id="c80b1-120">인증된 호출만 API 앱에 도달하게 하려면 **로그인 방법...** 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-120">If you want only authenticated calls to reach your API app, choose one of the **Log in with ...** options.</span></span> <span data-ttu-id="c80b1-121">이 옵션을 사용하면 안에서 실행되는 코드를 작성하지 않고도 API 앱을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-121">This option enables you to protect the API app without writing any code that runs in it.</span></span>
   * <span data-ttu-id="c80b1-122">모든 호출이 API 앱에 도달하게 하려면 **요청 허용(작업 없음)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-122">If you want all calls to reach your API app, choose **Allow request (no action)**.</span></span> <span data-ttu-id="c80b1-123">이 옵션을 사용하여 인증되지 않은 호출자를 선택된 인증 공급자에게 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-123">You can use this option to direct unauthenticated callers to a choice of authentication providers.</span></span> <span data-ttu-id="c80b1-124">이 옵션에서는 권한 부여를 처리하는 코드를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-124">With this option you have to write code to handle authorization.</span></span>
     
     <span data-ttu-id="c80b1-125">자세한 내용은 [Azure 앱 서비스의 API 앱에 대한 인증 및 권한 부여](app-service-api-authentication.md#multiple-protection-options)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c80b1-125">For more information, see [Authentication and authorization for API Apps in Azure App Service](app-service-api-authentication.md#multiple-protection-options).</span></span>
4. <span data-ttu-id="c80b1-126">하나 이상의 **인증 공급자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-126">Select one or more of the **Authentication Providers**.</span></span>
   
    <span data-ttu-id="c80b1-127">아래 이미지는 Azure AD에서 모든 호출자를 인증하도록 하는 선택 항목을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-127">The image shows    choices that require all callers to be authenticated by Azure AD.</span></span>
   
    ![Azure 포털 인증/권한 부여 블레이드](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    <span data-ttu-id="c80b1-129">인증 공급자를 선택하면 해당 공급자에 대해 구성 블레이드가 포털에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-129">When you choose an authentication provider, the portal displays a configuration blade for that provider.</span></span> 
   
    <span data-ttu-id="c80b1-130">인증 공급자 구성 블레이드를 구성하는 방법을 설명하는 자세한 지침은 [Azure Active Directory 로그인을 사용하도록 앱 서비스 응용 프로그램을 구성하는 방법](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c80b1-130">For detailed instructions that explain how to configure the authentication provider configuration blades, see [How to configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span> <span data-ttu-id="c80b1-131">이 링크는 Azure AD에 대한 문서로 이동하지만 문서 자체에 다른 인증 공급자에 대한 글로 연결되는 탭이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-131">(The link goes to an article about Azure AD, but the article itself contains tabs that link to articles for the other authentication providers.)</span></span>
5. <span data-ttu-id="c80b1-132">인증 공급자 구성 블레이드를 마치면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-132">When you're done with the authentication provider configuration blade, click **OK**.</span></span>
6. <span data-ttu-id="c80b1-133">**인증/권한 부여** 블레이드에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-133">In the **Authentication / Authorization** blade, click **Save**.</span></span>

<span data-ttu-id="c80b1-134">이 작업을 마치면 앱 서비스는 API 호출이 API 앱에 도달하기 전에 모든 API 호출을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-134">When this is done, App Service authenticates all API calls before they reach the API app.</span></span> <span data-ttu-id="c80b1-135">인증 서비스는 .NET, Node.js, Java 등, API 서비스가 지원하는 모든 언어에 동일하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-135">The authentication services work the same for all languages that App service supports, including .NET, Node.js, and Java.</span></span> 

<span data-ttu-id="c80b1-136">인증된 API를 호출하려면 호출자가 인증 공급자의 OAuth 2.0 전달자 토큰을 HTTP 요청의 Authorization 헤더에 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-136">To make authenticated API calls, the caller includes the authentication provider's OAuth 2.0 bearer token in the Authorization header of HTTP requests.</span></span> <span data-ttu-id="c80b1-137">이 토큰은 인증 공급자의 SDK를 사용하여 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-137">The token can be acquired by using the authentication provider's SDK.</span></span>

## <span data-ttu-id="c80b1-138"><a id="tutorialstart"></a> .NET API 앱 자습서 계속</span><span class="sxs-lookup"><span data-stu-id="c80b1-138"><a id="tutorialstart"></a> Continuing the .NET API Apps tutorials</span></span>
<span data-ttu-id="c80b1-139">API 앱에 대한 Node.js 또는 Java 자습서를 진행 중인 경우 다음 글인 [API 앱용 서비스 주체 인증](app-service-api-dotnet-service-principal-auth.md)으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-139">If you are following the Node.js or Java tutorials for API apps, skip to the next article, [service principal authentication for API apps](app-service-api-dotnet-service-principal-auth.md).</span></span> 

<span data-ttu-id="c80b1-140">API 앱에 대한 .NET 자습서를 따르고 있고 이미 [첫 번째](app-service-api-dotnet-get-started.md) 및 [두 번째](app-service-api-cors-consume-javascript.md) 자습서에서 지시한 대로 샘플 응용 프로그램을 배포한 경우 [App Service와 Azure AD에서 인증 설정](#azureauth) 섹션으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-140">If you are following the .NET tutorial series for API apps and have already deployed the sample application as directed in the [first](app-service-api-dotnet-get-started.md) and [second](app-service-api-cors-consume-javascript.md) tutorials, skip to the [Set up authentication in App Service and Azure AD](#azureauth) section.</span></span>

<span data-ttu-id="c80b1-141">첫 번째 및 두 번째 자습서를 통하지 않고 이 자습서를 수행하려는 경우 샘플 응용 프로그램을 배포하기 위해 자동화된 프로세스를 사용하여 시작하는 방법을 설명하는 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-141">If you want to follow this tutorial without going through the first and second tutorials, do the following steps which explain how to get started by using an automated process to deploy the sample application.</span></span>

> [!NOTE]
> <span data-ttu-id="c80b1-142">다음 단계는 마치 앞 쪽의 두 가지 자습서를 수행한 것 같이, 동일한 시작 지점을 만들어 주지만, 한가지 예외 사항이 있습니다. Visual Studio에서는 각 프로젝트가 배포되는 웹앱 또는 API 앱이 무엇인지 알지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-142">The following steps get you to the same starting point as if you did the first two tutorials, with one exception: Visual Studio won't already know which web app or API app that each project gets deployed to.</span></span> <span data-ttu-id="c80b1-143">즉, 이 자습서에는 올바른 대상에 배포하는 방법을 설명하는 정확한 지침이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-143">That means you won't have exact instructions in this tutorial that explain how to deploy to the right targets.</span></span> <span data-ttu-id="c80b1-144">직접 배포 단계를 수행하는 방법을 알아내기 어려운 경우 자동화된 배포 프로세스를 시작하지 않고 [첫 번째 자습서](app-service-api-dotnet-get-started.md)에서 자습서 시리즈를 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-144">If you're not comfortable with figuring out how to do the deployment steps on your own, it's better to follow the tutorial series from the [first tutorial](app-service-api-dotnet-get-started.md) than to start with this automated deployment process.</span></span>
> 
> 

1. <span data-ttu-id="c80b1-145">[첫 번째 자습서](app-service-api-dotnet-get-started.md)에 나열된 모든 필수 조건이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-145">Make sure that you have all of the prerequisites listed in the [first tutorial](app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="c80b1-146">필수 조건 목록 외에도, 이 인증 자습서에서는 Visual Studio 및 Azure 포털에서 앱 서비스 웹앱 및 API 앱 작업을 수행한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-146">In addition to the prerequisites listed, these authentication tutorials assume that you have worked with App Service web apps and API apps in Visual Studio and the Azure portal.</span></span>
2. <span data-ttu-id="c80b1-147">[To Do List 샘플 리포지토리 추가 정보 파일](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md)의 **Azure에 배포** 단추를 클릭하여 API 앱을 웹앱에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-147">Click the **Deploy to Azure** button in the [To Do List sample repository readme file](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) to deploy the API apps and the web app.</span></span> <span data-ttu-id="c80b1-148">생성되는 Azure리소스 그룹을 기록해 둡니다. 나중에 웹앱 및 API 앱 이름을 조회하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-148">Make a note of the Azure resource group that gets created, as you can use this later to look up web app and API app names.</span></span>
3. <span data-ttu-id="c80b1-149">Visual Studio로 로컬에서 작업할 코드를 가져오려면 [To Do List 샘플 리포지토리](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) 를 다운로드하거나 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-149">Download or clone the [To Do List sample repository](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) to get the code that you'll work with locally in Visual Studio.</span></span>

## <span data-ttu-id="c80b1-150"><a id="azureauth"></a> 앱 서비스와 Azure AD에서 인증 설정</span><span class="sxs-lookup"><span data-stu-id="c80b1-150"><a id="azureauth"></a> Set up authentication in App Service and Azure AD</span></span>
<span data-ttu-id="c80b1-151">이제 사용자 인증을 요구하지 않고 Azure 앱 서비스를 실행하는 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-151">You now have the application running in Azure App Service without requiring that users be authenticated.</span></span> <span data-ttu-id="c80b1-152">이 섹션에서는 다음 작업을 수행하여 인증을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-152">In this section you add authentication by doing the following tasks:</span></span>

* <span data-ttu-id="c80b1-153">중간 계층 API 앱을 호출하기 위해 Azure AD(Active Directory) 인증을 요구하는 앱 서비스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-153">Configure App Service to require Azure Active Directory (Azure AD) authentication for calling the middle tier API app.</span></span>
* <span data-ttu-id="c80b1-154">Azure AD 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-154">Create an Azure AD application.</span></span>
* <span data-ttu-id="c80b1-155">로그온 후 AngularJS 프런트 엔드에 로그온한 후 전달자 토큰을 보내도록 Azure AD 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-155">Configure the Azure AD application to send the bearer token after logon to the AngularJS front end.</span></span> 

<span data-ttu-id="c80b1-156">자습서의 지침을 수행하는 동안 문제가 발생하는 경우 자습서 끝부분의 [문제 해결](#troubleshooting) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c80b1-156">If you run into problems while following the tutorial directions, see the [Troubleshooting](#troubleshooting) section at the end of the tutorial.</span></span> 

### <a name="configure-authentication-for-the-middle-tier-api-app"></a><span data-ttu-id="c80b1-157">중간 계층 API 앱에 대한 인증 구성</span><span class="sxs-lookup"><span data-stu-id="c80b1-157">Configure authentication for the middle tier API app</span></span>
1. <span data-ttu-id="c80b1-158">[Azure Portal](https://portal.azure.com/)에서 ToDoListAPI 프로젝트에 대해 만든 API 앱의 **설정** 블레이드로 이동하고 **기능** 섹션을 찾은 후 **인증/권한 부여**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-158">In the [Azure portal](https://portal.azure.com/), navigate to the **Settings** blade of the API app that you created for the ToDoListAPI project, find the **Features** section, and then click **Authentication / Authorization**.</span></span>
   
    ![Azure 포털 인증/권한 부여](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. <span data-ttu-id="c80b1-160">**인증/권한 부여** 블레이드에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-160">In the **Authentication / Authorization** blade, click **On**.</span></span>
3. <span data-ttu-id="c80b1-161">**요청이 인증되지 않은 경우에 수행할 동작** 드롭다운 목록에서 **Azure Active Directory를 사용하여 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-161">In the **Action to take when request is not authenticated** drop-down list, select **Log in with Azure Active Directory**.</span></span>
   
    <span data-ttu-id="c80b1-162">이 옵션을 사용하면 인증되지 않은 요청이 API 앱에 도달할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-162">This option ensures that no unauathenticated requests will reach the API app.</span></span> 
4. <span data-ttu-id="c80b1-163">**인증 공급자** 아래에서 **Azure Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-163">Under **Authentication Providers**, click **Azure Active Directory**.</span></span>
   
    ![Azure 포털 인증/권한 부여 블레이드](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. <span data-ttu-id="c80b1-165">**Azure Active Directory 설정** 블레이드에서 **Express**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-165">In the **Azure Active Directory Settings** blade, click **Express**</span></span>
   
    ![Azure 포털 인증/권한 부여 Express 옵션](./media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    <span data-ttu-id="c80b1-167">**Express** 옵션을 사용하면 Azure AD [테넌트](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant)에서 App Service가 자동으로 Azure AD 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-167">With the **Express** option, App Service can automatically create an Azure AD application in your Azure AD [tenant](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant).</span></span> 
   
    <span data-ttu-id="c80b1-168">자동으로 모든 Azure 계정에 하나씩 있기 때문에 테넌트를 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-168">You don't have to create a tenant, because every Azure account automatically has one.</span></span>
6. <span data-ttu-id="c80b1-169">**관리 모드** 아래에서 아직 선택되지 않은 경우 **새 AD 앱 만들기**를 클릭하고 **앱 만들기** 텍스트 상자에 있는 값을 확인합니다. 나중에 Azure 클래식 포털의 AAD 응용 프로그램에서 이 값을 조회합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-169">Under **Management mode**, click **Create New AD App** if it isn't already selected, and notice the value that is in the **Create App** text box; you'll look up this AAD application in the Azure classic portal later.</span></span>
   
    ![Azure 포털 Azure AD 설정](./media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    <span data-ttu-id="c80b1-171">Azure AD 테넌트에 표시된 이름으로 Azure AD 응용 프로그램이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-171">Azure will automatically create an Azure AD application with the indicated name in your Azure AD tenant.</span></span> <span data-ttu-id="c80b1-172">기본적으로 Azure AD 응용 프로그램의 이름은 API 앱과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-172">By default, the Azure AD application is named the same as the API app.</span></span> <span data-ttu-id="c80b1-173">원하는 경우 다른 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-173">If you prefer, you can enter a different name.</span></span>
7. <span data-ttu-id="c80b1-174">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-174">Click **OK**.</span></span>
8. <span data-ttu-id="c80b1-175">**인증/권한 부여** 블레이드에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-175">In the **Authentication / Authorization** blade, click **Save**.</span></span>
   
    ![저장을 클릭합니다.](./media/app-service-api-dotnet-user-principal-auth/authsave.png)

<span data-ttu-id="c80b1-177">이제 Azure AD 테넌트에 있는 사용자만 API 앱을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-177">Now only users in your Azure AD tenant can call the API app.</span></span>

### <a name="optional-test-the-api-app"></a><span data-ttu-id="c80b1-178">선택 사항: API 앱 테스트</span><span class="sxs-lookup"><span data-stu-id="c80b1-178">Optional: Test the API app</span></span>
1. <span data-ttu-id="c80b1-179">브라우저에서 API 앱의 URL로 이동: Azure Portal에서 **API 앱** 블레이드에서 **URL** 아래 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-179">In a browser go to the URL of the API app: in the **API app** blade in the Azure portal, click the link under **URL**.</span></span>  
   
    <span data-ttu-id="c80b1-180">인증되지 않은 요청은 API 앱에 도달할 수 없으므로 로그인 화면으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-180">You are redirected to a login screen because unauthenticated requests are not allowed to reach the API app.</span></span>
   
    <span data-ttu-id="c80b1-181">브라우저가 "만들기 성공" 페이지로 이동하면 브라우저에서 이미 로그온했을 수 있습니다. 이 경우 InPrivate 또는 Incognito 창을 열고 API 앱의 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-181">If your browser goes to the "successfully created" page, the browser might already be logged on -- in that case, open an InPrivate or Incognito window and go to the API app's URL.</span></span>
2. <span data-ttu-id="c80b1-182">Azure AD의 사용자에 대한 자격 증명으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-182">Log on using credentials for a user in your Azure AD tenant.</span></span>
   
    <span data-ttu-id="c80b1-183">로그온하면 "만들기 성공" 페이지가 브라우저에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-183">When you're logged on, the "successfully created" page appears in the browser.</span></span>
3. <span data-ttu-id="c80b1-184">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-184">Close the browser.</span></span>

### <a name="configure-the-azure-ad-application"></a><span data-ttu-id="c80b1-185">Azure AD 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="c80b1-185">Configure the Azure AD application</span></span>
<span data-ttu-id="c80b1-186">Azure AD 인증을 구성하면 앱 서비스가 사용자에 대한 Azure AD 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-186">When you configured Azure AD authentication, App Service created an Azure AD application for you.</span></span> <span data-ttu-id="c80b1-187">기본적으로 새 Azure AD 응용 프로그램은 API 앱의 URL에 전달자 토큰을 제공하도록 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-187">By default the new Azure AD application was configured to provide the bearer token to the API app's URL.</span></span> <span data-ttu-id="c80b1-188">이 섹션에서는 전달자 토큰을 중간 계층 API 앱에 직접 전달하는 대신 AngularJS 프런트 엔드에 제공하도록 Azure AD 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-188">In this section you configure the Azure AD application to provide the bearer token to the AngularJS front end instead of directly to the middle tier API app.</span></span> <span data-ttu-id="c80b1-189">AngularJS 프런트 엔드는 API 앱을 호출할 때 API 앱에 토큰을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-189">The AngularJS front end will send the token to the API app when it calls the API app.</span></span>

> [!NOTE]
> <span data-ttu-id="c80b1-190">프로세스를 가능한 단순하게 유지하기 위해 이 자습서에서는 프런트 엔드와 중간 계층 API 앱 모두에 대해 단일 Azure AD 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-190">To keep the process as simple as possible, this tutorial uses a single Azure AD application for both the front end and the middle tier API app.</span></span> <span data-ttu-id="c80b1-191">다른 방법은 두 개의 Azure AD 응용 프로그램을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-191">Another option is to use two Azure AD applications.</span></span> <span data-ttu-id="c80b1-192">이 경우 중간 계층의 Azure AD 응용 프로그램을 호출할 수 있는 프런트 엔드의 Azure AD 응용 프로그램 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-192">In that case you would have to give the front end's Azure AD application permission to call the middle tier's Azure AD application.</span></span> <span data-ttu-id="c80b1-193">다중 응용 프로그램 방법을 사용하면 각 계층에 대한 권한을 보다 세부적으로 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-193">This multi-application approach would give you more granular control over permissions to each tier.</span></span>
> 
> 

1. <span data-ttu-id="c80b1-194">[Azure 클래식 포털](https://manage.windowsazure.com/)에서 **Azure Active Directory**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-194">In the [Azure classic portal](https://manage.windowsazure.com/), go to **Azure Active Directory**.</span></span>
   
   <span data-ttu-id="c80b1-195">액세스해야 하는 특정 Azure Active Directory 설정을 아직 현재 Azure 포털에서 사용할 수 없으므로 클래식 포털을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-195">You have to use the classic portal because certain Azure Active Directory settings that you need access to are not yet available in the current Azure portal.</span></span>
2. <span data-ttu-id="c80b1-196">**디렉터리** 탭에서 AAD 테넌트를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-196">On the **Directory** tab, click your AAD tenant.</span></span>
   
   ![클래식 포털에서 Azure AD](./media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. <span data-ttu-id="c80b1-198">**응용 프로그램 > 회사 소유 응용 프로그램**을 클릭한 다음 확인 표시를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-198">Click **Applications > Applications my company owns**, and then click the check mark.</span></span>
   
   <span data-ttu-id="c80b1-199">페이지를 새로 고쳐야 새 응용 프로그램이 나타날 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-199">You might also have to refresh the page to see the new application.</span></span>
4. <span data-ttu-id="c80b1-200">응용 프로그램 목록에서 API 앱에 대한 인증을 활성화할 때 만들어진 응용 프로그램의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-200">In the list of applications, click the name of the one that Azure created for you when you enabled authentication for your API app.</span></span>
   
   ![Azure AD 응용 프로그램 탭](./media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. <span data-ttu-id="c80b1-202">**Configure**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-202">Click **Configure**.</span></span>
   
   ![Azure AD 구성 탭](./media/app-service-api-dotnet-user-principal-auth/configure.png)
6. <span data-ttu-id="c80b1-204">**로그온 URL**을 AngularJS 웹앱의 URL로 설정합니다. 마지막 슬래시는 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-204">Set **Sign-on URL** to the URL for your AngularJS web app, no trailing slash.</span></span>
   
   <span data-ttu-id="c80b1-205">예: https://todolistangular.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="c80b1-205">For example: https://todolistangular.azurewebsites.net</span></span>
   
   ![로그온 URL](./media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. <span data-ttu-id="c80b1-207">**회신 URL**을 웹앱의 URL로 설정합니다. 마지막 슬래시는 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-207">Set **Reply URL** to the URL for your web app, no trailing slash.</span></span>
   
   <span data-ttu-id="c80b1-208">예: https://todolistsangular.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="c80b1-208">For example: https://todolistsangular.azurewebsites.net</span></span>
8. <span data-ttu-id="c80b1-209">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-209">Click **Save**.</span></span>
   
   ![회신 URL](./media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. <span data-ttu-id="c80b1-211">페이지의 아래쪽에서 **매니페스트 관리 > 매니페스트 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-211">At the bottom of the page, click **Manage manifest > Download manifest**.</span></span>
   
   ![매니페스트 다운로드](./media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. <span data-ttu-id="c80b1-213">편집할 수 있는 위치에 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-213">Download the file to a location where you can edit it.</span></span>
11. <span data-ttu-id="c80b1-214">다운로드한 매니페스트 파일에서 `oauth2AllowImplicitFlow` 속성을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-214">In the downloaded manifest file, search for the  `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="c80b1-215">이 속성의 값을 `false`에서 `true`로 변경하고 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-215">Change the value of this property from `false` to `true`, and then save the file.</span></span>
    
    <span data-ttu-id="c80b1-216">이 설정은 JavaScript 단일 페이지 응용 프로그램에서 액세스를 위해 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-216">This setting is required for access from a JavaScript single-page application.</span></span> <span data-ttu-id="c80b1-217">Oauth 2.0 전달자 토큰이 URL 조각에 반환되게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-217">It enables the Oauth 2.0 bearer token to be returned in the URL fragment.</span></span>
12. <span data-ttu-id="c80b1-218">**매니페스트 관리 > 매니페스트 업로드**를 클릭하고 이전 단계에서 업데이트한 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-218">Click **Manage manifest > Upload manifest**, and upload the file that you updated in the preceding step.</span></span>
    
    ![매니페스트 업로드](./media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. <span data-ttu-id="c80b1-220">**클라이언트 ID** 값을 복사하여 나중에 가져올 수 있는 위치에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-220">Copy the **Client ID** value and save it somewhere you can get it from later.</span></span>

## <a name="configure-the-todolistangular-project-to-use-authentication"></a><span data-ttu-id="c80b1-221">인증을 사용하도록 ToDoListAngular 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="c80b1-221">Configure the ToDoListAngular project to use authentication</span></span>
<span data-ttu-id="c80b1-222">이 섹션에서는 JS에 ADAL(Active Directory 인증 라이브러리)을 사용하여 Azure AD로부터 로그온한 사용자의 전달자 토큰을 획득하도록 AngularJS 프런트 엔드를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-222">In this section you change the AngularJS front end so that it uses Active Directory Authentication Library (ADAL) for JS to acquire a bearer token for the logged-on user from Azure AD.</span></span> <span data-ttu-id="c80b1-223">이 코드는 다음 다이어그램에서처럼 중간 계층으로 보낸 HTTP 요청에 토큰을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-223">The code will include the token in HTTP requests sent to the middle tier, as shown in the following diagram.</span></span> 

![사용자 인증 다이어그램](./media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

<span data-ttu-id="c80b1-225">ToDoListAngular 프로젝트의 파일을 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-225">Make the following changes to files in the ToDoListAngular project.</span></span>

1. <span data-ttu-id="c80b1-226">*Index.cshtml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-226">Open the *index.cshtml* file.</span></span>
2. <span data-ttu-id="c80b1-227">ADAL(Active Directory 인증 라이브러리)를 참조하는 줄의 주석 처리를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-227">Uncomment the lines that reference the Active Directory Authentication Library (ADAL) for JS scripts.</span></span>
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. <span data-ttu-id="c80b1-228">*app/scripts/app.js* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-228">Open the *app/scripts/app.js* file.</span></span>
4. <span data-ttu-id="c80b1-229">"without authentication"으로 표시된 코드 블록을 주석 처리하고 "with authentication"으로 표시된 코드 블록의 주석 처리를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-229">Comment out the block of code marked for "without authentication" and uncomment the block of code marked for "with authentication".</span></span>
   
    <span data-ttu-id="c80b1-230">이 변경에서는 ADAL JS 인증 공급자를 참조하며 해당 항목에 구성 값을 공급합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-230">This change references the ADAL JS authentication provider and provides configuration values to it.</span></span> <span data-ttu-id="c80b1-231">다음 단계에서는 API 앱 및 Azure AD 응용 프로그램에 대 한 구성 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-231">In the following steps you set the configuration values for your API app and Azure AD application.</span></span>
5. <span data-ttu-id="c80b1-232">`endpoints` 변수를 설정하는 코드에서 API URL을, ToDoListAPI에 대해 만든 API 앱의 URL로 변경하고 Azure AD 응용 프로그램 ID를 Azure 클래식 포털에서 복사한 클라이언트 ID로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-232">In the code that sets the `endpoints` variable, set the API URL to the URL of the API app that you created for the ToDoListAPI project, and set the Azure AD application ID to the client ID that you copied from the Azure classic portal.</span></span>
   
    <span data-ttu-id="c80b1-233">이제 코드는 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-233">The code is now similar to the following example.</span></span>
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. <span data-ttu-id="c80b1-234">`adalProvider.init` 호출에서 `tenant`를 해당 테넌트 이름으로 설정하고 `clientId`는 이전 단계에서 사용한 것과 같은 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-234">In the call to `adalProvider.init`, set `tenant` to your tenant name and `clientId` to same value you used in the previous step.</span></span>
   
    <span data-ttu-id="c80b1-235">이제 코드는 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-235">The code is now similar to the following example.</span></span>
   
        adalProvider.init(
            {
                instance: 'https://login.microsoftonline.com/', 
                tenant: 'contoso.onmicrosoft.com',
                clientId: '1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3',
                extraQueryParameter: 'nux=1',
                endpoints: endpoints
            },
            $httpProvider
            );
   
    <span data-ttu-id="c80b1-236">이러한 `app.js` 변경은 호출하는 코드와 호출되는 API가 동일한 Azure AD 응용 프로그램에 있도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-236">These changes to `app.js` specify that the calling code and the called API are in the same Azure AD application.</span></span>
7. <span data-ttu-id="c80b1-237">*app/scripts/homeCtrl.js* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-237">Open the *app/scripts/homeCtrl.js* file.</span></span>
8. <span data-ttu-id="c80b1-238">"without authentication"으로 표시된 코드 블록을 주석 처리하고 "with authentication"으로 표시된 코드 블록의 주석 처리를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-238">Comment out the block of code marked for "without authentication" and uncomment the block of code marked for "with authentication".</span></span>
9. <span data-ttu-id="c80b1-239">*app/scripts/indexCtrl.js* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-239">Open the *app/scripts/indexCtrl.js* file.</span></span>
10. <span data-ttu-id="c80b1-240">"without authentication"으로 표시된 코드 블록을 주석 처리하고 "with authentication"으로 표시된 코드 블록의 주석 처리를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-240">Comment out the block of code marked for "without authentication" and uncomment the block of code marked for "with authentication".</span></span>

### <a name="deploy-the-todolistangular-project-to-azure"></a><span data-ttu-id="c80b1-241">Azure에 ToDoListAngular 프로젝트 배포</span><span class="sxs-lookup"><span data-stu-id="c80b1-241">Deploy the ToDoListAngular project to Azure</span></span>
1. <span data-ttu-id="c80b1-242">**솔루션 탐색기**에서 ToDoListAngular 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-242">In **Solution Explorer**, right-click the ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="c80b1-243">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-243">Click **Publish**.</span></span>
   
    <span data-ttu-id="c80b1-244">Visual Studio가 프로젝트를 배포하고 웹앱의 기본 URL로 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-244">Visual Studio deploys the project and opens a browser to the web app's base URL.</span></span> <span data-ttu-id="c80b1-245">일반적으로 브라우저에서 Web API 기본 URL로 이동하려고 하는 403 오류 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-245">This will show a 403 error page, which is normal for an attempt to go to a Web API base URL from a browser.</span></span>
   
    <span data-ttu-id="c80b1-246">응용 프로그램을 테스트하려면 여전히 중간 계층 API 앱을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-246">You still have to make a change to the middle tier API app before you can test the application.</span></span>
3. <span data-ttu-id="c80b1-247">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-247">Close the browser.</span></span>

## <a name="configure-the-todolistapi-project-to-use-authentication"></a><span data-ttu-id="c80b1-248">인증을 사용하도록 ToDoListAPI프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="c80b1-248">Configure the ToDoListAPI project to use authentication</span></span>
<span data-ttu-id="c80b1-249">현재 ToDoListAPI 프로젝트는 "*"를 `owner` 값으로 ToDoListDataAPI에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-249">Currently the ToDoListAPI project sends "*" as the `owner` value to ToDoListDataAPI.</span></span> <span data-ttu-id="c80b1-250">이 섹션에서는 로그온한 사용자의 ID를 보내도록 코드를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-250">In this section you change the code to send the ID of the logged-on user.</span></span>

<span data-ttu-id="c80b1-251">ToDoListAPI 프로젝트를 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-251">Make the following changes in the ToDoListAPI project.</span></span>

1. <span data-ttu-id="c80b1-252">*Controllers/ToDoListController.cs* 파일을 열고 `owner`를 Azure AD `NameIdentifier` 클레임 값으로 설정하는 각 작업 메서드의 줄에 대한 주석 처리를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-252">Open the *Controllers/ToDoListController.cs* file, and uncomment the line in each action method that sets `owner` to the Azure AD `NameIdentifier` claim value.</span></span> <span data-ttu-id="c80b1-253">예:</span><span class="sxs-lookup"><span data-stu-id="c80b1-253">For example:</span></span>
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    <span data-ttu-id="c80b1-254">**중요**: `ToDoListDataAPI` 메서드에서 코드의 주석을 제거하지 마세요. 나중에 서비스 주체 인증 자습서에서 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-254">**Important**: Don't uncomment code in the `ToDoListDataAPI` method; you'll do that later for the service principal authentication tutorial.</span></span>

### <a name="deploy-the-todolistapi-project-to-azure"></a><span data-ttu-id="c80b1-255">Azure에 ToDoListAPI 프로젝트배포 </span><span class="sxs-lookup"><span data-stu-id="c80b1-255">Deploy the ToDoListAPI project to Azure</span></span>
1. <span data-ttu-id="c80b1-256">**솔루션 탐색기**에서 ToDoListAPI 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-256">In **Solution Explorer**, right-click the ToDoListAPI project, and then click **Publish**.</span></span>
2. <span data-ttu-id="c80b1-257">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-257">Click **Publish**.</span></span>
   
    <span data-ttu-id="c80b1-258">Visual Studio가 프로젝트를 배포하고 API 앱의 기본 URL로 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-258">Visual Studio deploys the project and opens a browser to the API app's base URL.</span></span>
3. <span data-ttu-id="c80b1-259">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-259">Close the browser.</span></span>

### <a name="test-the-application"></a><span data-ttu-id="c80b1-260">응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="c80b1-260">Test the application</span></span>
1. <span data-ttu-id="c80b1-261">**HTTP가 아닌 HTTPS를 사용 하여**웹앱의 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-261">Go to the URL of the web app, **using HTTPS, not HTTP**.</span></span>
2. <span data-ttu-id="c80b1-262">**할 일 목록** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-262">Click the **To Do List** tab.</span></span>
   
    <span data-ttu-id="c80b1-263">로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-263">You are prompted to log in.</span></span>
3. <span data-ttu-id="c80b1-264">AAD 테넌트의 사용자 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-264">Log in with the credentials of a user in your AAD tenant.</span></span>
4. <span data-ttu-id="c80b1-265">**할 일 목록** 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-265">The **To Do List** page appears.</span></span>
   
   ![할 일 목록 페이지](./media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   <span data-ttu-id="c80b1-267">지금까지는 모두 소유자 "*"에 대한 것이기 때문에 할 일 항목이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-267">No to-do items are displayed because until now they have all been for owner "*".</span></span> <span data-ttu-id="c80b1-268">이제 중간 계층에서 로그온한 사용자에 대한 항목을 요청하고, 아직은 아무 것도 만들지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-268">Now the middle tier is requesting items for the logged-on user, and none have been created yet.</span></span>
5. <span data-ttu-id="c80b1-269">응용 프로그램이 작동하고 있는지 확인하려면 새 할 일 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-269">Add new to-do items to verify that the application is working.</span></span>
6. <span data-ttu-id="c80b1-270">다른 브라우저 창에서 ToDoListDataAPI API 앱에 대한 Swagger UI URL로 이동하고 **ToDoList > 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-270">In another browser window, go to the Swagger UI URL for the ToDoListDataAPI API app and click **ToDoList > Get**.</span></span> <span data-ttu-id="c80b1-271">`owner` 매개 변수에 별표를 입력하고 **사용해 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-271">Enter an asterisk for the `owner` parameter, and then click **Try it out**.</span></span>
   
   <span data-ttu-id="c80b1-272">응답에 보면 새 할 일 항목의 소Owner 속성에 실제 Azure AD 사용자 ID가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-272">The response shows that the new to-do items have the actual Azure AD user ID in the Owner property.</span></span>
   
   ![JSON 응답에서 소유자 ID](./media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-the-projects-from-scratch"></a><span data-ttu-id="c80b1-274">처음부터 프로젝트 빌드</span><span class="sxs-lookup"><span data-stu-id="c80b1-274">Building the projects from scratch</span></span>
<span data-ttu-id="c80b1-275">**Azure API 앱** 프로젝트 템플릿을 사용하고 기본 Values 컨트롤러를 ToDoList 컨트롤러로 대체하여 두 개의 웹 API 프로젝트가 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-275">The two Web API projects were created by using the **Azure API App** project template and replacing the default Values controller with a ToDoList controller.</span></span> 

<span data-ttu-id="c80b1-276">웹 API 2 백 엔드를 통한 AngularJS 단일 페이지 응용 프로그램을 만드는 방법에 대한 내용은 [Hands On Lab: ASP.NET Web API 및 Angular.js를 통해 SPA(단일 페이지 응용 프로그램) 빌드](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c80b1-276">For information about how to  create an AngularJS single-page application with a Web API 2 back end, see  [Hands On Lab: Build a Single Page Application (SPA) with ASP.NET Web API and Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs).</span></span> <span data-ttu-id="c80b1-277">Azure AD 인증 코드를 추가하는 방법에 대한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c80b1-277">For information about how to add Azure AD authentication code, see the following resources:</span></span>

* <span data-ttu-id="c80b1-278">[Azure AD를 사용하여 AngularJS 단일 페이지 앱 보안 유지](../active-directory/active-directory-devquickstarts-angular.md)</span><span class="sxs-lookup"><span data-stu-id="c80b1-278">[Securing AngularJS Single Page Apps with Azure AD](../active-directory/active-directory-devquickstarts-angular.md).</span></span>
* [<span data-ttu-id="c80b1-279">ADAL JS v1 소개</span><span class="sxs-lookup"><span data-stu-id="c80b1-279">Introducing ADAL JS v1</span></span>](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a><span data-ttu-id="c80b1-280">문제 해결</span><span class="sxs-lookup"><span data-stu-id="c80b1-280">Troubleshooting</span></span>
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* <span data-ttu-id="c80b1-281">ToDoListAPI(중간 계층) 및 ToDoListDataAPI(데이터 계층)를 혼동하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-281">Make sure that you don't confuse ToDoListAPI (middle tier) and ToDoListDataAPI (data tier).</span></span> <span data-ttu-id="c80b1-282">예를 들어 데이터 계층이 아닌 중간 계층 API 앱에 인증을 추가했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-282">For example, verify that you added authentication to the middle tier API app, not the data tier.</span></span> 
* <span data-ttu-id="c80b1-283">AngularJS 소스 코드가 중간 계층 API 앱 URL(ToDoListDataAPI가 아닌 ToDoListAPI) 및 올바른 Azure AD 클라이언트 ID를 참조하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-283">Make sure that the AngularJS source code references the middle tier API app URL (ToDoListAPI, not ToDoListDataAPI)and the correct Azure AD client ID.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c80b1-284">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c80b1-284">Next steps</span></span>
<span data-ttu-id="c80b1-285">이 자습서에서는 API 앱에 앱 서비스 인증을 사용하는 방법과, ADAL JS 라이브러리를 사용하여 API 앱을 호출하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-285">In this tutorial you learned how to use App Service authentication for an API app and how to call the API app by using the ADAL JS library.</span></span> <span data-ttu-id="c80b1-286">다음 자습서에서는 [서비스 간 시나리오에 대해 API 앱에 대한 액세스를 보호](app-service-api-dotnet-service-principal-auth.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c80b1-286">In the next tutorial you'll learn how to [secure access to your API app for service-to-service scenarios](app-service-api-dotnet-service-principal-auth.md).</span></span>

