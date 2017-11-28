---
title: "aaaUse Azure Active Directory tooauthenticate Azure 배치 서비스 솔루션 | Microsoft Docs"
description: "일괄 처리는 hello 일괄 처리 서비스에서에서 인증을 위한 Azure AD를 지원합니다."
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
ms.openlocfilehash: 6c825c30f1c80bb059a797a2e78367e599acd109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a><span data-ttu-id="e63c4-103">Active Directory를 사용하여 Batch 서비스 솔루션 인증</span><span class="sxs-lookup"><span data-stu-id="e63c4-103">Authenticate Batch service solutions with Active Directory</span></span>

<span data-ttu-id="e63c4-104">Azure Batch는 [Azure Active Directory][aad_about](Azure AD) 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="e63c4-105">Azure AD는 Microsoft의 다중 테넌트 클라우드 기반 디렉터리 및 ID 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="e63c4-106">Azure는 고객, 서비스 관리자 및 조직 사용자가 Azure AD tooauthenticate 자체가 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-106">Azure itself uses Azure AD tooauthenticate its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="e63c4-107">Azure Batch와 함께 Azure AD 인증을 사용할 때 다음 두 가지 방법 중 하나로 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-107">When using Azure AD authentication with Azure Batch, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="e63c4-108">사용 하 여 **통합된 인증** tooauthenticate가 hello 응용 프로그램 상호 작용 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-108">By using **integrated authentication** tooauthenticate a user that is interacting with hello application.</span></span> <span data-ttu-id="e63c4-109">통합된 인증을 사용 하 여 응용 프로그램 사용자의 자격 증명을 수집 하 고 해당 자격 증명 tooauthenticate tooBatch 리소스에 액세스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-109">An application using integrated authentication gathers a user's credentials and uses those credentials tooauthenticate access tooBatch resources.</span></span>
- <span data-ttu-id="e63c4-110">사용 하 여 한 **서비스 사용자** tooauthenticate 무인된 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-110">By using a **service principal** tooauthenticate an unattended application.</span></span> <span data-ttu-id="e63c4-111">서비스 사용자는 런타임에 리소스에 액세스할 때 순서 toorepresent hello 응용 프로그램에 hello 정책 및 응용 프로그램에 대 한 사용 권한을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-111">A service principal defines hello policy and permissions for an application in order toorepresent hello application when accessing resources at runtime.</span></span>

<span data-ttu-id="e63c4-112">Azure AD에 대해 자세히 toolearn 참조 hello [Azure Active Directory 설명서](https://docs.microsoft.com/azure/active-directory/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-112">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span>

## <a name="authentication-and-pool-allocation-mode"></a><span data-ttu-id="e63c4-113">인증 및 풀 할당 모드</span><span class="sxs-lookup"><span data-stu-id="e63c4-113">Authentication and pool allocation mode</span></span>

<span data-ttu-id="e63c4-114">배치 계정을 만들 때 해당 계정에 대해 생성된 풀을 할당해야 하는 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-114">When you create a Batch account, you can specify where pools created for that account should be allocated.</span></span> <span data-ttu-id="e63c4-115">사용자 구독 또는 hello 기본 일괄 처리 서비스 구독에 tooallocate 풀을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-115">You can choose tooallocate pools either in hello default Batch service subscription or in a user subscription.</span></span> <span data-ttu-id="e63c4-116">사용자가 선택한 해당 계정에 대 한 액세스 tooresources를 인증 하는 방법에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-116">Your choice affects how you authenticate access tooresources in that account.</span></span>

- <span data-ttu-id="e63c4-117">**Batch 서비스 구독** -</span><span class="sxs-lookup"><span data-stu-id="e63c4-117">**Batch service subscription**.</span></span> <span data-ttu-id="e63c4-118">기본적으로 Batch 풀은 Batch 서비스 구독에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-118">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="e63c4-119">이 옵션을 선택 하는 경우를 인증할 수 있습니다 액세스 tooresources 해당 계정에서 사용 하 여 [공유 키](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) 또는 Azure AD와 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-119">If you choose this option, you can authenticate access tooresources in that account either with [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) or with Azure AD.</span></span>
- <span data-ttu-id="e63c4-120">**사용자 구독** -</span><span class="sxs-lookup"><span data-stu-id="e63c4-120">**User subscription.**</span></span> <span data-ttu-id="e63c4-121">지정한 사용자 구독에 tooallocate 일괄 처리 풀을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-121">You can choose tooallocate Batch pools in a user subscription that you specify.</span></span> <span data-ttu-id="e63c4-122">이 옵션을 선택하는 경우 Azure AD로 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-122">If you choose this option, you must authenticate with Azure AD.</span></span>

## <a name="endpoints-for-authentication"></a><span data-ttu-id="e63c4-123">인증에 대한 끝점</span><span class="sxs-lookup"><span data-stu-id="e63c4-123">Endpoints for authentication</span></span>

<span data-ttu-id="e63c4-124">tooinclude 해야 Azure AD와 tooauthenticate 일괄 처리 응용 프로그램 코드에서 잘 알려진 일부 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-124">tooauthenticate Batch applications with Azure AD, you need tooinclude some well-known endpoints in your code.</span></span>

### <a name="azure-ad-endpoint"></a><span data-ttu-id="e63c4-125">Azure AD 끝점</span><span class="sxs-lookup"><span data-stu-id="e63c4-125">Azure AD endpoint</span></span>

<span data-ttu-id="e63c4-126">기본 hello Azure AD 권한 끝점은:</span><span class="sxs-lookup"><span data-stu-id="e63c4-126">hello base Azure AD authority endpoint is:</span></span>

`https://login.microsoftonline.com/`

<span data-ttu-id="e63c4-127">Azure AD와 tooauthenticate, hello 테 넌 트 ID (디렉터리 ID)와 함께이 끝점을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-127">tooauthenticate with Azure AD, you use this endpoint together with hello tenant ID (directory ID).</span></span> <span data-ttu-id="e63c4-128">hello 테 넌 트 ID를 인증에 대 한 hello Azure AD 테 넌 트 toouse를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-128">hello tenant ID identifies hello Azure AD tenant toouse for authentication.</span></span> <span data-ttu-id="e63c4-129">tooretrieve hello 테 넌 트 ID에 설명 된 hello 단계에 따라 [hello 테 넌 트 ID를 Azure Active Directory에 대 한 가져오기](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="e63c4-129">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> <span data-ttu-id="e63c4-130">서비스 사용자를 사용 하 여 인증 hello 테 넌 트 별 끝점이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-130">hello tenant-specific endpoint is required when you authenticate using a service principal.</span></span> 
> 
> <span data-ttu-id="e63c4-131">hello 테 넌 트 별 끝점 통합된 인증을 사용 하 여 인증 하는 경우 선택 사항 이지만 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-131">hello tenant-specific endpoint is optional when you authenticate using integrated authentication, but recommended.</span></span> <span data-ttu-id="e63c4-132">그러나 hello Azure AD의 공통 끝점을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-132">However, you can also use hello Azure AD common endpoint.</span></span> <span data-ttu-id="e63c4-133">hello 일반 끝점이 특정 테 넌 트가 제공 되지 않으면 인터페이스 수집 일반 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-133">hello common endpoint provides a generic credential gathering interface when a specific tenant is not provided.</span></span> <span data-ttu-id="e63c4-134">hello 공용 끝점을 `https://login.microsoftonline.com/common`합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-134">hello common endpoint is `https://login.microsoftonline.com/common`.</span></span>
>
>

<span data-ttu-id="e63c4-135">Azure AD 끝점에 대한 자세한 내용은 [Azure AD의 인증 시나리오][aad_auth_scenarios]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e63c4-135">For more information about Azure AD endpoints, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="batch-resource-endpoint"></a><span data-ttu-id="e63c4-136">Batch 리소스 끝점</span><span class="sxs-lookup"><span data-stu-id="e63c4-136">Batch resource endpoint</span></span>

<span data-ttu-id="e63c4-137">사용 하 여 hello **Azure 배치 리소스 끝점** tooacquire 인증을 위한 토큰 toohello 일괄 처리 서비스를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-137">Use hello **Azure Batch resource endpoint** tooacquire a token for authenticating requests toohello Batch service:</span></span>

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a><span data-ttu-id="e63c4-138">테넌트에 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="e63c4-138">Register your application with a tenant</span></span>

<span data-ttu-id="e63c4-139">hello tooauthenticate Azure AD를 사용 하 여 첫 번째 단계는 Azure AD 테 넌 트의 응용 프로그램을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-139">hello first step in using Azure AD tooauthenticate is registering your application in an Azure AD tenant.</span></span> <span data-ttu-id="e63c4-140">Toocall hello Azure 응용 프로그램을 등록 하면 [Active Directory 인증 라이브러리] [ aad_adal] (ADAL) 사용자 코드에서.</span><span class="sxs-lookup"><span data-stu-id="e63c4-140">Registering your application enables you toocall hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) from your code.</span></span> <span data-ttu-id="e63c4-141">ADAL hello 응용 프로그램에서 Azure AD에 인증 하기 위해 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-141">hello ADAL provides an API for authenticating with Azure AD from your application.</span></span> <span data-ttu-id="e63c4-142">Toouse 통합된 인증 또는 서비스 사용자를 계획 하 고 있는지 여부를 응용 프로그램 등록가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-142">Registering your application is required whether you plan toouse integrated authentication or a service principal.</span></span>

<span data-ttu-id="e63c4-143">응용 프로그램을 등록 하는 경우에 프로그램 응용 프로그램 tooAzure AD에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-143">When you register your application, you supply information about your application tooAzure AD.</span></span> <span data-ttu-id="e63c4-144">그런 다음 azure AD는 응용 프로그램 ID를 제공 합니다. 사용 하는 tooassociate 응용 프로그램 런타임 시 Azure AD와 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-144">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="e63c4-145">hello 응용 프로그램 ID에 대해 자세히 toolearn 참조 [응용 프로그램 및 Azure Active Directory에서 서비스 보안 주체 개체](../active-directory/develop/active-directory-application-objects.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-145">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="e63c4-146">tooregister hello의 hello 단계에 따라 일괄 처리 응용 프로그램 [응용 프로그램 추가](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) 섹션 [Azure Active Directory와 응용 프로그램 통합][aad_integrate]합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-146">tooregister your Batch application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="e63c4-147">Hello에 대 한 모든 유효한 URI를 지정할 수는 네이티브 응용 프로그램으로 응용 프로그램을 등록 하는 경우 **리디렉션 URI**합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-147">If you register your application as a Native Application, you can specify any valid URI for hello **Redirect URI**.</span></span> <span data-ttu-id="e63c4-148">실제 끝점 toobe가 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-148">It does not need toobe a real endpoint.</span></span>

<span data-ttu-id="e63c4-149">응용 프로그램에 등록 한 후 hello 응용 프로그램 ID에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-149">After you've registered your application, you'll see hello application ID:</span></span>

![Azure AD에 Batch 응용 프로그램 등록](./media/batch-aad-auth/app-registration-data-plane.png)

<span data-ttu-id="e63c4-151">Azure AD에 응용 프로그램을 등록하는 방법에 대한 자세한 내용은 [Azure AD의 인증 시나리오](../active-directory/develop/active-directory-authentication-scenarios.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e63c4-151">For more information about registering an application with Azure AD, see [Authentication Scenarios for Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span></span>

## <a name="get-hello-tenant-id-for-your-active-directory"></a><span data-ttu-id="e63c4-152">Active Directory에 대 한 hello 테 넌 트 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="e63c4-152">Get hello tenant ID for your Active Directory</span></span>

<span data-ttu-id="e63c4-153">hello 테 넌 트 ID 인증 서비스 tooyour 응용 프로그램을 제공 hello Azure AD 테 넌 트를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-153">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="e63c4-154">tooget hello 테 넌 트 ID, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-154">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="e63c4-155">Hello Azure 포털에서에서 Active Directory를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-155">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="e63c4-156">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-156">Click **Properties**.</span></span>
3. <span data-ttu-id="e63c4-157">Hello 디렉터리 ID에 대해 제공 된 hello GUID 값 복사</span><span class="sxs-lookup"><span data-stu-id="e63c4-157">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="e63c4-158">이 값은 테 넌 트 ID hello 라고도</span><span class="sxs-lookup"><span data-stu-id="e63c4-158">This value is also called hello tenant ID.</span></span>

![Hello 디렉터리 ID 복사](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a><span data-ttu-id="e63c4-160">통합 인증 사용</span><span class="sxs-lookup"><span data-stu-id="e63c4-160">Use integrated authentication</span></span>

<span data-ttu-id="e63c4-161">통합 인증으로 tooauthenticate toogrant 응용 프로그램 사용 권한 tooconnect toohello 일괄 처리 서비스 API를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-161">tooauthenticate with integrated authentication, you need toogrant your application permissions tooconnect toohello Batch service API.</span></span> <span data-ttu-id="e63c4-162">이 단계에서는 Azure AD와 응용 프로그램 tooauthenticate 호출 toohello 일괄 처리 서비스 API입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-162">This step enables your application tooauthenticate calls toohello Batch service API with Azure AD.</span></span>

<span data-ttu-id="e63c4-163">한 후 [응용 프로그램 등록](#register-your-application-with-an-azure-ad-tenant), hello toohello 일괄 처리 서비스에 액세스 하는 Azure 포털 toogrant에서에서 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-163">Once you've [registered your application](#register-your-application-with-an-azure-ad-tenant), follow these steps in hello Azure portal toogrant it access toohello Batch service:</span></span>

1. <span data-ttu-id="e63c4-164">Hello hello Azure 포털의 왼쪽 탐색 창에서 선택 **더 서비스**, 클릭 **앱 등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-164">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="e63c4-165">응용 프로그램 등록의 hello 목록에서 응용 프로그램의 hello 이름 검색:</span><span class="sxs-lookup"><span data-stu-id="e63c4-165">Search for hello name of your application in hello list of app registrations:</span></span>

    ![응용 프로그램 이름 검색](./media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="e63c4-167">열기 hello **설정을** 블레이드 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-167">Open hello **Settings** blade for your application.</span></span> <span data-ttu-id="e63c4-168">Hello에 **API 액세스** 섹션에서 **필요한 권한**합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-168">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="e63c4-169">Hello에 **필요한 권한** 블레이드에서 hello 클릭 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-169">In hello **Required permissions** blade, click hello **Add** button.</span></span>
5. <span data-ttu-id="e63c4-170">1 단계에서 일괄 처리 API hello에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-170">In step 1, search for hello Batch API.</span></span> <span data-ttu-id="e63c4-171">Hello API를 찾을 때까지 이러한 문자열에 대 한 검색:</span><span class="sxs-lookup"><span data-stu-id="e63c4-171">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="e63c4-172">**MicrosoftAzureBatch**</span><span class="sxs-lookup"><span data-stu-id="e63c4-172">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="e63c4-173">**Microsoft Azure Batch** -</span><span class="sxs-lookup"><span data-stu-id="e63c4-173">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="e63c4-174">최신 Azure AD 테넌트에서는 이 이름을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-174">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="e63c4-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** hello 일괄 처리 API에 대 한 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 
6. <span data-ttu-id="e63c4-176">일괄 처리 API hello를 찾은 후 선택 하 고 hello 클릭 **선택** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-176">Once you find hello Batch API, select it and click hello **Select** button.</span></span>
6. <span data-ttu-id="e63c4-177">2 단계에서 선택 hello 확인란 옆 너무**Access Azure 일괄 처리 서비스** hello 클릭 **선택** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-177">In step 2, select hello check box next too**Access Azure Batch Service** and click hello **Select** button.</span></span>
7. <span data-ttu-id="e63c4-178">Hello 클릭 **수행** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-178">Click hello **Done** button.</span></span>

<span data-ttu-id="e63c4-179">hello **필요한 권한** 블레이드 이제 Azure AD 응용 프로그램에 표시 tooboth ADAL에 액세스 하 고 일괄 처리 서비스 API hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-179">hello **Required Permissions** blade now shows that your Azure AD application has access tooboth ADAL and hello Batch service API.</span></span> <span data-ttu-id="e63c4-180">먼저 Azure AD에 앱을 등록 하는 경우 권한은 tooADAL은 자동으로 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-180">Permissions are granted tooADAL automatically when you first register your app with Azure AD.</span></span>

![API 권한 부여](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a><span data-ttu-id="e63c4-182">서비스 주체 사용</span><span class="sxs-lookup"><span data-stu-id="e63c4-182">Use a service principal</span></span> 

<span data-ttu-id="e63c4-183">tooauthenticate 무인 모드로 실행 되는 응용 프로그램, 서비스 사용자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-183">tooauthenticate an application that runs unattended, you use a service principal.</span></span> <span data-ttu-id="e63c4-184">응용 프로그램에 등록 한 후에 hello Azure 포털 tooconfigure 서비스 사용자의 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="e63c4-184">After you've registered your application, follow these steps in hello Azure portal tooconfigure a service principal:</span></span>

1. <span data-ttu-id="e63c4-185">응용 프로그램에 대한 비밀 키를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-185">Request a secret key for your application.</span></span>
2. <span data-ttu-id="e63c4-186">RBAC 역할 tooyour 응용 프로그램을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-186">Assign an RBAC role tooyour application.</span></span>

### <a name="request-a-secret-key-for-your-application"></a><span data-ttu-id="e63c4-187">응용 프로그램에 대한 비밀 키 요청</span><span class="sxs-lookup"><span data-stu-id="e63c4-187">Request a secret key for your application</span></span>

<span data-ttu-id="e63c4-188">응용 프로그램 서비스 사용자를 인증 하는 경우 hello 응용 프로그램 ID 및 비밀 키 tooAzure AD 모두 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-188">When your application authenticates with a service principal, it sends both hello application ID and a secret key tooAzure AD.</span></span> <span data-ttu-id="e63c4-189">Toocreate 필요 하 고 사용자 코드에서 비밀 키 toouse hello를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-189">You'll need toocreate and copy hello secret key toouse from your code.</span></span>

<span data-ttu-id="e63c4-190">Hello Azure 포털에서에서 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-190">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="e63c4-191">Hello hello Azure 포털의 왼쪽 탐색 창에서 선택 **더 서비스**, 클릭 **앱 등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-191">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="e63c4-192">응용 프로그램 등록의 hello 목록에서 응용 프로그램의 hello 이름을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-192">Search for hello name of your application in hello list of app registrations.</span></span>
3. <span data-ttu-id="e63c4-193">디스플레이 hello **설정을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-193">Display hello **Settings** blade.</span></span> <span data-ttu-id="e63c4-194">Hello에 **API 액세스** 섹션에서 **키**합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-194">In hello **API Access** section, select **Keys**.</span></span>
4. <span data-ttu-id="e63c4-195">키를 toocreate hello 키에 대 한 설명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-195">toocreate a key, enter a description for hello key.</span></span> <span data-ttu-id="e63c4-196">하나 또는 두 개의 년의 hello 키에 대 한 기간을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-196">Then select a duration for hello key of either one or two years.</span></span> 
5. <span data-ttu-id="e63c4-197">Hello 클릭 **저장** toocreate 단추 및 hello 키를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-197">Click hello **Save** button toocreate and display hello key.</span></span> <span data-ttu-id="e63c4-198">수 tooaccess 수 없을 것 처럼 hello 키 값 tooa 안전한 곳을 복사 후 다시 hello 블레이드를 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-198">Copy hello key value tooa safe place, as you won't be able tooaccess it again after you leave hello blade.</span></span> 

    ![비밀 키 만들기](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a><span data-ttu-id="e63c4-200">RBAC 역할 tooyour 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="e63c4-200">Assign an RBAC role tooyour application</span></span>

<span data-ttu-id="e63c4-201">서비스 사용자와 tooauthenticate, tooassign RBAC 역할 tooyour 응용 프로그램이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-201">tooauthenticate with a service principal, you need tooassign an RBAC role tooyour application.</span></span> <span data-ttu-id="e63c4-202">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="e63c4-202">Follow these steps:</span></span>

1. <span data-ttu-id="e63c4-203">Hello Azure 포털에서에서 응용 프로그램에서 사용 하는 일괄 처리 계정 toohello를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-203">In hello Azure portal, navigate toohello Batch account used by your application.</span></span>
2. <span data-ttu-id="e63c4-204">Hello에 **설정** 선택 hello 일괄 처리 계정에 대 한 블레이드 **액세스 제어 (IAM)**합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-204">In hello **Settings** blade for hello Batch account, select **Access Control (IAM)**.</span></span>
3. <span data-ttu-id="e63c4-205">Hello 클릭 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-205">Click hello **Add** button.</span></span> 
4. <span data-ttu-id="e63c4-206">Hello에서 **역할** 드롭다운 목록에서 선택 하거나 hello _참가자_ 또는 _판독기_ 응용 프로그램에 대 한 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-206">From hello **Role** drop-down, choose either hello _Contributor_ or _Reader_ role for your application.</span></span> <span data-ttu-id="e63c4-207">이러한 역할에 대 한 자세한 내용은 참조 하십시오. [hello Azure 포털에서에서 역할 기반 액세스 제어를 시작 하려면](../active-directory/role-based-access-control-what-is.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-207">For more information on these roles, see [Get started with Role-Based Access Control in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  
5. <span data-ttu-id="e63c4-208">Hello에 **선택** 필드에, 응용 프로그램의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-208">In hello **Select** field, enter hello name of your application.</span></span> <span data-ttu-id="e63c4-209">Hello 목록에서 응용 프로그램을 선택 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-209">Select your application from hello list, and click **Save**.</span></span>

<span data-ttu-id="e63c4-210">이제 액세스 제어 설정에서 RBAC 역할이 할당된 응용 프로그램이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-210">Your application should now appear in your access control settings with an RBAC role assigned.</span></span> 

![RBAC 역할 tooyour 응용 프로그램 할당](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a><span data-ttu-id="e63c4-212">Azure Active Directory에 대 한 hello 테 넌 트 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="e63c4-212">Get hello tenant ID for your Azure Active Directory</span></span>

<span data-ttu-id="e63c4-213">hello 테 넌 트 ID 인증 서비스 tooyour 응용 프로그램을 제공 hello Azure AD 테 넌 트를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-213">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="e63c4-214">tooget hello 테 넌 트 ID, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-214">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="e63c4-215">Hello Azure 포털에서에서 Active Directory를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-215">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="e63c4-216">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-216">Click **Properties**.</span></span>
3. <span data-ttu-id="e63c4-217">Hello 디렉터리 ID에 대해 제공 된 hello GUID 값 복사</span><span class="sxs-lookup"><span data-stu-id="e63c4-217">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="e63c4-218">이 값은 테 넌 트 ID hello 라고도</span><span class="sxs-lookup"><span data-stu-id="e63c4-218">This value is also called hello tenant ID.</span></span>

![Hello 디렉터리 ID 복사](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a><span data-ttu-id="e63c4-220">코드 예제</span><span class="sxs-lookup"><span data-stu-id="e63c4-220">Code examples</span></span>

<span data-ttu-id="e63c4-221">이 섹션의 hello 코드 예제에는 통합 인증을 사용 하 여 Azure AD와 tooauthenticate 하는 방법 및 서비스 사용자와 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-221">hello code examples in this section show how tooauthenticate with Azure AD using integrated authentication and with a service principal.</span></span> <span data-ttu-id="e63c4-222">이러한 코드 예제에서는.NET을 사용 하지만 hello 개념은 다른 언어에 대 한 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-222">These code examples use .NET, but hello concepts are similar for other languages.</span></span>

> [!NOTE]
> <span data-ttu-id="e63c4-223">Azure AD 인증 토큰은 1시간 후 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-223">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="e63c4-224">수명이 긴을 사용 하는 경우 **BatchClient** 개체 토큰을 검색 하는 것이 좋습니다 모든 요청 tooensure에 ADAL에서 항상 유효한 토큰을 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-224">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request tooensure you always have a valid token.</span></span> 
>
>
> <span data-ttu-id="e63c4-225">tooachieve.net에서는이 메서드를 작성 검색 hello Azure AD에서 토큰 및 해당 메서드 tooa 전달 **BatchTokenCredentials** 대리자로 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-225">tooachieve this in .NET, write a method that retrieves hello token from Azure AD and pass that method tooa **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="e63c4-226">유효한 토큰을 제공 하는 모든 요청 toohello 일괄 처리 서비스 tooensure hello 대리자 메서드 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-226">hello delegate method is called on every request toohello Batch service tooensure that a valid token is provided.</span></span> <span data-ttu-id="e63c4-227">기본적으로 ADAL은 토큰을 캐시하므로 필요한 경우 Azure AD에서 새 토큰이 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-227">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="e63c4-228">Azure AD의 토큰에 대한 자세한 내용은 [Azure AD의 인증 시나리오][aad_auth_scenarios]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e63c4-228">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a><span data-ttu-id="e63c4-229">코드 예제: Batch .NET에서 Azure AD 통합 인증 사용</span><span class="sxs-lookup"><span data-stu-id="e63c4-229">Code example: Using Azure AD integrated authentication with Batch .NET</span></span>

<span data-ttu-id="e63c4-230">일괄 처리.NET, 참조 hello에서에서 통합된 인증으로 tooauthenticate [Azure 일괄 처리.NET](https://www.nuget.org/packages/Azure.Batch/) 패키지 및 hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-230">tooauthenticate with integrated authentication from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="e63c4-231">Hello 다음이 포함 `using` 사용자 코드에서 문:</span><span class="sxs-lookup"><span data-stu-id="e63c4-231">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="e63c4-232">참조 hello hello를 비롯 하 여 코드에서 Azure AD 끝점 id입니다. 테 넌 트</span><span class="sxs-lookup"><span data-stu-id="e63c4-232">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="e63c4-233">tooretrieve hello 테 넌 트 ID에 설명 된 hello 단계에 따라 [hello 테 넌 트 ID를 Azure Active Directory에 대 한 가져오기](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="e63c4-233">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="e63c4-234">참조 hello 일괄 처리 서비스 리소스 끝점:</span><span class="sxs-lookup"><span data-stu-id="e63c4-234">Reference hello Batch service resource endpoint:</span></span>

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="e63c4-235">배치 계정 참조:</span><span class="sxs-lookup"><span data-stu-id="e63c4-235">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="e63c4-236">응용 프로그램에 대 한 hello 응용 프로그램 ID (클라이언트 ID)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-236">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="e63c4-237">hello 응용 프로그램 ID는 hello Azure 포털에서에서 응용 프로그램 등록에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-237">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="e63c4-238">또한 hello 리디렉션 hello 등록 프로세스 중에 지정 된 URI를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-238">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="e63c4-239">코드에서 지정 된 URI는 hello 리디렉션 hello 리디렉션 URI hello 응용 프로그램 등록 시 입력 한 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-239">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application:</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="e63c4-240">Azure AD에서 콜백 메서드 tooacquire hello 인증 토큰을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-240">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="e63c4-241">hello **GetAuthenticationTokenAsync** 여기에 표시 된 콜백 메서드는 ADAL tooauthenticate hello 응용 프로그램과 상호 작용 하는 사용자를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-241">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL tooauthenticate a user who is interacting with hello application.</span></span> <span data-ttu-id="e63c4-242">hello **AcquireTokenAsync** 메서드 ADAL에서 표시 되는 메시지는 사용자 자격 증명에 대 한 hello 및 hello 응용 프로그램을 한 번 계속 hello 사용자 제공 제공 (없는 경우 자격 증명 캐시 된 이미):</span><span class="sxs-lookup"><span data-stu-id="e63c4-242">hello **AcquireTokenAsync** method provided by ADAL prompts hello user for their credentials, and hello application proceeds once hello user provides them (unless it has already cached credentials):</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire hello authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

<span data-ttu-id="e63c4-243">생성 된 **BatchTokenCredentials** hello 대리자를 매개 변수로 사용 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-243">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="e63c4-244">이러한 자격 증명 tooopen를 사용 하 여 한 **BatchClient** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-244">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="e63c4-245">이 사용할 수 **BatchClient** hello 일괄 처리 서비스에 대 한 후속 작업에 대 한 개체:</span><span class="sxs-lookup"><span data-stu-id="e63c4-245">You can use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

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

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a><span data-ttu-id="e63c4-246">코드 예제: Batch .NET에서 Azure AD 서비스 주체 사용</span><span class="sxs-lookup"><span data-stu-id="e63c4-246">Code example: Using an Azure AD service principal with Batch .NET</span></span>

<span data-ttu-id="e63c4-247">일괄 처리.NET, 참조 hello에서에서 서비스 사용자와 tooauthenticate [Azure 일괄 처리.NET](https://www.nuget.org/packages/Azure.Batch/) 패키지 및 hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-247">tooauthenticate with a service principal from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="e63c4-248">Hello 다음이 포함 `using` 사용자 코드에서 문:</span><span class="sxs-lookup"><span data-stu-id="e63c4-248">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="e63c4-249">참조 hello hello를 비롯 하 여 코드에서 Azure AD 끝점 id입니다. 테 넌 트</span><span class="sxs-lookup"><span data-stu-id="e63c4-249">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="e63c4-250">서비스 주체를 사용하는 경우 테넌트별 끝점을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-250">When using a service principal, you must provide a tenant-specific endpoint.</span></span> <span data-ttu-id="e63c4-251">tooretrieve hello 테 넌 트 ID에 설명 된 hello 단계에 따라 [hello 테 넌 트 ID를 Azure Active Directory에 대 한 가져오기](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="e63c4-251">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="e63c4-252">참조 hello 일괄 처리 서비스 리소스 끝점:</span><span class="sxs-lookup"><span data-stu-id="e63c4-252">Reference hello Batch service resource endpoint:</span></span>  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="e63c4-253">배치 계정 참조:</span><span class="sxs-lookup"><span data-stu-id="e63c4-253">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="e63c4-254">응용 프로그램에 대 한 hello 응용 프로그램 ID (클라이언트 ID)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-254">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="e63c4-255">hello 응용 프로그램 ID는 hello Azure 포털에서에서 응용 프로그램 등록에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-255">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="e63c4-256">Hello Azure 포털에서에서 복사한 hello 비밀 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-256">Specify hello secret key that you copied from hello Azure portal:</span></span>

```csharp
private const string ClientKey = "<secret-key>";
```

<span data-ttu-id="e63c4-257">Azure AD에서 콜백 메서드 tooacquire hello 인증 토큰을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-257">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="e63c4-258">hello **GetAuthenticationTokenAsync** 여기 무인된 인증에 대 한 ADAL 호출에 표시 된 콜백 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-258">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL for unattended authentication:</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

<span data-ttu-id="e63c4-259">생성 된 **BatchTokenCredentials** hello 대리자를 매개 변수로 사용 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-259">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="e63c4-260">이러한 자격 증명 tooopen를 사용 하 여 한 **BatchClient** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-260">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="e63c4-261">그런 다음이 사용할 수 **BatchClient** hello 일괄 처리 서비스에 대 한 후속 작업에 대 한 개체:</span><span class="sxs-lookup"><span data-stu-id="e63c4-261">You can then use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e63c4-262">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e63c4-262">Next steps</span></span>

<span data-ttu-id="e63c4-263">Azure AD에 대해 자세히 toolearn 참조 hello [Azure Active Directory 설명서](https://docs.microsoft.com/azure/active-directory/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-263">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="e63c4-264">ADAL toouse hello에서 사용할 수 있는 방법을 보여 주는 상세한 예제 [Azure 코드 예제](https://azure.microsoft.com/resources/samples/?service=active-directory) 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-264">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="e63c4-265">서비스 사용자에 대해 자세히 toolearn 참조 [응용 프로그램 및 Azure Active Directory에서 서비스 보안 주체 개체](../active-directory/develop/active-directory-application-objects.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-265">toolearn more about service principals, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span> <span data-ttu-id="e63c4-266">서비스 보안 주체를 사용 하 여 toocreate hello Azure 포털에서 참조 [포털 toocreate Active Directory 응용 프로그램 및 리소스에 액세스할 수 있는 서비스 보안 주체를 사용 하 여](../resource-group-create-service-principal-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-266">toocreate a service principal using hello Azure portal, see [Use portal toocreate Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="e63c4-267">또한 PowerShell 또는 Azure CLI를 사용하여 서비스 주체를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-267">You can also create a service principal with PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="e63c4-268">Azure AD를 사용 하 여 tooauthenticate 일괄 처리 관리 응용 프로그램 참조 [Active Directory를 사용 하 여 일괄 처리 관리 인증 솔루션](batch-aad-auth-management.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e63c4-268">tooauthenticate Batch Management applications using Azure AD, see [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span> 

[aad_about]: ../active-directory/active-directory-whatis.md "Azure Active Directory란?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD의 인증 시나리오"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Azure Active Directory와 응용 프로그램 통합"
[azure_portal]: http://portal.azure.com
