---
title: "Ruby에서 Blob Storage(개체 저장소)를 사용하는 방법 | Microsoft Docs"
description: "Azure Blob 저장소(개체 저장소)를 사용하여 클라우드에 구조화되지 않은 데이터를 저장합니다."
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e2fe4c45-27b0-4d15-b3fb-e7eb574db717
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: d27cf1594d6a31a746ca85b5c3184f8a5dbbaa54
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-ruby"></a><span data-ttu-id="0b73f-103">Ruby에서 Blob Storage를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="0b73f-103">How to use Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="0b73f-104">개요</span><span class="sxs-lookup"><span data-stu-id="0b73f-104">Overview</span></span>
<span data-ttu-id="0b73f-105">Azure Blob 저장소는 클라우드에 구조화되지 않은 데이터를 개체/Blob로 저장하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="0b73f-106">Blob 저장소는 문서, 미디어 파일 또는 응용 프로그램 설치 프로그램과 같은 모든 종류의 텍스트 또는 이진 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="0b73f-107">또한 Blob Storage를 개체 저장소라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="0b73f-108">이 가이드에서는 Blob Storage를 사용하여 일반 시나리오를 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-108">This guide will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="0b73f-109">샘플은 Ruby API를 사용하여 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-109">The samples are written using the Ruby API.</span></span> <span data-ttu-id="0b73f-110">여기서 다루는 시나리오에는 Blob **업로드, 나열, 다운로드** 및 **삭제**가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-110">The scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="0b73f-111">Ruby 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="0b73f-111">Create a Ruby application</span></span>
<span data-ttu-id="0b73f-112">Ruby 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-112">Create a Ruby application.</span></span> <span data-ttu-id="0b73f-113">지침은 [Azure VM의 Ruby on Rails 웹 응용 프로그램](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b73f-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="0b73f-114">저장소에 액세스하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="0b73f-114">Configure your application to access Storage</span></span>
<span data-ttu-id="0b73f-115">Azure 저장소를 사용하려면 저장소 REST 서비스와 통신하는 편리한 라이브러리 집합이 포함된 Ruby Azure 패키지를 다운로드하여 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-115">To use Azure Storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="0b73f-116">RubyGems를 사용하여 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="0b73f-116">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="0b73f-117">**PowerShell**(Windows), **Terminal**(Mac) 또는 **Bash**(Unix)와 같은 명령줄 인터페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="0b73f-118">명령 창에 "gem install azure"를 입력하여 gem 및 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-118">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="0b73f-119">패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="0b73f-119">Import the package</span></span>
<span data-ttu-id="0b73f-120">원하는 텍스트 편집기를 사용하여 저장소를 사용하려는 Ruby 파일의 맨 위에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-120">Using your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="0b73f-121">Azure Storage 연결 설정</span><span class="sxs-lookup"><span data-stu-id="0b73f-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="0b73f-122">Azure 모듈은 **AZURE\_STORAGE\_ACCOUNT** 및 **AZURE\_STORAGE\_ACCESS_KEY** 환경 변수를 읽고 Azure Storage 계정에 연결하는 데 필요한 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-122">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="0b73f-123">이러한 환경 변수가 설정되지 않으면 **Azure::Blob::BlobService** 를 사용하기 전에 다음 코드로 계정 정보를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-123">If these environment variables are not set, you must specify the account information before using **Azure::Blob::BlobService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="0b73f-124">Azure 포털의 클래식 또는 Resource Manager 저장소 계정에서 이러한 값을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="0b73f-124">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="0b73f-125">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-125">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0b73f-126">사용하려는 저장소 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-126">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="0b73f-127">오른쪽의 설정 블레이드에서 **액세스 키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-127">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="0b73f-128">나타나는 액세스 키 블레이드에 액세스 키 1 및 액세스 키 2가 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-128">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="0b73f-129">이 둘 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-129">You can use either of these.</span></span>
5. <span data-ttu-id="0b73f-130">복사 아이콘을 클릭하여 키를 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-130">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="0b73f-131">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="0b73f-131">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="0b73f-132">**Azure::Blob::BlobService** 개체를 통해 컨테이너 및 Blob에 대한 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-132">The **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="0b73f-133">컨테이너를 만들려면 **create\_container()** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-133">To create a container, use the **create\_container()** method.</span></span>

<span data-ttu-id="0b73f-134">다음 코드 예제에서는 컨테이너를 만들거나, 컨테이너가 있을 경우 오류를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-134">The following code example creates a container or prints the error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="0b73f-135">컨테이너 파일을 공용으로 지정하려는 경우 컨테이너의 사용 권한을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-135">If you want to make the files in the container public, you can set the container's permissions.</span></span>

<span data-ttu-id="0b73f-136"><strong>create\_container()</strong> 호출을 수정하기만 하면 **:public\_access\_level** 옵션을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-136">You can just modify the <strong>create\_container()</strong> call to pass the **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="0b73f-137">유효한 **:public\_access\_level** 옵션 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-137">Valid values for the **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="0b73f-138">**blob:** BLOB에 대한 공용 읽기 권한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-138">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="0b73f-139">이 컨테이너 내의 Blob 데이터는 익명 요청을 통해 읽을 수 있으나 컨테이너 데이터는 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-139">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="0b73f-140">클라이언트는 익명 요청을 통해 컨테이너 내의 Blob을 열거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-140">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="0b73f-141">**container:** 컨테이너 및 BLOB 데이터에 대한 전체 공용 읽기 액세스 권한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-141">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="0b73f-142">클라이언트는 익명 요청을 통해 컨테이너 내에서 Blob을 열거할 수 있지만 저장소 계정 내에서 컨테이너를 열거할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-142">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="0b73f-143">또는 **set\_container\_acl()** 메서드로 공용 액세스 수준을 지정하여 컨테이너의 공용 액세스 수준을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-143">Alternatively, you can modify the public access level of a container by using **set\_container\_acl()** method to specify the public access level.</span></span>

<span data-ttu-id="0b73f-144">다음 코드 예제에서는 공용 액세스 수준을 **container**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-144">The following code example changes the public access level to **container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="0b73f-145">컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="0b73f-145">Upload a blob into a container</span></span>
<span data-ttu-id="0b73f-146">Blob에 콘텐츠를 업로드하려면 **create\_block\_blob()** 메서드를 사용하여 Blob을 만들고 Blob의 콘텐츠로 파일이나 문자열을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-146">To upload content to a blob, use the **create\_block\_blob()** method to create the blob, use a file or string as the content of the blob.</span></span>

<span data-ttu-id="0b73f-147">다음 코드에서는 **test.png** 파일을 "image-blob"이라는 새 Blob으로 컨테이너에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-147">The following code uploads the file **test.png** as a new blob named "image-blob" in the container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="0b73f-148">컨테이너의 Blob 나열</span><span class="sxs-lookup"><span data-stu-id="0b73f-148">List the blobs in a container</span></span>
<span data-ttu-id="0b73f-149">컨테이너를 나열하려면 **list_containers()** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-149">To list the containers, use **list_containers()** method.</span></span>
<span data-ttu-id="0b73f-150">컨테이너 내에 Blob을 나열하려면 **list\_blobs()** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-150">To list the blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="0b73f-151">이 메서드는 계정에 대해 모든 컨테이너에 있는 모든 Blob의 URL을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-151">This outputs the urls of all the blobs in all the containers for the account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="0b73f-152">Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="0b73f-152">Download blobs</span></span>
<span data-ttu-id="0b73f-153">Blob을 다운로드하려면 **get\_blob()** 메서드를 사용하여 콘텐츠를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-153">To download blobs, use the **get\_blob()** method to retrieve the contents.</span></span>

<span data-ttu-id="0b73f-154">다음 코드 예제에서는 **get\_blob()**을 사용하여 "image-blob"의 콘텐츠를 다운로드하고 그 콘텐츠를 로컬 파일에 쓰는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-154">The following code example demonstrates using **get\_blob()** to download the contents of "image-blob" and write it to a local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="0b73f-155">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="0b73f-155">Delete a Blob</span></span>
<span data-ttu-id="0b73f-156">마지막으로 Blob을 삭제하려면 **delete\_blob()** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-156">Finally, to delete a blob, use the **delete\_blob()** method.</span></span> <span data-ttu-id="0b73f-157">다음 코드 예제에서는 Blob을 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b73f-157">The following code example demonstrates how to delete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="0b73f-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0b73f-158">Next steps</span></span>
<span data-ttu-id="0b73f-159">더 복잡한 저장소 작업에 대해 알아보려면 다음 링크를 따라가세요.</span><span class="sxs-lookup"><span data-stu-id="0b73f-159">To learn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="0b73f-160">Azure 저장소 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="0b73f-160">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="0b73f-161">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) (영문) 리포지토리</span><span class="sxs-lookup"><span data-stu-id="0b73f-161">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="0b73f-162">AzCopy 명령줄 유틸리티로 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="0b73f-162">Transfer data with the AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

