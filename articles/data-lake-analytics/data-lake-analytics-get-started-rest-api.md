---
title: "REST API를 사용 하 여 Data Lake 분석 aaaGet 시작 | Microsoft Docs"
description: "데이터 레이크 분석에서 tooperform 작업 WebHDFS REST Api를 사용 하 여"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 5e133d92-baaa-44c9-890c-ab2d85c91122
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: jgao
ms.openlocfilehash: a0b13d521821fd2d74716cc52485585feb7c51b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a><span data-ttu-id="89799-103">REST API을 사용하여 Azure Data Lake Analytics 시작</span><span class="sxs-lookup"><span data-stu-id="89799-103">Get started with Azure Data Lake Analytics using REST APIs</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="89799-104">방법 toouse WebHDFS REST Api 및 데이터 레이크 분석 REST Api toomanage Data Lake 분석 계정, 작업, 및 카탈로그에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="89799-104">Learn how toouse WebHDFS REST APIs and Data Lake Analytics REST APIs toomanage Data Lake Analytics accounts, jobs, and catalog.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="89799-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="89799-105">Prerequisites</span></span>
* <span data-ttu-id="89799-106">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="89799-106">**An Azure subscription**.</span></span> <span data-ttu-id="89799-107">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89799-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="89799-108">**Azure Active Directory 응용 프로그램을 만듭니다**.</span><span class="sxs-lookup"><span data-stu-id="89799-108">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="89799-109">Azure AD와 hello Azure AD 응용 프로그램 tooauthenticate hello Data Lake 분석 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-109">You use hello Azure AD application tooauthenticate hello Data Lake Analytics application with Azure AD.</span></span> <span data-ttu-id="89799-110">없는 Azure AD와 다양 한 접근 방법 tooauthenticate 않는 **최종 사용자 인증** 또는 **서비스 간 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-110">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="89799-111">지침 및 방법에 대 한 자세한 내용은 tooauthenticate, 참조 [Azure Active Directory를 사용 하 여 Data Lake 분석으로 인증](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-111">For instructions and more information on how tooauthenticate, see [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="89799-112">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="89799-112">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="89799-113">이 문서에서는 cURL toodemonstrate Data Lake 분석 계정에 대해 toomake REST API 호출 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="89799-113">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Analytics account.</span></span>

## <a name="authenticate-with-azure-active-directory"></a><span data-ttu-id="89799-114">Azure Active Directory를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="89799-114">Authenticate with Azure Active Directory</span></span>
<span data-ttu-id="89799-115">Azure Active Directory로 인증하는 방법에는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89799-115">There are two methods for authenticating with Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="89799-116">최종 사용자 인증(대화형)</span><span class="sxs-lookup"><span data-stu-id="89799-116">End-user authentication (interactive)</span></span>
<span data-ttu-id="89799-117">이 메서드를 사용 하 여 응용 프로그램에서 사용자 toolog hello에서 표시 및 hello 사용자의 hello 컨텍스트에서 모든 hello 작업이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89799-117">Using this method, application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> 

<span data-ttu-id="89799-118">대화형 인증을 위해 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-118">Follow these steps for interactive authentication:</span></span>

1. <span data-ttu-id="89799-119">응용 프로그램을 통해 hello 사용자 toohello url 리디렉션:</span><span class="sxs-lookup"><span data-stu-id="89799-119">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="89799-120">\<리디렉션 URI > toobe 인코딩된 URL에서 사용 하기 위해 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-120">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="89799-121">따라서 https://localhost의 경우 `https%3A%2F%2Flocalhost`)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-121">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="89799-122">이 자습서의 hello 용도로 위에 hello URL에서 자리 표시자 값 hello 바꾸고 웹 브라우저의 주소 표시줄에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="89799-122">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="89799-123">Azure 로그인을 사용 하 여 리디렉션된 tooauthenticate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89799-123">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="89799-124">하면 성공적으로 로그인 되 면 hello 응답이 hello 브라우저의 주소 표시줄에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89799-124">Once you succesfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="89799-125">hello 응답 형식에 따라 hello에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89799-125">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="89799-126">Hello 응답 hello 권한 부여 코드를 캡처하십시오.</span><span class="sxs-lookup"><span data-stu-id="89799-126">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="89799-127">이 자습서에서는 hello 인증 코드 hello 웹 브라우저의 주소 표시줄 hello에서에서 복사한 아래와 같이 hello POST 요청 toohello 토큰 끝점에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89799-127">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="89799-128">이 경우 hello \<리디렉션 URI > 인코딩할 수 없는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-128">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="89799-129">hello 응답은 액세스 토큰을 포함 하는 JSON 개체 (예: `"access_token": "<ACCESS_TOKEN>"`) 및 새로 고침 토큰 (예: `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="89799-129">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="89799-130">응용 프로그램 사용 hello 액세스 토큰 새로 고침 토큰 tooget hello Azure 데이터 레이크 저장소에 액세스할 때 다른 액세스 토큰 액세스 토큰이 만료 된 경우 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-130">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="89799-131">Hello 액세스 토큰이 만료 되 면 아래와 같이 hello 새로 고침 토큰을 사용 하 여 새 액세스 토큰을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89799-131">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="89799-132">대화형 사용자 인증에 대한 자세한 내용은 [인증 코드 부여 흐름](https://msdn.microsoft.com/library/azure/dn645542.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89799-132">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="89799-133">서비스 간 인증(비대화형)</span><span class="sxs-lookup"><span data-stu-id="89799-133">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="89799-134">이 메서드를 사용 하 여 응용 프로그램 자체 자격 증명 tooperform hello 연산을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-134">Using this method, application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="89799-135">이 경우 hello 아래와 같은 POST 요청을 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-135">For this, you must issue a POST request like hello one shown below:</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="89799-136">이 요청의 hello 출력 권한 부여 토큰에 포함 됩니다 (가리키는 `access-token` hello 출력 아래에)는 REST API 호출으로 전달 이후에 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-136">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="89799-137">이 인증 토큰은 이 문서의 뒷부분에서 필요하므로 텍스트 파일에 저장해 두세요.</span><span class="sxs-lookup"><span data-stu-id="89799-137">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="89799-138">이 문서에서는 hello **비 대화형** 접근 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="89799-138">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="89799-139">비 대화형 (서비스 간 호출)에 대 한 자세한 내용은 참조 하십시오. [서비스 자격 증명을 사용 하 여 tooservice 호출](https://msdn.microsoft.com/library/azure/dn645543.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-139">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="89799-140">Data Lake 분석 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="89799-140">Create a Data Lake Analytics account</span></span>
<span data-ttu-id="89799-141">Data Lake Analytics 계정을 만들기 전에 Azure 리소스 그룹과 Data Lake Store 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-141">You must create an Azure Resource group, and a Data Lake Store account before you can create a Data Lake Analytics account.</span></span>  <span data-ttu-id="89799-142">[Data Lake Store 계정 만들기](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89799-142">See [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span></span>

<span data-ttu-id="89799-143">Curl 명령 표시 방법을 따라 hello toocreate 계정:</span><span class="sxs-lookup"><span data-stu-id="89799-143">hello following Curl command shows how toocreate an account:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

<span data-ttu-id="89799-144">대체 \< `REDACTED` \> hello 권한 부여 토큰으로 \< `AzureSubscriptionID` \> 를 구독 ID로, \< `AzureResourceGroupName` \> 는 기존 Azure 리소스와 함께 그룹 이름 및 \< `NewAzureDataLakeAnalyticsAccountName` \> 새 데이터 레이크 분석 계정 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-144">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`NewAzureDataLakeAnalyticsAccountName`\> with a new Data Lake Analytics Account name.</span></span> <span data-ttu-id="89799-145">이 명령에 대 한 hello 요청 페이로드 hello에 포함 된 **CreateDatalakeAnalyticsAccountRequest.json** hello에 대 한 제공 되는 파일 `-d` 위의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="89799-145">hello request payload for this command is contained in hello **CreateDatalakeAnalyticsAccountRequest.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="89799-146">hello input.json 파일의 내용을 hello hello 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-146">hello contents of hello input.json file resemble hello following:</span></span>

    {  
        "location": "East US 2",  
        "name": "myadla1004",  
        "tags": {},  
        "properties": {  
            "defaultDataLakeStoreAccount": "my1004store",  
            "dataLakeStoreAccounts": [  
                {  
                    "name": "my1004store"  
                }     
            ]
        }  
    }  


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a><span data-ttu-id="89799-147">구독에 Data Lake Analytics 계정 나열</span><span class="sxs-lookup"><span data-stu-id="89799-147">List Data Lake Analytics accounts in a subscription</span></span>
<span data-ttu-id="89799-148">다음 Curl 명령을 hello toolist 구독에서 계정을 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="89799-148">hello following Curl command shows how toolist accounts in a subscription:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

<span data-ttu-id="89799-149">대체 \< `REDACTED` \> hello 권한 부여 토큰으로 \< `AzureSubscriptionID` \> 구독 ID로</span><span class="sxs-lookup"><span data-stu-id="89799-149">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID.</span></span> <span data-ttu-id="89799-150">hello 출력은 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-150">hello output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla0831.azuredatalakeanalytics.net",
                "accountId": "21e74660-0941-4880-ae72-b143c2615ea9",
                "creationTime": "2016-09-01T12:49:12.7451428Z",
                "lastModifiedTime": "2016-09-01T12:49:12.7451428Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla0831rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla0831",
            "name": "myadla0831",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            },
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla1004.azuredatalakeanalytics.net",
                "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
                "creationTime": "2016-10-04T20:46:42.287147Z",
                "lastModifiedTime": "2016-10-04T20:46:42.287147Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
            "name": "myadla1004",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            }
        ]
    }

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="89799-151">Data Lake Analytics 계정에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="89799-151">Get information about a Data Lake Analytics account</span></span>
<span data-ttu-id="89799-152">Curl 명령 표시 방법을 따라 hello tooget 계정 정보:</span><span class="sxs-lookup"><span data-stu-id="89799-152">hello following Curl command shows how tooget an account information:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

<span data-ttu-id="89799-153">대체 \< `REDACTED` \> hello 권한 부여 토큰으로 \< `AzureSubscriptionID` \> 를 구독 ID로, \< `AzureResourceGroupName` \> 는 기존 Azure 리소스와 함께 그룹 이름 및 \< `DataLakeAnalyticsAccountName` \> 기존 데이터 레이크 분석 계정의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-153">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="89799-154">hello 출력은 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-154">hello output is similar to:</span></span>

    {
        "properties": {
            "defaultDataLakeStoreAccount": "my1004store",
            "dataLakeStoreAccounts": [
            {
                "properties": {
                "suffix": "azuredatalakestore.net"
                },
                "name": "my1004store"
            }
            ],
            "provisioningState": "Creating",
            "state": null,
            "endpoint": null,
            "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
            "creationTime": null,
            "lastModifiedTime": null
        },
        "location": "East US 2",
        "tags": {},
        "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
        "name": "myadla1004",
        "type": "Microsoft.DataLakeAnalytics/accounts"
    }

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a><span data-ttu-id="89799-155">Data Lake Analytics 계정의 Data Lake Stores 나열</span><span class="sxs-lookup"><span data-stu-id="89799-155">List Data Lake Stores of a Data Lake Analytics account</span></span>
<span data-ttu-id="89799-156">다음 Curl 명령을 hello toolist 데이터 레이크 계정 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="89799-156">hello following Curl command shows how toolist Data Lake Stores of an account:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

<span data-ttu-id="89799-157">대체 \< `REDACTED` \> hello 권한 부여 토큰으로 \< `AzureSubscriptionID` \> 를 구독 ID로, \< `AzureResourceGroupName` \> 는 기존 Azure 리소스와 함께 그룹 이름 및 \< `DataLakeAnalyticsAccountName` \> 기존 데이터 레이크 분석 계정의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-157">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="89799-158">hello 출력은 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-158">hello output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "suffix": "azuredatalakestore.net"
            },
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004/dataLakeStoreAccounts/my1004store",
            "name": "my1004store",
            "type": "Microsoft.DataLakeAnalytics/accounts/dataLakeStoreAccounts"
            }
        ]
    }

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="89799-159">U-SQL 작업 제출</span><span class="sxs-lookup"><span data-stu-id="89799-159">Submit U-SQL jobs</span></span>
<span data-ttu-id="89799-160">Curl 명령 표시 방법을 따라 hello toosubmit는 U-SQL 작업:</span><span class="sxs-lookup"><span data-stu-id="89799-160">hello following Curl command shows how toosubmit a U-SQL job:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

<span data-ttu-id="89799-161">대체 \< `REDACTED` \> hello 권한 부여 토큰으로 \< `DataLakeAnalyticsAccountName` \> 기존 데이터 레이크 분석 계정의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-161">Replace \<`REDACTED`\> with hello authorization token, \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="89799-162">이 명령에 대 한 hello 요청 페이로드 hello에 포함 된 **SubmitADLAJob.json** hello에 대 한 제공 되는 파일 `-d` 위의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="89799-162">hello request payload for this command is contained in hello **SubmitADLAJob.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="89799-163">hello input.json 파일의 내용을 hello hello 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-163">hello contents of hello input.json file resemble hello following:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "properties": {
            "type": "USql",
            "script": "@searchlog =\n    EXTRACT UserId          int,\n            Start           DateTime,\n            Region          string,\n            Query          
        string,\n            Duration        int?,\n            Urls            string,\n            ClickedUrls     string\n    FROM \"/Samples/Data/SearchLog.tsv\"\n    US
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    too\"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

<span data-ttu-id="89799-164">hello 출력은 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-164">hello output is similar to:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "myadl@SPI",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "2016-10-05T13:54:59.9871859+00:00",
        "state": "Compiling",
        "result": "Succeeded",
        "stateAuditRecords": [
            {
            "newState": "New",
            "timeStamp": "2016-10-05T13:54:59.9871859+00:00",
            "details": "userName:myadl@SPI;submitMachine:N/A"
            }
        ],
        "properties": {
            "owner": "myadl@SPI",
            "resources": [],
            "runtimeVersion": "default",
            "rootProcessNodeId": "00000000-0000-0000-0000-000000000000",
            "algebraFilePath": "adl://myadls0831.azuredatalakestore.net/system/jobservice/jobs/Usql/2016/10/05/13/54/8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a/algebra.xml",
            "compileMode": "Semantic",
            "errorSource": "Unknown",
            "totalCompilationTime": "PT0S",
            "totalPausedTime": "PT0S",
            "totalQueuedTime": "PT0S",
            "totalRunningTime": "PT0S",
            "type": "USql"
        }
    }


## <a name="list-u-sql-jobs"></a><span data-ttu-id="89799-165">U-SQL 작업 나열</span><span class="sxs-lookup"><span data-stu-id="89799-165">List U-SQL jobs</span></span>
<span data-ttu-id="89799-166">Curl 명령 표시 방법을 따라 hello toolist U-SQL 작업:</span><span class="sxs-lookup"><span data-stu-id="89799-166">hello following Curl command shows how toolist U-SQL jobs:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

<span data-ttu-id="89799-167">대체 \< `REDACTED` \> hello 권한 부여 토큰으로 및 \< `DataLakeAnalyticsAccountName` \> 기존 데이터 레이크 분석 계정의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-167">Replace \<`REDACTED`\> with hello authorization token, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> 

<span data-ttu-id="89799-168">hello 출력은 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-168">hello output is similar to:</span></span>

    {
    "value": [
        {
        "jobId": "65cf1691-9dbe-43cd-90ed-1cafbfb406fb",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someone@microsoft.com",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:46:53 GMT",
        "startTime": "Wed, 05 Oct 2016 13:47:33 GMT",
        "endTime": "Wed, 05 Oct 2016 13:48:07 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        },
        {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someoneadl@SPI",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:54:59 GMT",
        "startTime": "Wed, 05 Oct 2016 13:55:43 GMT",
        "endTime": "Wed, 05 Oct 2016 13:56:11 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        }
    ],
    "nextLink": null,
    "count": null
    }


## <a name="get-catalog-items"></a><span data-ttu-id="89799-169">카탈로그 항목 가져오기</span><span class="sxs-lookup"><span data-stu-id="89799-169">Get catalog items</span></span>
<span data-ttu-id="89799-170">다음 Curl 명령을 hello tooget hello 데이터베이스에서 카탈로그를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="89799-170">hello following Curl command shows how tooget hello databases from hello catalog:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

<span data-ttu-id="89799-171">hello 출력은 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-171">hello output is similar to:</span></span>

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a><span data-ttu-id="89799-172">참고 항목</span><span class="sxs-lookup"><span data-stu-id="89799-172">See also</span></span>
* <span data-ttu-id="89799-173">toosee 복잡 한 쿼리를 참조 [분석 웹 사이트 Azure 데이터 레이크 분석을 사용 하 여 로그](data-lake-analytics-analyze-weblogs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-173">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="89799-174">U-SQL 응용 프로그램 개발 시작 tooget 참조 [데이터 레이크 도구를 사용 하 여 Visual Studio에 대 한 개발 U-SQL 스크립트](data-lake-analytics-data-lake-tools-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-174">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="89799-175">toolearn U SQL 참조 [Azure 데이터 레이크 분석 U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-175">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="89799-176">관리 작업을 보려면 [Azure Portal을 사용하여 Azure Data Lake Analytics 관리](data-lake-analytics-manage-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89799-176">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="89799-177">데이터 레이크 분석의 개요는 tooget 참조 [Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-177">tooget an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="89799-178">toosee hello 같은 다른 도구를 사용 하 여 자습서 hello hello 페이지 위쪽에 hello 탭 선택기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="89799-178">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>

