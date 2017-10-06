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
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a>Node.js용 Azure SDK를 사용하여 Azure Data Lake Store 시작
> [!div class="op_single_selector"]
> * [포털](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.JS](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> 업로드 하 고 많은 양의 데이터 (대형 파일, 많은 수의 파일, 또는 둘 다)을 다운로드에 대 한 hello를 사용 하는 권장 [Python SDK](data-lake-store-get-started-python.md), hello [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), 또는 [Azure PowerShell](data-lake-store-get-started-powershell.md)합니다. 이러한 옵션은 더 나은 성능을 여러 스레드 tooparallelize hello 데이터 이동의 사용 합니다.
> 
> 

어떻게 toouse hello Azure SDK Node.js toocreate에 대 한 Azure 데이터 레이크 저장소 계정에 알아봅니다 폴더를 만들어 업로드 및 다운로드 데이터 파일 등의 기본 작업을 수행 하 고 계정, 등을 삭제 합니다. Data Lake Store에 대한 자세한 내용은 [Data Lake Store 개요](data-lake-store-overview.md)를 참조하세요. 현재 hello SDK 지원

* **Node.js 버전: 0.10.0 이상**
* **계정에 대한 REST API 버전: 2015-10-01-preview**
* **FileSystem용 REST API 버전: 2015-10-01-preview**

## <a name="prerequisites"></a>필수 조건
이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* **Azure Active Directory 응용 프로그램을 만듭니다**. Azure AD와 hello Azure AD 응용 프로그램 tooauthenticate hello Data Lake 저장소 응용 프로그램을 사용 합니다. 없는 Azure AD와 다양 한 접근 방법 tooauthenticate 않는 **최종 사용자 인증** 또는 **서비스 간 인증**합니다. 지침 및 방법에 대 한 자세한 내용은 tooauthenticate, 참조 [최종 사용자 인증](data-lake-store-end-user-authenticate-using-active-directory.md) 또는 [서비스 간 인증](data-lake-store-authenticate-using-active-directory.md)합니다.

## <a name="how-tooinstall"></a>어떻게 tooInstall
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a>Azure Active Directory를 사용하여 인증
아래 hello 조각은 Azure AD를 사용 하 여 데이터 레이크 저장소를 사용 하 여 인증 하는 두 개의 별도 방법을 보여 줍니다. 데이터 레이크 저장소와 인증에 대 한 다양 한 메서드 toouse에 대 한 자세한 내용은 참조 하십시오. [Azure Active Directory를 사용 하 여 데이터 레이크 저장소로 인증](data-lake-store-authenticate-using-active-directory.md)합니다.

아래 hello 조각 유사 하 게 Azure AD 도메인 이름, 클라이언트 ID 등 Azure AD 앱에 대 한 입력 해야합니다. 이러한 모든 세부이 정보 hello 세부 사항으로 위의 링크에도 포함 되어 Azure AD 만든 응용 프로그램에서 수행 해야 하는, 검색할 수 있습니다.

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-store-clients"></a>Hello 데이터 레이크 저장소 클라이언트를 만듭니다.
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a>Data Lake 저장소 계정 만들기
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

## <a name="create-a-file-with-content"></a>콘텐츠를 포함하는 파일 만들기
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

## <a name="get-a-list-of-files-and-folders"></a>파일 및 폴더 목록 가져오기
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

## <a name="see-also"></a>참고 항목
* [Node.js용 Microsoft Azure SDK](https://github.com/azure/azure-sdk-for-node)
* [Node.js용 Microsoft Azure SDK - Data Lake 분석 관리](https://www.npmjs.com/package/azure-arm-datalake-analytics)

