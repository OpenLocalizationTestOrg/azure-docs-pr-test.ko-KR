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
ms.openlocfilehash: 474c4263a4bfbd61bfa39e4fdb01ddd9c3829c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ios"></a><span data-ttu-id="2bfbc-103">어떻게 toouse iOS에서 Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="2bfbc-103">How toouse Blob storage from iOS</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="2bfbc-104">개요</span><span class="sxs-lookup"><span data-stu-id="2bfbc-104">Overview</span></span>
<span data-ttu-id="2bfbc-105">이 문서에서 그 방법을 보여줍니다 Microsoft Azure Blob 저장소를 사용 하 여 tooperform 일반적인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-105">This article will show you how tooperform common scenarios using Microsoft Azure Blob storage.</span></span> <span data-ttu-id="2bfbc-106">hello 샘플 Objective-c 작성 되 고 hello를 사용 하 여 [iOS에 대 한 Azure 저장소 클라이언트 라이브러리](https://github.com/Azure/azure-storage-ios)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-106">hello samples are written in Objective-C and use hello [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span></span> <span data-ttu-id="2bfbc-107">hello 가이드에서 다루는 시나리오 포함 **업로드**, **나열**, **다운로드**, 및 **삭제** blob입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-107">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="2bfbc-108">Blob에 대 한 자세한 내용은 참조 hello [다음 단계](#next-steps) 섹션.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-108">For more information on blobs, see hello [Next Steps](#next-steps) section.</span></span> <span data-ttu-id="2bfbc-109">Hello를 다운로드할 수도 있습니다 [샘플 응용 프로그램](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly 참조 hello iOS 응용 프로그램에서 Azure 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-109">You can also download hello [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly see hello use of Azure Storage in an iOS application.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a><span data-ttu-id="2bfbc-110">응용 프로그램에 hello Azure 저장소 iOS 라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="2bfbc-110">Import hello Azure Storage iOS library into your application</span></span>
<span data-ttu-id="2bfbc-111">라이브러리 가져올 수 있습니다 hello Azure 저장소 iOS 응용 프로그램에 hello를 사용 하 여 [Azure 저장소 CocoaPod](https://cocoapods.org/pods/AZSClient) 또는 hello를 가져와서 **프레임 워크** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-111">You can import hello Azure Storage iOS library into your application either by using hello [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing hello **Framework** file.</span></span> <span data-ttu-id="2bfbc-112">그러나 CocoaPod는 hello 통합 hello 라이브러리 hello 프레임 워크 파일에서 가져올 낮습니다 기존 프로젝트에 보다 쉽게 채택할 방법을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-112">CocoaPod is hello recommended way as it makes integrating hello library easier, however importing from hello framework file is less intrusive for your existing project.</span></span>

<span data-ttu-id="2bfbc-113">toouse 다음 hello 해야이 라이브러리:</span><span class="sxs-lookup"><span data-stu-id="2bfbc-113">toouse this library, you need hello following:</span></span>
- <span data-ttu-id="2bfbc-114">iOS 8+</span><span class="sxs-lookup"><span data-stu-id="2bfbc-114">iOS 8+</span></span>
- <span data-ttu-id="2bfbc-115">Xcode 7+</span><span class="sxs-lookup"><span data-stu-id="2bfbc-115">Xcode 7+</span></span>

## <a name="cocoapod"></a><span data-ttu-id="2bfbc-116">CocoaPod</span><span class="sxs-lookup"><span data-stu-id="2bfbc-116">CocoaPod</span></span>
1. <span data-ttu-id="2bfbc-117">아직 그렇게 하지 않은 경우 [설치 CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) 터미널 윈도우를 열고 다음 명령을 hello를 실행 하 여 컴퓨터에</span><span class="sxs-lookup"><span data-stu-id="2bfbc-117">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running hello following command</span></span>
    
    ```shell   
    sudo gem install cocoapods
    ```

2. <span data-ttu-id="2bfbc-118">다음으로 hello 프로젝트 디렉터리 (.xcodeproj 파일을 포함 하는 hello 디렉터리)에 새 파일을 만들 _Podfile_(파일 확장명 없음).</span><span class="sxs-lookup"><span data-stu-id="2bfbc-118">Next, in hello project directory (hello directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span></span> <span data-ttu-id="2bfbc-119">Hello too_Podfile_ 다음을 추가 하 고 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-119">Add hello following too_Podfile_ and save.</span></span>

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. <span data-ttu-id="2bfbc-120">Hello 터미널 창에서 다음 명령이 실행된 hello 및 toohello 프로젝트 디렉터리 이동</span><span class="sxs-lookup"><span data-stu-id="2bfbc-120">In hello terminal window, navigate toohello project directory and run hello following command</span></span>

    ```shell    
    pod install
    ```

4. <span data-ttu-id="2bfbc-121">Xcode에서 .xcodeproj가 열려 있으면 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-121">If your .xcodeproj is open in Xcode, close it.</span></span> <span data-ttu-id="2bfbc-122">프로젝트 디렉터리 열기 hello 새로 만든 프로젝트 파일의 hello.xcworkspace 확장명입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-122">In your project directory open hello newly created project file which will have hello .xcworkspace extension.</span></span> <span data-ttu-id="2bfbc-123">작업 합니다에 대 한 이제에 hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-123">This is hello file you'll work from for now on.</span></span>

## <a name="framework"></a><span data-ttu-id="2bfbc-124">프레임워크</span><span class="sxs-lookup"><span data-stu-id="2bfbc-124">Framework</span></span>
<span data-ttu-id="2bfbc-125">수동으로 toouse hello 라이브러리는 toobuild hello 프레임 워크는 다른 방법으로 hello:</span><span class="sxs-lookup"><span data-stu-id="2bfbc-125">hello other way toouse hello library is toobuild hello framework manually:</span></span>

1. <span data-ttu-id="2bfbc-126">첫 번째, 다운로드 또는 복제 hello [azure-저장소-ios 리포지토리](https://github.com/azure/azure-storage-ios)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-126">First, download or clone hello [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span></span>
2. <span data-ttu-id="2bfbc-127">*azure-storage-ios* -> *Lib* -> *Azure 저장소 클라이언트 라이브러리*로 이동하고 X 코드에서 `AZSClient.xcodeproj`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-127">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open `AZSClient.xcodeproj` in Xcode.</span></span>
3. <span data-ttu-id="2bfbc-128">왼쪽 위 변경 hello Xcode의 활성 hello에 스키마에서 "Azure 저장소 클라이언트 라이브러리" 너무 "프레임 워크"입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-128">At hello top-left of Xcode, change hello active scheme from "Azure Storage Client Library" too"Framework".</span></span>
4. <span data-ttu-id="2bfbc-129">(⌘ + B) hello 프로젝트를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-129">Build hello project (⌘+B).</span></span> <span data-ttu-id="2bfbc-130">그러면 바탕 화면에 `AZSClient.framework` 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-130">This will create an `AZSClient.framework` file on your Desktop.</span></span>

<span data-ttu-id="2bfbc-131">그런 다음 응용 프로그램에 hello 다음을 수행 하 여 hello 프레임 워크 파일을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-131">You can then import hello framework file into your application by doing hello following:</span></span>

1. <span data-ttu-id="2bfbc-132">새 프로젝트를 만들거나 Xcode에서 기존 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-132">Create a new project or open up your existing project in Xcode.</span></span>
2. <span data-ttu-id="2bfbc-133">끌어서 놓기 hello `AZSClient.framework` Xcode 프로젝트 탐색기에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-133">Drag and drop hello `AZSClient.framework` into your Xcode project navigator.</span></span>
3. <span data-ttu-id="2bfbc-134">*필요한 경우 항목 복사*를 선택하고 *마침*을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-134">Select *Copy items if needed*, and click on *Finish*.</span></span>
4. <span data-ttu-id="2bfbc-135">Hello 왼쪽 탐색 창에서 프로젝트를 클릭 하 고 hello 클릭 *일반* hello 위쪽 hello 프로젝트 편집기의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-135">Click on your project in hello left-hand navigation and click hello *General* tab at hello top of hello project editor.</span></span>
5. <span data-ttu-id="2bfbc-136">Hello에서 *Linked Frameworks and Libraries* 섹션에서 hello 추가 (+) 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-136">Under hello *Linked Frameworks and Libraries* section, click hello Add button (+).</span></span>
6. <span data-ttu-id="2bfbc-137">Hello 이미 제공 하는 라이브러리 목록에서 검색할 `libxml2.2.tbd` tooyour 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-137">In hello list of libraries already provided, search for `libxml2.2.tbd` and add it tooyour project.</span></span>

## <a name="import-hello-library"></a><span data-ttu-id="2bfbc-138">Hello 라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="2bfbc-138">Import hello Library</span></span> 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

<span data-ttu-id="2bfbc-139">Swift를 사용 하는 경우 toocreate 브리징 헤더 필요 하 고 있는 < AZSClient/AZSClient.h > 가져온 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-139">If you are using Swift, you will need toocreate a bridging header and import <AZSClient/AZSClient.h> there:</span></span>

1. <span data-ttu-id="2bfbc-140">헤더 파일 만들기 `Bridging-Header.h`, hello 위에 import 문 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-140">Create a header file `Bridging-Header.h`, and add hello above import statement.</span></span>
2. <span data-ttu-id="2bfbc-141">Toohello 이동 *빌드 설정* 탭을 검색할 *Objective-c 브리징 헤더*합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-141">Go toohello *Build Settings* tab, and search for *Objective-C Bridging Header*.</span></span>
3. <span data-ttu-id="2bfbc-142">hello 필드에 두 번 클릭 *Objective-c 브리징 헤더* hello 경로 tooyour 헤더 파일을 추가 합니다.`ProjectName/Bridging-Header.h`</span><span class="sxs-lookup"><span data-stu-id="2bfbc-142">Double-click on hello field of *Objective-C Bridging Header* and add hello path tooyour header file: `ProjectName/Bridging-Header.h`</span></span>
4. <span data-ttu-id="2bfbc-143">Xcode에서 브리징 헤더 hello 빌드 hello 프로젝트 (⌘ + B) tooverify 선택 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-143">Build hello project (⌘+B) tooverify that hello bridging header was picked up by Xcode.</span></span>
5. <span data-ttu-id="2bfbc-144">Hello 라이브러리를 사용 하 여 모든 Swift 파일에서 직접 시작, 가져오기 문에 대 한 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-144">Start using hello library directly in any Swift file, there is no need for import statements.</span></span>

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a><span data-ttu-id="2bfbc-145">비동기 작업</span><span class="sxs-lookup"><span data-stu-id="2bfbc-145">Asynchronous Operations</span></span>
> [!NOTE]
> <span data-ttu-id="2bfbc-146">Hello 서비스에 대 한 요청을 수행 하는 모든 메서드는 비동기 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-146">All methods that perform a request against hello service are asynchronous operations.</span></span> <span data-ttu-id="2bfbc-147">Hello 코드 샘플에서 이러한 메서드는 완료 처리기를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-147">In hello code samples, you'll find that these methods have a completion handler.</span></span> <span data-ttu-id="2bfbc-148">Hello 완료 처리기 내 코드가 실행 되는 **후** hello 요청을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-148">Code inside hello completion handler will run **after** hello request is completed.</span></span> <span data-ttu-id="2bfbc-149">Hello 완료 처리기가 실행 한 후 코드 **동안** hello 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-149">Code after hello completion handler will run **while** hello request is being made.</span></span>
> 
> 

## <a name="create-a-container"></a><span data-ttu-id="2bfbc-150">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="2bfbc-150">Create a container</span></span>
<span data-ttu-id="2bfbc-151">Azure 저장소의 모든 Blob는 컨테이너에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-151">Every blob in Azure Storage must reside in a container.</span></span> <span data-ttu-id="2bfbc-152">hello 다음 예제에서는 호출 방법을 보여 줍니다 toocreate 컨테이너 *newcontainer*, 존재 하지 않는 경우 저장소 계정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-152">hello following example shows how toocreate a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span></span> <span data-ttu-id="2bfbc-153">컨테이너 이름의 선택할 때는 hello 명명 위에서 언급 한 규칙에 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-153">When choosing a name for your container, be mindful of hello naming rules mentioned above.</span></span>

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

<span data-ttu-id="2bfbc-154">Hello 확인 하 여 작동 하는지 확인할 수 있습니다 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com) 인지 확인 하 고 *newcontainer* hello 저장소 계정에 대 한 컨테이너의 변수 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-154">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in hello list of containers for your Storage account.</span></span>

## <a name="set-container-permissions"></a><span data-ttu-id="2bfbc-155">컨테이너 사용 권한 설정</span><span class="sxs-lookup"><span data-stu-id="2bfbc-155">Set Container Permissions</span></span>
<span data-ttu-id="2bfbc-156">기본적으로 컨테이너의 사용 권한은 **개인** 액세스용으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-156">A container's permissions are configured for **Private** access by default.</span></span> <span data-ttu-id="2bfbc-157">그러나 컨테이너는 컨테이너 액세스에 대한 몇 가지 다른 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-157">However, containers provide a few different options for container access:</span></span>

* <span data-ttu-id="2bfbc-158">**개인**: hello 계정 소유자만 컨테이너 및 blob 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-158">**Private**: Container and blob data can be read by hello account owner only.</span></span>
* <span data-ttu-id="2bfbc-159">**Blob**: 이 컨테이너 내의 Blob 데이터는 익명 요청을 통해 읽을 수 있으나 컨테이너 데이터는 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-159">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="2bfbc-160">클라이언트는 익명 요청을 통해 hello 컨테이너 내 blob를 열거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-160">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="2bfbc-161">**컨테이너**: 익명 요청을 통해 컨테이너와 Blob 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-161">**Container**: Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="2bfbc-162">클라이언트가 익명 요청을 통해 hello 컨테이너 내 blob를 열거할 수 있지만 hello 저장소 계정 내 컨테이너는 열거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-162">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="2bfbc-163">hello 다음 예제에서는 방법을 보여 줍니다가 있는 컨테이너는 toocreate **컨테이너** 액세스 권한 hello 인터넷에 있는 모든 사용자에 대 한 공용 읽기 전용 액세스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-163">hello following example shows you how toocreate a container with **Container** access permissions, which will allow public, read-only access for all users on hello Internet:</span></span>

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

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="2bfbc-164">컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="2bfbc-164">Upload a blob into a container</span></span>
<span data-ttu-id="2bfbc-165">Hello에 설명 된 대로 [Blob 서비스 개념](#blob-service-concepts) 섹션, Blob 저장소에서는 세 가지 유형의 blob: 블록 blob, 추가 blob 및 페이지 blob입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-165">As mentioned in hello [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span></span> <span data-ttu-id="2bfbc-166">hello Azure 저장소 iOS 라이브러리는 세 가지 유형의 blob 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-166">hello Azure Storage iOS library supports all three types of blobs.</span></span> <span data-ttu-id="2bfbc-167">대부분의 경우에서 블록 blob는 형식 toouse 권장 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-167">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="2bfbc-168">다음 예제는 hello는 NSString에서 tooupload 블록 blob 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-168">hello following example shows how tooupload a block blob from an NSString.</span></span> <span data-ttu-id="2bfbc-169">경우 이름이 같은이 컨테이너에 이미 있습니다. hello로 blob이이 blob의 hello 내용은 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-169">If a blob with hello same name already exists in this container, hello contents of this blob will be overwritten.</span></span>

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

<span data-ttu-id="2bfbc-170">Hello 확인 하 여 작동 하는지 확인할 수 있습니다 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com) 해당 hello 컨테이너를 확인 하 고 *containerpublic*, hello blob이 포함 된 *sampleblob*.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-170">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that hello container, *containerpublic*, contains hello blob, *sampleblob*.</span></span> <span data-ttu-id="2bfbc-171">이 샘플에서는이 응용 프로그램 이동 toohello blob URI에서 작동 하는지 확인할 수 있도록 공용 컨테이너 사용:</span><span class="sxs-lookup"><span data-stu-id="2bfbc-171">In this sample, we used a public container so you can also verify that this application worked by going toohello blobs URI:</span></span>

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

<span data-ttu-id="2bfbc-172">또한 블록 blob는 NSString toouploading 유사한 가지가 NSData, NSInputStream, 또는 로컬 파일에 대 한 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-172">In addition toouploading a block blob from an NSString, similar methods exist for NSData, NSInputStream, or a local file.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="2bfbc-173">컨테이너에서 hello blob 나열</span><span class="sxs-lookup"><span data-stu-id="2bfbc-173">List hello blobs in a container</span></span>
<span data-ttu-id="2bfbc-174">hello 다음 예제에서는 toolist 모든 컨테이너에 blob 하는 방법</span><span class="sxs-lookup"><span data-stu-id="2bfbc-174">hello following example shows how toolist all blobs in a container.</span></span> <span data-ttu-id="2bfbc-175">이 작업을 수행할 때는 hello 매개 변수 뒤에 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-175">When performing this operation, be mindful of hello following parameters:</span></span>     

* <span data-ttu-id="2bfbc-176">**continuationToken** -hello hello 나열 작업에서 시작 해야 할 연속 토큰을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-176">**continuationToken** - hello continuation token represents where hello listing operation should start.</span></span> <span data-ttu-id="2bfbc-177">없는 토큰을 지정 하는 경우에 hello 처음부터 blob를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-177">If no token is provided, it will list blobs from hello beginning.</span></span> <span data-ttu-id="2bfbc-178">최대 설정 tooa 0에서 blob 개수에 관계 없이 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-178">Any number of blobs can be listed, from zero up tooa set maximum.</span></span> <span data-ttu-id="2bfbc-179">이 메서드는 경우 빈 결과 반환 하는 경우에 `results.continuationToken` 가, nil이 아닌 hello 서비스에 나열 되지 않은 blob이 더 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-179">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on hello service that have not been listed.</span></span>
* <span data-ttu-id="2bfbc-180">**접두사** -blob 목록에 대 한 접두사 toouse hello를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-180">**prefix** - You can specify hello prefix toouse for blob listing.</span></span> <span data-ttu-id="2bfbc-181">이 접두사로 시작하는 Blob만 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-181">Only blobs that begin with this prefix will be listed.</span></span>
* <span data-ttu-id="2bfbc-182">**useFlatBlobListing** hello에 설명 된 대로- [이름 지정 및 참조 하는 컨테이너 및 blob](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) 섹션 hello Blob 서비스는 플랫 저장소 스키마를 만들 수 있습니다는 가상 계층 경로 사용 하 여 blob 이름을 지정 하 여 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-182">**useFlatBlobListing** - As mentioned in hello [Naming and referencing containers and blobs](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) section, although hello Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span></span> <span data-ttu-id="2bfbc-183">그러나 현재는 플랫이 아닌 목록은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-183">However, non-flat listing is currently not supported.</span></span> <span data-ttu-id="2bfbc-184">이 기능은 곧 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-184">This feature is coming soon.</span></span> <span data-ttu-id="2bfbc-185">현재 이 값은 **YES**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-185">For now, this value should be **YES**.</span></span>

* <span data-ttu-id="2bfbc-186">**blobListingDetails** -blob을 나열 하는 경우에 어떤 항목 tooinclude을 지정할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="2bfbc-186">**blobListingDetails** - You can specify which items tooinclude when listing blobs</span></span>
  * <span data-ttu-id="2bfbc-187">_AZSBlobListingDetailsNone_: 커밋된 Blob만 나열하고 Blob 메타데이터는 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-187">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span></span>
  * <span data-ttu-id="2bfbc-188">_AZSBlobListingDetailsSnapshots_: 커밋된 Blob과 Blob 스냅숏을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-188">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span></span>
  * <span data-ttu-id="2bfbc-189">_AZSBlobListingDetailsMetadata_: hello 목록에 각 blob에 대 한 메타 데이터를 검색할 blob를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-189">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in hello listing.</span></span>
  * <span data-ttu-id="2bfbc-190">_AZSBlobListingDetailsUncommittedBlobs_: 커밋된 Blob과 커밋되지 않은 Blob을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-190">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span></span>
  * <span data-ttu-id="2bfbc-191">_AZSBlobListingDetailsCopy_: 복사본 포함 hello 목록에는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-191">_AZSBlobListingDetailsCopy_: Include copy properties in hello listing.</span></span>
  * <span data-ttu-id="2bfbc-192">_AZSBlobListingDetailsAll_: 사용 가능한 커밋된 Blob, 커밋되지 않은 Blob 및 스냅숏을 모두 나열하고 해당 Blob의 메타데이터와 복사 상태를 모두 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-192">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span></span>
* <span data-ttu-id="2bfbc-193">**maxResults** -hello 결과 tooreturn이이 작업에 대 한 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-193">**maxResults** - hello maximum number of results tooreturn for this operation.</span></span> <span data-ttu-id="2bfbc-194">-1 사용 하 여 toonot 제한을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-194">Use -1 toonot set a limit.</span></span>
* <span data-ttu-id="2bfbc-195">**completionHandler** -hello 나열 작업의 hello 결과 함께 코드 tooexecute hello 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-195">**completionHandler** - hello block of code tooexecute with hello results of hello listing operation.</span></span>

<span data-ttu-id="2bfbc-196">이 예제에서는 도우미 메서드는 연속 토큰이 반환 될 때마다 사용 되는 toorecursively 호출 hello 목록 blob 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-196">In this example, a helper method is used toorecursively call hello list blobs method every time a continuation token is returned.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="2bfbc-197">Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="2bfbc-197">Download a blob</span></span>
<span data-ttu-id="2bfbc-198">hello 방법을 예제와 다음 toodownload blob tooa NSString 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-198">hello following example shows how toodownload a blob tooa NSString object.</span></span>

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

## <a name="delete-a-blob"></a><span data-ttu-id="2bfbc-199">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="2bfbc-199">Delete a blob</span></span>
<span data-ttu-id="2bfbc-200">hello 방법을 예제와 다음 toodelete blob입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-200">hello following example shows how toodelete a blob.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="2bfbc-201">Blob 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="2bfbc-201">Delete a blob container</span></span>
<span data-ttu-id="2bfbc-202">hello 방법을 예제와 다음 toodelete 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-202">hello following example shows how toodelete a container.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2bfbc-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2bfbc-203">Next steps</span></span>
<span data-ttu-id="2bfbc-204">지금까지 학습 했으므로 어떻게 iOS에서 Blob 저장소 toouse 이러한 링크 toolearn hello iOS 라이브러리에 대 한 자세한 따르고 hello 저장소 서비스 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-204">Now that you've learned how toouse Blob Storage from iOS, follow these links toolearn more about hello iOS library and hello Storage service.</span></span>

* [<span data-ttu-id="2bfbc-205">iOS용 Azure 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="2bfbc-205">Azure Storage Client Library for iOS</span></span>](https://github.com/azure/azure-storage-ios)
* [<span data-ttu-id="2bfbc-206">Azure Storage iOS 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="2bfbc-206">Azure Storage iOS Reference Documentation</span></span>](http://azure.github.io/azure-storage-ios/)
* [<span data-ttu-id="2bfbc-207">Azure 저장소 서비스 REST API</span><span class="sxs-lookup"><span data-stu-id="2bfbc-207">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="2bfbc-208">Azure 저장소 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="2bfbc-208">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage)

<span data-ttu-id="2bfbc-209">이 라이브러리에 대 한 질문이 있으면 느껴집니다 무료 toopost tooour [Azure MSDN 포럼](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) 또는 [스택 오버플로](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-209">If you have questions regarding this library, feel free toopost tooour [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span></span>
<span data-ttu-id="2bfbc-210">Azure 저장소에 대 한 제안을 설정한 경우 게시 하세요 너무[Azure 저장소 피드백](https://feedback.azure.com/forums/217298-storage/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfbc-210">If you have feature suggestions for Azure Storage, please post too[Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span></span>

