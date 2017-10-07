---
title: "데이터 레이크 저장소 aaaUse hello REST API tooget 시작 | Microsoft Docs"
description: "데이터 레이크 저장소의 tooperform 작업 WebHDFS REST Api를 사용 하 여"
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
ms.openlocfilehash: 62fce8293dfee730a61f2a3d37fc138ce7c3afdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a><span data-ttu-id="ef262-103">REST API를 사용하여 Azure Data Lake 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="ef262-103">Get started with Azure Data Lake Store using REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef262-104">포털</span><span class="sxs-lookup"><span data-stu-id="ef262-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="ef262-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef262-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="ef262-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="ef262-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="ef262-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="ef262-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="ef262-108">REST API</span><span class="sxs-lookup"><span data-stu-id="ef262-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="ef262-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ef262-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="ef262-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="ef262-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="ef262-111">Python</span><span class="sxs-lookup"><span data-stu-id="ef262-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="ef262-112">이 문서에서는 toouse WebHDFS REST Api와 데이터 레이크 저장소 REST Api tooperform Azure 데이터 레이크 저장소의 파일 시스템 작업 뿐 아니라 관리 계정 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-112">In this article, you will learn how toouse WebHDFS REST APIs and Data Lake Store REST APIs tooperform account management as well as filesystem operations on Azure Data Lake Store.</span></span> <span data-ttu-id="ef262-113">Azure Data Lake 저장소는 계정 관리 작업을 위해 자체 REST API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-113">Azure Data Lake Store exposes its own REST APIs for account management operations.</span></span> <span data-ttu-id="ef262-114">그러나 Data Lake 저장소는 HDFS 및 Hadoop 에코시스템과 호환되기 때문에 파일 시스템 작업에 WebHDFS REST API를 사용하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-114">However, because Data Lake Store is compatible with HDFS and Hadoop ecosystem, it supports using WebHDFS REST APIs for filesystem operations.</span></span>

> [!NOTE]
> <span data-ttu-id="ef262-115">데이터 레이크 저장소에 대 한 REST API 지원 hello에 대 한 자세한 내용은 참조 하십시오. [Azure 데이터 레이크 저장소 REST API 참조](https://msdn.microsoft.com/library/mt693424.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-115">For detailed information on hello REST API support for Data Lake Store, see [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ef262-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ef262-116">Prerequisites</span></span>
* <span data-ttu-id="ef262-117">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="ef262-117">**An Azure subscription**.</span></span> <span data-ttu-id="ef262-118">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef262-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ef262-119">**Azure Active Directory 응용 프로그램을 만듭니다**.</span><span class="sxs-lookup"><span data-stu-id="ef262-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="ef262-120">Azure AD와 hello Azure AD 응용 프로그램 tooauthenticate hello Data Lake 저장소 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="ef262-121">없는 Azure AD와 다양 한 접근 방법 tooauthenticate 않는 **최종 사용자 인증** 또는 **서비스 간 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="ef262-122">지침 및 방법에 대 한 자세한 내용은 tooauthenticate, 참조 [최종 사용자 인증](data-lake-store-end-user-authenticate-using-active-directory.md) 또는 [서비스 간 인증](data-lake-store-authenticate-using-active-directory.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="ef262-123">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="ef262-123">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="ef262-124">이 문서에서는 cURL toodemonstrate toomake REST API 데이터 레이크 저장소 계정에 대해 호출 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-124">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Store account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="ef262-125">Azure Active Directory를 사용하여 인증하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="ef262-125">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="ef262-126">Azure Active Directory를 사용 하 여 두 가지 접근 방식을 tooauthenticate를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-126">You can use two approaches tooauthenticate using Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="ef262-127">최종 사용자 인증(대화형)</span><span class="sxs-lookup"><span data-stu-id="ef262-127">End-user authentication (interactive)</span></span>
<span data-ttu-id="ef262-128">이 시나리오에서는 hello 응용 프로그램에서 사용자 toolog hello를 표시 하 고 모든 hello 작업이 hello 사용자의 hello 컨텍스트에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-128">In this scenario, hello application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> <span data-ttu-id="ef262-129">Hello 대화형 인증에 대 한 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-129">Perform hello following steps for interactive authentication.</span></span>

1. <span data-ttu-id="ef262-130">응용 프로그램을 통해 hello 사용자 toohello url 리디렉션:</span><span class="sxs-lookup"><span data-stu-id="ef262-130">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="ef262-131">\<리디렉션 URI > toobe 인코딩된 URL에서 사용 하기 위해 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-131">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="ef262-132">따라서 https://localhost의 경우 `https%3A%2F%2Flocalhost`)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-132">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="ef262-133">이 자습서의 hello 용도로 위에 hello URL에서 자리 표시자 값 hello 바꾸고 웹 브라우저의 주소 표시줄에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-133">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="ef262-134">Azure 로그인을 사용 하 여 리디렉션된 tooauthenticate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-134">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="ef262-135">에 성공적으로 로그인 hello 응답이 hello 브라우저의 주소 표시줄에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-135">Once you successfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="ef262-136">hello 응답 형식에 따라 hello에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-136">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="ef262-137">Hello 응답 hello 권한 부여 코드를 캡처하십시오.</span><span class="sxs-lookup"><span data-stu-id="ef262-137">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="ef262-138">이 자습서에서는 hello 인증 코드 hello 웹 브라우저의 주소 표시줄 hello에서에서 복사한 아래와 같이 hello POST 요청 toohello 토큰 끝점에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-138">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="ef262-139">이 경우 hello \<리디렉션 URI > 인코딩할 수 없는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-139">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="ef262-140">hello 응답은 액세스 토큰을 포함 하는 JSON 개체 (예: `"access_token": "<ACCESS_TOKEN>"`) 및 새로 고침 토큰 (예: `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="ef262-140">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="ef262-141">응용 프로그램 사용 hello 액세스 토큰 새로 고침 토큰 tooget hello Azure 데이터 레이크 저장소에 액세스할 때 다른 액세스 토큰 액세스 토큰이 만료 된 경우 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-141">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="ef262-142">Hello 액세스 토큰이 만료 되 면 아래와 같이 hello 새로 고침 토큰을 사용 하 여 새 액세스 토큰을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-142">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="ef262-143">대화형 사용자 인증에 대한 자세한 내용은 [인증 코드 부여 흐름](https://msdn.microsoft.com/library/azure/dn645542.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef262-143">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="ef262-144">서비스 간 인증(비대화형)</span><span class="sxs-lookup"><span data-stu-id="ef262-144">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="ef262-145">이 시나리오에서는 hello hello 응용 프로그램 tooperform hello 작업 자체 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-145">In this scenario, hello hello application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="ef262-146">이 경우 hello 아래와 같은 POST 요청을 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-146">For this, you must issue a POST request like hello one shown below.</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="ef262-147">이 요청의 hello 출력 권한 부여 토큰에 포함 됩니다 (가리키는 `access-token` hello 출력 아래에)는 REST API 호출으로 전달 이후에 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-147">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="ef262-148">이 인증 토큰은 이 문서의 뒷부분에서 필요하므로 텍스트 파일에 저장해 두세요.</span><span class="sxs-lookup"><span data-stu-id="ef262-148">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="ef262-149">이 문서에서는 hello **비 대화형** 접근 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-149">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="ef262-150">비 대화형 (서비스 간 호출)에 대 한 자세한 내용은 참조 하십시오. [서비스 자격 증명을 사용 하 여 tooservice 호출](https://msdn.microsoft.com/library/azure/dn645543.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-150">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="ef262-151">Data Lake 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="ef262-151">Create a Data Lake Store account</span></span>
<span data-ttu-id="ef262-152">이 작업이 정의 된 hello REST API 호출 기반 [여기](https://msdn.microsoft.com/library/mt694078.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-152">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694078.aspx).</span></span>

<span data-ttu-id="ef262-153">다음 cURL 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-153">Use hello following cURL command.</span></span> <span data-ttu-id="ef262-154">**\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-154">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

<span data-ttu-id="ef262-155">명령 위에 hello, 바꿉니다 \< `REDACTED` \> hello 권한 부여 토큰으로 앞서 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-155">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="ef262-156">이 명령에 대 한 hello 요청 페이로드 hello에 포함 된 **input.json** hello에 대 한 제공 되는 파일 `-d` 위의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-156">hello request payload for this command is contained in hello **input.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="ef262-157">hello input.json 파일의 내용을 hello hello 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-157">hello contents of hello input.json file resemble hello following:</span></span>

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="ef262-158">Data Lake 저장소 계정에서 폴더 만들기</span><span class="sxs-lookup"><span data-stu-id="ef262-158">Create folders in a Data Lake Store account</span></span>
<span data-ttu-id="ef262-159">이 작업이 정의 된 hello WebHDFS REST API 호출 기반 [여기](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-159">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span></span>

<span data-ttu-id="ef262-160">다음 cURL 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-160">Use hello following cURL command.</span></span> <span data-ttu-id="ef262-161">**\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-161">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

<span data-ttu-id="ef262-162">명령 위에 hello, 바꿉니다 \< `REDACTED` \> hello 권한 부여 토큰으로 앞서 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-162">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="ef262-163">이 명령은 라는 디렉터리를 만듭니다. **mytempdir** hello 루트 폴더에 데이터 레이크 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-163">This command creates a directory called **mytempdir** under hello root folder of your Data Lake Store account.</span></span>

<span data-ttu-id="ef262-164">Hello 작업이 성공적으로 완료 되 면 다음과 같은 응답이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-164">You should see a response like this if hello operation completes successfully:</span></span>

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a><span data-ttu-id="ef262-165">Data Lake 저장소 계정의 폴더 나열</span><span class="sxs-lookup"><span data-stu-id="ef262-165">List folders in a Data Lake Store account</span></span>
<span data-ttu-id="ef262-166">이 작업이 정의 된 hello WebHDFS REST API 호출 기반 [여기](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-166">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span></span>

<span data-ttu-id="ef262-167">다음 cURL 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-167">Use hello following cURL command.</span></span> <span data-ttu-id="ef262-168">**\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-168">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

<span data-ttu-id="ef262-169">명령 위에 hello, 바꿉니다 \< `REDACTED` \> hello 권한 부여 토큰으로 앞서 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-169">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span>

<span data-ttu-id="ef262-170">Hello 작업이 성공적으로 완료 되 면 다음과 같은 응답이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-170">You should see a response like this if hello operation completes successfully:</span></span>

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

## <a name="upload-data-into-a-data-lake-store-account"></a><span data-ttu-id="ef262-171">Data Lake 저장소 계정에 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="ef262-171">Upload data into a Data Lake Store account</span></span>
<span data-ttu-id="ef262-172">이 작업이 정의 된 hello WebHDFS REST API 호출 기반 [여기](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-172">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span></span>

<span data-ttu-id="ef262-173">다음 cURL 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-173">Use hello following cURL command.</span></span> <span data-ttu-id="ef262-174">**\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-174">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

<span data-ttu-id="ef262-175">위의 구문 hello에 **-T** 매개 변수는 hello 파일 업로드 하는 hello 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-175">In hello above syntax **-T** parameter is hello location of hello file you are uploading.</span></span>

<span data-ttu-id="ef262-176">hello 출력은 toohello 다음과 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-176">hello output is similar toohello following:</span></span>
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a><span data-ttu-id="ef262-177">Data Lake 저장소 계정에서 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="ef262-177">Read data from a Data Lake Store account</span></span>
<span data-ttu-id="ef262-178">이 작업이 정의 된 hello WebHDFS REST API 호출 기반 [여기](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-178">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span></span>

<span data-ttu-id="ef262-179">Data Lake 저장소 계정에서 데이터를 읽는 작업은 2단계 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-179">Reading data from a Data Lake Store account is a two-step process.</span></span>

* <span data-ttu-id="ef262-180">먼저 hello 끝점에 대해 GET 요청을 제출 `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-180">You first submit a GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span></span> <span data-ttu-id="ef262-181">위치 toosubmit hello 다음 GET 요청을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-181">This will return a location toosubmit hello next GET request to.</span></span>
* <span data-ttu-id="ef262-182">그런 다음 hello 끝점에 대해 hello GET 요청을 제출 하면 `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-182">You then submit hello GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span></span> <span data-ttu-id="ef262-183">이 hello hello 파일 내용의 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-183">This will display hello contents of hello file.</span></span>

<span data-ttu-id="ef262-184">그러나 차이점이 있기 때문에 hello에 hello 사이의 입력된 매개 변수 먼저 및 hello의 두 번째 단계, hello를 사용할 수 있습니다 `-L` 매개 변수 toosubmit hello에 대 한 첫 번째 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-184">However, because there is no difference in hello input parameters between hello first and hello second step, you can use hello `-L` parameter toosubmit hello first request.</span></span> <span data-ttu-id="ef262-185">`-L`기본적으로 옵션 위의 두 요청을 결합 하 고 cURL hello 새 위치에 대 한 hello 요청을 다시 실행 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-185">`-L` option essentially combines two requests into one and will make cURL redo hello request on hello new location.</span></span> <span data-ttu-id="ef262-186">마지막으로, hello 출력이 모든 hello 요청 호출이 표시 되며, 같은 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-186">Finally, hello output from all hello request calls is displayed, like shown below.</span></span> <span data-ttu-id="ef262-187">**\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-187">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

<span data-ttu-id="ef262-188">출력 유사한 toohello 다음을 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-188">You should see an output similar toohello following:</span></span>

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="ef262-189">Data Lake 저장소 계정에서 파일 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="ef262-189">Rename a file in a Data Lake Store account</span></span>
<span data-ttu-id="ef262-190">이 작업이 정의 된 hello WebHDFS REST API 호출 기반 [여기](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-190">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span></span>

<span data-ttu-id="ef262-191">사용 하 여 hello 다음 toorename 명령 파일을 cURL 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-191">Use hello following cURL command toorename a file.</span></span> <span data-ttu-id="ef262-192">**\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-192">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

<span data-ttu-id="ef262-193">출력 유사한 toohello 다음을 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-193">You should see an output similar toohello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a><span data-ttu-id="ef262-194">Data Lake 저장소 계정에서 파일 삭제</span><span class="sxs-lookup"><span data-stu-id="ef262-194">Delete a file from a Data Lake Store account</span></span>
<span data-ttu-id="ef262-195">이 작업이 정의 된 hello WebHDFS REST API 호출 기반 [여기](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-195">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span></span>

<span data-ttu-id="ef262-196">사용 하 여 hello 다음 toodelete 명령 파일을 cURL 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-196">Use hello following cURL command toodelete a file.</span></span> <span data-ttu-id="ef262-197">**\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-197">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

<span data-ttu-id="ef262-198">Hello 다음과 같은 출력을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-198">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="ef262-199">Data Lake 저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="ef262-199">Delete a Data Lake Store account</span></span>
<span data-ttu-id="ef262-200">이 작업이 정의 된 hello REST API 호출 기반 [여기](https://msdn.microsoft.com/library/mt694075.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-200">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694075.aspx).</span></span>

<span data-ttu-id="ef262-201">사용 하 여 hello 다음을 cURL 명령 toodelete 데이터 레이크 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-201">Use hello following cURL command toodelete a Data Lake Store account.</span></span> <span data-ttu-id="ef262-202">**\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-202">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

<span data-ttu-id="ef262-203">Hello 다음과 같은 출력을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef262-203">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a><span data-ttu-id="ef262-204">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ef262-204">See also</span></span>
* [<span data-ttu-id="ef262-205">Azure Data Lake 저장소와 호환되는 오픈 소스 빅 데이터 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ef262-205">Open Source Big Data applications compatible with Azure Data Lake Store</span></span>](data-lake-store-compatible-oss-other-applications.md)

