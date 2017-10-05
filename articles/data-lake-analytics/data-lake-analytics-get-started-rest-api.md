---
title: "REST API를 사용하여 Data Lake Analytics 시작 | Microsoft Docs"
description: "WebHDFS REST API를 사용하여 Data Lake Analytics에 대한 작업 수행"
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
ms.openlocfilehash: 332d7af2539eea8890745005104ac5b0921c2b7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a><span data-ttu-id="45a0a-103">REST API을 사용하여 Azure Data Lake Analytics 시작</span><span class="sxs-lookup"><span data-stu-id="45a0a-103">Get started with Azure Data Lake Analytics using REST APIs</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="45a0a-104">WebHDFS REST API 및 Data Lake Analytics REST API를 사용하여 Data Lake Analytics 계정, 작업 및 카탈로그를 관리하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-104">Learn how to use WebHDFS REST APIs and Data Lake Analytics REST APIs to manage Data Lake Analytics accounts, jobs, and catalog.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="45a0a-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="45a0a-105">Prerequisites</span></span>
* <span data-ttu-id="45a0a-106">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="45a0a-106">**An Azure subscription**.</span></span> <span data-ttu-id="45a0a-107">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45a0a-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="45a0a-108">**Azure Active Directory 응용 프로그램을 만듭니다**.</span><span class="sxs-lookup"><span data-stu-id="45a0a-108">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="45a0a-109">Azure AD 응용 프로그램을 사용하여 Azure AD로 Data Lake Analytics 응용 프로그램을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-109">You use the Azure AD application to authenticate the Data Lake Analytics application with Azure AD.</span></span> <span data-ttu-id="45a0a-110">Azure AD로 인증하는 여러 접근 방법에는 **최종 사용자 인증** 또는 **서비스 간 인증**이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-110">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="45a0a-111">인증하는 방법에 대한 지침 및 자세한 내용은 [Azure Active Directory를 사용하여 Data Lake Analytics로 인증](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45a0a-111">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="45a0a-112">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="45a0a-112">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="45a0a-113">이 문서에서는 cURL을 사용하여 Data Lake Analytics 계정에 대해 REST API 호출을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-113">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Analytics account.</span></span>

## <a name="authenticate-with-azure-active-directory"></a><span data-ttu-id="45a0a-114">Azure Active Directory를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="45a0a-114">Authenticate with Azure Active Directory</span></span>
<span data-ttu-id="45a0a-115">Azure Active Directory로 인증하는 방법에는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-115">There are two methods for authenticating with Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="45a0a-116">최종 사용자 인증(대화형)</span><span class="sxs-lookup"><span data-stu-id="45a0a-116">End-user authentication (interactive)</span></span>
<span data-ttu-id="45a0a-117">이 방법을 사용하여 응용 프로그램은 로그인하라는 메시지를 표시하고 모든 작업은 사용자의 컨텍스트에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-117">Using this method, application prompts the user to log in and all the operations are performed in the context of the user.</span></span> 

<span data-ttu-id="45a0a-118">대화형 인증을 위해 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-118">Follow these steps for interactive authentication:</span></span>

1. <span data-ttu-id="45a0a-119">응용 프로그램을 통해 다음 URL로 사용자를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-119">Through your application, redirect the user to the following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="45a0a-120">\<REDIRECT-URI>는 URL에서 사용하도록 인코딩되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-120">\<REDIRECT-URI> needs to be encoded for use in a URL.</span></span> <span data-ttu-id="45a0a-121">따라서 https://localhost의 경우 `https%3A%2F%2Flocalhost`)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-121">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="45a0a-122">이 자습서에서는 위의 URL에 있는 자리 표시자 값을 바꿀 수 있으며 이를 웹 브라우저의 주소 표시줄에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-122">For the purpose of this tutorial, you can replace the placeholder values in the URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="45a0a-123">Azure 로그인을 사용하여 인증하도록 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-123">You will be redirected to authenticate using your Azure login.</span></span> <span data-ttu-id="45a0a-124">성공적으로 로그인되면 응답은 브라우저의 주소 표시줄에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-124">Once you succesfully log in, the response is displayed in the browser's address bar.</span></span> <span data-ttu-id="45a0a-125">응답은 다음 형식으로 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-125">The response will be in the following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="45a0a-126">응답에서 인증 코드를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-126">Capture the authorization code from the response.</span></span> <span data-ttu-id="45a0a-127">이 자습서에서는 웹 브라우저의 주소 표시줄에서 인증 코드를 복사하고 아래와 같이 토큰 끝점에 대한 게시 요청에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-127">For this tutorial, you can copy the authorization code from the address bar of the web browser and pass it in the POST request to the token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="45a0a-128">이 경우에 \<REDIRECT-URI>는 인코딩되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-128">In this case, the \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="45a0a-129">응답은 액세스 토큰(예: `"access_token": "<ACCESS_TOKEN>"`) 및 새로 고침 토큰(예: `"refresh_token": "<REFRESH_TOKEN>"`)을 포함하는 JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-129">The response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="45a0a-130">응용 프로그램은 Azure Data Lake 저장소에 액세스할 때 액세스 토큰을 사용하고 액세스 토큰이 만료되면 다른 액세스 토큰을 가져오는 새로 고침 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-130">Your application uses the access token when accessing Azure Data Lake Store and the refresh token to get another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="45a0a-131">액세스 토큰이 만료되면 아래와 같이 새로 고침 토큰을 사용하여 새 액세스 토큰을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-131">When the access token expires, you can request a new access token using the refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="45a0a-132">대화형 사용자 인증에 대한 자세한 내용은 [인증 코드 부여 흐름](https://msdn.microsoft.com/library/azure/dn645542.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45a0a-132">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="45a0a-133">서비스 간 인증(비대화형)</span><span class="sxs-lookup"><span data-stu-id="45a0a-133">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="45a0a-134">이 방법을 사용하여 응용 프로그램은 고유한 자격 증명을 제공하여 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-134">Using this method, application provides its own credentials to perform the operations.</span></span> <span data-ttu-id="45a0a-135">이를 위해 다음과 같은 POST 요청을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-135">For this, you must issue a POST request like the one shown below:</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="45a0a-136">이 요청의 출력에는 이후에 REST API 호출을 사용하여 전달할 권한 부여 토큰(아래 출력의 `access-token` 에서 지정)이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-136">The output of this request will include an authorization token (denoted by `access-token` in the output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="45a0a-137">이 인증 토큰은 이 문서의 뒷부분에서 필요하므로 텍스트 파일에 저장해 두세요.</span><span class="sxs-lookup"><span data-stu-id="45a0a-137">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="45a0a-138">이 문서에서는 **비대화형** 접근 방식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-138">This article uses the **non-interactive** approach.</span></span> <span data-ttu-id="45a0a-139">비대화형(서비스 간 호출)에 대한 자세한 내용은 [자격 증명을 사용하여 서비스 간 호출](https://msdn.microsoft.com/library/azure/dn645543.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45a0a-139">For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="45a0a-140">Data Lake 분석 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="45a0a-140">Create a Data Lake Analytics account</span></span>
<span data-ttu-id="45a0a-141">Data Lake Analytics 계정을 만들기 전에 Azure 리소스 그룹과 Data Lake Store 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-141">You must create an Azure Resource group, and a Data Lake Store account before you can create a Data Lake Analytics account.</span></span>  <span data-ttu-id="45a0a-142">[Data Lake Store 계정 만들기](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45a0a-142">See [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span></span>

<span data-ttu-id="45a0a-143">다음 Curl 명령에서는 계정을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-143">The following Curl command shows how to create an account:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

<span data-ttu-id="45a0a-144">\<`REDACTED`\>을 권한 부여 토큰으로, \<`AzureSubscriptionID`\>를 구독 ID로, \<`AzureResourceGroupName`\>을 기존 Azure 리소스 그룹 이름으로, \<`NewAzureDataLakeAnalyticsAccountName`\>을 새 Data Lake Analytics 계정 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-144">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`NewAzureDataLakeAnalyticsAccountName`\> with a new Data Lake Analytics Account name.</span></span> <span data-ttu-id="45a0a-145">이 명령에 대한 요청 페이로드는 위의 `-d` 매개 변수에 대해 제공된 **CreateDatalakeAnalyticsAccountRequest.json** 파일에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-145">The request payload for this command is contained in the **CreateDatalakeAnalyticsAccountRequest.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="45a0a-146">input.json 파일의 내용은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-146">The contents of the input.json file resemble the following:</span></span>

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


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a><span data-ttu-id="45a0a-147">구독에 Data Lake Analytics 계정 나열</span><span class="sxs-lookup"><span data-stu-id="45a0a-147">List Data Lake Analytics accounts in a subscription</span></span>
<span data-ttu-id="45a0a-148">다음 Curl 명령에서는 구독에서 계정을 나열하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-148">The following Curl command shows how to list accounts in a subscription:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

<span data-ttu-id="45a0a-149">\<`REDACTED`\>을 권한 부여 토큰으로 바꾸고 \<`AzureSubscriptionID`\>을 구독 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-149">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID.</span></span> <span data-ttu-id="45a0a-150">다음과 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-150">The output is similar to:</span></span>

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

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="45a0a-151">Data Lake Analytics 계정에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="45a0a-151">Get information about a Data Lake Analytics account</span></span>
<span data-ttu-id="45a0a-152">다음 Curl 명령에서는 계정 정보를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-152">The following Curl command shows how to get an account information:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

<span data-ttu-id="45a0a-153">\<`REDACTED`\>을 권한 부여 토큰으로, \<`AzureSubscriptionID`\>를 구독 ID로, \<`AzureResourceGroupName`\>을 기존 Azure 리소스 그룹 이름으로, \<`DataLakeAnalyticsAccountName`\>을 기존 Data Lake Analytics 계정 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-153">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="45a0a-154">다음과 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-154">The output is similar to:</span></span>

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

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a><span data-ttu-id="45a0a-155">Data Lake Analytics 계정의 Data Lake Stores 나열</span><span class="sxs-lookup"><span data-stu-id="45a0a-155">List Data Lake Stores of a Data Lake Analytics account</span></span>
<span data-ttu-id="45a0a-156">다음 Curl 명령에서는 계정의 Data Lake Stores를 나열하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-156">The following Curl command shows how to list Data Lake Stores of an account:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

<span data-ttu-id="45a0a-157">\<`REDACTED`\>을 권한 부여 토큰으로, \<`AzureSubscriptionID`\>를 구독 ID로, \<`AzureResourceGroupName`\>을 기존 Azure 리소스 그룹 이름으로, \<`DataLakeAnalyticsAccountName`\>을 기존 Data Lake Analytics 계정 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-157">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="45a0a-158">다음과 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-158">The output is similar to:</span></span>

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

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="45a0a-159">U-SQL 작업 제출</span><span class="sxs-lookup"><span data-stu-id="45a0a-159">Submit U-SQL jobs</span></span>
<span data-ttu-id="45a0a-160">다음 Curl 명령에서는 U-SQL 작업을 제출하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-160">The following Curl command shows how to submit a U-SQL job:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

<span data-ttu-id="45a0a-161">\<`REDACTED`\>을 권한 부여 토큰으로 바꾸고 \<`DataLakeAnalyticsAccountName`\>을 기존 Data Lake Analytics 계정 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-161">Replace \<`REDACTED`\> with the authorization token, \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="45a0a-162">이 명령에 대한 요청 페이로드는 위의 `-d` 매개 변수에 대해 제공된 **SubmitADLAJob.json** 파일에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-162">The request payload for this command is contained in the **SubmitADLAJob.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="45a0a-163">input.json 파일의 내용은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-163">The contents of the input.json file resemble the following:</span></span>

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
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    TO \"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

<span data-ttu-id="45a0a-164">다음과 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-164">The output is similar to:</span></span>

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


## <a name="list-u-sql-jobs"></a><span data-ttu-id="45a0a-165">U-SQL 작업 나열</span><span class="sxs-lookup"><span data-stu-id="45a0a-165">List U-SQL jobs</span></span>
<span data-ttu-id="45a0a-166">다음 Curl 명령에서는 U-SQL 작업을 나열하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-166">The following Curl command shows how to list U-SQL jobs:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

<span data-ttu-id="45a0a-167">\<`REDACTED`\>을 권한 부여 토큰으로 바꾸고 \<`DataLakeAnalyticsAccountName`\>을 기존 Data Lake Analytics 계정 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-167">Replace \<`REDACTED`\> with the authorization token, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> 

<span data-ttu-id="45a0a-168">다음과 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-168">The output is similar to:</span></span>

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


## <a name="get-catalog-items"></a><span data-ttu-id="45a0a-169">카탈로그 항목 가져오기</span><span class="sxs-lookup"><span data-stu-id="45a0a-169">Get catalog items</span></span>
<span data-ttu-id="45a0a-170">다음 Curl 명령에서는 카탈로그에서 데이터베이스를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-170">The following Curl command shows how to get the databases from the catalog:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

<span data-ttu-id="45a0a-171">다음과 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-171">The output is similar to:</span></span>

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a><span data-ttu-id="45a0a-172">참고 항목</span><span class="sxs-lookup"><span data-stu-id="45a0a-172">See also</span></span>
* <span data-ttu-id="45a0a-173">더 복잡한 쿼리를 보려면 [Azure Data Lake Analytics을 사용하여 웹 사이트 로그 분석](data-lake-analytics-analyze-weblogs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45a0a-173">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="45a0a-174">U-SQL 응용 프로그램 개발을 시작하려면 [Visual Studio용 Data Lake 도구를 사용하여 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45a0a-174">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="45a0a-175">U-SQL을 알아보려면 [Azure Data Lake Analytics U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45a0a-175">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="45a0a-176">관리 작업을 보려면 [Azure Portal을 사용하여 Azure Data Lake Analytics 관리](data-lake-analytics-manage-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45a0a-176">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="45a0a-177">Data Lake Analytics에 대한 개요를 보려면 [Azure Data Lake Analytics 개요](data-lake-analytics-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45a0a-177">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="45a0a-178">다른 도구를 사용하여 같은 자습서를 보려면 페이지 맨 위의 탭 선택기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="45a0a-178">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>

