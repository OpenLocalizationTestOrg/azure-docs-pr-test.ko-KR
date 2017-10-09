---
title: "최종 사용자 인증: Azure Active Directory를 사용하여 Data Lake Store로 | Microsoft Docs"
description: "자세한 내용은 방법 tooachieve 최종 사용자 인증에 Azure Active Directory를 사용 하 여 데이터 레이크 저장소"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: fd58f4f2d8fc915b8bc51d9e5b040d2cee34047e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="584ad-103">Azure Active Directory를 사용하여 Data Lake Store로 최종 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="584ad-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="584ad-104">서비스 간 인증</span><span class="sxs-lookup"><span data-stu-id="584ad-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="584ad-105">최종 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="584ad-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="584ad-106">Azure Data Lake Store는 인증을 위해 Azure Active Directory를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="584ad-107">Azure 데이터 레이크 저장소 또는 Azure 데이터 레이크 분석을 사용 하는 응용 프로그램을 제작 하기 전에 먼저 결정 해야 방법을 원하는 tooauthenticate 응용 프로그램을 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="584ad-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like tooauthenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="584ad-108">hello 두 가지 주요 사용 가능한 옵션은:</span><span class="sxs-lookup"><span data-stu-id="584ad-108">hello two main options available are:</span></span>

* <span data-ttu-id="584ad-109">최종 사용자 인증(이 문서)</span><span class="sxs-lookup"><span data-stu-id="584ad-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="584ad-110">서비스 간 인증</span><span class="sxs-lookup"><span data-stu-id="584ad-110">Service-to-service authentication</span></span>

<span data-ttu-id="584ad-111">두이 옵션 모두 연결 된 tooeach 수행 된 요청 tooAzure 데이터 레이크 저장소 또는 Azure 데이터 레이크 분석을 가져오는 OAuth 2.0 토큰으로 제공 되 고 응용 프로그램에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached tooeach request made tooAzure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="584ad-112">이 문서는 최종 사용자 인증을 위한 **Azure AD 네이티브 응용 프로그램**을 만드는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="584ad-113">서비스 간 인증을 위해 Azure AD 응용 프로그램 구성을 수행하는 방법은 [Azure Active Directory를 사용하여 Data Lake Store로 서비스 간 인증](data-lake-store-authenticate-using-active-directory.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="584ad-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="584ad-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="584ad-114">Prerequisites</span></span>
* <span data-ttu-id="584ad-115">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="584ad-115">An Azure subscription.</span></span> <span data-ttu-id="584ad-116">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="584ad-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="584ad-117">구독 ID.</span><span class="sxs-lookup"><span data-stu-id="584ad-117">Your subscription ID.</span></span> <span data-ttu-id="584ad-118">Hello Azure 포털에서에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-118">You can retrieve it from hello Azure Portal.</span></span> <span data-ttu-id="584ad-119">예를 들어 hello Data Lake 저장소 계정 블레이드에서 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-119">For example, it is available from hello Data Lake Store account blade.</span></span>
  
    ![구독 ID 가져오기](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="584ad-121">Azure AD 도메인 이름.</span><span class="sxs-lookup"><span data-stu-id="584ad-121">Your Azure AD domain name.</span></span> <span data-ttu-id="584ad-122">Hello Azure 포털의 hello 오른쪽 위 모서리에 hello 마우스 호버 하 여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-122">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure Portal.</span></span> <span data-ttu-id="584ad-123">아래 hello 스크린샷에서에서 hello 도메인 이름이 **contoso.onmicrosoft.com**, 괄호 안에 hello GUID는 hello 테 넌 트 id입니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-123">From hello screenshot below, hello domain name is **contoso.onmicrosoft.com**, and hello GUID within brackets is hello tenant ID.</span></span> 
  
    ![AAD 도메인 가져오기](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a><span data-ttu-id="584ad-125">최종 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="584ad-125">End-user authentication</span></span>
<span data-ttu-id="584ad-126">이 Azure AD 통해 tooyour 응용 프로그램에는 최종 사용자 toolog 하려는 경우 권장 접근법 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-126">This is hello recommended approach if you want an end-user toolog in tooyour application via Azure AD.</span></span> <span data-ttu-id="584ad-127">응용 프로그램이 받을 수 tooaccess hello 사용 하 여 Azure 리소스에 기록 하는 hello 최종 사용자와 동일한 수준의 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-127">Your application will be able tooaccess Azure resources with hello same level of access as hello end-user that logged in.</span></span> <span data-ttu-id="584ad-128">최종 사용자는 응용 프로그램 toomaintain 액세스에 대 한 순서에 따라 정기적으로 자격 증명 tooprovide 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-128">Your end-user will need tooprovide their credentials periodically in order for your application toomaintain access.</span></span>

<span data-ttu-id="584ad-129">hello에 로그인 하는 hello 최종 사용자의 만들어집니다 액세스 토큰 및 새로 고침 토큰을 응용 프로그램 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-129">hello result of having hello end-user log in is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="584ad-130">hello 액세스 토큰 tooData Lake 저장소 또는 데이터 레이크 분석을 수행 하는 연결 된 tooeach 요청 가져오고 기본적으로 1 시간 동안 올바른지 합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-130">hello access token gets attached tooeach request made tooData Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="584ad-131">hello 새로 고침 토큰에는 새 액세스 토큰을 되며 적합 기본적으로 tootwo 주를 정기적으로 사용 하는 경우 사용 되는 tooobtain 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-131">hello refresh token can be used tooobtain a new access token, and it is valid for up tootwo weeks by default, if used regularly.</span></span> <span data-ttu-id="584ad-132">최종 사용자 로그인에 두 가지 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-132">You can use two different approaches for end-user log in.</span></span>

### <a name="using-hello-oauth-20-pop-up"></a><span data-ttu-id="584ad-133">OAuth 2.0 hello 팝업을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="584ad-133">Using hello OAuth 2.0 pop-up</span></span>
<span data-ttu-id="584ad-134">응용 프로그램이 OAuth 2.0 권한 부여 팝업이 최종 사용자는 hello에 자격 증명을 입력할 수를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which hello end-user can enter their credentials.</span></span> <span data-ttu-id="584ad-135">필요한 경우이 팝업 hello (2FA) Azure AD 2 단계 인증 프로세스와도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-135">This pop-up also works with hello Azure AD Two-factor Authentication (2FA) process, if required.</span></span> 

> [!NOTE]
> <span data-ttu-id="584ad-136">이 메서드는 아직 지원 되지 hello Azure AD 인증 라이브러리 (ADAL)에 대 한 Python, Java.</span><span class="sxs-lookup"><span data-stu-id="584ad-136">This method is not yet supported in hello Azure AD Authentication Library (ADAL) for Python or Java.</span></span>
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="584ad-137">사용자 자격 증명에서 직접 전달</span><span class="sxs-lookup"><span data-stu-id="584ad-137">Directly passing in user credentials</span></span>
<span data-ttu-id="584ad-138">응용 프로그램에서 사용자 자격 증명 tooAzure AD 제공할 직접 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-138">Your application can directly provide user credentials tooAzure AD.</span></span> <span data-ttu-id="584ad-139">이 방법은 조직 ID 사용자 계정과만 작동합니다. @outlook.com 또는 @live.com으로 끝나는 계정을 포함한 개인/"live ID" 사용자 계정과 호환되지 않습니다. 또한 이 방법은 Azure AD 2단계 인증(2FA)이 필요한 사용자 계정과 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com. Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-toouse-this-approach"></a><span data-ttu-id="584ad-140">무엇을이 이렇게 toouse 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="584ad-140">What do I need toouse this approach?</span></span>
* <span data-ttu-id="584ad-141">Azure AD 도메인 이름.</span><span class="sxs-lookup"><span data-stu-id="584ad-141">Azure AD domain name.</span></span> <span data-ttu-id="584ad-142">이 테이블은이 문서의 hello 전제 조건에서 이미 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-142">This is already listed in hello prerequisite of this article.</span></span>
* <span data-ttu-id="584ad-143">Azure AD **네이티브 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="584ad-143">Azure AD **native application**</span></span>
* <span data-ttu-id="584ad-144">Azure AD hello 네이티브 응용 프로그램에 대 한 응용 프로그램 ID</span><span class="sxs-lookup"><span data-stu-id="584ad-144">Application ID for hello Azure AD native application</span></span>
* <span data-ttu-id="584ad-145">Hello Azure AD에 네이티브 응용 프로그램에 대 한 리디렉션 URI</span><span class="sxs-lookup"><span data-stu-id="584ad-145">Redirect URI for hello Azure AD native application</span></span>
* <span data-ttu-id="584ad-146">위임된 권한 설정</span><span class="sxs-lookup"><span data-stu-id="584ad-146">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-native-application"></a><span data-ttu-id="584ad-147">1단계: Active Directory 네이티브 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="584ad-147">Step 1: Create an Active Directory native application</span></span>

<span data-ttu-id="584ad-148">Azure Active Directory를 사용하여 Azure Data Lake Store로 최종 사용자 인증을 위한 Azure AD 네이티브 응용 프로그램을 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-148">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="584ad-149">지침에 대해서는 [Azure AD 응용 프로그램 만들기](../azure-resource-manager/resource-group-create-service-principal-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="584ad-149">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="584ad-150">링크 위에 hello에 hello 지침을 따르면 하는 동안 선택 했는지 확인 **네이티브** 아래 hello 스크린샷에 표시 된 대로 응용 프로그램 종류에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-150">While following hello instructions at hello above link, make sure you select **Native** for application type, as shown in hello screenshot below.</span></span>

<span data-ttu-id="584ad-151">![웹앱 만들기](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "네이티브 앱 만들기")</span><span class="sxs-lookup"><span data-stu-id="584ad-151">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-application-id-and-redirect-uri"></a><span data-ttu-id="584ad-152">2단계: 응용 프로그램 ID 및 리디렉션 URI 가져오기</span><span class="sxs-lookup"><span data-stu-id="584ad-152">Step 2: Get application id and redirect URI</span></span>

<span data-ttu-id="584ad-153">참조 [hello 응용 프로그램 ID 가져오기](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve hello 응용 프로그램 (클라이언트 ID hello hello Azure 클래식 포털에서에서) hello Azure AD 네이티브 응용 프로그램의 id입니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-153">See [Get hello application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve hello application id (also called hello client ID in hello Azure classic portal) of hello Azure AD native application.</span></span>

<span data-ttu-id="584ad-154">tooretrieve hello 리디렉션 URI, 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-154">tooretrieve hello redirect URI, follow hello steps below.</span></span>

1. <span data-ttu-id="584ad-155">Hello Azure 포털에서에서 선택 **Azure Active Directory**, 클릭 **앱 등록**와 다음을 찾고 방금 만든 hello Azure AD 네이티브 응용 프로그램을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-155">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="584ad-156">Hello에서 **설정** 블레이드 hello 응용 프로그램에 대 한 클릭 **리디렉션 Uri**합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-156">From hello **Settings** blade for hello application, click **Redirect URIs**.</span></span>

    ![리디렉션 URI 가져오기](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="584ad-158">표시 되는 hello 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-158">Copy hello value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="584ad-159">3단계: 사용 권한 설정</span><span class="sxs-lookup"><span data-stu-id="584ad-159">Step 3: Set permissions</span></span>

1. <span data-ttu-id="584ad-160">Hello Azure 포털에서에서 선택 **Azure Active Directory**, 클릭 **앱 등록**와 다음을 찾고 방금 만든 hello Azure AD 네이티브 응용 프로그램을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-160">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="584ad-161">Hello에서 **설정** 블레이드 hello 응용 프로그램에 대 한 클릭 **필요한 권한**, 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-161">From hello **Settings** blade for hello application, click **Required permissions**, and then click **Add**.</span></span>

    ![클라이언트 ID](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="584ad-163">Hello에 **API 액세스 추가** 블레이드에서 클릭 **API 선택**, 클릭 **Azure 데이터 레이크**, 클릭 하 고 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-163">In hello **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![클라이언트 ID](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="584ad-165">Hello에 **API 액세스 추가** 블레이드에서 클릭 **사용 권한을 선택**, 선택 확인란 toogive hello **전체 tooData 레이크 스토어에 액세스**, 클릭 하 고 **선택** .</span><span class="sxs-lookup"><span data-stu-id="584ad-165">In hello **Add API Access** blade, click **Select permissions**, select hello check box toogive **Full access tooData Lake Store**, and then click **Select**.</span></span>

    ![클라이언트 ID](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="584ad-167">**Done**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-167">Click **Done**.</span></span>

5. <span data-ttu-id="584ad-168">반복 hello 마지막 두 단계에 대 한 권한을 toogrant **Windows Azure 서비스 관리 API** 도 합니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-168">Repeat hello last two steps toogrant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="584ad-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="584ad-169">Next steps</span></span>
<span data-ttu-id="584ad-170">이 문서에서 Azure AD 네이티브 응용 프로그램을 만든 및.NET SDK, Java SDK, REST API 등을 사용 하 여 제작 하는 클라이언트 응용 프로그램에서 필요한 hello 정보를 수집 합니다. 이제 toohello 다음 toouse hello Azure AD 웹 응용 프로그램 toofirst 데이터 레이크 저장소와 인증 하는 방법에 대해 설명 하 고 다음 hello 저장소에서 다른 작업을 수행 하는 문서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="584ad-170">In this article you created an Azure AD native application and gathered hello information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed toohello following articles that talk about how toouse hello Azure AD web application toofirst authenticate with Data Lake Store and then perform other operations on hello store.</span></span>

* [<span data-ttu-id="584ad-171">.NET SDK를 사용하여 Azure 데이터 레이크 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="584ad-171">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="584ad-172">Java SDK를 사용하여 Azure Data Lake Store 시작</span><span class="sxs-lookup"><span data-stu-id="584ad-172">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="584ad-173">REST API를 사용하여 Azure Data Lake 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="584ad-173">Get started with Azure Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)

