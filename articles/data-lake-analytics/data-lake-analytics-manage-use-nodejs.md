---
title: "Node.js 용 Azure SDK를 사용 하 여 Azure Data Lake 분석 aaaManage | Microsoft Docs"
description: "Toomanage Data Lake 분석 계정, 데이터 원본 작업 하는 방법 및 Node.js 용 Azure SDK를 사용 하 여 사용자에 알아봅니다"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 9de1bcf4-b15b-4d0b-9284-8889ecf0c438
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 07acd058bf252af2fc98c4cfe87a135e0b79900f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-sdk-for-nodejs"></a><span data-ttu-id="d31c8-103">Node.js용 Azure SDK를 사용하여 Azure 데이터 레이크 분석 관리</span><span class="sxs-lookup"><span data-stu-id="d31c8-103">Manage Azure Data Lake Analytics using Azure SDK for Node.js</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="d31c8-104">Azure Data Lake 분석 계정, 작업 및 카탈로그를 관리 하기 위한 hello Node.js 용 Azure SDK를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d31c8-104">hello Azure SDK for Node.js can be used for managing Azure Data Lake Analytics accounts, jobs and catalogs.</span></span> <span data-ttu-id="d31c8-105">다른 도구를 사용 하 여 toosee 관리 항목을 클릭 하 여 위의 hello 탭 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d31c8-105">toosee management topic using other tools, click hello tab select above.</span></span>

<span data-ttu-id="d31c8-106">현재는 다음이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d31c8-106">Right now it supports:</span></span>

* <span data-ttu-id="d31c8-107">**Node.js 버전: 0.10.0 이상**</span><span class="sxs-lookup"><span data-stu-id="d31c8-107">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="d31c8-108">**계정에 대한 REST API 버전: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="d31c8-108">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="d31c8-109">**카탈로그에 대한 REST API 버전: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="d31c8-109">**REST API version for Catalog: 2015-10-01-preview**</span></span>
* <span data-ttu-id="d31c8-110">**작업에 대한 REST API 버전: 2016-03-20-preview**</span><span class="sxs-lookup"><span data-stu-id="d31c8-110">**REST API version for Job: 2016-03-20-preview**</span></span>

## <a name="features"></a><span data-ttu-id="d31c8-111">기능</span><span class="sxs-lookup"><span data-stu-id="d31c8-111">Features</span></span>
* <span data-ttu-id="d31c8-112">계정 관리: 만들기, 가져오기, 나열, 업데이트 및 삭제</span><span class="sxs-lookup"><span data-stu-id="d31c8-112">Account management: create, get, list, update, and delete.</span></span>
* <span data-ttu-id="d31c8-113">작업 관리: 제출, 가져오기, 나열, 취소</span><span class="sxs-lookup"><span data-stu-id="d31c8-113">Job management: submit, get, list, and cancel.</span></span>
* <span data-ttu-id="d31c8-114">카탈로그 관리: 가져오기 및 나열</span><span class="sxs-lookup"><span data-stu-id="d31c8-114">Catalog management: get and list.</span></span>

## <a name="how-tooinstall"></a><span data-ttu-id="d31c8-115">어떻게 tooInstall</span><span class="sxs-lookup"><span data-stu-id="d31c8-115">How tooInstall</span></span>
```bash
npm install azure-arm-datalake-analytics
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="d31c8-116">Azure Active Directory를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="d31c8-116">Authenticate using Azure Active Directory</span></span>
 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-analytics-client"></a><span data-ttu-id="d31c8-117">Hello Data Lake 분석 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="d31c8-117">Create hello Data Lake Analytics client</span></span>
```javascript
var adlaManagement = require("azure-arm-datalake-analytics");
var acccountClient = new adlaManagement.DataLakeAnalyticsAccountClient(credentials, 'your-subscription-id');
var jobClient = new adlaManagement.DataLakeAnalyticsJobClient(credentials, 'azuredatalakeanalytics.net');
var catalogClient = new adlaManagement.DataLakeAnalyticsCatalogClient(credentials, 'azuredatalakeanalytics.net');
```

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="d31c8-118">Data Lake 분석 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="d31c8-118">Create a Data Lake Analytics account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlaacct';
var location = 'eastus2';

// A Data Lake Store account must already have been created toocreate
// a Data Lake Analytics account. See hello Data Lake Store readme for
// information on doing so. For now, we assume one exists already.
var datalakeStoreAccountName = 'existingadlsaccount';

// account object toocreate
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location,
  properties: {
    defaultDataLakeStoreAccount: datalakeStoreAccountName,
    dataLakeStoreAccounts: [
      {
        name: datalakeStoreAccountName
      }
    ]
  }
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

## <a name="get-a-list-of-jobs"></a><span data-ttu-id="d31c8-119">작업 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="d31c8-119">Get a list of jobs</span></span>
```javascript
var util = require('util');
var accountName = 'testadlaacct';
jobClient.job.list(accountName, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="get-a-list-of-databases-in-hello-data-lake-analytics-catalog"></a><span data-ttu-id="d31c8-120">데이터 레이크 분석 카탈로그 hello에 데이터베이스의 목록을 보려면</span><span class="sxs-lookup"><span data-stu-id="d31c8-120">Get a list of databases in hello Data Lake Analytics Catalog</span></span>
```javascript
var util = require('util');
var accountName = 'testadlaacct';
catalogClient.catalog.listDatabases(accountName, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a><span data-ttu-id="d31c8-121">참고 항목</span><span class="sxs-lookup"><span data-stu-id="d31c8-121">See also</span></span>
* [<span data-ttu-id="d31c8-122">Node.js용 Microsoft Azure SDK</span><span class="sxs-lookup"><span data-stu-id="d31c8-122">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="d31c8-123">Node.js용 Microsoft Azure SDK - Data Lake 저장소 관리</span><span class="sxs-lookup"><span data-stu-id="d31c8-123">Microsoft Azure SDK for Node.js - Data Lake Store Management</span></span>](https://github.com/Azure/azure-sdk-for-node/tree/autorest/lib/services/dataLake.Store)

