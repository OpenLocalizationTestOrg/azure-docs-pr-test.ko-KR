---
title: "Node.js 용 Azure SDK를 사용 하 여 Azure 데이터 레이크 저장소 aaaGet 시작 | Microsoft Docs"
description: "데이터 레이크 저장소 계정 및 hello toouse Node.js toowork 파일 시스템 방법에 대해 알아봅니다."
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 2fee173c-69ae-4e1d-8773-48618cda9e16
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: nitinme
ms.openlocfilehash: ce36a2e0de4e091a4e85ed784a3381415ef6f9e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a><span data-ttu-id="d71d6-103">Node.js용 Azure SDK를 사용하여 Azure Data Lake Store 시작</span><span class="sxs-lookup"><span data-stu-id="d71d6-103">Get started with Azure Data Lake Store using Azure SDK for Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d71d6-104">포털</span><span class="sxs-lookup"><span data-stu-id="d71d6-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="d71d6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d71d6-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="d71d6-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="d71d6-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="d71d6-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="d71d6-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="d71d6-108">REST API</span><span class="sxs-lookup"><span data-stu-id="d71d6-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="d71d6-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d71d6-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="d71d6-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="d71d6-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="d71d6-111">Python</span><span class="sxs-lookup"><span data-stu-id="d71d6-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> <span data-ttu-id="d71d6-112">업로드 하 고 많은 양의 데이터 (대형 파일, 많은 수의 파일, 또는 둘 다)을 다운로드에 대 한 hello를 사용 하는 권장 [Python SDK](data-lake-store-get-started-python.md), hello [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), 또는 [Azure PowerShell](data-lake-store-get-started-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d71d6-112">For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use hello [Python SDK](data-lake-store-get-started-python.md), hello [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md).</span></span> <span data-ttu-id="d71d6-113">이러한 옵션은 더 나은 성능을 여러 스레드 tooparallelize hello 데이터 이동의 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d71d6-113">These options have better performance as they use multiple threads tooparallelize hello data movement.</span></span>
> 
> 

<span data-ttu-id="d71d6-114">어떻게 toouse hello Azure SDK Node.js toocreate에 대 한 Azure 데이터 레이크 저장소 계정에 알아봅니다 폴더를 만들어 업로드 및 다운로드 데이터 파일 등의 기본 작업을 수행 하 고 계정, 등을 삭제 합니다. Data Lake Store에 대한 자세한 내용은 [Data Lake Store 개요](data-lake-store-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d71d6-114">Learn how toouse hello Azure SDK for Node.js toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span> <span data-ttu-id="d71d6-115">현재 hello SDK 지원</span><span class="sxs-lookup"><span data-stu-id="d71d6-115">Currently, hello SDK supports</span></span>

* <span data-ttu-id="d71d6-116">**Node.js 버전: 0.10.0 이상**</span><span class="sxs-lookup"><span data-stu-id="d71d6-116">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="d71d6-117">**계정에 대한 REST API 버전: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="d71d6-117">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="d71d6-118">**FileSystem용 REST API 버전: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="d71d6-118">**REST API version for FileSystem: 2015-10-01-preview**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d71d6-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d71d6-119">Prerequisites</span></span>
<span data-ttu-id="d71d6-120">이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d71d6-120">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="d71d6-121">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="d71d6-121">**An Azure subscription**.</span></span> <span data-ttu-id="d71d6-122">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d71d6-122">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d71d6-123">**Azure Active Directory 응용 프로그램을 만듭니다**.</span><span class="sxs-lookup"><span data-stu-id="d71d6-123">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="d71d6-124">Azure AD와 hello Azure AD 응용 프로그램 tooauthenticate hello Data Lake 저장소 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d71d6-124">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="d71d6-125">없는 Azure AD와 다양 한 접근 방법 tooauthenticate 않는 **최종 사용자 인증** 또는 **서비스 간 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="d71d6-125">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="d71d6-126">지침 및 방법에 대 한 자세한 내용은 tooauthenticate, 참조 [최종 사용자 인증](data-lake-store-end-user-authenticate-using-active-directory.md) 또는 [서비스 간 인증](data-lake-store-authenticate-using-active-directory.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d71d6-126">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="how-tooinstall"></a><span data-ttu-id="d71d6-127">어떻게 tooInstall</span><span class="sxs-lookup"><span data-stu-id="d71d6-127">How tooInstall</span></span>
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="d71d6-128">Azure Active Directory를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="d71d6-128">Authenticate using Azure Active Directory</span></span>
<span data-ttu-id="d71d6-129">아래 hello 조각은 Azure AD를 사용 하 여 데이터 레이크 저장소를 사용 하 여 인증 하는 두 개의 별도 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d71d6-129">hello snippets below show two separate ways of authenticating with Data Lake Store using Azure AD.</span></span> <span data-ttu-id="d71d6-130">데이터 레이크 저장소와 인증에 대 한 다양 한 메서드 toouse에 대 한 자세한 내용은 참조 하십시오. [Azure Active Directory를 사용 하 여 데이터 레이크 저장소로 인증](data-lake-store-authenticate-using-active-directory.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d71d6-130">For a detailed discussion on various methods toouse for authentication with Data Lake Store, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="d71d6-131">아래 hello 조각 유사 하 게 Azure AD 도메인 이름, 클라이언트 ID 등 Azure AD 앱에 대 한 입력 해야합니다. 이러한 모든 세부이 정보 hello 세부 사항으로 위의 링크에도 포함 되어 Azure AD 만든 응용 프로그램에서 수행 해야 하는, 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d71d6-131">hello snippet below also requires inputs like Azure AD domain name, client ID for an Azure AD app, etc. All these details can be retrieved from an Azure AD application that you must created, hello details of which are also included in link above.</span></span>

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-store-clients"></a><span data-ttu-id="d71d6-132">Hello 데이터 레이크 저장소 클라이언트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d71d6-132">Create hello Data Lake Store Clients</span></span>
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="d71d6-133">Data Lake 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="d71d6-133">Create a Data Lake Store Account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object toocreate
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location
};

client.account.create(resourceGroupName, accountName, accountToCreate, function (err, result, request, response) {
  if (err) {
    console.log(err);
    /*err has reference toohello actual request and response, so you can see what was sent and received on hello wire.
      hello structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'hello response body if any',
        request: reference tooa stripped version of http request
        response: reference tooa stripped version of hello response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a><span data-ttu-id="d71d6-134">콘텐츠를 포함하는 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="d71d6-134">Create a file with content</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var fileToCreate = '/myfolder/myfile.txt';
var options = {
  streamContents: new Buffer('some string content')
}

filesystemClient.fileSystem.listFileStatus(accountName, fileToCreate, options, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    // no result is returned, only a 201 response for success.
    console.log('response is: ' + util.inspect(response, {depth: null}));
  }
});
```

## <a name="get-a-list-of-files-and-folders"></a><span data-ttu-id="d71d6-135">파일 및 폴더 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="d71d6-135">Get a list of files and folders</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var pathToEnumerate = '/myfolder';
filesystemClient.fileSystem.listFileStatus(accountName, pathToEnumerate, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a><span data-ttu-id="d71d6-136">참고 항목</span><span class="sxs-lookup"><span data-stu-id="d71d6-136">See also</span></span>
* [<span data-ttu-id="d71d6-137">Node.js용 Microsoft Azure SDK</span><span class="sxs-lookup"><span data-stu-id="d71d6-137">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="d71d6-138">Node.js용 Microsoft Azure SDK - Data Lake 분석 관리</span><span class="sxs-lookup"><span data-stu-id="d71d6-138">Microsoft Azure SDK for Node.js - Data Lake Analytics Management</span></span>](https://www.npmjs.com/package/azure-arm-datalake-analytics)

