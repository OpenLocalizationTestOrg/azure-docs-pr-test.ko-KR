---
title: "iOS에서 Azure Blob Storage를 사용하는 방법 | Microsoft Docs"
description: "Azure Blob 저장소(개체 저장소)를 사용하여 클라우드에 구조화되지 않은 데이터를 저장합니다."
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
ms.openlocfilehash: cb2810636c8c23dbd476dc2adf58b17d1887d575
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-blob-storage-from-ios"></a><span data-ttu-id="8ace9-103">iOS에서 Blob 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="8ace9-103">How to use Blob storage from iOS</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="8ace9-104">개요</span><span class="sxs-lookup"><span data-stu-id="8ace9-104">Overview</span></span>
<span data-ttu-id="8ace9-105">이 문서에서는 Microsoft Azure Blob 저장소를 사용하여 일반 시나리오를 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-105">This article will show you how to perform common scenarios using Microsoft Azure Blob storage.</span></span> <span data-ttu-id="8ace9-106">샘플은 Objective-C로 작성되었으며 [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-106">The samples are written in Objective-C and use the [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span></span> <span data-ttu-id="8ace9-107">여기서 다루는 시나리오에는 Blob **업로드**, **나열**, **다운로드** 및 **삭제**가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-107">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="8ace9-108">Blob에 대한 자세한 내용은 [다음 단계](#next-steps) 섹션을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="8ace9-108">For more information on blobs, see the [Next Steps](#next-steps) section.</span></span> <span data-ttu-id="8ace9-109">또한 [샘플 앱](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample)을 다운로드하여 iOS 응용 프로그램에서 Azure 저장소의 사용을 신속하게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-109">You can also download the [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) to quickly see the use of Azure Storage in an iOS application.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="import-the-azure-storage-ios-library-into-your-application"></a><span data-ttu-id="8ace9-110">Azure 저장소 iOS 라이브러리를 응용 프로그램으로 가져오기</span><span class="sxs-lookup"><span data-stu-id="8ace9-110">Import the Azure Storage iOS library into your application</span></span>
<span data-ttu-id="8ace9-111">[Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient)를 사용하거나 **프레임워크** 파일을 가져와 Azure Storage iOS 라이브러리를 응용 프로그램으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-111">You can import the Azure Storage iOS library into your application either by using the [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing the **Framework** file.</span></span> <span data-ttu-id="8ace9-112">CocoaPod는 라이브러리를 손쉽게 통합하는 반면, 프레임워크 파일에서 가져오기는 기존 프로젝트에 대해 덜 침입적이기 때문에 권장되는 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-112">CocoaPod is the recommended way as it makes integrating the library easier, however importing from the framework file is less intrusive for your existing project.</span></span>

<span data-ttu-id="8ace9-113">이 라이브러리를 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-113">To use this library, you need the following:</span></span>
- <span data-ttu-id="8ace9-114">iOS 8+</span><span class="sxs-lookup"><span data-stu-id="8ace9-114">iOS 8+</span></span>
- <span data-ttu-id="8ace9-115">Xcode 7+</span><span class="sxs-lookup"><span data-stu-id="8ace9-115">Xcode 7+</span></span>

## <a name="cocoapod"></a><span data-ttu-id="8ace9-116">CocoaPod</span><span class="sxs-lookup"><span data-stu-id="8ace9-116">CocoaPod</span></span>
1. <span data-ttu-id="8ace9-117">컴퓨터에 [CocoaPod](https://guides.cocoapods.org/using/getting-started.html#toc_3)를 아직 설치하지 않은 경우 터미널 창을 열고 다음 명령을 실행하여 컴퓨터에 이 프로그램을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-117">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running the following command</span></span>
    
    ```shell   
    sudo gem install cocoapods
    ```

2. <span data-ttu-id="8ace9-118">그런 다음 프로젝트 디렉터리(.xcodeproj 파일이 포함된 디렉터리)에서 _Podfile_(파일 확장명 없음)이라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-118">Next, in the project directory (the directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span></span> <span data-ttu-id="8ace9-119">_Podfile_에 다음을 추가한 후 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-119">Add the following to _Podfile_ and save.</span></span>

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. <span data-ttu-id="8ace9-120">터미널 창에서 프로젝트 디렉터리로 이동하고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-120">In the terminal window, navigate to the project directory and run the following command</span></span>

    ```shell    
    pod install
    ```

4. <span data-ttu-id="8ace9-121">Xcode에서 .xcodeproj가 열려 있으면 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-121">If your .xcodeproj is open in Xcode, close it.</span></span> <span data-ttu-id="8ace9-122">프로젝트 디렉터리에서 확장명이 .xcworkspace인 새로 만든 프로젝트 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-122">In your project directory open the newly created project file which will have the .xcworkspace extension.</span></span> <span data-ttu-id="8ace9-123">지금부터 이 파일로 작업하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-123">This is the file you'll work from for now on.</span></span>

## <a name="framework"></a><span data-ttu-id="8ace9-124">프레임워크</span><span class="sxs-lookup"><span data-stu-id="8ace9-124">Framework</span></span>
<span data-ttu-id="8ace9-125">라이브러리를 사용하는 다른 방법은 프레임워크를 수동으로 빌드하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-125">The other way to use the library is to build the framework manually:</span></span>

1. <span data-ttu-id="8ace9-126">먼저, [azure-storage-ios repo](https://github.com/azure/azure-storage-ios)를 다운로드하거나 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-126">First, download or clone the [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span></span>
2. <span data-ttu-id="8ace9-127">*azure-storage-ios* -> *Lib* -> *Azure 저장소 클라이언트 라이브러리*로 이동하고 X 코드에서 `AZSClient.xcodeproj`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-127">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open `AZSClient.xcodeproj` in Xcode.</span></span>
3. <span data-ttu-id="8ace9-128">Xcode의 왼쪽 위에서 "Azure 저장소 클라이언트 라이브러리"의 활성 구성표를 "프레임워크"로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-128">At the top-left of Xcode, change the active scheme from "Azure Storage Client Library" to "Framework".</span></span>
4. <span data-ttu-id="8ace9-129">프로젝트를 빌드합니다(⌘+B).</span><span class="sxs-lookup"><span data-stu-id="8ace9-129">Build the project (⌘+B).</span></span> <span data-ttu-id="8ace9-130">그러면 바탕 화면에 `AZSClient.framework` 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-130">This will create an `AZSClient.framework` file on your Desktop.</span></span>

<span data-ttu-id="8ace9-131">그런 후 다음을 수행하여 프레임워크 파일을 응용 프로그램으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-131">You can then import the framework file into your application by doing the following:</span></span>

1. <span data-ttu-id="8ace9-132">새 프로젝트를 만들거나 Xcode에서 기존 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-132">Create a new project or open up your existing project in Xcode.</span></span>
2. <span data-ttu-id="8ace9-133">`AZSClient.framework`를 Xcode 프로젝트 탐색기에 끌어다 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-133">Drag and drop the `AZSClient.framework` into your Xcode project navigator.</span></span>
3. <span data-ttu-id="8ace9-134">*필요한 경우 항목 복사*를 선택하고 *마침*을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-134">Select *Copy items if needed*, and click on *Finish*.</span></span>
4. <span data-ttu-id="8ace9-135">왼쪽의 탐색에서 프로젝트를 클릭하고 프로젝트 편집기의 위에서 *일반* 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-135">Click on your project in the left-hand navigation and click the *General* tab at the top of the project editor.</span></span>
5. <span data-ttu-id="8ace9-136">*연결된 프레임워크 및 라이브러리* 섹션 아래에서 추가 단추 (+)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-136">Under the *Linked Frameworks and Libraries* section, click the Add button (+).</span></span>
6. <span data-ttu-id="8ace9-137">이미 제공된 라이브러리 목록에서 `libxml2.2.tbd`를 검색하고 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-137">In the list of libraries already provided, search for `libxml2.2.tbd` and add it to your project.</span></span>

## <a name="import-the-library"></a><span data-ttu-id="8ace9-138">라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="8ace9-138">Import the Library</span></span> 
```objc
// Include the following import statement to use blob APIs.
#import <AZSClient/AZSClient.h>
```

<span data-ttu-id="8ace9-139">Swift를 사용하는 경우에 브리징 헤더를 만들고 <AZSClient/AZSClient.h>를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-139">If you are using Swift, you will need to create a bridging header and import <AZSClient/AZSClient.h> there:</span></span>

1. <span data-ttu-id="8ace9-140">헤더 파일 `Bridging-Header.h`를 만들고 위의 import 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-140">Create a header file `Bridging-Header.h`, and add the above import statement.</span></span>
2. <span data-ttu-id="8ace9-141">*빌드 설정* 탭으로 이동하고 *Objective-C 브리징 헤더*를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-141">Go to the *Build Settings* tab, and search for *Objective-C Bridging Header*.</span></span>
3. <span data-ttu-id="8ace9-142">*Objective-C 브리징 헤더*의 필드를 두 번 클릭하고 다음 헤더 파일에 경로를 추가합니다.`ProjectName/Bridging-Header.h`</span><span class="sxs-lookup"><span data-stu-id="8ace9-142">Double-click on the field of *Objective-C Bridging Header* and add the path to your header file: `ProjectName/Bridging-Header.h`</span></span>
4. <span data-ttu-id="8ace9-143">프로젝트(⌘+B)를 빌드하여 Xcode로 브리징 헤더를 받았음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-143">Build the project (⌘+B) to verify that the bridging header was picked up by Xcode.</span></span>
5. <span data-ttu-id="8ace9-144">Swift 파일에서 직접 라이브러리를 사용하여 시작하면 import 문이 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-144">Start using the library directly in any Swift file, there is no need for import statements.</span></span>

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a><span data-ttu-id="8ace9-145">비동기 작업</span><span class="sxs-lookup"><span data-stu-id="8ace9-145">Asynchronous Operations</span></span>
> [!NOTE]
> <span data-ttu-id="8ace9-146">서비스에 대한 요청을 수행하는 모든 메서드는 비동기 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-146">All methods that perform a request against the service are asynchronous operations.</span></span> <span data-ttu-id="8ace9-147">코드 샘플에서 이러한 메서드에는 완료 처리기가 있음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-147">In the code samples, you'll find that these methods have a completion handler.</span></span> <span data-ttu-id="8ace9-148">완료 처리기 내에 있는 코드는 요청이 완료된 **후** 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-148">Code inside the completion handler will run **after** the request is completed.</span></span> <span data-ttu-id="8ace9-149">완료 처리기 이후 코드는 요청이 이루어지는 **동안** 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-149">Code after the completion handler will run **while** the request is being made.</span></span>
> 
> 

## <a name="create-a-container"></a><span data-ttu-id="8ace9-150">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="8ace9-150">Create a container</span></span>
<span data-ttu-id="8ace9-151">Azure 저장소의 모든 Blob는 컨테이너에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-151">Every blob in Azure Storage must reside in a container.</span></span> <span data-ttu-id="8ace9-152">다음 예제에서는 *newcontainer*라는 컨테이너를 저장소 계정에 만드는 방법을 보여 줍니다(아직 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="8ace9-152">The following example shows how to create a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span></span> <span data-ttu-id="8ace9-153">컨테이너에 대한 이름을 선택할 때 위에서 언급한 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-153">When choosing a name for your container, be mindful of the naming rules mentioned above.</span></span>

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

    // Create container in your Storage account if the container doesn't already exist
    [blobContainer createContainerIfNotExistsWithCompletionHandler:^(NSError *error, BOOL exists) {
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

<span data-ttu-id="8ace9-154">[Microsoft Azure Storage Explorer](http://storageexplorer.com)를 확인하고 해당 *newcontainer*가 저장소 계정에 대한 컨테이너 목록에 있는지 확인하여 이 작업을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-154">You can confirm that this works by looking at the [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in the list of containers for your Storage account.</span></span>

## <a name="set-container-permissions"></a><span data-ttu-id="8ace9-155">컨테이너 사용 권한 설정</span><span class="sxs-lookup"><span data-stu-id="8ace9-155">Set Container Permissions</span></span>
<span data-ttu-id="8ace9-156">기본적으로 컨테이너의 사용 권한은 **개인** 액세스용으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-156">A container's permissions are configured for **Private** access by default.</span></span> <span data-ttu-id="8ace9-157">그러나 컨테이너는 컨테이너 액세스에 대한 몇 가지 다른 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-157">However, containers provide a few different options for container access:</span></span>

* <span data-ttu-id="8ace9-158">**개인**: 계정 소유자만 컨테이너 및 Blob 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-158">**Private**: Container and blob data can be read by the account owner only.</span></span>
* <span data-ttu-id="8ace9-159">**Blob**: 이 컨테이너 내의 Blob 데이터는 익명 요청을 통해 읽을 수 있으나 컨테이너 데이터는 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-159">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="8ace9-160">클라이언트는 익명 요청을 통해 컨테이너 내의 Blob을 열거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-160">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="8ace9-161">**컨테이너**: 익명 요청을 통해 컨테이너와 Blob 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-161">**Container**: Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="8ace9-162">클라이언트는 익명 요청을 통해 컨테이너 내에서 Blob을 열거할 수 있지만 저장소 계정 내에서 컨테이너를 열거할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-162">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="8ace9-163">다음 예제에서는 인터넷에서 모든 사용자의 공용, 읽기 전용 액세스를 허용할 **컨테이너** 액세스 권한으로 컨테이너를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-163">The following example shows you how to create a container with **Container** access permissions, which will allow public, read-only access for all users on the Internet:</span></span>

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

    // Create container in your Storage account if the container doesn't already exist
    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists){
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="8ace9-164">컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="8ace9-164">Upload a blob into a container</span></span>
<span data-ttu-id="8ace9-165">[Blob 서비스 개념](#blob-service-concepts) 섹션에서 설명한 것처럼 Blob 저장소는 블록 Blob, 추가 Blob, 페이지 Blob의 서로 다른 Blob 유형을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-165">As mentioned in the [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span></span> <span data-ttu-id="8ace9-166">Azure Storage iOS 라이브러리는 세 가지 형식의 Blob을 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-166">The Azure Storage iOS library supports all three types of blobs.</span></span> <span data-ttu-id="8ace9-167">대부분의 경우에는 블록 Blob을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-167">In most cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="8ace9-168">다음 예제에서는 NSString에서 블록 Blob를 업로드하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-168">The following example shows how to upload a block blob from an NSString.</span></span> <span data-ttu-id="8ace9-169">같은 이름의 Blob가 이 컨테이너에 이미 있는 경우 이 Blob의 내용을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-169">If a blob with the same name already exists in this container, the contents of this blob will be overwritten.</span></span>

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

                // Upload blob to Storage
                [blockBlob uploadFromText:@"This text will be uploaded to Blob Storage." completionHandler:^(NSError *error) {
                    if (error){
                        NSLog(@"Error in creating blob.");
                    }
                }];
            }
        }];
}
```

<span data-ttu-id="8ace9-170">[Microsoft Azure Storage Explorer](http://storageexplorer.com)를 확인하고 컨테이너 *containerpublic*이 Blob *sampleblob*을 포함하는지 확인하여 이 작업을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-170">You can confirm that this works by looking at the [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that the container, *containerpublic*, contains the blob, *sampleblob*.</span></span> <span data-ttu-id="8ace9-171">이 샘플에서는 공용 컨테이너를 사용했으므로 Blob URI로 이동하여 이 응용 프로그램 작업을 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-171">In this sample, we used a public container so you can also verify that this application worked by going to the blobs URI:</span></span>

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

<span data-ttu-id="8ace9-172">NSString에서 블록 Blob을 업로드하는 것 외에도 이와 유사한 메서드가 NSData, NSInputStream 또는 로컬 파일에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-172">In addition to uploading a block blob from an NSString, similar methods exist for NSData, NSInputStream, or a local file.</span></span>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="8ace9-173">컨테이너의 Blob 나열</span><span class="sxs-lookup"><span data-stu-id="8ace9-173">List the blobs in a container</span></span>
<span data-ttu-id="8ace9-174">다음 예제에서는 컨테이너의 모든 Blob를 나열하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-174">The following example shows how to list all blobs in a container.</span></span> <span data-ttu-id="8ace9-175">이 작업을 수행할 때는 다음 매개 변수를 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-175">When performing this operation, be mindful of the following parameters:</span></span>     

* <span data-ttu-id="8ace9-176">**continuationToken** - 연속 토큰은 목록 작업을 시작할 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-176">**continuationToken** - The continuation token represents where the listing operation should start.</span></span> <span data-ttu-id="8ace9-177">토큰이 제공되지 않는 경우 처음부터 Blob를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-177">If no token is provided, it will list blobs from the beginning.</span></span> <span data-ttu-id="8ace9-178">0에서 최대 설정까지 개수에 관계 없이 Blob를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-178">Any number of blobs can be listed, from zero up to a set maximum.</span></span> <span data-ttu-id="8ace9-179">이 메서드가 0개의 결과를 반환하더라도 `results.continuationToken` 이 nil이 아니면 서비스에 나열되지 않은 더 많은 Blob이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-179">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on the service that have not been listed.</span></span>
* <span data-ttu-id="8ace9-180">**prefix** - Blob 목록에 사용할 접두사를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-180">**prefix** - You can specify the prefix to use for blob listing.</span></span> <span data-ttu-id="8ace9-181">이 접두사로 시작하는 Blob만 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-181">Only blobs that begin with this prefix will be listed.</span></span>
* <span data-ttu-id="8ace9-182">**useFlatBlobListing** - [컨테이너 및 Blob 이름 명명 및 참조](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) 섹션에서 설명한 것처럼 Blob 서비스가 플랫 저장소 스키마인 경우에도 경로 정보로 Blob 이름을 지정하여 가상 계층 구조를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-182">**useFlatBlobListing** - As mentioned in the [Naming and referencing containers and blobs](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) section, although the Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span></span> <span data-ttu-id="8ace9-183">그러나 현재는 플랫이 아닌 목록은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-183">However, non-flat listing is currently not supported.</span></span> <span data-ttu-id="8ace9-184">이 기능은 곧 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-184">This feature is coming soon.</span></span> <span data-ttu-id="8ace9-185">현재 이 값은 **YES**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-185">For now, this value should be **YES**.</span></span>

* <span data-ttu-id="8ace9-186">**blobListingDetails** - Blob을 나열할 때 포함할 항목을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-186">**blobListingDetails** - You can specify which items to include when listing blobs</span></span>
  * <span data-ttu-id="8ace9-187">_AZSBlobListingDetailsNone_: 커밋된 Blob만 나열하고 Blob 메타데이터는 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-187">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span></span>
  * <span data-ttu-id="8ace9-188">_AZSBlobListingDetailsSnapshots_: 커밋된 Blob과 Blob 스냅숏을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-188">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span></span>
  * <span data-ttu-id="8ace9-189">_AZSBlobListingDetailsMetadata_: 목록에 반환된 각 Blob에 대한 Blob 메타데이터를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-189">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in the listing.</span></span>
  * <span data-ttu-id="8ace9-190">_AZSBlobListingDetailsUncommittedBlobs_: 커밋된 Blob과 커밋되지 않은 Blob을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-190">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span></span>
  * <span data-ttu-id="8ace9-191">_AZSBlobListingDetailsCopy_: 목록에 복사 속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-191">_AZSBlobListingDetailsCopy_: Include copy properties in the listing.</span></span>
  * <span data-ttu-id="8ace9-192">_AZSBlobListingDetailsAll_: 사용 가능한 커밋된 Blob, 커밋되지 않은 Blob 및 스냅숏을 모두 나열하고 해당 Blob의 메타데이터와 복사 상태를 모두 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-192">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span></span>
* <span data-ttu-id="8ace9-193">**maxResults** - 이 작업에 대해 반환할 결과의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-193">**maxResults** - The maximum number of results to return for this operation.</span></span> <span data-ttu-id="8ace9-194">제한을 설정하지 않으려면 -1을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-194">Use -1 to not set a limit.</span></span>
* <span data-ttu-id="8ace9-195">**completionHandler** - 나열 작업의 결과와 함께 실행할 코드 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-195">**completionHandler** - The block of code to execute with the results of the listing operation.</span></span>

<span data-ttu-id="8ace9-196">이 예제에서는 연속 토큰이 반환될 때마다 나열 Blob 메서드를 재귀적으로 호출하는 데 도우미 메서드가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-196">In this example, a helper method is used to recursively call the list blobs method every time a continuation token is returned.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="8ace9-197">Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="8ace9-197">Download a blob</span></span>
<span data-ttu-id="8ace9-198">다음 예제에서는 NSString 개체로 Blob를 다운로드하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-198">The following example shows how to download a blob to a NSString object.</span></span>

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

## <a name="delete-a-blob"></a><span data-ttu-id="8ace9-199">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="8ace9-199">Delete a blob</span></span>
<span data-ttu-id="8ace9-200">다음 예제에서는 Blob를 삭제하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-200">The following example shows how to delete a blob.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="8ace9-201">Blob 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="8ace9-201">Delete a blob container</span></span>
<span data-ttu-id="8ace9-202">다음 예제에서는 컨테이너를 삭제하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ace9-202">The following example shows how to delete a container.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8ace9-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8ace9-203">Next steps</span></span>
<span data-ttu-id="8ace9-204">지금까지 iOS에서 Blob 저장소를 사용하는 방법을 살펴보았으므로 다음 링크를 따라 이동하여 iOS 라이브러리 및 저장소 서비스에 대한 자세한 내용을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="8ace9-204">Now that you've learned how to use Blob Storage from iOS, follow these links to learn more about the iOS library and the Storage service.</span></span>

* [<span data-ttu-id="8ace9-205">iOS용 Azure 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="8ace9-205">Azure Storage Client Library for iOS</span></span>](https://github.com/azure/azure-storage-ios)
* [<span data-ttu-id="8ace9-206">Azure Storage iOS 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="8ace9-206">Azure Storage iOS Reference Documentation</span></span>](http://azure.github.io/azure-storage-ios/)
* [<span data-ttu-id="8ace9-207">Azure 저장소 서비스 REST API</span><span class="sxs-lookup"><span data-stu-id="8ace9-207">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="8ace9-208">Azure 저장소 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="8ace9-208">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage)

<span data-ttu-id="8ace9-209">이 라이브러리에 대한 문의 사항이 있는 경우 [MSDN Azure 포럼](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) 또는 [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files)에 자유롭게 게시해 주세요.</span><span class="sxs-lookup"><span data-stu-id="8ace9-209">If you have questions regarding this library, feel free to post to our [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span></span>
<span data-ttu-id="8ace9-210">Azure Storage에 대한 기능 제안 사항이 있는 경우 [Azure Storage 피드백](https://feedback.azure.com/forums/217298-storage/)에 게시해 주세요.</span><span class="sxs-lookup"><span data-stu-id="8ace9-210">If you have feature suggestions for Azure Storage, please post to [Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span></span>

