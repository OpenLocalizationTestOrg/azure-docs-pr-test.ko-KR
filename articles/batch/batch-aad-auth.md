---
title: "Azure Active Directory를 사용하여 Azure Batch 서비스 솔루션 인증 | Microsoft Docs"
description: "Batch는 Batch 서비스의 인증을 위해 Azure AD를 지원합니다."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/20/2017
ms.author: tamram
ms.openlocfilehash: 9c03bde919c46cd301229255c0b12ee69dda6f78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a><span data-ttu-id="2d358-103">Active Directory를 사용하여 Batch 서비스 솔루션 인증</span><span class="sxs-lookup"><span data-stu-id="2d358-103">Authenticate Batch service solutions with Active Directory</span></span>

<span data-ttu-id="2d358-104">Azure Batch는 [Azure Active Directory][aad_about](Azure AD) 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="2d358-105">Azure AD는 Microsoft의 다중 테넌트 클라우드 기반 디렉터리 및 ID 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="2d358-106">Azure에서는 Azure AD를 자체적으로 사용하여 고객, 서비스 관리자 및 조직 사용자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-106">Azure itself uses Azure AD to authenticate its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="2d358-107">Azure Batch와 함께 Azure AD 인증을 사용할 때 다음 두 가지 방법 중 하나로 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-107">When using Azure AD authentication with Azure Batch, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="2d358-108">**통합 인증**을 사용하여 응용 프로그램과 상호 작용하는 사용자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-108">By using **integrated authentication** to authenticate a user that is interacting with the application.</span></span> <span data-ttu-id="2d358-109">통합 인증을 사용하는 응용 프로그램에서는 사용자의 자격 증명을 수집하고 해당 자격 증명을 사용하여 Batch 리소스에 대한 액세스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-109">An application using integrated authentication gathers a user's credentials and uses those credentials to authenticate access to Batch resources.</span></span>
- <span data-ttu-id="2d358-110">**서비스 주체**를 사용하여 무인으로 실행되는 응용 프로그램을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-110">By using a **service principal** to authenticate an unattended application.</span></span> <span data-ttu-id="2d358-111">서비스 주체는 런타임에 리소스에 액세스할 때 응용 프로그램을 나타내기 위해 응용 프로그램에 대한 정책과 권한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-111">A service principal defines the policy and permissions for an application in order to represent the application when accessing resources at runtime.</span></span>

<span data-ttu-id="2d358-112">Azure AD에 대한 자세한 내용은 [Azure Active Directory 설명서](https://docs.microsoft.com/azure/active-directory/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d358-112">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span>

## <a name="authentication-and-pool-allocation-mode"></a><span data-ttu-id="2d358-113">인증 및 풀 할당 모드</span><span class="sxs-lookup"><span data-stu-id="2d358-113">Authentication and pool allocation mode</span></span>

<span data-ttu-id="2d358-114">배치 계정을 만들 때 해당 계정에 대해 생성된 풀을 할당해야 하는 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-114">When you create a Batch account, you can specify where pools created for that account should be allocated.</span></span> <span data-ttu-id="2d358-115">기본 Batch 서비스 구독 또는 사용자 구독 중 하나에서 풀을 할당하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-115">You can choose to allocate pools either in the default Batch service subscription or in a user subscription.</span></span> <span data-ttu-id="2d358-116">사용자의 선택은 해당 계정의 리소스에 대한 액세스를 인증하는 방법에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-116">Your choice affects how you authenticate access to resources in that account.</span></span>

- <span data-ttu-id="2d358-117">**Batch 서비스 구독** -</span><span class="sxs-lookup"><span data-stu-id="2d358-117">**Batch service subscription**.</span></span> <span data-ttu-id="2d358-118">기본적으로 Batch 풀은 Batch 서비스 구독에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-118">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="2d358-119">이 옵션을 선택하면 [공유 키](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) 또는 Azure AD로 해당 계정의 리소스에 대한 액세스를 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-119">If you choose this option, you can authenticate access to resources in that account either with [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) or with Azure AD.</span></span>
- <span data-ttu-id="2d358-120">**사용자 구독** -</span><span class="sxs-lookup"><span data-stu-id="2d358-120">**User subscription.**</span></span> <span data-ttu-id="2d358-121">지정한 사용자 구독에 Batch 풀을 할당하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-121">You can choose to allocate Batch pools in a user subscription that you specify.</span></span> <span data-ttu-id="2d358-122">이 옵션을 선택하는 경우 Azure AD로 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-122">If you choose this option, you must authenticate with Azure AD.</span></span>

## <a name="endpoints-for-authentication"></a><span data-ttu-id="2d358-123">인증에 대한 끝점</span><span class="sxs-lookup"><span data-stu-id="2d358-123">Endpoints for authentication</span></span>

<span data-ttu-id="2d358-124">Azure AD로 Batch 응용 프로그램을 인증하려면 코드에서 잘 알려진 몇 가지 끝점을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-124">To authenticate Batch applications with Azure AD, you need to include some well-known endpoints in your code.</span></span>

### <a name="azure-ad-endpoint"></a><span data-ttu-id="2d358-125">Azure AD 끝점</span><span class="sxs-lookup"><span data-stu-id="2d358-125">Azure AD endpoint</span></span>

<span data-ttu-id="2d358-126">기본 Azure AD 인증 기관 끝점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-126">The base Azure AD authority endpoint is:</span></span>

`https://login.microsoftonline.com/`

<span data-ttu-id="2d358-127">Azure AD로 인증하려면 이 끝점을 테넌트 ID(디렉터리 ID)와 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-127">To authenticate with Azure AD, you use this endpoint together with the tenant ID (directory ID).</span></span> <span data-ttu-id="2d358-128">테넌트 ID는 인증에 사용할 Azure AD 테넌트를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-128">The tenant ID identifies the Azure AD tenant to use for authentication.</span></span> <span data-ttu-id="2d358-129">테넌트 ID를 검색하려면 [Azure Active Directory에 대한 테넌트 ID 가져오기](#get-the-tenant-id-for-your-active-directory)에서 설명하는 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-129">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> <span data-ttu-id="2d358-130">테넌트별 끝점은 서비스 주체를 사용하여 인증할 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-130">The tenant-specific endpoint is required when you authenticate using a service principal.</span></span> 
> 
> <span data-ttu-id="2d358-131">통합 인증을 사용하여 인증할 때 테넌트별 끝점은 선택 사항이지만 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-131">The tenant-specific endpoint is optional when you authenticate using integrated authentication, but recommended.</span></span> <span data-ttu-id="2d358-132">그러나 Azure AD 공통 끝점도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-132">However, you can also use the Azure AD common endpoint.</span></span> <span data-ttu-id="2d358-133">공통 끝점은 특정 테넌트를 제공하지 않을 때 일반 자격 증명 수집 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-133">The common endpoint provides a generic credential gathering interface when a specific tenant is not provided.</span></span> <span data-ttu-id="2d358-134">공통 끝점은 `https://login.microsoftonline.com/common`입니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-134">The common endpoint is `https://login.microsoftonline.com/common`.</span></span>
>
>

<span data-ttu-id="2d358-135">Azure AD 끝점에 대한 자세한 내용은 [Azure AD의 인증 시나리오][aad_auth_scenarios]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d358-135">For more information about Azure AD endpoints, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="batch-resource-endpoint"></a><span data-ttu-id="2d358-136">Batch 리소스 끝점</span><span class="sxs-lookup"><span data-stu-id="2d358-136">Batch resource endpoint</span></span>

<span data-ttu-id="2d358-137">**Azure Batch 리소스 끝점**을 사용하여 Batch 서비스에 대한 요청을 인증하는 토큰을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-137">Use the **Azure Batch resource endpoint** to acquire a token for authenticating requests to the Batch service:</span></span>

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a><span data-ttu-id="2d358-138">테넌트에 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="2d358-138">Register your application with a tenant</span></span>

<span data-ttu-id="2d358-139">Azure AD를 사용하여 인증하는 첫 번째 단계는 Azure AD 테넌트에 응용 프로그램을 등록하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-139">The first step in using Azure AD to authenticate is registering your application in an Azure AD tenant.</span></span> <span data-ttu-id="2d358-140">응용 프로그램을 등록하면 코드에서 Azure [Active Directory 인증 라이브러리][aad_adal](ADAL)를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-140">Registering your application enables you to call the Azure [Active Directory Authentication Library][aad_adal] (ADAL) from your code.</span></span> <span data-ttu-id="2d358-141">ADAL은 응용 프로그램에서 Azure AD로 인증하는 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-141">The ADAL provides an API for authenticating with Azure AD from your application.</span></span> <span data-ttu-id="2d358-142">통합 인증 또는 서비스 주체를 사용하려면 응용 프로그램을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-142">Registering your application is required whether you plan to use integrated authentication or a service principal.</span></span>

<span data-ttu-id="2d358-143">응용 프로그램을 등록할 때 응용 프로그램에 대한 정보를 Azure AD에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-143">When you register your application, you supply information about your application to Azure AD.</span></span> <span data-ttu-id="2d358-144">그런 다음 Azure AD는 런타임 시 응용 프로그램을 Azure AD와 연결하는 데 사용하는 응용 프로그램 ID를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-144">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="2d358-145">응용 프로그램 ID에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 및 서비스 주체 개체](../active-directory/develop/active-directory-application-objects.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d358-145">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="2d358-146">Batch 응용 프로그램을 등록하려면 [Azure Active Directory와 응용 프로그램 통합][aad_integrate]에서 [응용 프로그램 추가](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) 섹션의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-146">To register your Batch application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="2d358-147">응용 프로그램을 네이티브 응용 프로그램으로 등록하는 경우 **리디렉션 URI**에 유효한 URI를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-147">If you register your application as a Native Application, you can specify any valid URI for the **Redirect URI**.</span></span> <span data-ttu-id="2d358-148">실제 끝점일 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-148">It does not need to be a real endpoint.</span></span>

<span data-ttu-id="2d358-149">응용 프로그램을 등록하면 응용 프로그램 ID가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-149">After you've registered your application, you'll see the application ID:</span></span>

![Azure AD에 Batch 응용 프로그램 등록](./media/batch-aad-auth/app-registration-data-plane.png)

<span data-ttu-id="2d358-151">Azure AD에 응용 프로그램을 등록하는 방법에 대한 자세한 내용은 [Azure AD의 인증 시나리오](../active-directory/develop/active-directory-authentication-scenarios.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d358-151">For more information about registering an application with Azure AD, see [Authentication Scenarios for Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span></span>

## <a name="get-the-tenant-id-for-your-active-directory"></a><span data-ttu-id="2d358-152">Active Directory에 대한 테넌트 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="2d358-152">Get the tenant ID for your Active Directory</span></span>

<span data-ttu-id="2d358-153">테넌트 ID는 응용 프로그램에 인증 서비스를 제공하는 Azure AD 테넌트를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-153">The tenant ID identifies the Azure AD tenant that provides authentication services to your application.</span></span> <span data-ttu-id="2d358-154">테넌트 ID를 얻으려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-154">To get the tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="2d358-155">Azure Portal에서 Active Directory를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-155">In the Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="2d358-156">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-156">Click **Properties**.</span></span>
3. <span data-ttu-id="2d358-157">디렉터리 ID에 제공된 GUID 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-157">Copy the GUID value provided for the directory ID.</span></span> <span data-ttu-id="2d358-158">이 값은 테넌트 ID라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-158">This value is also called the tenant ID.</span></span>

![디렉터리 ID 복사](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a><span data-ttu-id="2d358-160">통합 인증 사용</span><span class="sxs-lookup"><span data-stu-id="2d358-160">Use integrated authentication</span></span>

<span data-ttu-id="2d358-161">통합 인증으로 인증하려면 Batch 서비스 API에 연결하기 위한 권한을 응용 프로그램에 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-161">To authenticate with integrated authentication, you need to grant your application permissions to connect to the Batch service API.</span></span> <span data-ttu-id="2d358-162">이 단계에서는 응용 프로그램에서 Azure AD를 사용하여 Batch 서비스 API에 대한 호출을 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-162">This step enables your application to authenticate calls to the Batch service API with Azure AD.</span></span>

<span data-ttu-id="2d358-163">[응용 프로그램을 등록](#register-your-application-with-an-azure-ad-tenant)했으면 Azure Portal에서 다음 단계에 따라 Batch 서비스에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-163">Once you've [registered your application](#register-your-application-with-an-azure-ad-tenant), follow these steps in the Azure portal to grant it access to the Batch service:</span></span>

1. <span data-ttu-id="2d358-164">Azure Portal의 왼쪽 탐색 창에서 **추가 서비스**를 선택하고 **앱 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-164">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="2d358-165">앱 등록의 목록에서 응용 프로그램의 이름을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-165">Search for the name of your application in the list of app registrations:</span></span>

    ![응용 프로그램 이름 검색](./media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="2d358-167">응용 프로그램에 대한**설정** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-167">Open the **Settings** blade for your application.</span></span> <span data-ttu-id="2d358-168">**API 액세스** 섹션에서 **필요한 사용 권한**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-168">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="2d358-169">**필요한 사용 권한** 블레이드에서 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-169">In the **Required permissions** blade, click the **Add** button.</span></span>
5. <span data-ttu-id="2d358-170">1단계에서 Batch API를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-170">In step 1, search for the Batch API.</span></span> <span data-ttu-id="2d358-171">API를 찾을 때까지 다음 문자열 각각을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-171">Search for each of these strings until you find the API:</span></span>
    1. <span data-ttu-id="2d358-172">**MicrosoftAzureBatch**</span><span class="sxs-lookup"><span data-stu-id="2d358-172">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="2d358-173">**Microsoft Azure Batch** -</span><span class="sxs-lookup"><span data-stu-id="2d358-173">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="2d358-174">최신 Azure AD 테넌트에서는 이 이름을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-174">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="2d358-175">**ddbf3205-c6bd-46ae-8127-60eb93363864**는 Batch API에 대한 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is the ID for the Batch API.</span></span> 
6. <span data-ttu-id="2d358-176">Batch API를 찾으면 해당 API를 선택하고 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-176">Once you find the Batch API, select it and click the **Select** button.</span></span>
6. <span data-ttu-id="2d358-177">2단계에서 **Azure Batch 서비스에 액세스** 옆의 확인란을 선택하고 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-177">In step 2, select the check box next to **Access Azure Batch Service** and click the **Select** button.</span></span>
7. <span data-ttu-id="2d358-178">**완료** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-178">Click the **Done** button.</span></span>

<span data-ttu-id="2d358-179">이제 **필요한 권한** 블레이드에서 Azure AD 응용 프로그램에 ADAL 및 Batch 서비스 API 모두에 대한 액세스 권한이 있음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-179">The **Required Permissions** blade now shows that your Azure AD application has access to both ADAL and the Batch service API.</span></span> <span data-ttu-id="2d358-180">Azure AD에 앱을 처음 등록할 때 자동으로 ADAL에 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-180">Permissions are granted to ADAL automatically when you first register your app with Azure AD.</span></span>

![API 권한 부여](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a><span data-ttu-id="2d358-182">서비스 주체 사용</span><span class="sxs-lookup"><span data-stu-id="2d358-182">Use a service principal</span></span> 

<span data-ttu-id="2d358-183">무인으로 실행되는 응용 프로그램을 인증하려면 서비스 사용자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-183">To authenticate an application that runs unattended, you use a service principal.</span></span> <span data-ttu-id="2d358-184">응용 프로그램을 등록했으면 Azure Portal에서 다음 단계에 따라 서비스 주체를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-184">After you've registered your application, follow these steps in the Azure portal to configure a service principal:</span></span>

1. <span data-ttu-id="2d358-185">응용 프로그램에 대한 비밀 키를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-185">Request a secret key for your application.</span></span>
2. <span data-ttu-id="2d358-186">응용 프로그램에 RBAC 역할을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-186">Assign an RBAC role to your application.</span></span>

### <a name="request-a-secret-key-for-your-application"></a><span data-ttu-id="2d358-187">응용 프로그램에 대한 비밀 키 요청</span><span class="sxs-lookup"><span data-stu-id="2d358-187">Request a secret key for your application</span></span>

<span data-ttu-id="2d358-188">응용 프로그램에서 서비스 주체를 사용하여 인증하는 경우 Azure AD에 응용 프로그램 ID와 비밀 키를 모두 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-188">When your application authenticates with a service principal, it sends both the application ID and a secret key to Azure AD.</span></span> <span data-ttu-id="2d358-189">코드에서 사용할 비밀 키를 만들고 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-189">You'll need to create and copy the secret key to use from your code.</span></span>

<span data-ttu-id="2d358-190">Azure Portal에서 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-190">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="2d358-191">Azure Portal의 왼쪽 탐색 창에서 **추가 서비스**를 선택하고 **앱 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-191">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="2d358-192">앱 등록 목록에서 응용 프로그램의 이름을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-192">Search for the name of your application in the list of app registrations.</span></span>
3. <span data-ttu-id="2d358-193">**설정** 블레이드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-193">Display the **Settings** blade.</span></span> <span data-ttu-id="2d358-194">**API 액세스** 섹션에서 **키**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-194">In the **API Access** section, select **Keys**.</span></span>
4. <span data-ttu-id="2d358-195">키를 만들려면 키에 대한 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-195">To create a key, enter a description for the key.</span></span> <span data-ttu-id="2d358-196">그런 다음 키의 기간으로 1년 또는 2년을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-196">Then select a duration for the key of either one or two years.</span></span> 
5. <span data-ttu-id="2d358-197">**저장** 단추를 클릭하여 키를 만들고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-197">Click the **Save** button to create and display the key.</span></span> <span data-ttu-id="2d358-198">블레이드를 닫은 후에 다시 액세스할 수 없으므로 키 값을 안전한 곳에 복사해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-198">Copy the key value to a safe place, as you won't be able to access it again after you leave the blade.</span></span> 

    ![비밀 키 만들기](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-to-your-application"></a><span data-ttu-id="2d358-200">응용 프로그램에 RBAC 역할 할당</span><span class="sxs-lookup"><span data-stu-id="2d358-200">Assign an RBAC role to your application</span></span>

<span data-ttu-id="2d358-201">서비스 주체로 인증하려면 응용 프로그램에 RBAC 역할을 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-201">To authenticate with a service principal, you need to assign an RBAC role to your application.</span></span> <span data-ttu-id="2d358-202">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="2d358-202">Follow these steps:</span></span>

1. <span data-ttu-id="2d358-203">Azure Portal에서 응용 프로그램에서 사용되는 배치 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-203">In the Azure portal, navigate to the Batch account used by your application.</span></span>
2. <span data-ttu-id="2d358-204">배치 계정의 **설정** 블레이드에서 **액세스 제어(IAM)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-204">In the **Settings** blade for the Batch account, select **Access Control (IAM)**.</span></span>
3. <span data-ttu-id="2d358-205">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-205">Click the **Add** button.</span></span> 
4. <span data-ttu-id="2d358-206">**역할** 드롭다운에서 응용 프로그램에 대한 _참가자_ 또는 _읽기 권한자_ 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-206">From the **Role** drop-down, choose either the _Contributor_ or _Reader_ role for your application.</span></span> <span data-ttu-id="2d358-207">이러한 역할에 대한 자세한 내용은 [Azure Portal에서 액세스 관리 시작](../active-directory/role-based-access-control-what-is.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d358-207">For more information on these roles, see [Get started with Role-Based Access Control in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  
5. <span data-ttu-id="2d358-208">**선택** 필드에서 응용 프로그램의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-208">In the **Select** field, enter the name of your application.</span></span> <span data-ttu-id="2d358-209">목록에서 응용 프로그램을 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-209">Select your application from the list, and click **Save**.</span></span>

<span data-ttu-id="2d358-210">이제 액세스 제어 설정에서 RBAC 역할이 할당된 응용 프로그램이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-210">Your application should now appear in your access control settings with an RBAC role assigned.</span></span> 

![응용 프로그램에 RBAC 역할 할당](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-the-tenant-id-for-your-azure-active-directory"></a><span data-ttu-id="2d358-212">Azure Active Directory에 대한 테넌트 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="2d358-212">Get the tenant ID for your Azure Active Directory</span></span>

<span data-ttu-id="2d358-213">테넌트 ID는 응용 프로그램에 인증 서비스를 제공하는 Azure AD 테넌트를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-213">The tenant ID identifies the Azure AD tenant that provides authentication services to your application.</span></span> <span data-ttu-id="2d358-214">테넌트 ID를 얻으려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-214">To get the tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="2d358-215">Azure Portal에서 Active Directory를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-215">In the Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="2d358-216">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-216">Click **Properties**.</span></span>
3. <span data-ttu-id="2d358-217">디렉터리 ID에 제공된 GUID 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-217">Copy the GUID value provided for the directory ID.</span></span> <span data-ttu-id="2d358-218">이 값은 테넌트 ID라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-218">This value is also called the tenant ID.</span></span>

![디렉터리 ID 복사](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a><span data-ttu-id="2d358-220">코드 예제</span><span class="sxs-lookup"><span data-stu-id="2d358-220">Code examples</span></span>

<span data-ttu-id="2d358-221">이 섹션의 코드 예제에서는 Azure AD에서 통합 인증과 서비스 주체를 사용하여 인증하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-221">The code examples in this section show how to authenticate with Azure AD using integrated authentication and with a service principal.</span></span> <span data-ttu-id="2d358-222">이 코드 예제에서 .NET을 사용하지만, 개념은 다른 언어와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-222">These code examples use .NET, but the concepts are similar for other languages.</span></span>

> [!NOTE]
> <span data-ttu-id="2d358-223">Azure AD 인증 토큰은 1시간 후 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-223">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="2d358-224">수명이 긴 **BatchClient** 개체를 사용하는 경우 항상 유효한 토큰을 갖도록 모든 요청에 대해 ADAL에서 토큰을 검색하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-224">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request to ensure you always have a valid token.</span></span> 
>
>
> <span data-ttu-id="2d358-225">이를 위해 .NET에서 Azure AD에서 토큰을 검색하는 메서드를 작성하고 해당 메서드를 대리자로 **BatchTokenCredentials** 개체에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-225">To achieve this in .NET, write a method that retrieves the token from Azure AD and pass that method to a **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="2d358-226">대리자 메서드는 유효한 토큰이 제공되었는지 확인하도록 Batch 서비스에 대한 모든 요청에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-226">The delegate method is called on every request to the Batch service to ensure that a valid token is provided.</span></span> <span data-ttu-id="2d358-227">기본적으로 ADAL은 토큰을 캐시하므로 필요한 경우 Azure AD에서 새 토큰이 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-227">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="2d358-228">Azure AD의 토큰에 대한 자세한 내용은 [Azure AD의 인증 시나리오][aad_auth_scenarios]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d358-228">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a><span data-ttu-id="2d358-229">코드 예제: Batch .NET에서 Azure AD 통합 인증 사용</span><span class="sxs-lookup"><span data-stu-id="2d358-229">Code example: Using Azure AD integrated authentication with Batch .NET</span></span>

<span data-ttu-id="2d358-230">Batch .NET의 통합 인증으로 인증하려면 [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) 패키지 및 [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) 패키지를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-230">To authenticate with integrated authentication from Batch .NET, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="2d358-231">코드에 다음 `using` 문을 포함시킵니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-231">Include the following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="2d358-232">코드에서 테넌트 ID를 포함하여 Azure AD 끝점을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-232">Reference the Azure AD endpoint in your code, including the tenant ID.</span></span> <span data-ttu-id="2d358-233">테넌트 ID를 검색하려면 [Azure Active Directory에 대한 테넌트 ID 가져오기](#get-the-tenant-id-for-your-active-directory)에서 설명하는 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-233">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="2d358-234">Batch 서비스 리소스 끝점 참조:</span><span class="sxs-lookup"><span data-stu-id="2d358-234">Reference the Batch service resource endpoint:</span></span>

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="2d358-235">배치 계정 참조:</span><span class="sxs-lookup"><span data-stu-id="2d358-235">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="2d358-236">응용 프로그램에 대한 응용 프로그램 ID(클라이언트 ID)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-236">Specify the application ID (client ID) for your application.</span></span> <span data-ttu-id="2d358-237">응용 프로그램 ID는 Azure Portal의 앱 등록에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-237">The application ID is available from your app registration in the Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="2d358-238">또한 등록 프로세스 중 지정한 리디렉션 URI를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-238">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="2d358-239">코드에 지정된 리디렉션 URI는 응용 프로그램을 등록할 때 제공한 리디렉션 URI와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-239">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application:</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="2d358-240">Azure AD에서 인증 토큰을 획득하는 콜백 메서드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-240">Write a callback method to acquire the authentication token from Azure AD.</span></span> <span data-ttu-id="2d358-241">여기에 표시된 **GetAuthenticationTokenAsync** 콜백 메서드는 ADAL을 호출하여 응용 프로그램과 상호 작용하는 사용자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-241">The **GetAuthenticationTokenAsync** callback method shown here calls ADAL to authenticate a user who is interacting with the application.</span></span> <span data-ttu-id="2d358-242">ADAL에서 제공하는 **AcquireTokenAsync** 메서드는 사용자에게 자격 증명을 묻는 메시지를 표시하고, 사용자가 자격 증명을 제공하면 응용 프로그램이 계속 진행됩니다(이미 캐시된 자격 증명이 있는 경우 제외).</span><span class="sxs-lookup"><span data-stu-id="2d358-242">The **AcquireTokenAsync** method provided by ADAL prompts the user for their credentials, and the application proceeds once the user provides them (unless it has already cached credentials):</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire the authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

<span data-ttu-id="2d358-243">매개 변수로 대리자를 사용자는 **BatchTokenCredentials** 개체를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-243">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span></span> <span data-ttu-id="2d358-244">이러한 자격 증명을 사용하여 **BatchClient** 개체를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-244">Use those credentials to open a **BatchClient** object.</span></span> <span data-ttu-id="2d358-245">Batch 서비스에 대한 후속 작업에 대해 해당 **BatchClient** 개체를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-245">You can use that **BatchClient** object for subsequent operations against the Batch service:</span></span>

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a><span data-ttu-id="2d358-246">코드 예제: Batch .NET에서 Azure AD 서비스 주체 사용</span><span class="sxs-lookup"><span data-stu-id="2d358-246">Code example: Using an Azure AD service principal with Batch .NET</span></span>

<span data-ttu-id="2d358-247">Batch .NET의 서비스 주체로 인증하려면 [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) 패키지 및 [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) 패키지를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-247">To authenticate with a service principal from Batch .NET, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="2d358-248">코드에 다음 `using` 문을 포함시킵니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-248">Include the following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="2d358-249">코드에서 테넌트 ID를 포함하여 Azure AD 끝점을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-249">Reference the Azure AD endpoint in your code, including the tenant ID.</span></span> <span data-ttu-id="2d358-250">서비스 주체를 사용하는 경우 테넌트별 끝점을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-250">When using a service principal, you must provide a tenant-specific endpoint.</span></span> <span data-ttu-id="2d358-251">테넌트 ID를 검색하려면 [Azure Active Directory에 대한 테넌트 ID 가져오기](#get-the-tenant-id-for-your-active-directory)에서 설명하는 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-251">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="2d358-252">Batch 서비스 리소스 끝점 참조:</span><span class="sxs-lookup"><span data-stu-id="2d358-252">Reference the Batch service resource endpoint:</span></span>  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="2d358-253">배치 계정 참조:</span><span class="sxs-lookup"><span data-stu-id="2d358-253">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="2d358-254">응용 프로그램에 대한 응용 프로그램 ID(클라이언트 ID)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-254">Specify the application ID (client ID) for your application.</span></span> <span data-ttu-id="2d358-255">응용 프로그램 ID는 Azure Portal의 앱 등록에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-255">The application ID is available from your app registration in the Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="2d358-256">Azure Portal에서 복사한 비밀 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-256">Specify the secret key that you copied from the Azure portal:</span></span>

```csharp
private const string ClientKey = "<secret-key>";
```

<span data-ttu-id="2d358-257">Azure AD에서 인증 토큰을 획득하는 콜백 메서드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-257">Write a callback method to acquire the authentication token from Azure AD.</span></span> <span data-ttu-id="2d358-258">여기에 표시된 **GetAuthenticationTokenAsync** 콜백 메서드는 무인 인증을 위해 ADAL을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-258">The **GetAuthenticationTokenAsync** callback method shown here calls ADAL for unattended authentication:</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

<span data-ttu-id="2d358-259">매개 변수로 대리자를 사용자는 **BatchTokenCredentials** 개체를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-259">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span></span> <span data-ttu-id="2d358-260">이러한 자격 증명을 사용하여 **BatchClient** 개체를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-260">Use those credentials to open a **BatchClient** object.</span></span> <span data-ttu-id="2d358-261">그런 다음 Batch 서비스에 대한 후속 작업에 대해 해당 **BatchClient** 개체를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-261">You can then use that **BatchClient** object for subsequent operations against the Batch service:</span></span>

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="2d358-262">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2d358-262">Next steps</span></span>

<span data-ttu-id="2d358-263">Azure AD에 대한 자세한 내용은 [Azure Active Directory 설명서](https://docs.microsoft.com/azure/active-directory/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d358-263">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="2d358-264">ADAL을 사용하는 방법을 보여 주는 자세한 예제는 [Azure 코드 샘플](https://azure.microsoft.com/resources/samples/?service=active-directory) 라이브러리에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-264">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="2d358-265">서비스 주체에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 및 서비스 주체 개체](../active-directory/develop/active-directory-application-objects.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d358-265">To learn more about service principals, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span> <span data-ttu-id="2d358-266">Azure Portal을 사용하여 서비스 주체를 만들려면 [포털을 사용하여 리소스에 액세스할 수 있는 Active Directory 응용 프로그램 및 서비스 주체 만들기](../resource-group-create-service-principal-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d358-266">To create a service principal using the Azure portal, see [Use portal to create Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="2d358-267">또한 PowerShell 또는 Azure CLI를 사용하여 서비스 주체를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d358-267">You can also create a service principal with PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="2d358-268">Azure AD를 사용하여 Batch Management 응용 프로그램을 인증하려면 [Active Directory를 사용하여 Batch Management 솔루션 인증](batch-aad-auth-management.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d358-268">To authenticate Batch Management applications using Azure AD, see [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span> 

<span data-ttu-id="2d358-269">[aad_about]: ../active-directory/active-directory-whatis.md "Azure Active Directory란?"</span><span class="sxs-lookup"><span data-stu-id="2d358-269">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="2d358-270">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD의 인증 시나리오"</span><span class="sxs-lookup"><span data-stu-id="2d358-270">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="2d358-271">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Azure Active Directory와 응용 프로그램 통합"</span><span class="sxs-lookup"><span data-stu-id="2d358-271">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[azure_portal]: http://portal.azure.com
