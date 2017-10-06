---
title: "aaaHow toouse Ruby에서 Blob 저장소 (개체 저장소) | Microsoft Docs"
description: "Azure Blob 저장소 (개체 저장소)를 사용 하는 hello 클라우드에 구조화 되지 않은 데이터를 저장 합니다."
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
ms.openlocfilehash: 638826777f5a7ae8330fd67cdbb51d5eee1736a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ruby"></a><span data-ttu-id="0e369-103">어떻게 toouse Ruby에서 Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="0e369-103">How toouse Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="0e369-104">개요</span><span class="sxs-lookup"><span data-stu-id="0e369-104">Overview</span></span>
<span data-ttu-id="0e369-105">Azure Blob 저장소는 hello 클라우드에서 개체/blob으로 구조화 되지 않은 데이터를 저장 하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="0e369-106">Blob storage는 문서, 미디어 파일 또는 응용 프로그램 설치 프로그램과 같은 모든 종류의 텍스트 또는 이진 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="0e369-107">Blob 저장소 참조 tooas 개체 저장소 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="0e369-108">이 가이드에서는 설명 어떻게 tooperform Blob 저장소를 사용 하는 일반적인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-108">This guide will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="0e369-109">hello 샘플 hello Ruby API를 사용 하 여 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-109">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="0e369-110">hello 가이드에서 다루는 시나리오 포함 **업로드, 나열, 다운로드,** 및 **삭제** blob입니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-110">hello scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="0e369-111">Ruby 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="0e369-111">Create a Ruby application</span></span>
<span data-ttu-id="0e369-112">Ruby 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-112">Create a Ruby application.</span></span> <span data-ttu-id="0e369-113">지침은 [Azure VM의 Ruby on Rails 웹 응용 프로그램](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e369-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="0e369-114">사용자 응용 프로그램 tooaccess 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="0e369-114">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="0e369-115">Azure 저장소 toouse toodownload 및 사용 하 여 hello hello 저장소 REST 서비스와 통신 하는 편리한 라이브러리의 집합을 포함 하는 Ruby azure 패키지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-115">toouse Azure Storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="0e369-116">RubyGems tooobtain hello 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="0e369-116">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="0e369-117">**PowerShell**(Windows), **Terminal**(Mac) 또는 **Bash**(Unix)와 같은 명령줄 인터페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="0e369-118">"보석" 설치 azure의 hello 명령 창 tooinstall hello 보석 및 종속성을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-118">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="0e369-119">Hello 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="0e369-119">Import hello package</span></span>
<span data-ttu-id="0e369-120">원하는 텍스트 편집기를 사용 하 여 hello toohello 위쪽 hello toouse 저장소 이점을 얻을 수 Ruby 파일에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-120">Using your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="0e369-121">Azure Storage 연결 설정</span><span class="sxs-lookup"><span data-stu-id="0e369-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="0e369-122">hello azure 모듈 hello 환경 변수는 읽기 **AZURE\_저장소\_계정** 및 **AZURE\_저장소\_ACCESS_KEY** 에 대 한 정보는 tooconnect tooyour Azure 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-122">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="0e369-123">사용 하기 전에 hello 계정 정보를 지정 해야 이러한 환경 변수가 설정 되지 않은 경우 **Azure::Blob::BlobService** 코드 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="0e369-123">If these environment variables are not set, you must specify hello account information before using **Azure::Blob::BlobService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="0e369-124">tooobtain hello Azure 포털에서에서 기존 또는 리소스 관리자 저장소에서 이러한 값 계정:</span><span class="sxs-lookup"><span data-stu-id="0e369-124">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="0e369-125">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-125">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0e369-126">Toouse 사용할 toohello 저장소 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-126">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="0e369-127">Hello 오른쪽에 hello 설정 블레이드에서 클릭 **선택 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-127">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="0e369-128">나타나는 hello 액세스 키 블레이드에서 hello 선택 키 1 및 2 선택 키 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-128">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="0e369-129">이 둘 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-129">You can use either of these.</span></span>
5. <span data-ttu-id="0e369-130">Hello 아이콘 toocopy hello 키 toohello 클립보드로 복사를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-130">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

<span data-ttu-id="0e369-131">tooobtain 클래식 저장소에서 이러한 값 hello 클래식 Azure 포털의 계정:</span><span class="sxs-lookup"><span data-stu-id="0e369-131">tooobtain these values from a classic storage account in hello classic Azure portal:</span></span>

1. <span data-ttu-id="0e369-132">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-132">Log in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="0e369-133">Toouse 사용할 toohello 저장소 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-133">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="0e369-134">클릭 **액세스 키 관리** hello hello 탐색 창 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-134">Click **MANAGE ACCESS KEYS** at hello bottom of hello navigation pane.</span></span>
4. <span data-ttu-id="0e369-135">Hello 팝업 대화 상자에서 hello 저장소 계정 이름, 기본 액세스 키 및 보조 액세스 키 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-135">In hello pop-up dialog, you'll see hello storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="0e369-136">선택 키에 대 한 hello 기본 또는 보조 로케이터로 hello 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-136">For access key, you can use either hello primary one or hello secondary one.</span></span>
5. <span data-ttu-id="0e369-137">Hello 아이콘 toocopy hello 키 toohello 클립보드로 복사를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-137">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="0e369-138">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="0e369-138">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="0e369-139">hello **Azure::Blob::BlobService** 개체 컨테이너 및 blob를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-139">hello **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="0e369-140">toocreate 컨테이너를 사용 하 여 hello **만들\_container()** 메서드.</span><span class="sxs-lookup"><span data-stu-id="0e369-140">toocreate a container, use hello **create\_container()** method.</span></span>

<span data-ttu-id="0e369-141">hello 다음 코드 예제에서는 컨테이너 만들거나 되어 hello 오류를 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-141">hello following code example creates a container or prints hello error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="0e369-142">Hello 컨테이너에서 hello 파일 toomake를 지정 하려면 공용 hello 컨테이너의 사용 권한을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-142">If you want toomake hello files in hello container public, you can set hello container's permissions.</span></span>

<span data-ttu-id="0e369-143">Hello만 수정할 수 있습니다 <strong>만들\_container()</strong> 호출 toopass hello **: 공용\_액세스\_수준** 옵션:</span><span class="sxs-lookup"><span data-stu-id="0e369-143">You can just modify hello <strong>create\_container()</strong> call toopass hello **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="0e369-144">Hello에 대 한 유효한 값 **: 공용\_액세스\_수준** 옵션:</span><span class="sxs-lookup"><span data-stu-id="0e369-144">Valid values for hello **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="0e369-145">**blob:** BLOB에 대한 공용 읽기 권한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-145">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="0e369-146">이 컨테이너 내의 Blob 데이터는 익명 요청을 통해 읽을 수 있으나 컨테이너 데이터는 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-146">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="0e369-147">클라이언트는 익명 요청을 통해 hello 컨테이너 내 blob를 열거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-147">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="0e369-148">**container:** 컨테이너 및 BLOB 데이터에 대한 전체 공용 읽기 액세스 권한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-148">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="0e369-149">클라이언트가 익명 요청을 통해 hello 컨테이너 내 blob를 열거할 수 있지만 hello 저장소 계정 내 컨테이너는 열거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-149">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="0e369-150">컨테이너의 공용 액세스 수준을 hello를 사용 하 여 수정할 수 있습니다 또는 **설정\_컨테이너\_acl()** 메서드 toospecify hello 공용 액세스 수준을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-150">Alternatively, you can modify hello public access level of a container by using **set\_container\_acl()** method toospecify hello public access level.</span></span>

<span data-ttu-id="0e369-151">다음 코드 예제에서는 변경 내용을 hello 공용 액세스 수준을 너무 hello**컨테이너**:</span><span class="sxs-lookup"><span data-stu-id="0e369-151">hello following code example changes hello public access level too**container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="0e369-152">컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="0e369-152">Upload a blob into a container</span></span>
<span data-ttu-id="0e369-153">tooupload 콘텐츠 tooa blob을 사용 하 여 hello **만들\_블록\_blob()** 메서드 toocreate hello blob 파일을 사용 또는 hello blob의 콘텐츠를 hello로 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-153">tooupload content tooa blob, use hello **create\_block\_blob()** method toocreate hello blob, use a file or string as hello content of hello blob.</span></span>

<span data-ttu-id="0e369-154">hello 다음 코드 파일을 업로드 hello **test.png** 라는 "이미지 blob" hello 컨테이너에서 새 blob으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-154">hello following code uploads hello file **test.png** as a new blob named "image-blob" in hello container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="0e369-155">컨테이너에서 hello blob 나열</span><span class="sxs-lookup"><span data-stu-id="0e369-155">List hello blobs in a container</span></span>
<span data-ttu-id="0e369-156">toolist hello 컨테이너를 사용 하 여 **list_containers()** 메서드.</span><span class="sxs-lookup"><span data-stu-id="0e369-156">toolist hello containers, use **list_containers()** method.</span></span>
<span data-ttu-id="0e369-157">toolist hello blob는 컨테이너 내에서 사용 하 여 **목록\_blobs()** 메서드.</span><span class="sxs-lookup"><span data-stu-id="0e369-157">toolist hello blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="0e369-158">모든 hello blob hello 계정에 대 한 모든 hello 컨테이너에서 hello url를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-158">This outputs hello urls of all hello blobs in all hello containers for hello account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="0e369-159">Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="0e369-159">Download blobs</span></span>
<span data-ttu-id="0e369-160">toodownload blob을 사용 하 여 hello **가져오기\_blob()** 메서드 tooretrieve hello 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-160">toodownload blobs, use hello **get\_blob()** method tooretrieve hello contents.</span></span>

<span data-ttu-id="0e369-161">hello 다음 코드 예제에서는 사용 하 여 **가져오기\_blob()** toodownload "이미지 blob"의 내용을 hello 및 tooa 로컬 파일을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-161">hello following code example demonstrates using **get\_blob()** toodownload hello contents of "image-blob" and write it tooa local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="0e369-162">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="0e369-162">Delete a Blob</span></span>
<span data-ttu-id="0e369-163">Blob를 toodelete hello를 사용 하는 마지막으로, **삭제\_blob()** 메서드.</span><span class="sxs-lookup"><span data-stu-id="0e369-163">Finally, toodelete a blob, use hello **delete\_blob()** method.</span></span> <span data-ttu-id="0e369-164">hello 다음 코드 예제에서는 어떻게 toodelete blob입니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-164">hello following code example demonstrates how toodelete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="0e369-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0e369-165">Next steps</span></span>
<span data-ttu-id="0e369-166">더 복잡 한 저장소 작업에 대 한 toolearn 다음 링크:</span><span class="sxs-lookup"><span data-stu-id="0e369-166">toolearn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="0e369-167">Azure 저장소 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="0e369-167">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="0e369-168">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) (영문) 리포지토리</span><span class="sxs-lookup"><span data-stu-id="0e369-168">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="0e369-169">Hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e369-169">Transfer data with hello AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

