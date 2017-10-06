---
title: "iOS에서 Azure Blob 저장소 aaaHow toouse | Microsoft Docs"
description: "Azure Blob 저장소 (개체 저장소)를 사용 하는 hello 클라우드에 구조화 되지 않은 데이터를 저장 합니다."
services: storage
documentationcenter: ios
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: df188021-86fc-4d31-a810-1b0e7bcd814b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: objective-c
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: cc08b76b682537a9a51e970c76bd76c7c06a4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ios"></a>어떻게 toouse iOS에서 Blob 저장소
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>개요
이 문서에서 그 방법을 보여줍니다 Microsoft Azure Blob 저장소를 사용 하 여 tooperform 일반적인 시나리오입니다. hello 샘플 Objective-c 작성 되 고 hello를 사용 하 여 [iOS에 대 한 Azure 저장소 클라이언트 라이브러리](https://github.com/Azure/azure-storage-ios)합니다. hello 가이드에서 다루는 시나리오 포함 **업로드**, **나열**, **다운로드**, 및 **삭제** blob입니다. Blob에 대 한 자세한 내용은 참조 hello [다음 단계](#next-steps) 섹션. Hello를 다운로드할 수도 있습니다 [샘플 응용 프로그램](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly 참조 hello iOS 응용 프로그램에서 Azure 저장소를 사용 합니다.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a>응용 프로그램에 hello Azure 저장소 iOS 라이브러리 가져오기
라이브러리 가져올 수 있습니다 hello Azure 저장소 iOS 응용 프로그램에 hello를 사용 하 여 [Azure 저장소 CocoaPod](https://cocoapods.org/pods/AZSClient) 또는 hello를 가져와서 **프레임 워크** 파일입니다. 그러나 CocoaPod는 hello 통합 hello 라이브러리 hello 프레임 워크 파일에서 가져올 낮습니다 기존 프로젝트에 보다 쉽게 채택할 방법을 권장 합니다.

toouse 다음 hello 해야이 라이브러리:
- iOS 8+
- Xcode 7+

## <a name="cocoapod"></a>CocoaPod
1. 아직 그렇게 하지 않은 경우 [설치 CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) 터미널 윈도우를 열고 다음 명령을 hello를 실행 하 여 컴퓨터에
    
    ```shell   
    sudo gem install cocoapods
    ```

2. 다음으로 hello 프로젝트 디렉터리 (.xcodeproj 파일을 포함 하는 hello 디렉터리)에 새 파일을 만들 _Podfile_(파일 확장명 없음). Hello too_Podfile_ 다음을 추가 하 고 저장 합니다.

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. Hello 터미널 창에서 다음 명령이 실행된 hello 및 toohello 프로젝트 디렉터리 이동

    ```shell    
    pod install
    ```

4. Xcode에서 .xcodeproj가 열려 있으면 닫습니다. 프로젝트 디렉터리 열기 hello 새로 만든 프로젝트 파일의 hello.xcworkspace 확장명입니다. 작업 합니다에 대 한 이제에 hello 파일입니다.

## <a name="framework"></a>프레임워크
수동으로 toouse hello 라이브러리는 toobuild hello 프레임 워크는 다른 방법으로 hello:

1. 첫 번째, 다운로드 또는 복제 hello [azure-저장소-ios 리포지토리](https://github.com/azure/azure-storage-ios)합니다.
2. *azure-storage-ios* -> *Lib* -> *Azure 저장소 클라이언트 라이브러리*로 이동하고 X 코드에서 `AZSClient.xcodeproj`를 엽니다.
3. 왼쪽 위 변경 hello Xcode의 활성 hello에 스키마에서 "Azure 저장소 클라이언트 라이브러리" 너무 "프레임 워크"입니다.
4. (⌘ + B) hello 프로젝트를 빌드하십시오. 그러면 바탕 화면에 `AZSClient.framework` 파일이 만들어집니다.

그런 다음 응용 프로그램에 hello 다음을 수행 하 여 hello 프레임 워크 파일을 가져올 수 있습니다.

1. 새 프로젝트를 만들거나 Xcode에서 기존 프로젝트를 엽니다.
2. 끌어서 놓기 hello `AZSClient.framework` Xcode 프로젝트 탐색기에 있습니다.
3. *필요한 경우 항목 복사*를 선택하고 *마침*을 클릭합니다.
4. Hello 왼쪽 탐색 창에서 프로젝트를 클릭 하 고 hello 클릭 *일반* hello 위쪽 hello 프로젝트 편집기의 탭 합니다.
5. Hello에서 *Linked Frameworks and Libraries* 섹션에서 hello 추가 (+) 단추를 클릭 합니다.
6. Hello 이미 제공 하는 라이브러리 목록에서 검색할 `libxml2.2.tbd` tooyour 프로젝트에 추가 합니다.

## <a name="import-hello-library"></a>Hello 라이브러리 가져오기 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

Swift를 사용 하는 경우 toocreate 브리징 헤더 필요 하 고 있는 < AZSClient/AZSClient.h > 가져온 합니다.

1. 헤더 파일 만들기 `Bridging-Header.h`, hello 위에 import 문 추가 합니다.
2. Toohello 이동 *빌드 설정* 탭을 검색할 *Objective-c 브리징 헤더*합니다.
3. hello 필드에 두 번 클릭 *Objective-c 브리징 헤더* hello 경로 tooyour 헤더 파일을 추가 합니다.`ProjectName/Bridging-Header.h`
4. Xcode에서 브리징 헤더 hello 빌드 hello 프로젝트 (⌘ + B) tooverify 선택 되었습니다.
5. Hello 라이브러리를 사용 하 여 모든 Swift 파일에서 직접 시작, 가져오기 문에 대 한 필요가 없습니다.

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a>비동기 작업
> [!NOTE]
> Hello 서비스에 대 한 요청을 수행 하는 모든 메서드는 비동기 작업입니다. Hello 코드 샘플에서 이러한 메서드는 완료 처리기를 찾을 수 있습니다. Hello 완료 처리기 내 코드가 실행 되는 **후** hello 요청을 완료 합니다. Hello 완료 처리기가 실행 한 후 코드 **동안** hello 요청 합니다.
> 
> 

## <a name="create-a-container"></a>컨테이너 만들기
Azure 저장소의 모든 Blob는 컨테이너에 있어야 합니다. hello 다음 예제에서는 호출 방법을 보여 줍니다 toocreate 컨테이너 *newcontainer*, 존재 하지 않는 경우 저장소 계정에 있습니다. 컨테이너 이름의 선택할 때는 hello 명명 위에서 언급 한 규칙에 주의 해야 합니다.

```objc
-(void)createContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"newcontainer"];

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithCompletionHandler:^(NSError *error, BOOL exists) {
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

Hello 확인 하 여 작동 하는지 확인할 수 있습니다 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com) 인지 확인 하 고 *newcontainer* hello 저장소 계정에 대 한 컨테이너의 변수 목록입니다.

## <a name="set-container-permissions"></a>컨테이너 사용 권한 설정
기본적으로 컨테이너의 사용 권한은 **개인** 액세스용으로 구성됩니다. 그러나 컨테이너는 컨테이너 액세스에 대한 몇 가지 다른 옵션을 제공합니다.

* **개인**: hello 계정 소유자만 컨테이너 및 blob 데이터를 읽을 수 있습니다.
* **Blob**: 이 컨테이너 내의 Blob 데이터는 익명 요청을 통해 읽을 수 있으나 컨테이너 데이터는 읽을 수 없습니다. 클라이언트는 익명 요청을 통해 hello 컨테이너 내 blob를 열거할 수 없습니다.
* **컨테이너**: 익명 요청을 통해 컨테이너와 Blob 데이터를 읽을 수 있습니다. 클라이언트가 익명 요청을 통해 hello 컨테이너 내 blob를 열거할 수 있지만 hello 저장소 계정 내 컨테이너는 열거할 수 없습니다.

hello 다음 예제에서는 방법을 보여 줍니다가 있는 컨테이너는 toocreate **컨테이너** 액세스 권한 hello 인터넷에 있는 모든 사용자에 대 한 공용 읽기 전용 액세스를 허용 합니다.

```objc
-(void)createContainerWithPublicAccess{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists){
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

## <a name="upload-a-blob-into-a-container"></a>컨테이너에 Blob 업로드
Hello에 설명 된 대로 [Blob 서비스 개념](#blob-service-concepts) 섹션, Blob 저장소에서는 세 가지 유형의 blob: 블록 blob, 추가 blob 및 페이지 blob입니다. hello Azure 저장소 iOS 라이브러리는 세 가지 유형의 blob 모두 지원합니다. 대부분의 경우에서 블록 blob는 형식 toouse 권장 hello를 사용 합니다.

다음 예제는 hello는 NSString에서 tooupload 블록 blob 하는 방법을 보여 줍니다. 경우 이름이 같은이 컨테이너에 이미 있습니다. hello로 blob이이 blob의 hello 내용은 덮어씁니다.

```objc
-(void)uploadBlobToContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists)
        {
            if (error){
                NSLog(@"Error in creating container.");
            }
            else{
                // Create a local blob object
                AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

                // Upload blob tooStorage
                [blockBlob uploadFromText:@"This text will be uploaded tooBlob Storage." completionHandler:^(NSError *error) {
                    if (error){
                        NSLog(@"Error in creating blob.");
                    }
                }];
            }
        }];
}
```

Hello 확인 하 여 작동 하는지 확인할 수 있습니다 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com) 해당 hello 컨테이너를 확인 하 고 *containerpublic*, hello blob이 포함 된 *sampleblob*. 이 샘플에서는이 응용 프로그램 이동 toohello blob URI에서 작동 하는지 확인할 수 있도록 공용 컨테이너 사용:

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

또한 블록 blob는 NSString toouploading 유사한 가지가 NSData, NSInputStream, 또는 로컬 파일에 대 한 있습니다.

## <a name="list-hello-blobs-in-a-container"></a>컨테이너에서 hello blob 나열
hello 다음 예제에서는 toolist 모든 컨테이너에 blob 하는 방법 이 작업을 수행할 때는 hello 매개 변수 뒤에 주의 해야 합니다.     

* **continuationToken** -hello hello 나열 작업에서 시작 해야 할 연속 토큰을 나타냅니다. 없는 토큰을 지정 하는 경우에 hello 처음부터 blob를 나열 합니다. 최대 설정 tooa 0에서 blob 개수에 관계 없이 나열할 수 있습니다. 이 메서드는 경우 빈 결과 반환 하는 경우에 `results.continuationToken` 가, nil이 아닌 hello 서비스에 나열 되지 않은 blob이 더 이상 있을 수 있습니다.
* **접두사** -blob 목록에 대 한 접두사 toouse hello를 지정할 수 있습니다. 이 접두사로 시작하는 Blob만 나열됩니다.
* **useFlatBlobListing** hello에 설명 된 대로- [이름 지정 및 참조 하는 컨테이너 및 blob](#naming-and-referencing-containers-and-blobs) 섹션 hello Blob 서비스는 플랫 저장소 스키마를 만들 수 있습니다는 가상 계층 경로 사용 하 여 blob 이름을 지정 하 여 정보입니다. 그러나 현재는 플랫이 아닌 목록은 지원되지 않습니다. 이 기능은 곧 제공됩니다. 현재 이 값은 **YES**여야 합니다.
* **blobListingDetails** -blob을 나열 하는 경우에 어떤 항목 tooinclude을 지정할 수 있습니다
  * _AZSBlobListingDetailsNone_: 커밋된 Blob만 나열하고 Blob 메타데이터는 반환하지 않습니다.
  * _AZSBlobListingDetailsSnapshots_: 커밋된 Blob과 Blob 스냅숏을 나열합니다.
  * _AZSBlobListingDetailsMetadata_: hello 목록에 각 blob에 대 한 메타 데이터를 검색할 blob를 반환 합니다.
  * _AZSBlobListingDetailsUncommittedBlobs_: 커밋된 Blob과 커밋되지 않은 Blob을 나열합니다.
  * _AZSBlobListingDetailsCopy_: 복사본 포함 hello 목록에는 속성입니다.
  * _AZSBlobListingDetailsAll_: 사용 가능한 커밋된 Blob, 커밋되지 않은 Blob 및 스냅숏을 모두 나열하고 해당 Blob의 메타데이터와 복사 상태를 모두 반환합니다.
* **maxResults** -hello 결과 tooreturn이이 작업에 대 한 최대 수입니다. -1 사용 하 여 toonot 제한을 설정 합니다.
* **completionHandler** -hello 나열 작업의 hello 결과 함께 코드 tooexecute hello 블록입니다.

이 예제에서는 도우미 메서드는 연속 토큰이 반환 될 때마다 사용 되는 toorecursively 호출 hello 목록 blob 메서드입니다.

```objc
-(void)listBlobsInContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    //List all blobs in container
    [self listBlobsInContainerHelper:blobContainer continuationToken:nil prefix:nil blobListingDetails:AZSBlobListingDetailsAll maxResults:-1 completionHandler:^(NSError *error) {
        if (error != nil){
            NSLog(@"Error in creating container.");
        }
    }];
}

//List blobs helper method
-(void)listBlobsInContainerHelper:(AZSCloudBlobContainer *)container continuationToken:(AZSContinuationToken *)continuationToken prefix:(NSString *)prefix blobListingDetails:(AZSBlobListingDetails)blobListingDetails maxResults:(NSUInteger)maxResults completionHandler:(void (^)(NSError *))completionHandler
{
    [container listBlobsSegmentedWithContinuationToken:continuationToken prefix:prefix useFlatBlobListing:YES blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:^(NSError *error, AZSBlobResultSegment *results) {
        if (error)
        {
            completionHandler(error);
        }
        else
        {
            for (int i = 0; i < results.blobs.count; i++) {
                NSLog(@"%@",[(AZSCloudBlockBlob *)results.blobs[i] blobName]);
            }
            if (results.continuationToken)
            {
                [self listBlobsInContainerHelper:container continuationToken:results.continuationToken prefix:prefix blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:completionHandler];
            }
            else
            {
                completionHandler(nil);
            }
        }
    }];
}
```

## <a name="download-a-blob"></a>Blob 다운로드
hello 방법을 예제와 다음 toodownload blob tooa NSString 개체입니다.

```objc
-(void)downloadBlobToString{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

    // Download blob
    [blockBlob downloadToTextWithCompletionHandler:^(NSError *error, NSString *text) {
        if (error) {
            NSLog(@"Error in downloading blob");
        }
        else{
            NSLog(@"%@",text);
        }
    }];
}
```

## <a name="delete-a-blob"></a>Blob 삭제
hello 방법을 예제와 다음 toodelete blob입니다.

```objc
-(void)deleteBlob{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob1"];

    // Delete blob
    [blockBlob deleteWithCompletionHandler:^(NSError *error) {
        if (error) {
            NSLog(@"Error in deleting blob.");
        }
    }];
}
```

## <a name="delete-a-blob-container"></a>Blob 컨테이너 삭제
hello 방법을 예제와 다음 toodelete 컨테이너입니다.

```objc
-(void)deleteContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Delete container
    [blobContainer deleteContainerIfExistsWithCompletionHandler:^(NSError *error, BOOL success) {
        if(error){
            NSLog(@"Error in deleting container");
        }
    }];
}
```

## <a name="next-steps"></a>다음 단계
지금까지 학습 했으므로 어떻게 iOS에서 Blob 저장소 toouse 이러한 링크 toolearn hello iOS 라이브러리에 대 한 자세한 따르고 hello 저장소 서비스 합니다.

* [iOS용 Azure 저장소 클라이언트 라이브러리](https://github.com/azure/azure-storage-ios)
* [Azure Storage iOS 참조 설명서](http://azure.github.io/azure-storage-ios/)
* [Azure 저장소 서비스 REST API](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage)

이 라이브러리에 대 한 질문이 있으면 느껴집니다 무료 toopost tooour [Azure MSDN 포럼](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) 또는 [스택 오버플로](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files)합니다.
Azure 저장소에 대 한 제안을 설정한 경우 게시 하세요 너무[Azure 저장소 피드백](https://feedback.azure.com/forums/217298-storage/)합니다.

