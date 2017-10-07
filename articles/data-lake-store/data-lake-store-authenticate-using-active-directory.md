---
title: "서비스 간 인증: Azure Active Directory를 사용하여 Data Lake Store로 | Microsoft Docs"
description: "자세한 내용은 방법 tooachieve 서비스 간 인증에 Azure Active Directory를 사용 하 여 데이터 레이크 저장소"
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
ms.openlocfilehash: 2e56237a75f020067b3248a1e1cfaf3c8df1371c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-to-service-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="a9803-103">Azure Active Directory를 사용하여 Data Lake Store로 서비스 간 인증</span><span class="sxs-lookup"><span data-stu-id="a9803-103">Service-to-service authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a9803-104">서비스 간 인증</span><span class="sxs-lookup"><span data-stu-id="a9803-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="a9803-105">최종 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="a9803-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="a9803-106">Azure Data Lake Store는 인증을 위해 Azure Active Directory를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="a9803-107">Azure 데이터 레이크 저장소 또는 Azure 데이터 레이크 분석을 사용 하는 응용 프로그램을 제작 하기 전에 먼저 결정 해야 방법을 원하는 tooauthenticate 응용 프로그램을 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a9803-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like tooauthenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="a9803-108">hello 두 가지 주요 사용 가능한 옵션은:</span><span class="sxs-lookup"><span data-stu-id="a9803-108">hello two main options available are:</span></span>

* <span data-ttu-id="a9803-109">최종 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="a9803-109">End-user authentication</span></span> 
* <span data-ttu-id="a9803-110">서비스 간 인증(이 문서)</span><span class="sxs-lookup"><span data-stu-id="a9803-110">Service-to-service authentication (this article)</span></span> 

<span data-ttu-id="a9803-111">두이 옵션 모두 연결 된 tooeach 수행 된 요청 tooAzure 데이터 레이크 저장소 또는 Azure 데이터 레이크 분석을 가져오는 OAuth 2.0 토큰으로 제공 되 고 응용 프로그램에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached tooeach request made tooAzure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="a9803-112">이 문서는 **서비스 간 인증을 위한 Azure AD 웹 응용 프로그램을 만드는** 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-112">This article talks about how create an **Azure AD web application for service-to-service authentication**.</span></span> <span data-ttu-id="a9803-113">최종 사용자 인증을 위해 Azure AD 응용 프로그램 구성을 수행하는 방법은 [Azure Active Directory를 사용하여 Data Lake Store로 최종 사용자 인증](data-lake-store-end-user-authenticate-using-active-directory.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9803-113">For instructions on Azure AD application configuration for end-user authentication see [End-user authentication with Data Lake Store using Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9803-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a9803-114">Prerequisites</span></span>
* <span data-ttu-id="a9803-115">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="a9803-115">An Azure subscription.</span></span> <span data-ttu-id="a9803-116">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9803-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="step-1-create-an-active-directory-web-application"></a><span data-ttu-id="a9803-117">1단계: Active Directory 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a9803-117">Step 1: Create an Active Directory web application</span></span>

<span data-ttu-id="a9803-118">Azure Active Directory를 사용하여 Azure Data Lake Store로 서비스 간 인증을 위한 Azure AD 웹 응용 프로그램을 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-118">Create and configure an Azure AD web application for service-to-service authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="a9803-119">지침에 대해서는 [Azure AD 응용 프로그램 만들기](../azure-resource-manager/resource-group-create-service-principal-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9803-119">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="a9803-120">링크 위에 hello에 hello 지침을 따르면 하는 동안 선택 했는지 확인 **웹 응용 프로그램 / API** 아래 hello 스크린샷에 표시 된 대로 응용 프로그램 종류에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-120">While following hello instructions at hello above link, make sure you select **Web App / API** for application type, as shown in hello screenshot below.</span></span>

<span data-ttu-id="a9803-121">![웹앱 만들기](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "웹앱 만들기")</span><span class="sxs-lookup"><span data-stu-id="a9803-121">![Create web app](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "Create web app")</span></span>

## <a name="step-2-get-application-id-authentication-key-and-tenant-id"></a><span data-ttu-id="a9803-122">2단계: 응용 프로그램 ID, 인증 키 및 테넌트 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="a9803-122">Step 2: Get application id, authentication key, and tenant id</span></span>
<span data-ttu-id="a9803-123">프로그래밍 방식으로 로그인 할 때 응용 프로그램에 대 한 hello id가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-123">When programmatically logging in, you need hello id for your application.</span></span> <span data-ttu-id="a9803-124">Hello 응용 프로그램 자체 자격 증명으로 실행 되는 인증 키를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-124">If hello application runs under its own credentials, you will also need an authentication key.</span></span>

* <span data-ttu-id="a9803-125">어떻게 tooretrieve hello 응용 프로그램 ID 및 인증 키 (도 호출된 hello 클라이언트 비밀) 응용 프로그램에 대 한 지침을 참조 하십시오. [Get 응용 프로그램 ID 및 인증 키](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-125">For instructions on how tooretrieve hello application ID and authentication key (also called hello client secret) for your application, see [Get application ID and authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).</span></span>

* <span data-ttu-id="a9803-126">참조에 대 한 지침은 어떻게 tooretrieve hello 테 넌 트 ID, [테 넌 트 ID 가져오기](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-126">For instructions on how tooretrieve hello tenant ID, see [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>

## <a name="step-3-assign-hello-azure-ad-application-toohello-azure-data-lake-store-account-file-or-folder-only-for-service-to-service-authentication"></a><span data-ttu-id="a9803-127">3 단계: hello Azure AD 응용 프로그램 toohello Azure 데이터 레이크 저장소 계정 파일 또는 폴더 (서비스 간 인증)에 할당</span><span class="sxs-lookup"><span data-stu-id="a9803-127">Step 3: Assign hello Azure AD application toohello Azure Data Lake Store account file or folder (only for service-to-service authentication)</span></span>
1. <span data-ttu-id="a9803-128">새 toohello 로그온 [Azure 포털](https://portal.azure.com) hello Azure Data Lake 저장소 계정이 이전에 만든 Azure Active Directory 응용 프로그램 hello로 tooassociate 원하는 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-128">Sign on toohello new [Azure portal](https://portal.azure.com) and open hello Azure Data Lake Store account that you want tooassociate with hello Azure Active Directory application you created earlier.</span></span>
2. <span data-ttu-id="a9803-129">데이터 레이크 저장소 계정 블레이드에서 **데이터 탐색기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-129">In your Data Lake Store account blade, click **Data Explorer**.</span></span>
   
    <span data-ttu-id="a9803-130">![Data Lake Store 계정에 디렉터리 만들기](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "Data Lake Store 계정에 디렉터리 만들기")</span><span class="sxs-lookup"><span data-stu-id="a9803-130">![Create directories in Data Lake Store account](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "Create directories in Data Lake account")</span></span>
3. <span data-ttu-id="a9803-131">Hello에 **데이터 탐색기** 블레이드에서 hello 파일 또는 폴더를 tooprovide access toohello Azure AD 응용 프로그램을 클릭 한 다음 클릭 **액세스**합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-131">In hello **Data Explorer** blade, click hello file or folder for which you want tooprovide access toohello Azure AD application, and then click **Access**.</span></span> <span data-ttu-id="a9803-132">클릭 해야 tooconfigure access tooa 파일 **액세스** hello에서 **파일 미리 보기** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-132">tooconfigure access tooa file, you must click **Access** from hello **File Preview** blade.</span></span>
   
    <span data-ttu-id="a9803-133">![Data Lake 파일 시스템에 ACL 설정](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "Data Lake 파일 시스템에 ACL 설정")</span><span class="sxs-lookup"><span data-stu-id="a9803-133">![Set ACLs on Data Lake file system](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "Set ACLs on Data Lake file system")</span></span>
4. <span data-ttu-id="a9803-134">hello **액세스** 블레이드 hello 표준 액세스를 나열 하 고 사용자 지정 액세스 toohello 루트 이미 할당 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-134">hello **Access** blade lists hello standard access and custom access already assigned toohello root.</span></span> <span data-ttu-id="a9803-135">Hello 클릭 **추가** 아이콘 tooadd 사용자 지정 수준 Acl 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-135">Click hello **Add** icon tooadd custom-level ACLs.</span></span>
   
    <span data-ttu-id="a9803-136">![표준 및 사용자 지정 액세스 나열](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "표준 및 사용자 지정 액세스 나열")</span><span class="sxs-lookup"><span data-stu-id="a9803-136">![List standard and custom access](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "List standard and custom access")</span></span>
5. <span data-ttu-id="a9803-137">Hello 클릭 **추가** 아이콘 tooopen hello **추가 사용자 지정 액세스** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-137">Click hello **Add** icon tooopen hello **Add Custom Access** blade.</span></span> <span data-ttu-id="a9803-138">이 블레이드에 클릭 **사용자 또는 그룹 선택**, 한 다음 **사용자 또는 그룹 선택** 블레이드를 앞에서 만든 hello Azure Active Directory 응용 프로그램을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-138">In this blade, click **Select User or Group**, and then in **Select User or Group** blade, look for hello Azure Active Directory application you created earlier.</span></span> <span data-ttu-id="a9803-139">그룹 toosearch 많지 hello 그룹 이름에 상위 toofilter hello에 hello 텍스트 상자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-139">If you have a lot of groups toosearch from, use hello text box at hello top toofilter on hello group name.</span></span> <span data-ttu-id="a9803-140">Hello 그룹 tooadd 하 고을 클릭 한 다음 클릭 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-140">Click hello group you want tooadd and then click **Select**.</span></span>
   
    <span data-ttu-id="a9803-141">![그룹 추가](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "그룹 추가")</span><span class="sxs-lookup"><span data-stu-id="a9803-141">![Add a group](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "Add a group")</span></span>
6. <span data-ttu-id="a9803-142">클릭 **Select 권한만**hello 권한 선택한 tooassign hello 사용 권한을 기본값으로 ACL 제거할지 ACL, 또는 둘 다에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-142">Click **Select Permissions**, select hello permissions and whether you want tooassign hello permissions as a default ACL, access ACL, or both.</span></span> <span data-ttu-id="a9803-143">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-143">Click **OK**.</span></span>
   
    <span data-ttu-id="a9803-144">![사용 권한을 toogroup 할당](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "toogroup 사용 권한 할당")</span><span class="sxs-lookup"><span data-stu-id="a9803-144">![Assign permissions toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "Assign permissions toogroup")</span></span>
   
    <span data-ttu-id="a9803-145">Data Lake Store의 사용 권한 및 기본/액세스 ACL에 대한 자세한 내용은 [Data Lake Store에서 액세스 제어](data-lake-store-access-control.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9803-145">For more information about permissions in Data Lake Store, and Default/Access ACLs, see [Access Control in Data Lake Store](data-lake-store-access-control.md).</span></span>
7. <span data-ttu-id="a9803-146">Hello에 **추가 사용자 지정 액세스** 블레이드에서 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-146">In hello **Add Custom Access** blade, click **OK**.</span></span> <span data-ttu-id="a9803-147">hello 새로 추가 된 hello 연결 된 사용 권한 가진 그룹 이제 hello에 나열 됩니다 **액세스** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-147">hello newly added group, with hello associated permissions, will now be listed in hello **Access** blade.</span></span>
   
    <span data-ttu-id="a9803-148">![사용 권한을 toogroup 할당](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "toogroup 사용 권한 할당")</span><span class="sxs-lookup"><span data-stu-id="a9803-148">![Assign permissions toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "Assign permissions toogroup")</span></span>

## <a name="step-4-get-hello-oauth-20-token-endpoint-only-for-java-based-applications"></a><span data-ttu-id="a9803-149">4 단계: (Java 기반 응용 프로그램)에 hello OAuth 2.0 토큰 끝점 가져오기</span><span class="sxs-lookup"><span data-stu-id="a9803-149">Step 4: Get hello OAuth 2.0 token endpoint (only for Java-based applications)</span></span>

1. <span data-ttu-id="a9803-150">새 toohello 로그온 [Azure 포털](https://portal.azure.com) hello 왼쪽된 창에서 Active Directory를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-150">Sign on toohello new [Azure portal](https://portal.azure.com) and click Active Directory from hello left pane.</span></span>

2. <span data-ttu-id="a9803-151">Hello 왼쪽된 창에서 클릭 **앱 등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-151">From hello left pane, click **App registrations**.</span></span>

3. <span data-ttu-id="a9803-152">Hello 응용 프로그램 등록 블레이드의 hello 위에서 클릭 **끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-152">From hello top of hello App registrations blade, click **Endpoints**.</span></span>

    <span data-ttu-id="a9803-153">![OAuth 토큰 끝점](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "OAuth 토큰 끝점")</span><span class="sxs-lookup"><span data-stu-id="a9803-153">![OAuth token endpoint](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "OAuth token endpoint")</span></span>

4. <span data-ttu-id="a9803-154">끝점의 hello 목록에서 hello OAuth 2.0 토큰 끝점을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-154">From hello list of endpoints, copy hello OAuth 2.0 token endpoint.</span></span>

    <span data-ttu-id="a9803-155">![OAuth 토큰 끝점](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "OAuth 토큰 끝점")</span><span class="sxs-lookup"><span data-stu-id="a9803-155">![OAuth token endpoint](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "OAuth token endpoint")</span></span>   

## <a name="next-steps"></a><span data-ttu-id="a9803-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a9803-156">Next steps</span></span>
<span data-ttu-id="a9803-157">이 문서에서 Azure AD 웹 응용 프로그램을 만든 및.NET SDK, Java SDK 등을 사용 하 여 제작 하는 클라이언트 응용 프로그램에서 필요한 hello 정보를 수집 합니다. 이제 toohello 다음 toouse hello Azure AD 웹 응용 프로그램 toofirst 데이터 레이크 저장소와 인증 하는 방법에 대해 설명 하 고 다음 hello 저장소에서 다른 작업을 수행 하는 문서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-157">In this article you created an Azure AD web application and gathered hello information you need in your client applications that you author using .NET SDK, Java SDK, etc. You can now proceed toohello following articles that talk about how toouse hello Azure AD web application toofirst authenticate with Data Lake Store and then perform other operations on hello store.</span></span>

* [<span data-ttu-id="a9803-158">.NET SDK를 사용하여 Azure 데이터 레이크 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="a9803-158">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="a9803-159">Java SDK를 사용하여 Azure Data Lake Store 시작</span><span class="sxs-lookup"><span data-stu-id="a9803-159">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)

<span data-ttu-id="a9803-160">이 문서는 방법은 이미 설명 hello 기본 단계에 대 한 필요한 tooget를 사용자 및 응용 프로그램에 대 한 실행 중인 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-160">This article walked you through hello basic steps needed tooget a user principal up and running for your application.</span></span> <span data-ttu-id="a9803-161">Hello 문서 tooget에 대 한 자세한 내용은 다음 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9803-161">You can look at hello following articles tooget further information:</span></span>
* [<span data-ttu-id="a9803-162">PowerShell toocreate 서비스 사용자를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a9803-162">Use PowerShell toocreate service principal</span></span>](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="a9803-163">서비스 주체 인증에 인증서 인증 사용</span><span class="sxs-lookup"><span data-stu-id="a9803-163">Use certificate authentication for service principal authentication</span></span>](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal#create-service-principal-with-certificate)
* [<span data-ttu-id="a9803-164">다른 메서드 tooauthenticate tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="a9803-164">Other methods tooauthenticate tooAzure AD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-authentication-scenarios)


