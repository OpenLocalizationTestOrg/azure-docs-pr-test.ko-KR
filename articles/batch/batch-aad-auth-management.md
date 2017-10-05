---
title: "Azure Active Directory를 사용하여 Batch Management 솔루션 인증 | Microsoft Docs"
description: "Azure Resource Manager로 구축된 응용 프로그램과 Batch 리소스 공급자는 Azure AD로 인증합니다."
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
ms.openlocfilehash: 26d4adf4f74f9aacc4cf8cf24be293ebdb4d63c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="40ef1-103">Active Directory를 사용하여 Batch Management 솔루션 인증</span><span class="sxs-lookup"><span data-stu-id="40ef1-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="40ef1-104">Azure Batch Management 서비스를 호출하는 응용 프로그램은 [Azure Active Directory][aad_about](Azure AD)로 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-104">Applications that call the Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="40ef1-105">Azure AD는 Microsoft의 다중 테넌트 클라우드 기반 디렉터리 및 ID 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="40ef1-106">Azure에서는 해당 고객, 서비스 관리자 및 조직 사용자의 인증을 위해 Azure AD를 자체적으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-106">Azure itself uses Azure AD for the authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="40ef1-107">Batch 관리 .NET 라이브러리는 배치 계정, 계정 키, 응용 프로그램 및 응용 프로그램 패키지를 사용하기 위한 종류를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-107">The Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="40ef1-108">Batch 관리 .NET 라이브러리는 Azure 리소스 공급자 클라이언트이며 [Azure Resource Manager][resman_overview]와 함께 프로그래밍 방식으로 해당 리소스를 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-108">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage these resources programmatically.</span></span> <span data-ttu-id="40ef1-109">Azure AD는 Batch 관리 .NET 라이브러리를 비롯한 Azure 리소스 공급자 클라이언트 및 [Azure Resource Manager][resman_overview]를 통해 만들어지는 요청을 인증하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-109">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="40ef1-110">이 문서에서는 Batch Management .NET 라이브러리를 사용하는 응용 프로그램에서 Azure AD를 사용하여 인증하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-110">In this article, we explore using Azure AD to authenticate from applications that use the Batch Management .NET library.</span></span> <span data-ttu-id="40ef1-111">Azure AD를 사용하여 통합 인증을 통해 구독 관리자 또는 공동 관리자를 인증하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-111">We show how to use Azure AD to authenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="40ef1-112">GitHub에서 사용할 수 있는 [AccountManagment][acct_mgmt_sample] 샘플 프로젝트에서 Batch Management .NET 라이브러리와 함께 Azure AD를 사용하도록 단계별로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-112">We use the [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, to walk through using Azure AD with the Batch Management .NET library.</span></span>

<span data-ttu-id="40ef1-113">Batch 관리 .NET 라이브러리 및 AccountManagement 샘플을 사용하는 방법에 대한 자세한 내용은 [.NET용 Batch 관리 클라이언트 라이브러리를 사용하여 배치 계정 및 할당량 관리](batch-management-dotnet.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40ef1-113">To learn more about using the Batch Management .NET library and the AccountManagement sample, see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="40ef1-114">Azure AD에 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="40ef1-114">Register your application with Azure AD</span></span>

<span data-ttu-id="40ef1-115">Azure [Active Directory 인증 라이브러리][aad_adal](ADAL)는 응용 프로그램 내에서 사용하기 위해 Azure AD에 프로그래밍 방식 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-115">The Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface to Azure AD for use within your applications.</span></span> <span data-ttu-id="40ef1-116">응용 프로그램에서 ADAL을 호출하려면 Azure AD 테넌트에 응용 프로그램을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-116">To call ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="40ef1-117">응용 프로그램을 등록할 때 Azure AD 테넌트 내에서 이름을 포함하여 응용 프로그램에 대한 Azure AD 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-117">When you register your application, you supply Azure AD with information about your application, including a name for it within the Azure AD tenant.</span></span> <span data-ttu-id="40ef1-118">그런 다음 Azure AD는 런타임 시 응용 프로그램을 Azure AD와 연결하는 데 사용하는 응용 프로그램 ID를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-118">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="40ef1-119">응용 프로그램 ID에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 및 서비스 주체 개체](../active-directory/develop/active-directory-application-objects.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40ef1-119">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="40ef1-120">AccountManagement 샘플 응용 프로그램을 등록하려면 [Azure Active Directory와 응용 프로그램 통합][aad_integrate]에서 [응용 프로그램 추가](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) 섹션의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-120">To register the AccountManagement sample application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="40ef1-121">응용 프로그램 유형으로 **네이티브 클라이언트 응용 프로그램**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-121">Specify **Native Client Application** for the type of application.</span></span> <span data-ttu-id="40ef1-122">**리디렉션 URI**의 업계 표준 OAuth 2.0 URI는 `urn:ietf:wg:oauth:2.0:oob`입니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-122">The industry standard OAuth 2.0 URI for the **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="40ef1-123">그러나 실제 끝점일 필요가 없으므로 `http://myaccountmanagementsample`리디렉션 URI**에 대한 유효한 URI(예:** )를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for the **Redirect URI**, as it does not need to be a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="40ef1-124">등록 프로세스를 완료한 후 응용 프로그램에 대해 나열된 응용 프로그램 ID 및 개체(서비스 주체) ID가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-124">Once you complete the registration process, you'll see the application ID and the object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-the-azure-resource-manager-api-access-to-your-application"></a><span data-ttu-id="40ef1-125">응용 프로그램에 대한 Azure Resource Manager API 액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="40ef1-125">Grant the Azure Resource Manager API access to your application</span></span>

<span data-ttu-id="40ef1-126">다음으로, Azure Resource Manager API에 응용 프로그램에 대한 액세스 권한을 위임해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-126">Next, you'll need to delegate access to your application to the Azure Resource Manager API.</span></span> <span data-ttu-id="40ef1-127">리소스 관리자 API에 대한 Azure AD 식별자는 **Windows Azure Service Management API**입니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-127">The Azure AD identifier for the Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="40ef1-128">Azure Portal에서 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-128">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="40ef1-129">Azure Portal의 왼쪽 탐색 창에서 **추가 서비스**를 선택하고 **앱 등록**을 클릭한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-129">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="40ef1-130">앱 등록의 목록에서 응용 프로그램의 이름을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-130">Search for the name of your application in the list of app registrations:</span></span>

    ![응용 프로그램 이름 검색](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="40ef1-132">**설정** 블레이드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-132">Display the **Settings** blade.</span></span> <span data-ttu-id="40ef1-133">**API 액세스** 섹션에서 **필요한 사용 권한**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-133">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="40ef1-134">**추가**를 클릭하여 새로운 필요한 사용 권한을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-134">Click **Add** to add a new required permission.</span></span> 
5. <span data-ttu-id="40ef1-135">1단계에서 **Windows Azure Service Management API**를 입력하고 결과 목록에서 해당 API를 선택하고 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-135">In step 1, enter **Windows Azure Service Management API**, select that API from the list of results, and click the **Select** button.</span></span>
6. <span data-ttu-id="40ef1-136">2단계에서 **조직 사용자로 Azure 클래식 배포 모델에 액세스** 옆의 확인란을 선택하고 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-136">In step 2, select the check box next to **Access Azure classic deployment model as organization users**, and click the **Select** button.</span></span>
7. <span data-ttu-id="40ef1-137">**완료** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-137">Click the **Done** button.</span></span>

<span data-ttu-id="40ef1-138">**필요한 사용 권한** 블레이드는 이제 응용 프로그램에 대한 권한이 ADAL과 리소스 관리자 API에 부여되었음을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-138">The **Required Permissions** blade now shows that permissions to your application are granted to both the ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="40ef1-139">Azure AD에 앱을 처음 등록할 때 사용 권한은 기본적으로 ADAL에 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-139">Permissions are granted to ADAL by default when you first register your app with Azure AD.</span></span>

![Azure Resource Manager API에 대한 권한 위임](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="40ef1-141">Azure AD 끝점</span><span class="sxs-lookup"><span data-stu-id="40ef1-141">Azure AD endpoints</span></span>

<span data-ttu-id="40ef1-142">Azure AD를 사용하여 Batch Management 솔루션을 인증하려면 잘 알려진 다음 두 개의 끝점이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-142">To authenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="40ef1-143">**Azure AD 공통 끝점**은 통합 인증의 경우와 같이 특정 테넌트를 제공하지 않을 때 일반 자격 증명 수집 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-143">The **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in the case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="40ef1-144">**Azure Resource Manager 끝점**은 Batch Management 서비스에 대한 요청을 인증하기 위한 토큰을 얻는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-144">The **Azure Resource Manager endpoint** is used to acquire a token for authenticating requests to the Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="40ef1-145">AccountManagement 샘플 응용 프로그램은 이러한 끝점에 대한 상수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-145">The AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="40ef1-146">해당 상수를 변경하지 않고 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="40ef1-147">응용 프로그램 ID 참조</span><span class="sxs-lookup"><span data-stu-id="40ef1-147">Reference your application ID</span></span> 

<span data-ttu-id="40ef1-148">클라이언트 응용 프로그램은 런타임 시 Azure AD에 액세스하기 위해 응용 프로그램 ID(클라이언트 ID라고도 함)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-148">Your client application uses the application ID (also referred to as the client ID) to access Azure AD at runtime.</span></span> <span data-ttu-id="40ef1-149">Azure Portal에서 응용 프로그램을 등록한 후 등록된 응용 프로그램에 대해 Azure AD에서 제공하는 응용 프로그램 ID를 사용하도록 코드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-149">Once you've registered your application in the Azure portal, update your code to use the application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="40ef1-150">AccountManagement 샘플 응용 프로그램에서 Azure Portal의 응용 프로그램 ID를 적절한 상수에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-150">In the AccountManagement sample application, copy your application ID from the Azure portal to the appropriate constant:</span></span>

```csharp
// Specify the unique identifier (the "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access the Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="40ef1-151">또한 등록 프로세스 중 지정한 리디렉션 URI를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-151">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="40ef1-152">코드에 지정된 리디렉션 URI는 응용 프로그램을 등록할 때 제공한 리디렉션 URI와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-152">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application.</span></span>

```csharp
// The URI to which Azure AD will redirect in response to an OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need to be a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="40ef1-153">Azure AD 인증 토큰 획득</span><span class="sxs-lookup"><span data-stu-id="40ef1-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="40ef1-154">Azure AD 테넌트에 AccountManagement 샘플을 등록하고 샘플 원본 코드를 값으로 업데이트하면 Azure AD를 사용하여 샘플을 인증할 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-154">After you register the AccountManagement sample in the Azure AD tenant and update the sample source code with your values, the sample is ready to authenticate using Azure AD.</span></span> <span data-ttu-id="40ef1-155">샘플을 실행할 때 ADAL은 인증 토큰을 획득하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-155">When you run the sample, the ADAL attempts to acquire an authentication token.</span></span> <span data-ttu-id="40ef1-156">이 단계에서 Microsoft 자격 증명을 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

```csharp
// Obtain an access token using the "common" AAD resource. This allows the application
// to query AAD for information that lies outside the application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

<span data-ttu-id="40ef1-157">자격 증명을 제공한 후 샘플 응용 프로그램은 Batch 관리 서비스에 인증된 요청을 발급하도록 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-157">After you provide your credentials, the sample application can proceed to issue authenticated requests to the Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="40ef1-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="40ef1-158">Next steps</span></span>

<span data-ttu-id="40ef1-159">[AccountManagement 샘플 응용 프로그램][acct_mgmt_sample] 실행에 대한 자세한 내용은 [.NET용 Batch 관리 클라이언트 라이브러리를 사용하여 배치 계정 및 할당량 관리](batch-management-dotnet.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40ef1-159">For more information on running the [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="40ef1-160">Azure AD에 대한 자세한 내용은 [Azure Active Directory 설명서](https://docs.microsoft.com/azure/active-directory/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40ef1-160">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="40ef1-161">ADAL을 사용하는 방법을 보여 주는 자세한 예제는 [Azure 코드 샘플](https://azure.microsoft.com/resources/samples/?service=active-directory) 라이브러리에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40ef1-161">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="40ef1-162">Azure AD를 사용하여 Batch 서비스 응용 프로그램을 인증하려면 [Active Directory를 사용하여 Batch 서비스 솔루션 인증](batch-aad-auth.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40ef1-162">To authenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


<span data-ttu-id="40ef1-163">[aad_about]: ../active-directory/active-directory-whatis.md "Azure Active Directory란?"</span><span class="sxs-lookup"><span data-stu-id="40ef1-163">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="40ef1-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD의 인증 시나리오"</span><span class="sxs-lookup"><span data-stu-id="40ef1-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="40ef1-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Azure Active Directory와 응용 프로그램 통합"</span><span class="sxs-lookup"><span data-stu-id="40ef1-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
