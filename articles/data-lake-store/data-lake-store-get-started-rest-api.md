---
title: "REST API를 사용하여 Data Lake Store 시작 | Microsoft Docs"
description: "WebHDFS REST API를 사용하여 Data Lake 저장소에 대한 작업 수행"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57ac6501-cb71-4f75-82c2-acc07c562889
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: dc2c8f58e0a2faf1b00f4903148328a5141a8637
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a><span data-ttu-id="2ce5e-103">REST API를 사용하여 Azure Data Lake 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="2ce5e-103">Get started with Azure Data Lake Store using REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2ce5e-104">포털</span><span class="sxs-lookup"><span data-stu-id="2ce5e-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="2ce5e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ce5e-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="2ce5e-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="2ce5e-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="2ce5e-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="2ce5e-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="2ce5e-108">REST API</span><span class="sxs-lookup"><span data-stu-id="2ce5e-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="2ce5e-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2ce5e-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="2ce5e-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="2ce5e-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="2ce5e-111">Python</span><span class="sxs-lookup"><span data-stu-id="2ce5e-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="2ce5e-112">이 문서에서는 WebHDFS REST API 및 Data Lake 저장소 REST API를 사용하여 Azure Data Lake 저장소에 대한 계정 관리 및 파일 시스템 작업을 수행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-112">In this article, you will learn how to use WebHDFS REST APIs and Data Lake Store REST APIs to perform account management as well as filesystem operations on Azure Data Lake Store.</span></span> <span data-ttu-id="2ce5e-113">Azure Data Lake 저장소는 계정 관리 작업을 위해 자체 REST API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-113">Azure Data Lake Store exposes its own REST APIs for account management operations.</span></span> <span data-ttu-id="2ce5e-114">그러나 Data Lake 저장소는 HDFS 및 Hadoop 에코시스템과 호환되기 때문에 파일 시스템 작업에 WebHDFS REST API를 사용하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-114">However, because Data Lake Store is compatible with HDFS and Hadoop ecosystem, it supports using WebHDFS REST APIs for filesystem operations.</span></span>

> [!NOTE]
> <span data-ttu-id="2ce5e-115">Data Lake 저장소의 REST API 지원에 대한 자세한 내용은 [Azure Data Lake 저장소 REST API 참조](https://msdn.microsoft.com/library/mt693424.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-115">For detailed information on the REST API support for Data Lake Store, see [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="2ce5e-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2ce5e-116">Prerequisites</span></span>
* <span data-ttu-id="2ce5e-117">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-117">**An Azure subscription**.</span></span> <span data-ttu-id="2ce5e-118">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2ce5e-119">**Azure Active Directory 응용 프로그램을 만듭니다**.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="2ce5e-120">Azure AD 응용 프로그램을 사용하여 Azure AD로 Data Lake Store 응용 프로그램을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-120">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="2ce5e-121">Azure AD로 인증하는 여러 접근 방법에는 **최종 사용자 인증** 또는 **서비스 간 인증**이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-121">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="2ce5e-122">지침 및 인증 방법에 대한 자세한 내용은 [최종 사용자 인증](data-lake-store-end-user-authenticate-using-active-directory.md) 또는 [서비스 간 인증](data-lake-store-authenticate-using-active-directory.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-122">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="2ce5e-123">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="2ce5e-123">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="2ce5e-124">이 문서에서는 cURL을 사용하여 Data Lake 저장소 계정에 대해 REST API 호출을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-124">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Store account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="2ce5e-125">Azure Active Directory를 사용하여 인증하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="2ce5e-125">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="2ce5e-126">Azure Active Directory를 사용한 인증에는 두 가지 접근 방식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-126">You can use two approaches to authenticate using Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="2ce5e-127">최종 사용자 인증(대화형)</span><span class="sxs-lookup"><span data-stu-id="2ce5e-127">End-user authentication (interactive)</span></span>
<span data-ttu-id="2ce5e-128">이 시나리오에서 응용 프로그램은 로그인하라는 메시지를 표시하고 모든 작업은 사용자의 컨텍스트에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-128">In this scenario, the application prompts the user to log in and all the operations are performed in the context of the user.</span></span> <span data-ttu-id="2ce5e-129">대화형 인증을 위한 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-129">Perform the following steps for interactive authentication.</span></span>

1. <span data-ttu-id="2ce5e-130">응용 프로그램을 통해 다음 URL로 사용자를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-130">Through your application, redirect the user to the following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="2ce5e-131">\<REDIRECT-URI>는 URL에서 사용하도록 인코딩되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-131">\<REDIRECT-URI> needs to be encoded for use in a URL.</span></span> <span data-ttu-id="2ce5e-132">따라서 https://localhost의 경우 `https%3A%2F%2Flocalhost`)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-132">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="2ce5e-133">이 자습서에서는 위의 URL에 있는 자리 표시자 값을 바꿀 수 있으며 이를 웹 브라우저의 주소 표시줄에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-133">For the purpose of this tutorial, you can replace the placeholder values in the URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="2ce5e-134">Azure 로그인을 사용하여 인증하도록 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-134">You will be redirected to authenticate using your Azure login.</span></span> <span data-ttu-id="2ce5e-135">성공적으로 로그인되면 응답은 브라우저의 주소 표시줄에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-135">Once you successfully log in, the response is displayed in the browser's address bar.</span></span> <span data-ttu-id="2ce5e-136">응답은 다음 형식으로 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-136">The response will be in the following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="2ce5e-137">응답에서 인증 코드를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-137">Capture the authorization code from the response.</span></span> <span data-ttu-id="2ce5e-138">이 자습서에서는 웹 브라우저의 주소 표시줄에서 인증 코드를 복사하고 아래와 같이 토큰 끝점에 대한 게시 요청에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-138">For this tutorial, you can copy the authorization code from the address bar of the web browser and pass it in the POST request to the token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="2ce5e-139">이 경우에 \<REDIRECT-URI>는 인코딩되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-139">In this case, the \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="2ce5e-140">응답은 액세스 토큰(예: `"access_token": "<ACCESS_TOKEN>"`) 및 새로 고침 토큰(예: `"refresh_token": "<REFRESH_TOKEN>"`)을 포함하는 JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-140">The response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="2ce5e-141">응용 프로그램은 Azure Data Lake 저장소에 액세스할 때 액세스 토큰을 사용하고 액세스 토큰이 만료되면 다른 액세스 토큰을 가져오는 새로 고침 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-141">Your application uses the access token when accessing Azure Data Lake Store and the refresh token to get another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="2ce5e-142">액세스 토큰이 만료되면 아래와 같이 새로 고침 토큰을 사용하여 새 액세스 토큰을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-142">When the access token expires, you can request a new access token using the refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="2ce5e-143">대화형 사용자 인증에 대한 자세한 내용은 [인증 코드 부여 흐름](https://msdn.microsoft.com/library/azure/dn645542.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-143">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="2ce5e-144">서비스 간 인증(비대화형)</span><span class="sxs-lookup"><span data-stu-id="2ce5e-144">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="2ce5e-145">이 시나리오에서 응용 프로그램은 고유한 자격 증명을 제공하여 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-145">In this scenario, the the application provides its own credentials to perform the operations.</span></span> <span data-ttu-id="2ce5e-146">이를 위해 다음과 같은 POST 요청을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-146">For this, you must issue a POST request like the one shown below.</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="2ce5e-147">이 요청의 출력에는 이후에 REST API 호출을 사용하여 전달할 권한 부여 토큰(아래 출력의 `access-token` 에서 지정)이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-147">The output of this request will include an authorization token (denoted by `access-token` in the output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="2ce5e-148">이 인증 토큰은 이 문서의 뒷부분에서 필요하므로 텍스트 파일에 저장해 두세요.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-148">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="2ce5e-149">이 문서에서는 **비대화형** 접근 방식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-149">This article uses the **non-interactive** approach.</span></span> <span data-ttu-id="2ce5e-150">비대화형(서비스 간 호출)에 대한 자세한 내용은 [자격 증명을 사용하여 서비스 간 호출](https://msdn.microsoft.com/library/azure/dn645543.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-150">For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="2ce5e-151">Data Lake 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="2ce5e-151">Create a Data Lake Store account</span></span>
<span data-ttu-id="2ce5e-152">이 작업은 [여기](https://msdn.microsoft.com/library/mt694078.aspx)에 정의된 REST API 호출을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-152">This operation is based on the REST API call defined [here](https://msdn.microsoft.com/library/mt694078.aspx).</span></span>

<span data-ttu-id="2ce5e-153">다음 cURL 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-153">Use the following cURL command.</span></span> <span data-ttu-id="2ce5e-154">**\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-154">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

<span data-ttu-id="2ce5e-155">위 명령에서 \<`REDACTED`\>을 이전에 검색한 권한 부여 토큰으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-155">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span> <span data-ttu-id="2ce5e-156">이 명령에 대한 요청 페이로드는 위의 `-d` 매개 변수에 대해 제공된 **input.json** 파일에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-156">The request payload for this command is contained in the **input.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="2ce5e-157">input.json 파일의 내용은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-157">The contents of the input.json file resemble the following:</span></span>

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="2ce5e-158">Data Lake 저장소 계정에서 폴더 만들기</span><span class="sxs-lookup"><span data-stu-id="2ce5e-158">Create folders in a Data Lake Store account</span></span>
<span data-ttu-id="2ce5e-159">이 작업은 [여기](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory)에 정의된 WebHDFS REST API 호출을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-159">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span></span>

<span data-ttu-id="2ce5e-160">다음 cURL 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-160">Use the following cURL command.</span></span> <span data-ttu-id="2ce5e-161">**\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-161">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

<span data-ttu-id="2ce5e-162">위 명령에서 \<`REDACTED`\>을 이전에 검색한 권한 부여 토큰으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-162">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span> <span data-ttu-id="2ce5e-163">이 명령은 Data Lake Store 계정의 루트 폴더에 **mytempdir** 이라는 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-163">This command creates a directory called **mytempdir** under the root folder of your Data Lake Store account.</span></span>

<span data-ttu-id="2ce5e-164">작업이 성공적으로 완료되면 다음과 유사한 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-164">You should see a response like this if the operation completes successfully:</span></span>

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a><span data-ttu-id="2ce5e-165">Data Lake 저장소 계정의 폴더 나열</span><span class="sxs-lookup"><span data-stu-id="2ce5e-165">List folders in a Data Lake Store account</span></span>
<span data-ttu-id="2ce5e-166">이 작업은 [여기](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory)에 정의된 WebHDFS REST API 호출을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-166">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span></span>

<span data-ttu-id="2ce5e-167">다음 cURL 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-167">Use the following cURL command.</span></span> <span data-ttu-id="2ce5e-168">**\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-168">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

<span data-ttu-id="2ce5e-169">위 명령에서 \<`REDACTED`\>을 이전에 검색한 권한 부여 토큰으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-169">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span>

<span data-ttu-id="2ce5e-170">작업이 성공적으로 완료되면 다음과 유사한 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-170">You should see a response like this if the operation completes successfully:</span></span>

    {
    "FileStatuses": {
        "FileStatus": [{
            "length": 0,
            "pathSuffix": "mytempdir",
            "type": "DIRECTORY",
            "blockSize": 268435456,
            "accessTime": 1458324719512,
            "modificationTime": 1458324719512,
            "replication": 0,
            "permission": "777",
            "owner": "NotSupportYet",
            "group": "NotSupportYet"
        }]
    }
    }

## <a name="upload-data-into-a-data-lake-store-account"></a><span data-ttu-id="2ce5e-171">Data Lake 저장소 계정에 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="2ce5e-171">Upload data into a Data Lake Store account</span></span>
<span data-ttu-id="2ce5e-172">이 작업은 [여기](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File)에 정의된 WebHDFS REST API 호출을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-172">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span></span>

<span data-ttu-id="2ce5e-173">다음 cURL 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-173">Use the following cURL command.</span></span> <span data-ttu-id="2ce5e-174">**\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-174">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

<span data-ttu-id="2ce5e-175">위의 구문에서 **-T** 매개 변수는 업로드하는 파일의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-175">In the above syntax **-T** parameter is the location of the file you are uploading.</span></span>

<span data-ttu-id="2ce5e-176">다음과 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-176">The output is similar to the following:</span></span>
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a><span data-ttu-id="2ce5e-177">Data Lake 저장소 계정에서 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="2ce5e-177">Read data from a Data Lake Store account</span></span>
<span data-ttu-id="2ce5e-178">이 작업은 [여기](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File)에 정의된 WebHDFS REST API 호출을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-178">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span></span>

<span data-ttu-id="2ce5e-179">Data Lake 저장소 계정에서 데이터를 읽는 작업은 2단계 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-179">Reading data from a Data Lake Store account is a two-step process.</span></span>

* <span data-ttu-id="2ce5e-180">먼저 끝점 `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`에 대해 GET 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-180">You first submit a GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span></span> <span data-ttu-id="2ce5e-181">다음 GET 요청을 제출할 위치가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-181">This will return a location to submit the next GET request to.</span></span>
* <span data-ttu-id="2ce5e-182">그러면 끝점 `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`에 대해 GET 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-182">You then submit the GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span></span> <span data-ttu-id="2ce5e-183">파일 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-183">This will display the contents of the file.</span></span>

<span data-ttu-id="2ce5e-184">그러나 첫 번째 단계와 두 번째 단계 간에 입력 매개 변수의 차이가 없으므로 `-L` 매개 변수를 사용하여 첫 번째 요청을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-184">However, because there is no difference in the input parameters between the first and the second step, you can use the `-L` parameter to submit the first request.</span></span> <span data-ttu-id="2ce5e-185">`-L` 옵션은 기본적으로 두 요청을 하나로 결합하며 cURL이 새 위치에서 요청을 다시 실행하도록 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-185">`-L` option essentially combines two requests into one and will make cURL redo the request on the new location.</span></span> <span data-ttu-id="2ce5e-186">마지막으로, 모든 요청 호출의 출력이 아래와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-186">Finally, the output from all the request calls is displayed, like shown below.</span></span> <span data-ttu-id="2ce5e-187">**\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-187">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

<span data-ttu-id="2ce5e-188">다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-188">You should see an output similar to the following:</span></span>

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="2ce5e-189">Data Lake 저장소 계정에서 파일 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="2ce5e-189">Rename a file in a Data Lake Store account</span></span>
<span data-ttu-id="2ce5e-190">이 작업은 [여기](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory)에 정의된 WebHDFS REST API 호출을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-190">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span></span>

<span data-ttu-id="2ce5e-191">파일의 이름을 바꾸려면 다음 cURL 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-191">Use the following cURL command to rename a file.</span></span> <span data-ttu-id="2ce5e-192">**\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-192">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

<span data-ttu-id="2ce5e-193">다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-193">You should see an output similar to the following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a><span data-ttu-id="2ce5e-194">Data Lake 저장소 계정에서 파일 삭제</span><span class="sxs-lookup"><span data-stu-id="2ce5e-194">Delete a file from a Data Lake Store account</span></span>
<span data-ttu-id="2ce5e-195">이 작업은 [여기](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory)에 정의된 WebHDFS REST API 호출을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-195">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span></span>

<span data-ttu-id="2ce5e-196">파일을 삭제하려면 다음 cURL 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-196">Use the following cURL command to delete a file.</span></span> <span data-ttu-id="2ce5e-197">**\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-197">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

<span data-ttu-id="2ce5e-198">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-198">You should see an output like the following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="2ce5e-199">Data Lake 저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="2ce5e-199">Delete a Data Lake Store account</span></span>
<span data-ttu-id="2ce5e-200">이 작업은 [여기](https://msdn.microsoft.com/library/mt694075.aspx)에 정의된 REST API 호출을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-200">This operation is based on the REST API call defined [here](https://msdn.microsoft.com/library/mt694075.aspx).</span></span>

<span data-ttu-id="2ce5e-201">Data Lake 저장소 계정을 삭제하려면 다음 cURL 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-201">Use the following cURL command to delete a Data Lake Store account.</span></span> <span data-ttu-id="2ce5e-202">**\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-202">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

<span data-ttu-id="2ce5e-203">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ce5e-203">You should see an output like the following:</span></span>

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a><span data-ttu-id="2ce5e-204">참고 항목</span><span class="sxs-lookup"><span data-stu-id="2ce5e-204">See also</span></span>
* [<span data-ttu-id="2ce5e-205">Azure Data Lake 저장소와 호환되는 오픈 소스 빅 데이터 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2ce5e-205">Open Source Big Data applications compatible with Azure Data Lake Store</span></span>](data-lake-store-compatible-oss-other-applications.md)

