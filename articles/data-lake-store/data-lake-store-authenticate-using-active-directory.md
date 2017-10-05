---
title: "서비스 간 인증: Azure Active Directory를 사용하여 Data Lake Store로 | Microsoft Docs"
description: "Azure Active Directory를 사용하여 Data Lake Store로 서비스 간 인증을 수행하는 방법을 알아봅니다."
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 820b7c5d-4863-4225-9bd1-df4d8f515537
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 27ec0a4f48115d44da98dd048868b044aedf173c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="service-to-service-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="599ed-103">Azure Active Directory를 사용하여 Data Lake Store로 서비스 간 인증</span><span class="sxs-lookup"><span data-stu-id="599ed-103">Service-to-service authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="599ed-104">서비스 간 인증</span><span class="sxs-lookup"><span data-stu-id="599ed-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="599ed-105">최종 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="599ed-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="599ed-106">Azure Data Lake Store는 인증을 위해 Azure Active Directory를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="599ed-107">Azure Data Lake Store 또는 Azure Data Lake Analytics와 함께 작동하는 응용 프로그램을 제작하기 전에 먼저 Azure Active Directory(Azure AD)를 사용하여 응용 프로그램을 인증하려는 방법을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like to authenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="599ed-108">사용할 수 있는 두 가지 주요 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-108">The two main options available are:</span></span>

* <span data-ttu-id="599ed-109">최종 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="599ed-109">End-user authentication</span></span> 
* <span data-ttu-id="599ed-110">서비스 간 인증(이 문서)</span><span class="sxs-lookup"><span data-stu-id="599ed-110">Service-to-service authentication (this article)</span></span> 

<span data-ttu-id="599ed-111">이 두 옵션 모두 Azure Data Lake Store 또는 Azure Data Lake Analytics에 대해 만들어진 각 요청에 연결하는 OAuth 2.0 토큰과 함께 제공되는 응용 프로그램에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached to each request made to Azure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="599ed-112">이 문서는 **서비스 간 인증을 위한 Azure AD 웹 응용 프로그램을 만드는** 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-112">This article talks about how create an **Azure AD web application for service-to-service authentication**.</span></span> <span data-ttu-id="599ed-113">최종 사용자 인증을 위해 Azure AD 응용 프로그램 구성을 수행하는 방법은 [Azure Active Directory를 사용하여 Data Lake Store로 최종 사용자 인증](data-lake-store-end-user-authenticate-using-active-directory.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="599ed-113">For instructions on Azure AD application configuration for end-user authentication see [End-user authentication with Data Lake Store using Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="599ed-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="599ed-114">Prerequisites</span></span>
* <span data-ttu-id="599ed-115">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="599ed-115">An Azure subscription.</span></span> <span data-ttu-id="599ed-116">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="599ed-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="step-1-create-an-active-directory-web-application"></a><span data-ttu-id="599ed-117">1단계: Active Directory 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="599ed-117">Step 1: Create an Active Directory web application</span></span>

<span data-ttu-id="599ed-118">Azure Active Directory를 사용하여 Azure Data Lake Store로 서비스 간 인증을 위한 Azure AD 웹 응용 프로그램을 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-118">Create and configure an Azure AD web application for service-to-service authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="599ed-119">지침에 대해서는 [Azure AD 응용 프로그램 만들기](../azure-resource-manager/resource-group-create-service-principal-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="599ed-119">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="599ed-120">위의 링크에 있는 지침을 수행하는 동안 아래 스크린샷과 같이 응용 프로그램 유형으로 **웹앱/API**를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-120">While following the instructions at the above link, make sure you select **Web App / API** for application type, as shown in the screenshot below.</span></span>

<span data-ttu-id="599ed-121">![웹앱 만들기](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "웹앱 만들기")</span><span class="sxs-lookup"><span data-stu-id="599ed-121">![Create web app](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "Create web app")</span></span>

## <a name="step-2-get-application-id-authentication-key-and-tenant-id"></a><span data-ttu-id="599ed-122">2단계: 응용 프로그램 ID, 인증 키 및 테넌트 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="599ed-122">Step 2: Get application id, authentication key, and tenant id</span></span>
<span data-ttu-id="599ed-123">프로그래밍 방식으로 로그인하는 경우 응용 프로그램에 대한 ID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-123">When programmatically logging in, you need the id for your application.</span></span> <span data-ttu-id="599ed-124">응용 프로그램이 자체 자격 증명에서 실행되는 경우 인증 키도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-124">If the application runs under its own credentials, you will also need an authentication key.</span></span>

* <span data-ttu-id="599ed-125">응용 프로그램에 대한 응용 프로그램 ID 및 인증 키(클라이언트 비밀이라고도 함)를 검색하는 방법에 대한 지침은 [응용 프로그램 ID 및 인증 키 가져오기](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="599ed-125">For instructions on how to retrieve the application ID and authentication key (also called the client secret) for your application, see [Get application ID and authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).</span></span>

* <span data-ttu-id="599ed-126">테넌트 ID를 검색하는 방법에 대한 지침은 [테넌트 ID 가져오기](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="599ed-126">For instructions on how to retrieve the tenant ID, see [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>

## <a name="step-3-assign-the-azure-ad-application-to-the-azure-data-lake-store-account-file-or-folder-only-for-service-to-service-authentication"></a><span data-ttu-id="599ed-127">3단계: Azure Data Lake Store 계정 파일 또는 폴더에 Azure AD 응용 프로그램 할당(서비스 간 인증에만 해당)</span><span class="sxs-lookup"><span data-stu-id="599ed-127">Step 3: Assign the Azure AD application to the Azure Data Lake Store account file or folder (only for service-to-service authentication)</span></span>
1. <span data-ttu-id="599ed-128">새 [Azure Portal](https://portal.azure.com)에 로그온하여 이전에 만든 Azure Active Directory 응용 프로그램에 연결할 Azure Data Lake Store 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-128">Sign on to the new [Azure portal](https://portal.azure.com) and open the Azure Data Lake Store account that you want to associate with the Azure Active Directory application you created earlier.</span></span>
2. <span data-ttu-id="599ed-129">데이터 레이크 저장소 계정 블레이드에서 **데이터 탐색기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-129">In your Data Lake Store account blade, click **Data Explorer**.</span></span>
   
    <span data-ttu-id="599ed-130">![Data Lake Store 계정에 디렉터리 만들기](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "Data Lake Store 계정에 디렉터리 만들기")</span><span class="sxs-lookup"><span data-stu-id="599ed-130">![Create directories in Data Lake Store account](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "Create directories in Data Lake account")</span></span>
3. <span data-ttu-id="599ed-131">**데이터 탐색기** 블레이드에서 Azure AD 응용 프로그램에 대한 액세스를 제공할 파일 또는 폴더를 클릭하고 **액세스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-131">In the **Data Explorer** blade, click the file or folder for which you want to provide access to the Azure AD application, and then click **Access**.</span></span> <span data-ttu-id="599ed-132">파일에 대한 액세스를 구성하려면 **파일 미리 보기** 블레이드에서 **액세스**를 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-132">To configure access to a file, you must click **Access** from the **File Preview** blade.</span></span>
   
    <span data-ttu-id="599ed-133">![Data Lake 파일 시스템에 ACL 설정](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "Data Lake 파일 시스템에 ACL 설정")</span><span class="sxs-lookup"><span data-stu-id="599ed-133">![Set ACLs on Data Lake file system](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "Set ACLs on Data Lake file system")</span></span>
4. <span data-ttu-id="599ed-134">**액세스** 블레이드는 루트에 이미 할당된 표준 액세스 및 사용자 지정 액세스를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-134">The **Access** blade lists the standard access and custom access already assigned to the root.</span></span> <span data-ttu-id="599ed-135">**추가** 아이콘을 클릭하여 사용자 지정 수준 ACL을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-135">Click the **Add** icon to add custom-level ACLs.</span></span>
   
    <span data-ttu-id="599ed-136">![표준 및 사용자 지정 액세스 나열](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "표준 및 사용자 지정 액세스 나열")</span><span class="sxs-lookup"><span data-stu-id="599ed-136">![List standard and custom access](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "List standard and custom access")</span></span>
5. <span data-ttu-id="599ed-137">**추가** 아이콘을 클릭하여 **사용자 지정 액세스 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-137">Click the **Add** icon to open the **Add Custom Access** blade.</span></span> <span data-ttu-id="599ed-138">이 블레이드에서 **사용자 또는 그룹 선택**을 클릭한 다음 **사용자 또는 그룹 선택** 블레이드에서 이전에 만든 Azure Active Directory 응용 프로그램을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-138">In this blade, click **Select User or Group**, and then in **Select User or Group** blade, look for the Azure Active Directory application you created earlier.</span></span> <span data-ttu-id="599ed-139">검색할 그룹이 많을 경우 위쪽의 텍스트 상자를 사용하여 그룹 이름을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-139">If you have a lot of groups to search from, use the text box at the top to filter on the group name.</span></span> <span data-ttu-id="599ed-140">추가하려는 그룹을 클릭한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-140">Click the group you want to add and then click **Select**.</span></span>
   
    <span data-ttu-id="599ed-141">![그룹 추가](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "그룹 추가")</span><span class="sxs-lookup"><span data-stu-id="599ed-141">![Add a group](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "Add a group")</span></span>
6. <span data-ttu-id="599ed-142">**사용 권한 선택**을 클릭하고 사용 권한 및 이러한 권한을 기본 ACL로 할당할지, 액세스 ALC로 할당할지 또는 둘 다로 할당할지 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-142">Click **Select Permissions**, select the permissions and whether you want to assign the permissions as a default ACL, access ACL, or both.</span></span> <span data-ttu-id="599ed-143">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-143">Click **OK**.</span></span>
   
    <span data-ttu-id="599ed-144">![그룹에 권한 할당](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "그룹에 권한 할당")</span><span class="sxs-lookup"><span data-stu-id="599ed-144">![Assign permissions to group](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "Assign permissions to group")</span></span>
   
    <span data-ttu-id="599ed-145">Data Lake Store의 사용 권한 및 기본/액세스 ACL에 대한 자세한 내용은 [Data Lake Store에서 액세스 제어](data-lake-store-access-control.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="599ed-145">For more information about permissions in Data Lake Store, and Default/Access ACLs, see [Access Control in Data Lake Store](data-lake-store-access-control.md).</span></span>
7. <span data-ttu-id="599ed-146">**사용자 지정 액세스 추가** 블레이드에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-146">In the **Add Custom Access** blade, click **OK**.</span></span> <span data-ttu-id="599ed-147">이제 연결된 권한으로 새롭게 추가된 그룹이 **액세스** 블레이드에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-147">The newly added group, with the associated permissions, will now be listed in the **Access** blade.</span></span>
   
    <span data-ttu-id="599ed-148">![그룹에 권한 할당](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "그룹에 권한 할당")</span><span class="sxs-lookup"><span data-stu-id="599ed-148">![Assign permissions to group](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "Assign permissions to group")</span></span>

## <a name="step-4-get-the-oauth-20-token-endpoint-only-for-java-based-applications"></a><span data-ttu-id="599ed-149">4단계: OAuth 2.0 토큰 끝점 가져오기(Java 기반 응용 프로그램만 해당)</span><span class="sxs-lookup"><span data-stu-id="599ed-149">Step 4: Get the OAuth 2.0 token endpoint (only for Java-based applications)</span></span>

1. <span data-ttu-id="599ed-150">새 [Azure Portal](https://portal.azure.com)에 로그온하고 왼쪽 창에서 Active Directory를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-150">Sign on to the new [Azure portal](https://portal.azure.com) and click Active Directory from the left pane.</span></span>

2. <span data-ttu-id="599ed-151">왼쪽 창에서 **앱 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-151">From the left pane, click **App registrations**.</span></span>

3. <span data-ttu-id="599ed-152">앱 등록 블레이드 맨 위에서 **끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-152">From the top of the App registrations blade, click **Endpoints**.</span></span>

    <span data-ttu-id="599ed-153">![OAuth 토큰 끝점](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "OAuth 토큰 끝점")</span><span class="sxs-lookup"><span data-stu-id="599ed-153">![OAuth token endpoint](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "OAuth token endpoint")</span></span>

4. <span data-ttu-id="599ed-154">끝점 목록에서 OAuth 2.0 토큰 끝점을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-154">From the list of endpoints, copy the OAuth 2.0 token endpoint.</span></span>

    <span data-ttu-id="599ed-155">![OAuth 토큰 끝점](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "OAuth 토큰 끝점")</span><span class="sxs-lookup"><span data-stu-id="599ed-155">![OAuth token endpoint](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "OAuth token endpoint")</span></span>   

## <a name="next-steps"></a><span data-ttu-id="599ed-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="599ed-156">Next steps</span></span>
<span data-ttu-id="599ed-157">이 문서에서는 Azure AD 웹 응용 프로그램을 만들고 .NET SDK, Java SDK 등을 사용하여 만든 클라이언트 응용 프로그램에 필요한 정보를 수집했습니다. 이제 다음 문서를 읽고 Azure AD 웹 응용 프로그램을 사용하여 Data Lake Store로 인증한 다음 저장소에서 다른 작업을 수행하는 방법에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-157">In this article you created an Azure AD web application and gathered the information you need in your client applications that you author using .NET SDK, Java SDK, etc. You can now proceed to the following articles that talk about how to use the Azure AD web application to first authenticate with Data Lake Store and then perform other operations on the store.</span></span>

* [<span data-ttu-id="599ed-158">.NET SDK를 사용하여 Azure 데이터 레이크 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="599ed-158">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="599ed-159">Java SDK를 사용하여 Azure Data Lake Store 시작</span><span class="sxs-lookup"><span data-stu-id="599ed-159">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)

<span data-ttu-id="599ed-160">이 문서에서는 응용 프로그램에 대해 사용자 주체를 작동하고 실행하는 데 필요한 기본 단계를 안내했습니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-160">This article walked you through the basic steps needed to get a user principal up and running for your application.</span></span> <span data-ttu-id="599ed-161">다음 문서에서 추가 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599ed-161">You can look at the following articles to get further information:</span></span>
* [<span data-ttu-id="599ed-162">PowerShell을 사용하여 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="599ed-162">Use PowerShell to create service principal</span></span>](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="599ed-163">서비스 주체 인증에 인증서 인증 사용</span><span class="sxs-lookup"><span data-stu-id="599ed-163">Use certificate authentication for service principal authentication</span></span>](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal#create-service-principal-with-certificate)
* [<span data-ttu-id="599ed-164">Azure AD에 인증하는 다른 방법</span><span class="sxs-lookup"><span data-stu-id="599ed-164">Other methods to authenticate to Azure AD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-authentication-scenarios)


