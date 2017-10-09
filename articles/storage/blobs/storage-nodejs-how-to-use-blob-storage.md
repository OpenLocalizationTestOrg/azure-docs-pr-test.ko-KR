---
title: "Node.js에서 Blob 저장소 aaaHow toouse | Microsoft Docs"
description: "Azure Blob 저장소 (개체 저장소)를 사용 하는 hello 클라우드에 구조화 되지 않은 데이터를 저장 합니다."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 572e7fc9f7b19ff01720a7cadd495c809ed49fb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a>어떻게 toouse Node.js에서 Blob 저장소
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>개요
이 문서에서는 Blob 저장소를 사용 하 여 tooperform 일반적인 시나리오입니다. hello 샘플 hello Node.js API를 통해 작성 됩니다. 가이드에서 다루는 hello 시나리오 tooupload를 나열, 다운로드 및 blob 삭제 방법을 포함 합니다.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Node.js 응용 프로그램 만들기
방법에 대 한 지침은 toocreate는 Node.js 응용 프로그램 참조 [Azure 앱 서비스에서 Node.js 웹 앱 만들기] [빌드하고 Node.js 응용 프로그램 tooan Azure 클라우드 서비스 배포](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) -Windows PowerShell을 사용 하 여 또는 [빌드 및 웹 매트릭스를 사용 하는 Node.js 웹 응용 프로그램 tooAzure 배포](https://www.microsoft.com/web/webmatrix/)합니다.

## <a name="configure-your-application-tooaccess-storage"></a>응용 프로그램 tooaccess 저장소 구성
Azure 저장소 toouse hello 저장소 REST 서비스와 통신 하는 편리한 라이브러리의 집합을 포함 하는 Node.js 용 hello Azure 저장소 SDK 할 수 있습니다.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>노드 패키지 관리자 (NPM) tooobtain hello 패키지 사용
1. 와 같은 명령줄 인터페이스를 사용 하 여 **PowerShell** (Windows) **터미널** (Mac) 또는 **를 이용한 적** (Unix) 샘플을 만들었으므로 toonavigate toohello 폴더 응용 프로그램입니다.
2. 형식 **npm 설치 azure storage** hello 명령 창에서. Hello 명령 출력은 다음 코드 예제와 비슷한 toohello입니다.

        azure-storage@0.5.0 node_modules\azure-storage
        +-- extend@1.2.1
        +-- xmlbuilder@0.4.3
        +-- mime@1.2.11
        +-- node-uuid@1.4.3
        +-- validator@3.22.2
        +-- underscore@1.4.4
        +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
        +-- xml2js@0.2.7 (sax@0.5.2)
        +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. Hello를 수동으로 실행할 수 있습니다 **ls** 명령 tooverify 하는 **노드\_모듈** 폴더를 만들었습니다. 해당 폴더 내의 hello 찾습니다 **azure 저장소** tooaccess 저장 해야 하는 hello 라이브러리를 포함 하는 패키지입니다.

### <a name="import-hello-package"></a>Hello 패키지 가져오기
메모장 이나 다른 텍스트 편집기를 사용 하 여 추가 hello toohello 맨 뒤 hello **server.js** toouse 저장소 이점을 얻을 수 hello 응용 프로그램의 파일:

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Azure 저장소 연결 설정
hello Azure 모듈 읽힙니다 hello 환경 변수 `AZURE_STORAGE_ACCOUNT` 및 `AZURE_STORAGE_ACCESS_KEY`, 또는 `AZURE_STORAGE_CONNECTION_STRING`, 필요한 tooconnect tooyour Azure 저장소 계정 정보에 대 한 합니다. 호출할 때 hello 계정 정보를 지정 해야 이러한 환경 변수가 설정 되지 않은 경우 **createBlobService**합니다.

Hello에 hello 환경 변수 설정에 대 한 예제 [Azure 포털](https://portal.azure.com) 는 Azure 웹 앱에 대 한 참조 [Azure 테이블 서비스 hello 사용 하 여 Node.js 웹 응용 프로그램](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)합니다.

## <a name="create-a-container"></a>컨테이너 만들기
hello **BlobService** 개체 컨테이너 및 blob를 사용할 수 있습니다. hello 다음 코드에서는 **BlobService** 개체입니다. hello 위쪽 hello 다음 추가 **server.js**:

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> 사용 하 여 blob을 익명으로 액세스할 수 있습니다 **createBlobServiceAnonymous** hello 호스트 주소를 제공 하 고 있습니다. 예를 들면 `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`를 사용합니다.
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

toocreate 새 컨테이너를 사용 하 여 **createContainerIfNotExists**합니다. hello 다음 코드 예제에서는 'mycontainer' 라는 새 컨테이너:

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

Hello 컨테이너를 새로 작성 하는 경우 `result.created` 그렇습니다. Hello 컨테이너에 이미 있으면 `result.created` 은 false입니다. `response`hello 컨테이너에 대 한 hello ETag 정보를 포함 하는 hello 작업에 대 한 정보를 포함 합니다.

### <a name="container-security"></a>컨테이너 보안
기본적으로 새 컨테이너는 개인 컨테이너이며 익명으로 액세스할 수 없습니다. 익명으로 액세스할 수 있도록 공용 toomake hello 컨테이너 설정할 수 있습니다 hello 컨테이너의 액세스 수준을 너무**blob** 또는 **컨테이너**합니다.

* **blob** -익명 읽기 권한을 tooblob 콘텐츠 및이 컨테이너에 있는 메타 데이터는 있지만 하지 toocontainer 등의 메타 데이터 컨테이너 내 모든 blob을 나열 허용
* **컨테이너** -익명 읽기 권한을 tooblob 콘텐츠 및 메타 데이터 뿐 아니라 컨테이너 메타 데이터를 허용 합니다.

hello 다음 코드 예제에서는 hello 액세스 수준을 설정 너무**blob**:

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

컨테이너의 액세스 수준을 hello를 사용 하 여 수정할 수 있습니다 또는 **setContainerAcl** toospecify hello 액세스 수준입니다. hello 다음 코드 예제에서는 변경 내용을 hello 액세스 수준 toocontainer:

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

hello 결과 대 한 정보가 hello 현재 포함 하는 hello 작업 **ETag** hello 컨테이너에 대 한 합니다.

### <a name="filters"></a>필터
선택적 작업 수행 toooperations 사용 하는 필터를 적용할 수 있습니다 **BlobService**합니다. 필터링 작업은 로깅, 자동 재시도 등을 포함할 수 있습니다. 필터는 hello 서명으로 메서드를 구현 하는 개체:

```nodejs
function handle (requestOptions, next)
```

Hello 요청 옵션에 전처리를 수행한 후 hello 메서드는 toocall "다음" 필요 콜백을 뒤 서명에 hello로 전달 합니다.

```nodejs
function (returnObject, finalCallback, next)
```

이 콜백에서 hello returnObject (hello toohello 서버 요청에서에서 응답 hello)를 처리 한 후, hello 콜백 필요 tooeither 단순히 finalCallback tooend hello 서비스를 호출 하거나 다른 필터를 처리 하는 toocontinue 있는 경우 다음에 호출할 호출 합니다.

재시도 논리를 구현 하는 두 개의 필터 hello Node.js 용 Azure SDK에 포함 된 **ExponentialRetryPolicyFilter** 및 **LinearRetryPolicyFilter**합니다. hello 다음 만듭니다는 **BlobService** hello를 사용 하는 개체 **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a>컨테이너에 Blob 업로드
블록 Blob, 페이지 Blob 및 추가 Blob의 세 가지 Blob 유형이 있습니다. 블록 blob를 사용 하면 toomore 효율적으로 큰 데이터를 업로드 합니다. 추가 Blob은 추가 작업에 최적화되어 있습니다. 페이지 Blob은 읽기/쓰기 작업에 최적화되어 있습니다. 자세한 내용은 [블록 Blob, 추가 Blob 및 페이지 Blob 이해](http://msdn.microsoft.com/library/azure/ee691964.aspx)를 참조하세요.

### <a name="block-blobs"></a>블록 Blob
tooupload 데이터 tooa 블록 blob을 사용 하 여 hello 다음:

* **createBlockBlobFromLocalFile** -새 블록 blob를 만들고 업로드 된 파일의 내용을 hello
* **createBlockBlobFromStream** -새 블록 blob를 만들고 stream의 hello 내용 업로드
* **createBlockBlobFromText** -새 블록 blob를 만들고 문자열의 내용을 hello 업로드
* **createWriteStreamToBlockBlob** -쓰기 스트림을 tooa 블록 blob를 제공 합니다.

hello 다음 코드 예제에서는 업로드 hello 내용의 hello **test.txt** 파일 **myblob**합니다.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

hello `result` 이러한 메서드에 의해 반환 된 hello 등 hello 작업에 대 한 정보 **ETag** hello blob의 합니다.

### <a name="append-blobs"></a>추가 Blob
tooupload 데이터 tooa 새 blob을 추가, hello 다음을 사용 하 여:

* **createAppendBlobFromLocalFile** -새 blob를 만들고 업로드 된 파일의 내용을 hello
* **createAppendBlobFromStream** -새 blob를 만들고 stream의 hello 내용 업로드
* **createAppendBlobFromText** -새 blob를 만들고 문자열의 내용을 hello 업로드
* **createWriteStreamToNewAppendBlob** -새 blob 키를 만들고 다음 스트림 toowrite tooit 제공

hello 다음 코드 예제에서는 업로드 hello 내용의 hello **test.txt** 파일 **myappendblob**합니다.

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

tooappend 블록 tooan 기존 blob의 경우 다음 사용 하 여 hello를 추가 합니다.

* **appendFromLocalFile** -hello 내용을 추가 합니다. 기존 파일 tooan의 blob 추가
* **appendFromStream** -hello 내용을 추가할 추가 blob를 기존 스트림에 tooan의
* **appendFromText** -hello 내용을 추가 하는 문자열 tooan의 blob를 추가할 기존
* **appendBlockFromStream** -hello 내용을 추가할 추가 blob를 기존 스트림에 tooan의
* **appendBlockFromText** -hello 내용을 추가 하는 문자열 tooan의 blob를 추가할 기존

> [!NOTE]
> appendFromXXX Api는 일부 클라이언트 쪽 유효성 검사 toofail 빠른 tooavoid 불필요 한 서버 호출을 수행 합니다. appendBlockFromXXX는 이를 수행하지 않습니다.
>
>

hello 다음 코드 예제에서는 업로드 hello 내용의 hello **test.txt** 파일 **myappendblob**합니다.

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a>페이지 Blob
tooupload 데이터 tooa 페이지 blob의 경우 다음 사용 하 여 hello:

* **createPageBlob** - 특정 길이의 새 페이지 Blob을 만듭니다.
* **createPageBlobFromLocalFile** -새 페이지 blob를 만들고 업로드 된 파일의 내용을 hello
* **createPageBlobFromStream** -새 페이지 blob를 만들고 stream의 hello 내용 업로드
* **createWriteStreamToExistingPageBlob** -쓰기 스트림을 tooan 기존 페이지 blob를 제공 합니다.
* **createWriteStreamToNewPageBlob** -새 페이지 blob를 만들고 스트림 toowrite tooit를 제공 합니다

hello 다음 코드 예제에서는 업로드 hello 내용의 hello **test.txt** 파일 **mypageblob**합니다.

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> 페이지 Bobl은 512바이트의 '페이지'로 구성됩니다. 크기가 512의 배수가 아닌 경우에는 데이터를 업로드할 때 오류가 표시됩니다.
>
>

## <a name="list-hello-blobs-in-a-container"></a>컨테이너에서 hello blob 나열
toolist hello blob 컨테이너에서 hello를 사용 하 여 **listBlobsSegmented** 메서드. 사용 하 여 지정 된 접두사로 tooreturn blob를 원하는 경우 **listBlobsSegmentedWithPrefix**합니다.

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

hello `result` 포함 한 `entries` 컬렉션은 각 blob에 설명 하는 개체의 배열입니다. 모든 blob를 반환할 수 없는 경우 hello `result` 제공는 `continuationToken`, hello 두 번째 매개 변수 tooretrieve 추가 항목으로 사용할 수 있는 합니다.

## <a name="download-blobs"></a>Blob 다운로드
blob에서 toodownload 데이터 hello 다음을 사용 합니다.

* **getBlobToLocalFile** -hello blob 내용을 toofile 씁니다.
* **getBlobToStream** -hello blob 내용을 tooa 스트림에 씁니다.
* **getBlobToText** -hello blob 콘텐츠가 tooa 문자열을 씁니다.
* **createReadStream** -hello blob에서 스트림 tooread 제공

hello 다음 코드 예제에서는 사용 하 여 **getBlobToStream** toodownload hello 내용의 hello **myblob** blob 및 toohello 저장 **output.txt 라는** 사용 하 여 파일을 스트림:

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

hello `result` hello blob에 대 한 정보도 포함 하 여 **ETag** 정보입니다.

## <a name="delete-a-blob"></a>Blob 삭제
마지막으로, blob toodelete 호출 **deleteBlob**합니다. 다음 코드 예제에서는 삭제 hello 라는 blob hello **myblob**합니다.

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a>동시 액세스
사용할 수 있습니다 toosupport 동시 액세스 tooa 여러 클라이언트 또는 여러 프로세스에서 blob, **Etag** 또는 **임대**합니다.

* **Etag** -다른 프로세스에서 수정 했습니다. blob 또는 컨테이너 hello 하는 방식으로 toodetect 제공
* **임대** -tooobtain 단독, 갱신, 쓰기 방식으로 제공 하거나 일정 기간에 대 한 액세스 tooa blob 삭제

### <a name="etag"></a>ETag
여러 클라이언트 또는 인스턴스 toowrite toohello 블록 Blob 또는 페이지 Blob 동시에 tooallow 해야 할 경우 Etag를 사용 합니다. hello ETag 있습니다 toodetermine를 hello 컨테이너 또는 blob가 수정 되었으면 이후 처음 읽기 또는 생성자, 다른 클라이언트 또는 프로세스에 의해 커밋된 변경 내용을 덮어쓰지 tooavoid 있습니다.

선택적 hello를 사용 하 여 ETag 조건을 설정할 수 있습니다 `options.accessConditions` 매개 변수입니다. hello 다음 코드 예제에서는 업로드 hello **test.txt** hello blob에서 이미 존재 하 고 hello ETag 값이 파일에 포함 된 `etagToMatch`합니다.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

Etag를 사용 하는 hello 일반적인 패턴은:

1. 만들기, 목록 또는 가져오기 작업의 hello 결과로 hello를 ETag를 가져옵니다.
2. 해당 hello ETag 값을 수정 되지 않았는지 검사 동작을 수행 합니다.

Hello 값이 수정 된 경우 다른 클라이언트 또는 인스턴스 hello ETag 값을 가져온 이후 hello blob 또는 컨테이너를 수정 있음을 나타냅니다.

### <a name="lease"></a>임대
Hello를 사용 하 여 새로운 임대를 획득 수 **acquireLease** 메서드에 맞다면 tooobtain 임대에 hello blob 또는 컨테이너를 지정 합니다. Hello 코드 다음에 임대를 획득 하는 예를 들어 **myblob**합니다.

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

에 대 한 후속 작업 **myblob** hello를 제공 해야 `options.leaseId` 매개 변수입니다. ID가으로 반환 하는 hello 임대 `result.id` 에서 **acquireLease**합니다.

> [!NOTE]
> 기본적으로 hello 임대 기간이 무한정입니다. Hello를 제공 하 여 (15 ~ 60 초) 사이 유한 기간을 지정할 수 있습니다 `options.leaseDuration` 매개 변수입니다.
>
>

tooremove 임대를 사용 하 여 **releaseLease**합니다. 임대를 toobreak 하지만 다른 방지에서 hello 원래 지속 시간이 만료 될 때까지 새로운 임대를 획득할를 사용 하 여 **breakLease**합니다.

## <a name="work-with-shared-access-signatures"></a>공유 액세스 서명 작업
공유 액세스 서명 (SAS)은 안전 하 게 tooprovide 세부적인 액세스 tooblobs 및 저장소 계정 이름 또는 키를 제공 하지 않고 컨테이너입니다. 공유 액세스 서명에 사용 되는 tooprovide 제한 된 액세스 tooyour 데이터 tooaccess blob 모바일 앱을 허용 하는 등 경우가 많습니다.

> [!NOTE]
> Tooblobs 익명 액세스를 허용할 수도 있습니다 공유 액세스 서명을 수 제어 요소가 많은 tooprovide 액세스 hello SAS를 생성 해야 합니다.
>
>

클라우드 기반 서비스와 같은 신뢰할 수 있는 응용 hello를 사용 하 여 공유 액세스 서명을 생성 하 **generateSharedAccessSignature** 의 hello **BlobService**, 제공 하 고 신뢰할 수 없는 tooan 또는 모바일 앱과 같은 부분 신뢰 응용 프로그램입니다. 공유 액세스 서명을 hello 시작에 설명 하는 정책을 사용 하 여 생성할 및 종료 날짜는 hello 하는 동안 공유 액세스 서명에 유효 뿐 아니라 hello 수준 부여한 toohello 공유 액세스 서명을 홀더를 액세스 합니다.

hello 다음 코드 예제에서는 발생 하는 hello 공유 액세스 서명을 소유자 tooperform 읽기 hello에 대 한 작업을 허용 하는 새 공유 액세스 정책을 **myblob** blob, 이며 100 분 만들어질 hello 시간이 지난 후 만료 됩니다.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

Note 또한 필요에 따라 hello 공유 액세스 서명을 소유자가 시도할 때 tooaccess hello 컨테이너 제공 hello 호스트 정보 이어야 합니다.

hello 그런 다음 클라이언트 응용 프로그램 사용 하 여 공유 액세스 서명은 **BlobServiceWithSAS** hello blob에 대 한 tooperform 작업 합니다. hello 다음 정보를 가져옵니다에 대 한 **myblob**합니다.

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

Hello 공유 액세스 서명을 toomodify hello blob 하려고 시도 하는 경우 읽기 전용 액세스 권한으로 생성 된 이후 오류가 반환 됩니다.

### <a name="access-control-lists"></a>액세스 제어 목록
SAS에 대 한 액세스 제어 목록 (ACL) tooset hello 액세스 정책을 사용할 수도 있습니다. 각 클라이언트에 대 한 다른 액세스 정책을 제공 하지만 여러 클라이언트 tooaccess 컨테이너 tooallow 원하는 경우에 유용 합니다.

ACL은 각 정책에 ID가 연결된 액세스 정책 배열을 사용하여 구현됩니다. 다음 코드 예제는 hello 'user1' 및 'user2'에 대 한 두 개의 정책을 정의 합니다.

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

다음 코드 예제에서는 hello hello에 대 한 현재 ACL **mycontainer**, 다음 사용 하 여 hello 새 정책을 추가 **setBlobAcl**합니다. 이 접근 방식을 통해 다음을 수행할 수 있습니다.

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

한 번 hello ACL이 설정, 만들 수 있습니다는 정책에 대 한 hello ID에 따라 공유 액세스 서명 합니다. 다음 코드 예제는 hello 사용자 '2'에 대 한 새 공유 액세스 서명을 만듭니다.

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a>다음 단계
자세한 내용은 다음 리소스는 hello를 참조 하세요.

* [Node용 Azure Storage SDK API 참조][Node용 Azure Storage SDK API 참조]
* [Azure Storage 팀 블로그][Azure Storage 팀 블로그]
* GitHub의 [Azure Storage SDK for Node][Azure Storage SDK for Node] 리포지토리
* [Node.js 개발자 센터](https://azure.microsoft.com/develop/nodejs/)
* [Hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송 합니다.](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

[Hello Azure 테이블 서비스를 사용 하 여 Node.js 웹 응용 프로그램](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)    
[빌드하고 웹 매트릭스를 사용 하는 Node.js 웹 응용 프로그램 tooAzure 배포]: https://www.microsoft.com/web/webmatrix/  
[REST API를 hello를 사용 하 여]: [Azure 포털] http://msdn.microsoft.com/library/azure/hh264518.aspx: https://portal.azure.com [빌드하고 Node.js 응용 프로그램 tooan Azure 클라우드 서비스 배포](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Azure 저장소 팀 블로그]: http:// [Azure 저장소 노드 API 참조에 대 한 SDK] blogs.msdn.com/b/windowsazurestorage/: http://dl.windowsazure.com/nodestoragedocs/index.html
