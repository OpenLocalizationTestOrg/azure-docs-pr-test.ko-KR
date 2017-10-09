---
title: "Azure Active Directory tooauthenticate 일괄 처리 관리 솔루션 aaaUse | Microsoft Docs"
description: "Azure 리소스 관리자를 사용 하 여 빌드한 응용 프로그램 및 hello 일괄 처리 리소스 공급자는 Azure AD로 인증 합니다."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/27/2017
ms.author: tamram
ms.openlocfilehash: 192aa9f8d7cbfc0282a4a0c33ab1659f1f351525
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="b6fb6-103">Active Directory를 사용하여 Batch Management 솔루션 인증</span><span class="sxs-lookup"><span data-stu-id="b6fb6-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="b6fb6-104">Hello Azure 일괄 처리 관리 서비스를 호출 하는 응용 프로그램으로 인증 [Azure Active Directory] [ aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b6fb6-104">Applications that call hello Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="b6fb6-105">Azure AD는 Microsoft의 다중 테넌트 클라우드 기반 디렉터리 및 ID 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="b6fb6-106">Azure 자체가 hello 고객, 서비스 관리자 및 조직 사용자를 인증 하기 위해 Azure AD를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-106">Azure itself uses Azure AD for hello authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="b6fb6-107">hello Batch Management.NET 라이브러리는 일괄 처리 계정, 계정 키, 응용 프로그램 및 응용 프로그램 패키지를 사용 하기 위한 형식을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-107">hello Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="b6fb6-108">hello Batch Management.NET 라이브러리는 Azure 리소스 공급자 클라이언트 이며와 함께 사용 [Azure 리소스 관리자] [ resman_overview] toomanage 이러한 리소스 프로그래밍 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-108">hello Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] toomanage these resources programmatically.</span></span> <span data-ttu-id="b6fb6-109">Azure AD는 필요한 tooauthenticate 요청 및 모든 Azure 리소스 공급자를 포함 한 클라이언트 hello Batch Management.NET 라이브러리를 통해 [Azure 리소스 관리자][resman_overview]합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-109">Azure AD is required tooauthenticate requests made through any Azure resource provider client, including hello Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="b6fb6-110">이 문서에서는 Azure AD tooauthenticate hello Batch Management.NET 라이브러리를 사용 하는 응용 프로그램에서 사용 하 여 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-110">In this article, we explore using Azure AD tooauthenticate from applications that use hello Batch Management .NET library.</span></span> <span data-ttu-id="b6fb6-111">Azure AD toouse tooauthenticate 구독 관리자 또는 공동 관리자를 사용 하 여 통합 인증 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-111">We show how toouse Azure AD tooauthenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="b6fb6-112">사용 하 여 hello [AccountManagment] [ acct_mgmt_sample] 샘플 프로젝트를 Azure AD를 사용 하 여 hello Batch Management.NET 라이브러리를 통해 toowalk GitHub에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-112">We use hello [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, toowalk through using Azure AD with hello Batch Management .NET library.</span></span>

<span data-ttu-id="b6fb6-113">hello Batch Management.NET 라이브러리 및 hello AccountManagement 샘플 사용에 대 한 더 toolearn 참조 [일괄 처리 관리 계정 및 할당량.NET 용 hello 일괄 처리 관리 클라이언트 라이브러리와](batch-management-dotnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-113">toolearn more about using hello Batch Management .NET library and hello AccountManagement sample, see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="b6fb6-114">Azure AD에 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="b6fb6-114">Register your application with Azure AD</span></span>

<span data-ttu-id="b6fb6-115">Azure hello [Active Directory 인증 라이브러리] [ aad_adal] (ADAL)에 응용 프로그램 프로그래밍 인터페이스 tooAzure 사용 하기 위해 AD를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-115">hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface tooAzure AD for use within your applications.</span></span> <span data-ttu-id="b6fb6-116">응용 프로그램에서 ADAL을 toocall, Azure AD 테 넌 트에 응용 프로그램을 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-116">toocall ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="b6fb6-117">응용 프로그램을 등록 하는 경우에 hello Azure AD 테 넌 트 내에 대 한 이름을 포함 하 여 응용 프로그램에 대 한 정보로 Azure AD를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-117">When you register your application, you supply Azure AD with information about your application, including a name for it within hello Azure AD tenant.</span></span> <span data-ttu-id="b6fb6-118">그런 다음 azure AD는 응용 프로그램 ID를 제공 합니다. 사용 하는 tooassociate 응용 프로그램 런타임 시 Azure AD와 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-118">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="b6fb6-119">hello 응용 프로그램 ID에 대해 자세히 toolearn 참조 [응용 프로그램 및 Azure Active Directory에서 서비스 보안 주체 개체](../active-directory/develop/active-directory-application-objects.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-119">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="b6fb6-120">tooregister hello AccountManagement 샘플 응용 프로그램에서에서 다음과 같이 hello hello [응용 프로그램 추가](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) 섹션 [Azure Active Directory와 응용 프로그램 통합] [ aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="b6fb6-120">tooregister hello AccountManagement sample application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="b6fb6-121">지정 **네이티브 클라이언트 응용 프로그램** hello 유형의 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-121">Specify **Native Client Application** for hello type of application.</span></span> <span data-ttu-id="b6fb6-122">업계 hello hello에 대 한 표준 OAuth 2.0 URI **리디렉션 URI** 은 `urn:ietf:wg:oauth:2.0:oob`합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-122">hello industry standard OAuth 2.0 URI for hello **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="b6fb6-123">그러나 모든 유효한 URI를 지정할 수 있습니다 (같은 `http://myaccountmanagementsample`) hello에 대 한 **리디렉션 URI**마찬가지로 toobe 실제 끝점이 필요 하지 않습니다:</span><span class="sxs-lookup"><span data-stu-id="b6fb6-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for hello **Redirect URI**, as it does not need toobe a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="b6fb6-124">Hello 등록 과정을 완료 되 면 hello 응용 프로그램 ID를 참조 하 고 응용 프로그램에 대해 나열 된 개체 (서비스 주체) ID hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-124">Once you complete hello registration process, you'll see hello application ID and hello object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a><span data-ttu-id="b6fb6-125">Hello Azure 리소스 관리자 API 액세스 tooyour 응용 프로그램에 부여</span><span class="sxs-lookup"><span data-stu-id="b6fb6-125">Grant hello Azure Resource Manager API access tooyour application</span></span>

<span data-ttu-id="b6fb6-126">다음으로 toodelegate 액세스 tooyour 응용 프로그램 toohello Azure 리소스 관리자 API 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-126">Next, you'll need toodelegate access tooyour application toohello Azure Resource Manager API.</span></span> <span data-ttu-id="b6fb6-127">리소스 관리자 API hello에 대 한 Azure AD hello 식별자가 **Windows Azure 서비스 관리 API**합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-127">hello Azure AD identifier for hello Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="b6fb6-128">Hello Azure 포털에서에서 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-128">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="b6fb6-129">Hello hello Azure 포털의 왼쪽 탐색 창에서 선택 **더 서비스**, 클릭 **앱 등록**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-129">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="b6fb6-130">응용 프로그램 등록의 hello 목록에서 응용 프로그램의 hello 이름 검색:</span><span class="sxs-lookup"><span data-stu-id="b6fb6-130">Search for hello name of your application in hello list of app registrations:</span></span>

    ![응용 프로그램 이름 검색](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="b6fb6-132">디스플레이 hello **설정을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-132">Display hello **Settings** blade.</span></span> <span data-ttu-id="b6fb6-133">Hello에 **API 액세스** 섹션에서 **필요한 권한**합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-133">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="b6fb6-134">클릭 **추가** tooadd 새 필수 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-134">Click **Add** tooadd a new required permission.</span></span> 
5. <span data-ttu-id="b6fb6-135">1 단계에서 입력 **Windows Azure 서비스 관리 API**hello 결과 목록에서 해당 API를 선택 하 고 hello 클릭 **선택** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-135">In step 1, enter **Windows Azure Service Management API**, select that API from hello list of results, and click hello **Select** button.</span></span>
6. <span data-ttu-id="b6fb6-136">2 단계에서 선택 hello 확인란 옆 너무**조직 사용자로 Azure 액세스 클래식 배포 모델**, hello를 클릭 하 고 **선택** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-136">In step 2, select hello check box next too**Access Azure classic deployment model as organization users**, and click hello **Select** button.</span></span>
7. <span data-ttu-id="b6fb6-137">Hello 클릭 **수행** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-137">Click hello **Done** button.</span></span>

<span data-ttu-id="b6fb6-138">hello **필요한 권한** 블레이드 tooboth tooyour 응용 프로그램 사용 권한 부여 되었는지를 보여 줍니다. hello ADAL 및 리소스 관리자 Api는 이제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-138">hello **Required Permissions** blade now shows that permissions tooyour application are granted tooboth hello ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="b6fb6-139">먼저 Azure AD에 앱을 등록 하는 경우 권한은 기본적으로 tooADAL 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-139">Permissions are granted tooADAL by default when you first register your app with Azure AD.</span></span>

![대리자 사용 권한 toohello Azure 리소스 관리자 API](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="b6fb6-141">Azure AD 끝점</span><span class="sxs-lookup"><span data-stu-id="b6fb6-141">Azure AD endpoints</span></span>

<span data-ttu-id="b6fb6-142">tooauthenticate 일괄 처리 관리 솔루션을 Azure AD와 두 개의 잘 알려진 끝점이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-142">tooauthenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="b6fb6-143">hello **Azure AD의 공통 끝점** 통합된 인증의 hello 경우 처럼 특정 테 넌 트가 제공 되지 않으면 인터페이스 수집 일반 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-143">hello **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in hello case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="b6fb6-144">hello **Azure 리소스 관리자 끝점** 사용 되는 tooacquire 요청 toohello 일괄 처리 관리 서비스를 인증 하기 위한 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-144">hello **Azure Resource Manager endpoint** is used tooacquire a token for authenticating requests toohello Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="b6fb6-145">hello AccountManagement 샘플 응용 프로그램은 이러한 끝점에 대 한 상수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-145">hello AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="b6fb6-146">해당 상수를 변경하지 않고 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="b6fb6-147">응용 프로그램 ID 참조</span><span class="sxs-lookup"><span data-stu-id="b6fb6-147">Reference your application ID</span></span> 

<span data-ttu-id="b6fb6-148">클라이언트 응용 프로그램 런타임 시 hello 응용 프로그램 ID (또한 참조 tooas hello 클라이언트 ID) tooaccess Azure AD를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-148">Your client application uses hello application ID (also referred tooas hello client ID) tooaccess Azure AD at runtime.</span></span> <span data-ttu-id="b6fb6-149">Hello Azure 포털에서에서 응용 프로그램을 등록 한 후 등록 된 응용 프로그램에 대 한 Azure AD에서 제공 된 사용자 코드 toouse hello 응용 프로그램 ID를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-149">Once you've registered your application in hello Azure portal, update your code toouse hello application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="b6fb6-150">Hello AccountManagement 샘플 응용 프로그램에서는 hello Azure 포털 toohello 적절 한 상수에서 응용 프로그램 ID를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-150">In hello AccountManagement sample application, copy your application ID from hello Azure portal toohello appropriate constant:</span></span>

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="b6fb6-151">또한 hello 리디렉션 hello 등록 프로세스 중에 지정 된 URI를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-151">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="b6fb6-152">코드에서 지정 된 URI는 hello 리디렉션 hello 리디렉션 URI hello 응용 프로그램 등록 시 입력 한 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-152">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application.</span></span>

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="b6fb6-153">Azure AD 인증 토큰 획득</span><span class="sxs-lookup"><span data-stu-id="b6fb6-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="b6fb6-154">Hello AccountManagement 샘플 hello Azure AD 테 넌 트에 등록 하 고 원하는 값으로 hello 샘플 소스 코드를 업데이트 후 hello 샘플은 Azure AD를 사용 하 여 준비 tooauthenticate입니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-154">After you register hello AccountManagement sample in hello Azure AD tenant and update hello sample source code with your values, hello sample is ready tooauthenticate using Azure AD.</span></span> <span data-ttu-id="b6fb6-155">Hello 샘플을 실행 하면 hello ADAL tooacquire 인증 토큰을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-155">When you run hello sample, hello ADAL attempts tooacquire an authentication token.</span></span> <span data-ttu-id="b6fb6-156">이 단계에서 Microsoft 자격 증명을 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

```csharp
// Obtain an access token using hello "common" AAD resource. This allows hello application
// tooquery AAD for information that lies outside hello application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

<span data-ttu-id="b6fb6-157">자격 증명을 제공 hello 샘플 응용 프로그램 인증 tooissue 요청 toohello 일괄 처리 관리 서비스 계속 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-157">After you provide your credentials, hello sample application can proceed tooissue authenticated requests toohello Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b6fb6-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b6fb6-158">Next steps</span></span>

<span data-ttu-id="b6fb6-159">Hello 실행에 대 한 자세한 내용은 [AccountManagement 샘플 응용 프로그램][acct_mgmt_sample], 참조 [일괄 처리 관리 계정 및 할당량for.nethello일괄처리관리클라이언트라이브러리와](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="b6fb6-159">For more information on running hello [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="b6fb6-160">Azure AD에 대해 자세히 toolearn 참조 hello [Azure Active Directory 설명서](https://docs.microsoft.com/azure/active-directory/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-160">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="b6fb6-161">ADAL toouse hello에서 사용할 수 있는 방법을 보여 주는 상세한 예제 [Azure 코드 예제](https://azure.microsoft.com/resources/samples/?service=active-directory) 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-161">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="b6fb6-162">Azure AD를 사용 하 여 tooauthenticate 일괄 처리 서비스 응용 프로그램 참조 [Active Directory를 사용 하 여 인증 하는 일괄 처리 서비스 솔루션](batch-aad-auth.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b6fb6-162">tooauthenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


[aad_about]: ../active-directory/active-directory-whatis.md "Azure Active Directory란?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD의 인증 시나리오"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Azure Active Directory와 응용 프로그램 통합"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
