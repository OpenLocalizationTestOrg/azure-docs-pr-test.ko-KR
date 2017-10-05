---
title: "최종 사용자 인증: Azure Active Directory를 사용하여 Data Lake Store로 | Microsoft Docs"
description: "Azure Active Directory를 사용하여 Data Lake Store로 최종 사용자 인증을 수행하는 방법을 알아봅니다."
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
ms.openlocfilehash: c20f5c39b00992d801909c8e5de292f3c2f12673
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="6595f-103">Azure Active Directory를 사용하여 Data Lake Store로 최종 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="6595f-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6595f-104">서비스 간 인증</span><span class="sxs-lookup"><span data-stu-id="6595f-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="6595f-105">최종 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="6595f-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="6595f-106">Azure Data Lake Store는 인증을 위해 Azure Active Directory를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="6595f-107">Azure Data Lake Store 또는 Azure Data Lake Analytics와 함께 작동하는 응용 프로그램을 제작하기 전에 먼저 Azure Active Directory(Azure AD)를 사용하여 응용 프로그램을 인증하려는 방법을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like to authenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="6595f-108">사용할 수 있는 두 가지 주요 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-108">The two main options available are:</span></span>

* <span data-ttu-id="6595f-109">최종 사용자 인증(이 문서)</span><span class="sxs-lookup"><span data-stu-id="6595f-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="6595f-110">서비스 간 인증</span><span class="sxs-lookup"><span data-stu-id="6595f-110">Service-to-service authentication</span></span>

<span data-ttu-id="6595f-111">이 두 옵션 모두 Azure Data Lake Store 또는 Azure Data Lake Analytics에 대해 만들어진 각 요청에 연결하는 OAuth 2.0 토큰과 함께 제공되는 응용 프로그램에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached to each request made to Azure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="6595f-112">이 문서는 최종 사용자 인증을 위한 **Azure AD 네이티브 응용 프로그램**을 만드는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="6595f-113">서비스 간 인증을 위해 Azure AD 응용 프로그램 구성을 수행하는 방법은 [Azure Active Directory를 사용하여 Data Lake Store로 서비스 간 인증](data-lake-store-authenticate-using-active-directory.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6595f-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6595f-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6595f-114">Prerequisites</span></span>
* <span data-ttu-id="6595f-115">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="6595f-115">An Azure subscription.</span></span> <span data-ttu-id="6595f-116">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6595f-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="6595f-117">구독 ID.</span><span class="sxs-lookup"><span data-stu-id="6595f-117">Your subscription ID.</span></span> <span data-ttu-id="6595f-118">Azure Portal에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-118">You can retrieve it from the Azure Portal.</span></span> <span data-ttu-id="6595f-119">예를 들어 Data Lake Store 계정 블레이드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-119">For example, it is available from the Data Lake Store account blade.</span></span>
  
    ![구독 ID 가져오기](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="6595f-121">Azure AD 도메인 이름.</span><span class="sxs-lookup"><span data-stu-id="6595f-121">Your Azure AD domain name.</span></span> <span data-ttu-id="6595f-122">Azure Portal의 오른쪽 위 모서리에 마우스를 가져가서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-122">You can retrieve it by hovering the mouse in the top-right corner of the Azure Portal.</span></span> <span data-ttu-id="6595f-123">아래 스크린샷에서 도메인 이름은 **contoso.onmicrosoft.com**이며 괄호 안의 GUID는 테넌트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-123">From the screenshot below, the domain name is **contoso.onmicrosoft.com**, and the GUID within brackets is the tenant ID.</span></span> 
  
    ![AAD 도메인 가져오기](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a><span data-ttu-id="6595f-125">최종 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="6595f-125">End-user authentication</span></span>
<span data-ttu-id="6595f-126">최종 사용자가 Azure AD를 통해 응용 프로그램에 로그인하기를 원하는 경우 권장되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-126">This is the recommended approach if you want an end-user to log in to your application via Azure AD.</span></span> <span data-ttu-id="6595f-127">응용 프로그램은 로그인한 최종 사용자와 동일한 수준의 액세스로 Azure 리소스에 액세스할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-127">Your application will be able to access Azure resources with the same level of access as the end-user that logged in.</span></span> <span data-ttu-id="6595f-128">최종 사용자는 응용 프로그램이 액세스를 유지할 수 있도록 주기적으로 자격 증명을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-128">Your end-user will need to provide their credentials periodically in order for your application to maintain access.</span></span>

<span data-ttu-id="6595f-129">최종 사용자의 로그인으로 인해 응용 프로그램에 액세스 토큰 및 새로 고침 토큰이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-129">The result of having the end-user log in is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="6595f-130">액세스 토큰은 Data Lake Store 또는 Data Lake Analytics에 대해 만들어진 각 요청에 연결하며 기본적으로 1시간 동안 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-130">The access token gets attached to each request made to Data Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="6595f-131">새로 고침 토큰은 새 액세스 토큰을 가져오는 데 사용할 수 있고 정기적으로 사용되는 경우 기본적으로 최대 2주 동안 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-131">The refresh token can be used to obtain a new access token, and it is valid for up to two weeks by default, if used regularly.</span></span> <span data-ttu-id="6595f-132">최종 사용자 로그인에 두 가지 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-132">You can use two different approaches for end-user log in.</span></span>

### <a name="using-the-oauth-20-pop-up"></a><span data-ttu-id="6595f-133">OAuth 2.0 팝업 사용</span><span class="sxs-lookup"><span data-stu-id="6595f-133">Using the OAuth 2.0 pop-up</span></span>
<span data-ttu-id="6595f-134">응용 프로그램은 최종 사용자가 자격 증명을 입력할 수 있는 OAuth 2.0 권한 부여 팝업을 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which the end-user can enter their credentials.</span></span> <span data-ttu-id="6595f-135">이 팝업은 필요한 경우 Azure AD 2단계 인증(2FA) 프로세스와도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-135">This pop-up also works with the Azure AD Two-factor Authentication (2FA) process, if required.</span></span> 

> [!NOTE]
> <span data-ttu-id="6595f-136">이 방법은 Python 또는 Java용 Azure ADAL(AD 인증 라이브러리)에서 아직 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-136">This method is not yet supported in the Azure AD Authentication Library (ADAL) for Python or Java.</span></span>
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="6595f-137">사용자 자격 증명에서 직접 전달</span><span class="sxs-lookup"><span data-stu-id="6595f-137">Directly passing in user credentials</span></span>
<span data-ttu-id="6595f-138">응용 프로그램은 Azure AD에 사용자 자격 증명을 직접 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-138">Your application can directly provide user credentials to Azure AD.</span></span> <span data-ttu-id="6595f-139">이 방법은 조직 ID 사용자 계정과만 작동합니다. @outlook.com 또는 @live.com으로 끝나는 계정을 포함한 개인/"live ID" 사용자 계정과 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com.</span></span> <span data-ttu-id="6595f-140">또한 이 방법은 Azure AD 2단계 인증(2FA)이 필요한 사용자 계정과 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-140">Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-to-use-this-approach"></a><span data-ttu-id="6595f-141">이 방법을 사용하려면 무엇이 필요한가요?</span><span class="sxs-lookup"><span data-stu-id="6595f-141">What do I need to use this approach?</span></span>
* <span data-ttu-id="6595f-142">Azure AD 도메인 이름.</span><span class="sxs-lookup"><span data-stu-id="6595f-142">Azure AD domain name.</span></span> <span data-ttu-id="6595f-143">이 이름은 이 문서의 필수 구성 요소에 이미 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-143">This is already listed in the prerequisite of this article.</span></span>
* <span data-ttu-id="6595f-144">Azure AD **네이티브 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="6595f-144">Azure AD **native application**</span></span>
* <span data-ttu-id="6595f-145">Azure AD 네이티브 응용 프로그램에 대한 응용 프로그램 ID</span><span class="sxs-lookup"><span data-stu-id="6595f-145">Application ID for the Azure AD native application</span></span>
* <span data-ttu-id="6595f-146">Azure AD 네이티브 응용 프로그램에 대한 리디렉션 URI</span><span class="sxs-lookup"><span data-stu-id="6595f-146">Redirect URI for the Azure AD native application</span></span>
* <span data-ttu-id="6595f-147">위임된 권한 설정</span><span class="sxs-lookup"><span data-stu-id="6595f-147">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-native-application"></a><span data-ttu-id="6595f-148">1단계: Active Directory 네이티브 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="6595f-148">Step 1: Create an Active Directory native application</span></span>

<span data-ttu-id="6595f-149">Azure Active Directory를 사용하여 Azure Data Lake Store로 최종 사용자 인증을 위한 Azure AD 네이티브 응용 프로그램을 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-149">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="6595f-150">지침에 대해서는 [Azure AD 응용 프로그램 만들기](../azure-resource-manager/resource-group-create-service-principal-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6595f-150">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="6595f-151">위의 링크에 있는 지침을 수행하는 동안 아래 스크린샷과 같이 응용 프로그램 유형으로 **네이티브**를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-151">While following the instructions at the above link, make sure you select **Native** for application type, as shown in the screenshot below.</span></span>

<span data-ttu-id="6595f-152">![웹앱 만들기](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "네이티브 앱 만들기")</span><span class="sxs-lookup"><span data-stu-id="6595f-152">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-application-id-and-redirect-uri"></a><span data-ttu-id="6595f-153">2단계: 응용 프로그램 ID 및 리디렉션 URI 가져오기</span><span class="sxs-lookup"><span data-stu-id="6595f-153">Step 2: Get application id and redirect URI</span></span>

<span data-ttu-id="6595f-154">Azure AD 네이티브 응용 프로그램의 응용 프로그램 ID(Azure 클래식 포털에서는 클라이언트 ID라고도 함)를 검색하려면 [응용 프로그램 ID 가져오기](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6595f-154">See [Get the application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) to retrieve the application id (also called the client ID in the Azure classic portal) of the Azure AD native application.</span></span>

<span data-ttu-id="6595f-155">리디렉션 URI를 검색하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-155">To retrieve the redirect URI, follow the steps below.</span></span>

1. <span data-ttu-id="6595f-156">Azure Portal에서 **Azure Active Directory**를 선택하고 **앱 등록**을 클릭한 다음 방금 만든 Azure AD 네이티브 응용 프로그램을 찾아서 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-156">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="6595f-157">응용 프로그램에 대한 **설정** 블레이드에서 **리디렉션 URI**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-157">From the **Settings** blade for the application, click **Redirect URIs**.</span></span>

    ![리디렉션 URI 가져오기](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="6595f-159">표시되는 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-159">Copy the value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="6595f-160">3단계: 사용 권한 설정</span><span class="sxs-lookup"><span data-stu-id="6595f-160">Step 3: Set permissions</span></span>

1. <span data-ttu-id="6595f-161">Azure Portal에서 **Azure Active Directory**를 선택하고 **앱 등록**을 클릭한 다음 방금 만든 Azure AD 네이티브 응용 프로그램을 찾아서 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-161">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="6595f-162">응용 프로그램에 대한 **설정** 블레이드에서 **필요한 사용 권한**을 클릭하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-162">From the **Settings** blade for the application, click **Required permissions**, and then click **Add**.</span></span>

    ![클라이언트 ID](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="6595f-164">**API 액세스 추가** 블레이드에서 **API 선택**을 클릭하고 **Azure Data Lake**를 클릭한 후 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-164">In the **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![클라이언트 ID](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="6595f-166">**API 액세스 추가** 블레이드에서 **사용 권한 선택**을 클릭한 후 **Data Lake Store에 대한 모든 권한**을 부여하기 위한 확인란을 선택하고 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-166">In the **Add API Access** blade, click **Select permissions**, select the check box to give **Full access to Data Lake Store**, and then click **Select**.</span></span>

    ![클라이언트 ID](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="6595f-168">**Done**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-168">Click **Done**.</span></span>

5. <span data-ttu-id="6595f-169">마지막 두 단계를 반복하여 **Microsoft Azure Service Management API**에 대한 권한도 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-169">Repeat the last two steps to grant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="6595f-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6595f-170">Next steps</span></span>
<span data-ttu-id="6595f-171">이 문서에서는 Azure AD 네이티브 응용 프로그램을 만들고 .NET SDK, Java SDK, REST API 등을 사용하여 만든 클라이언트 응용 프로그램에 필요한 정보를 수집했습니다. 이제 다음 문서를 읽고 Azure AD 웹 응용 프로그램을 사용하여 Data Lake Store로 인증한 다음 저장소에서 다른 작업을 수행하는 방법에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6595f-171">In this article you created an Azure AD native application and gathered the information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed to the following articles that talk about how to use the Azure AD web application to first authenticate with Data Lake Store and then perform other operations on the store.</span></span>

* [<span data-ttu-id="6595f-172">.NET SDK를 사용하여 Azure 데이터 레이크 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="6595f-172">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="6595f-173">Java SDK를 사용하여 Azure Data Lake Store 시작</span><span class="sxs-lookup"><span data-stu-id="6595f-173">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="6595f-174">REST API를 사용하여 Azure Data Lake 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="6595f-174">Get started with Azure Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)

