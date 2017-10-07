---
title: "aaaIntroduction tooAzure 저장소 | Microsoft Docs"
description: "소개 tooAzure 저장소, hello 클라우드에서 Microsoft의 데이터를 저장 합니다."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: robinsh
ms.openlocfilehash: f61324f98d0a8eb24023e4344acdb4ca58bb27f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
<!-- this is hello same version that is in hello MVC branch -->
# <a name="introduction-toomicrosoft-azure-storage"></a><span data-ttu-id="e337d-103">Azure 저장소 소개 tooMicrosoft</span><span class="sxs-lookup"><span data-stu-id="e337d-103">Introduction tooMicrosoft Azure Storage</span></span>

<span data-ttu-id="e337d-104">Microsoft Azure Storage는 가용성, 보안, 내구성, 확장성 및 중복성이 높은 저장소를 제공하는 Microsoft 관리 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-104">Microsoft Azure Storage is a Microsoft-managed cloud service that provides storage that is highly available, secure, durable, scalable, and redundant.</span></span> <span data-ttu-id="e337d-105">Microsoft는 유지 관리를 담당하고 사용자에 대한 중요한 문제를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-105">Microsoft takes care of maintenance and handles critical problems for you.</span></span> 

<span data-ttu-id="e337d-106">Azure Storage는 Blob Storage, File Storage 및 Queue Storage라는 세 개의 데이터 서비스로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-106">Azure Storage consists of three data services: Blob storage, File storage, and Queue storage.</span></span> <span data-ttu-id="e337d-107">Blob 저장소는 프리미엄 저장소만 Ssd를 사용 하 여 가장 빠른 성능이 가능한 hello에 대 한 표준 및 프리미엄 저장소를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-107">Blob storage supports both standard and premium storage, with premium storage using only SSDs for hello fastest performance possible.</span></span> <span data-ttu-id="e337d-108">다른 기능은 toostorage 많은 양의 저렴 한 비용에 대 한 거의 액세스 하는 데이터를 허용 하는 쿨 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-108">Another feature is cool storage, allowing you toostorage large amounts of rarely accessed data for a lower cost.</span></span>

<span data-ttu-id="e337d-109">이 문서에서는 다음 hello에 대 한 설명:</span><span class="sxs-lookup"><span data-stu-id="e337d-109">In this article, you learn about hello following:</span></span>
* <span data-ttu-id="e337d-110">hello Azure 저장소 서비스</span><span class="sxs-lookup"><span data-stu-id="e337d-110">hello Azure Storage services</span></span>
* <span data-ttu-id="e337d-111">hello 종류의 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="e337d-111">hello types of storage accounts</span></span>
* <span data-ttu-id="e337d-112">Blob, 큐 및 파일에 액세스</span><span class="sxs-lookup"><span data-stu-id="e337d-112">accessing your blobs, queues, and files</span></span>
* <span data-ttu-id="e337d-113">암호화</span><span class="sxs-lookup"><span data-stu-id="e337d-113">encryption</span></span>
* <span data-ttu-id="e337d-114">복제</span><span class="sxs-lookup"><span data-stu-id="e337d-114">replication</span></span> 
* <span data-ttu-id="e337d-115">저장소 간에 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="e337d-115">transferring data into or out of storage</span></span>
* <span data-ttu-id="e337d-116">사용할 수 있는 많은 저장소 클라이언트 라이브러리를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-116">hello many storage client libraries available.</span></span> 


<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->


## <a name="introducing-hello-azure-storage-services"></a><span data-ttu-id="e337d-117">Hello Azure 저장소 서비스를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-117">Introducing hello Azure Storage services</span></span>

<span data-ttu-id="e337d-118">먼저 toouse hello 서비스 정보가 제공-Blob 저장소, 파일 저장 및 큐 저장소-Azure 저장소에서 저장소 계정을 만들고 해당 저장소 계정에 특정 서비스의 데이터를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-118">toouse any of hello services provided by Azure Storage -- Blob storage, File storage, and Queue storage -- you first create a storage account, and then you can transfer data to/from a specific service in that storage account.</span></span> 

## <a name="blob-storage"></a><span data-ttu-id="e337d-119">Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-119">Blob storage</span></span>

<span data-ttu-id="e337d-120">Blob은 기본적으로 사용자가 컴퓨터(또는 태블릿, 모바일 장치 등)에 저장한 항목과 같은 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-120">Blobs are basically files like those that you store on your computer (or tablet, mobile device, and so on).</span></span> <span data-ttu-id="e337d-121">사진, Microsoft Excel 파일, HTML 파일, 가상 하드 디스크(VHD), 로그와 같은 빅 데이터, 데이터베이스 백업 등 거의 모든 것이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-121">They can be pictures, Microsoft Excel files, HTML files, virtual hard disks (VHDs), big data such as logs, database backups  -- pretty much anything.</span></span> <span data-ttu-id="e337d-122">Blob은 유사한 toofolders 컨테이너에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-122">Blobs are stored in containers, which are similar toofolders.</span></span> 

<span data-ttu-id="e337d-123">Blob 저장소에 파일을 저장 한 후에 액세스할 수 있습니다 어디에서 나 Url을 사용 하는 hello world hello REST 인터페이스 또는 hello Azure SDK 저장소 클라이언트 라이브러리 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-123">After storing files in Blob storage, you can access them from anywhere in hello world using URLs, hello REST interface, or one of hello Azure SDK storage client libraries.</span></span> <span data-ttu-id="e337d-124">저장소 클라이언트 라이브러리는 Node.js, Java, PHP, Ruby, Python 및 .NET을 비롯한 여러 언어에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-124">Storage client libraries are available for multiple languages, including Node.js, Java, PHP, Ruby, Python, and .NET.</span></span> 

<span data-ttu-id="e337d-125">블록 Blob, 추가 Blob 및 페이지 Blob라는 세 가지 Blob 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-125">There are three types of blobs -- block blobs, append blobs, and page blobs (used for VHD files).</span></span>

* <span data-ttu-id="e337d-126">블록 blob는 tooabout 일반 파일을 사용 하는 toohold 4.7 TB입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-126">Block blobs are used toohold ordinary files up tooabout 4.7 TB.</span></span> 
* <span data-ttu-id="e337d-127">페이지 blob는 크기가 too8 TB 사용 하는 toohold 임의 액세스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-127">Page blobs are used toohold random access files up too8 TB in size.</span></span> <span data-ttu-id="e337d-128">이러한 Vm을 백업 하는 hello VHD 파일에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-128">These are used for hello VHD files that back VMs.</span></span>
* <span data-ttu-id="e337d-129">추가 blob는 hello 블록 blob와 같은 블록으로 구성 된 하지만에 맞게 최적화 된 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-129">Append blobs are made up of blocks like hello block blobs, but are optimized for append operations.</span></span> <span data-ttu-id="e337d-130">이러한 여러 Vm에서 동일한 blob 정보 toohello 로깅 등의 작업에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-130">These are used for things like logging information toohello same blob from multiple VMs.</span></span>

<span data-ttu-id="e337d-131">매우 큰 데이터 집합을 업로드 하거나 비현실적 hello 유선을 통해 데이터 tooBlob 저장소 다운로드 네트워크 제약 조건을 확인 하는 위치, 하드 드라이브 tooMicrosoft tooimport 집합이 제공 하거나 hello 데이터 센터에서 직접 데이터를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-131">For very large datasets where network constraints make uploading or downloading data tooBlob storage over hello wire unrealistic, you can ship a set of hard drives tooMicrosoft tooimport or export data directly from hello data center.</span></span> <span data-ttu-id="e337d-132">참조 [hello Microsoft Azure 가져오기/내보내기 서비스 tooTransfer 데이터 tooBlob 저장소를 사용 하 여](../storage-import-export-service.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-132">See [Use hello Microsoft Azure Import/Export Service tooTransfer Data tooBlob Storage](../storage-import-export-service.md).</span></span>

## <a name="file-storage"></a><span data-ttu-id="e337d-133">File Storage</span><span class="sxs-lookup"><span data-stu-id="e337d-133">File storage</span></span>

<span data-ttu-id="e337d-134">Azure 파일 서비스 hello hello 표준 서버 메시지 블록 (SMB) 프로토콜을 사용 하 여 액세스할 수 있는 항상 사용 가능한 네트워크 파일 공유를 tooset이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-134">hello Azure Files service enables you tooset up highly available network file shares that can be accessed by using hello standard Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="e337d-135">여러 Vm을 공유할 수 있다는 것을 의미 동일을 hello 읽기 및 쓰기 권한이 모두 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-135">That means that multiple VMs can share hello same files with both read and write access.</span></span> <span data-ttu-id="e337d-136">Hello REST 인터페이스 또는 hello 저장소 클라이언트 라이브러리를 사용 하 여 hello 파일을 읽을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-136">You can also read hello files using hello REST interface or hello storage client libraries.</span></span> 

<span data-ttu-id="e337d-137">Azure 파일 저장소에서 회사 파일 공유에 파일을 구별 하는 한 가지는 어디에서 든 hello 파일을 액세스할 수 있도록 toohello 파일을 가리키는 공유 액세스 서명 (SAS) 토큰을 포함 하는 URL을 사용 하는 hello world에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-137">One thing that distinguishes Azure File storage from files on a corporate file share is that you can access hello files from anywhere in hello world using a URL that points toohello file and includes a shared access signature (SAS) token.</span></span> <span data-ttu-id="e337d-138">SAS 토큰을 생성할 수 있습니다. 특정 기간에 대 한 특정 액세스 tooa 개인 자산을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-138">You can generate SAS tokens; they allow specific access tooa private asset for a specific amount of time.</span></span> 

<span data-ttu-id="e337d-139">파일 공유는 다음과 같은 여러 가지 일반적인 시나리오에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-139">File shares can be used for many common scenarios:</span></span> 

* <span data-ttu-id="e337d-140">여러 온-프레미스 응용 프로그램에서 파일 공유를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-140">Many on-premises applications use file shares.</span></span> <span data-ttu-id="e337d-141">이 기능을 통해 보다 쉽게 toomigrate 데이터 tooAzure를 공유 하는 해당 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-141">This feature makes it easier toomigrate those applications that share data tooAzure.</span></span> <span data-ttu-id="e337d-142">탑재할 hello에 같은 드라이브 문자 hello 하는 파일 공유 toohello 온-프레미스 응용 프로그램 사용 하 여, 있는 경우에 최소한 변경 하 여 hello 파일 공유에 액세스 하는 응용 프로그램의 hello 부분 작동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-142">If you mount hello file share toohello same drive letter that hello on-premises application uses, hello part of your application that accesses hello file share should work with minimal, if any, changes.</span></span>

* <span data-ttu-id="e337d-143">구성 파일을 파일 공유에 저장하고 여러 VM에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-143">Configuration files can be stored on a file share and accessed from multiple VMs.</span></span> <span data-ttu-id="e337d-144">도구 및 유틸리티를 그룹에 여러 개발자가 사용 되는 모든 사용자에 게 찾을 수 있도록, 확인 하는 파일 공유에 저장할 수 있으며를 사용 하는 hello 동일한 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-144">Tools and utilities used by multiple developers in a group can be stored on a file share, ensuring that everybody can find them, and that they use hello same version.</span></span>

* <span data-ttu-id="e337d-145">진단 로그, 메트릭 및 크래시 덤프는 세 개의 예 tooa 파일 공유를 작성 및 처리 하거나 나중에 분석할 수 있는 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-145">Diagnostic logs, metrics, and crash dumps are just three examples of data that can be written tooa file share and processed or analyzed later.</span></span>

<span data-ttu-id="e337d-146">이 시간, Active Directory 기반 인증 및 액세스 제어 목록 (Acl) 지원 되지 않으며, 없지만 이후 hello에 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-146">At this time, Active Directory-based authentication and access control lists (ACLs) are not supported, but they will be at some time in hello future.</span></span> <span data-ttu-id="e337d-147">hello 저장소 계정 자격 증명이 사용 되는 tooprovide 인증 액세스 toohello 파일 공유에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-147">hello storage account credentials are used tooprovide authentication for access toohello file share.</span></span> <span data-ttu-id="e337d-148">즉, 탑재 hello 공유와 모든 사용자가 모든 읽기/쓰기 액세스 toohello 공유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-148">This means anybody with hello share mounted will have full read/write access toohello share.</span></span>

## <a name="queue-storage"></a><span data-ttu-id="e337d-149">큐 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-149">Queue storage</span></span>

<span data-ttu-id="e337d-150">hello Azure 큐 서비스 사용 되는 toostore 및 검색 하 고 메시지 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-150">hello Azure Queue service is used toostore and retrieve messages.</span></span> <span data-ttu-id="e337d-151">큐 메시지의 크기 (kb) too64 될 수 있습니다 및 큐에는 수많은 메시지 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-151">Queue messages can be up too64 KB in size, and a queue can contain millions of messages.</span></span> <span data-ttu-id="e337d-152">큐는 일반적으로 사용 되는 toostore 목록이 메시지 toobe 비동기적으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-152">Queues are generally used toostore lists of messages toobe processed asynchronously.</span></span> 

<span data-ttu-id="e337d-153">예를 들어 고객 toobe 수 tooupload 그림 및 각 사진에 대 한 toocreate 축소판 그림을 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-153">For example, say you want your customers toobe able tooupload pictures, and you want toocreate thumbnails for each picture.</span></span> <span data-ttu-id="e337d-154">Hello 사진을 업로드 하는 동안 대기 하면 toocreate hello 미리 보기에 대 한 고객을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-154">You could have your customer wait for you toocreate hello thumbnails while uploading hello pictures.</span></span> <span data-ttu-id="e337d-155">대신 toouse 큐 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-155">An alternative would be toouse a queue.</span></span> <span data-ttu-id="e337d-156">Hello 고객 그의 업로드를 완료 하는 경우 메시지 toohello 큐를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-156">When hello customer finishes his upload, write a message toohello queue.</span></span> <span data-ttu-id="e337d-157">다음 기능이 Azure hello 큐에서 hello 메시지를 검색 하 고 hello 축소판 그림을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-157">Then have an Azure Function retrieve hello message from hello queue and create hello thumbnails.</span></span> <span data-ttu-id="e337d-158">이 처리 hello 부분의 각각을 확장할 수 있습니다 별도로 사용량에 대 한 튜닝 하는 경우 더 세밀 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-158">Each of hello parts of this processing can be scaled separately, giving you more control when tuning it for your usage.</span></span>

<!-- this bookmark is used by other articles; you'll need tooupdate them before this goes into production ROBIN-->
## <a name="table-storage"></a><span data-ttu-id="e337d-159">테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-159">Table storage</span></span>
<!-- add a link toohello old table storage toothis paragraph once it's moved -->
<span data-ttu-id="e337d-160">이제 표준 Azure Table Storage는 Cosmos DB의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-160">Standard Azure Table Storage is now part of Cosmos DB.</span></span> <span data-ttu-id="e337d-161">또한 처리량 최적화 테이블, 글로벌 분포 및 자동 보조 인덱스를 제공하는 Azure Table Storage에 대한 프리미엄 테이블이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-161">Also available is Premium Tables for Azure Table storage, offering throughput-optimized tables, global distribution, and automatic secondary indexes.</span></span> <span data-ttu-id="e337d-162">더 많은 toolearn을 시작 하 고 hello 새로운 premium 환경에서는 아웃 하십시오 체크 아웃 [Azure Cosmos DB: 테이블 API](https://aka.ms/premiumtables)합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-162">toolearn more and try out hello new premium experience, please check out [Azure Cosmos DB: Table API](https://aka.ms/premiumtables).</span></span>

## <a name="disk-storage"></a><span data-ttu-id="e337d-163">디스크 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-163">Disk storage</span></span>

<span data-ttu-id="e337d-164">또한 hello Azure 저장소 팀 디스크, 가상 컴퓨터에서 사용 하는 모든 관리 되는 hello 포함 되어 기능과 관리 되지 않는 디스크를 소유 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-164">hello Azure Storage team also owns Disks, which includes all of hello managed and unmanaged disk capabilities used by virtual machines.</span></span> <span data-ttu-id="e337d-165">이러한 기능에 대 한 자세한 내용은 hello를 참조 하십시오 [계산 서비스 설명서](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-165">For more information about these features, please see hello [Compute Service documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>

## <a name="types-of-storage-accounts"></a><span data-ttu-id="e337d-166">저장소 계정 유형</span><span class="sxs-lookup"><span data-stu-id="e337d-166">Types of storage accounts</span></span> 

<span data-ttu-id="e337d-167">이 표에 hello 다양 한 종류의 저장소 계정 및 개체를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-167">This table shows hello various kinds of storage accounts and which objects can be used with each.</span></span>

|<span data-ttu-id="e337d-168">**저장소 계정의 유형**</span><span class="sxs-lookup"><span data-stu-id="e337d-168">**Type of storage account**</span></span>|<span data-ttu-id="e337d-169">**범용 표준**</span><span class="sxs-lookup"><span data-stu-id="e337d-169">**General-purpose Standard**</span></span>|<span data-ttu-id="e337d-170">**범용 프리미엄**</span><span class="sxs-lookup"><span data-stu-id="e337d-170">**General-purpose Premium**</span></span>|<span data-ttu-id="e337d-171">**Blob Storage, 핫 및 쿨 액세스 계층**</span><span class="sxs-lookup"><span data-stu-id="e337d-171">**Blob storage, hot and cool access tiers**</span></span>|
|-----|-----|-----|-----|
|<span data-ttu-id="e337d-172">**지원되는 서비스**</span><span class="sxs-lookup"><span data-stu-id="e337d-172">**Services supported**</span></span>| <span data-ttu-id="e337d-173">Blob, File, Queue 서비스</span><span class="sxs-lookup"><span data-stu-id="e337d-173">Blob, File, Queue Services</span></span> | <span data-ttu-id="e337d-174">Blob Service</span><span class="sxs-lookup"><span data-stu-id="e337d-174">Blob Service</span></span> | <span data-ttu-id="e337d-175">Blob Service</span><span class="sxs-lookup"><span data-stu-id="e337d-175">Blob Service</span></span>|
|<span data-ttu-id="e337d-176">**지원되는 Blob 유형**</span><span class="sxs-lookup"><span data-stu-id="e337d-176">**Types of blobs supported**</span></span>|<span data-ttu-id="e337d-177">블록 Blob, 페이지 Blob 및 추가 Blob</span><span class="sxs-lookup"><span data-stu-id="e337d-177">Block blobs, page blobs, and append blobs</span></span> | <span data-ttu-id="e337d-178">페이지 Blob</span><span class="sxs-lookup"><span data-stu-id="e337d-178">Page blobs</span></span> | <span data-ttu-id="e337d-179">블록 Blob 및 추가 Blob</span><span class="sxs-lookup"><span data-stu-id="e337d-179">Block blobs and append blobs</span></span>|

### <a name="general-purpose-storage-accounts"></a><span data-ttu-id="e337d-180">범용 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="e337d-180">General-purpose storage accounts</span></span>

<span data-ttu-id="e337d-181">범용 저장소 계정에는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-181">There are two kinds of general-purpose storage accounts.</span></span> 

#### <a name="standard-storage"></a><span data-ttu-id="e337d-182">Standard Storage</span><span class="sxs-lookup"><span data-stu-id="e337d-182">Standard storage</span></span> 

<span data-ttu-id="e337d-183">hello 가장 널리 사용 되는 저장소 계정 되는 모든 유형의 데이터에 사용할 수 있는 표준 저장소 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-183">hello most widely used storage accounts are standard storage accounts, which can be used for all types of data.</span></span> <span data-ttu-id="e337d-184">표준 저장소 계정은 자기 미디어 toostore 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-184">Standard storage accounts use magnetic media toostore data.</span></span>

#### <a name="premium-storage"></a><span data-ttu-id="e337d-185">Premium Storage</span><span class="sxs-lookup"><span data-stu-id="e337d-185">Premium storage</span></span>

<span data-ttu-id="e337d-186">프리미엄 저장소는 VHD 파일에 주로 사용되는 페이지 Blob에 고성능 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-186">Premium storage provides high-performance storage for page blobs, which are primarily used for VHD files.</span></span> <span data-ttu-id="e337d-187">프리미엄 저장소 계정 SSD toostore 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-187">Premium storage accounts use SSD toostore data.</span></span> <span data-ttu-id="e337d-188">모든 VM에 Premium Storage를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-188">Microsoft recommends using Premium Storage for all of your VMs.</span></span>

### <a name="blob-storage-accounts"></a><span data-ttu-id="e337d-189">Blob Storage 계정</span><span class="sxs-lookup"><span data-stu-id="e337d-189">Blob Storage accounts</span></span>

<span data-ttu-id="e337d-190">hello Blob 저장소 계정은 특수 저장소 계정 toostore 블록 blob을 사용 하 고 추가 blob입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-190">hello Blob Storage account is a specialized storage account used toostore block blobs and append blobs.</span></span> <span data-ttu-id="e337d-191">이러한 계정에 페이지 Blob을 저장할 수 없습니다. 따라서 VHD 파일을 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-191">You can't store page blobs in these accounts, therefore you can't store VHD files.</span></span> <span data-ttu-id="e337d-192">액세스 계층 tooHot tooset 또는 쿨;이 계정을 사용 하면 hello 계층은 언제 든 지 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-192">These accounts allow you tooset an access tier tooHot or Cool; hello tier can be changed at any time.</span></span> 

<span data-ttu-id="e337d-193">자주 액세스 하는 파일에 대 한 hello 핫 액세스 계층은 사용 하는 등의 저장소에 대 한 비용이 많이 드는 비용을 지불 되지만 hello blob에 액세스 하는 hello 비용이 훨씬 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-193">hello hot access tier is used for files that are accessed frequently -- you pay a higher cost for storage, but hello cost of accessing hello blobs is much lower.</span></span> <span data-ttu-id="e337d-194">Hello 쿨 액세스 계층에 저장 된 blob에 대 한 hello blob 액세스를 위한 비용이 많이 드는 비용을 지불 있지만 hello 저장소 비용을 훨씬 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-194">For blobs stored in hello cool access tier, you pay a higher cost for accessing hello blobs, but hello cost of storage is much lower.</span></span>

## <a name="accessing-your-blobs-files-and-queues"></a><span data-ttu-id="e337d-195">Blob, 파일 및 큐에 액세스</span><span class="sxs-lookup"><span data-stu-id="e337d-195">Accessing your blobs, files, and queues</span></span>

<span data-ttu-id="e337d-196">각 저장소 계정에는 모든 작업에 사용할 수 있는 두 개의 인증 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-196">Each storage account has two authentication keys, either of which can be used for any operation.</span></span> <span data-ttu-id="e337d-197">Hello 롤오버할 수 있도록 두 개의 키 tooenhance 보안 키 가끔 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-197">There are two keys so you can roll over hello keys occasionally tooenhance security.</span></span> <span data-ttu-id="e337d-198">hello 계정 이름과 함께 소유 하는 hello 저장소 계정에서 tooall 데이터에 무제한 액세스를 허용 하기 때문에 이러한 키 수 안전 하 게 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-198">It is critical that these keys be kept secure because their possession, along with hello account name, allows unlimited access tooall data in hello storage account.</span></span> 

<span data-ttu-id="e337d-199">이 섹션은 두 가지 방법으로 toosecure hello 저장소 계정 및 해당 데이터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-199">This section looks two ways toosecure hello storage account and its data.</span></span> <span data-ttu-id="e337d-200">저장소 계정 및 사용자 데이터를 보호 하는 방법에 대 한 자세한 내용은 참조 hello [Azure 저장소 보안 가이드](storage-security-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-200">For detailed information about securing your storage account and your data, see hello [Azure Storage security guide](storage-security-guide.md).</span></span>

### <a name="securing-access-toostorage-accounts-using-azure-ad"></a><span data-ttu-id="e337d-201">Azure AD를 사용 하 여 toostorage 계정을 액세스 보안</span><span class="sxs-lookup"><span data-stu-id="e337d-201">Securing access toostorage accounts using Azure AD</span></span>

<span data-ttu-id="e337d-202">한 가지 방법은 toosecure 액세스 tooyour 저장소 데이터 액세스 toohello 저장소 계정 키를 제어 하 여는입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-202">One way toosecure access tooyour storage data is by controlling access toohello storage account keys.</span></span> <span data-ttu-id="e337d-203">리소스 관리자 역할 기반 액세스 제어 (RBAC) 사용 하 여 역할 toousers, 그룹 또는 응용 프로그램을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-203">With Resource Manager Role-Based Access Control (RBAC), you can assign roles toousers, groups, or applications.</span></span> <span data-ttu-id="e337d-204">이러한 역할에 연결 된 tooa 특정 집합이 허용 되거나 허용 되지 않는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-204">These roles are tied tooa specific set of actions that are allowed or disallowed.</span></span> <span data-ttu-id="e337d-205">Toogrant 액세스 tooa 저장소 계정 RBAC를 사용 하 여 hello 액세스 계층을 변경 하는 등 해당 저장소 계정에 대 한 hello 관리 작업을 처리만 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-205">Using RBAC toogrant access tooa storage account only handles hello management operations for that storage account, such as changing hello access tier.</span></span> <span data-ttu-id="e337d-206">특정 컨테이너 또는 파일 공유와 같은 RBAC toogrant 액세스 toodata 개체를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-206">You can't use RBAC toogrant access toodata objects like a specific container or file share.</span></span> <span data-ttu-id="e337d-207">그러나 RBAC toogrant 액세스 toohello 저장소 계정 키를 사용 하는 tooread hello 데이터 개체 수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-207">You can, however, use RBAC toogrant access toohello storage account keys, which can then be used tooread hello data objects.</span></span> 

### <a name="securing-access-using-shared-access-signatures"></a><span data-ttu-id="e337d-208">공유 액세스 서명을 사용하여 액세스 보호</span><span class="sxs-lookup"><span data-stu-id="e337d-208">Securing access using shared access signatures</span></span> 

<span data-ttu-id="e337d-209">액세스 정책 toosecure 데이터 개체를 저장 한 공유 액세스 서명을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-209">You can use shared access signatures and stored access policies toosecure your data objects.</span></span> <span data-ttu-id="e337d-210">공유 액세스 서명 (SAS) 일 수 있는 보안 토큰을 포함 하는 문자열 toohello URI toodelegate toospecific 저장소 개체 액세스 및 사용 권한 및 액세스의 hello 날짜/시간 범위와 같은 toospecify 제약 조건 수 있는 자산에 대 한 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-210">A shared access signature (SAS) is a string containing a security token that can be attached toohello URI for an asset that allows you toodelegate access toospecific storage objects and toospecify constraints such as permissions and hello date/time range of access.</span></span> <span data-ttu-id="e337d-211">이 기능에는 광범위한 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-211">This feature has extensive capabilities.</span></span> <span data-ttu-id="e337d-212">자세한 내용은 참조 너무[공유 액세스 서명 (SAS)를 사용 하 여](storage-dotnet-shared-access-signature-part-1.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-212">For detailed information, refer too[Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>

### <a name="public-access-tooblobs"></a><span data-ttu-id="e337d-213">공용 액세스 tooblobs</span><span class="sxs-lookup"><span data-stu-id="e337d-213">Public access tooblobs</span></span>

<span data-ttu-id="e337d-214">Blob 서비스 hello tooprovide 공용 액세스 tooa 컨테이너와 해당 blob 또는 blob에 특정 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-214">hello Blob Service allows you tooprovide public access tooa container and its blobs, or a specific blob.</span></span> <span data-ttu-id="e337d-215">컨테이너 또는 Blob을 공개로 지정하면 모든 사용자가 이 컨테이너 또는 Blob를 익명으로 읽을 수 있으며 인증이 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-215">When you indicate that a container or blob is public, anyone can read it anonymously; no authentication is required.</span></span> <span data-ttu-id="e337d-216">Toodo 하려는 경우의 예 이미지, 비디오 또는 Blob 저장소의 문서를 사용 하는 웹 사이트가 있는 경우 이것이입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-216">An example of when you would want toodo this is when you have a website that is using images, video, or documents from Blob storage.</span></span> <span data-ttu-id="e337d-217">자세한 내용은 참조 [익명 읽기 권한을 toocontainers 및 blob 관리](../blobs/storage-manage-access-to-resources.md)</span><span class="sxs-lookup"><span data-stu-id="e337d-217">For more information, see [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md)</span></span> 

## <a name="encryption"></a><span data-ttu-id="e337d-218">암호화</span><span class="sxs-lookup"><span data-stu-id="e337d-218">Encryption</span></span>

<span data-ttu-id="e337d-219">Hello 저장소 서비스에 사용할 수 있는 기본적인 종류의 암호화의 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-219">There are a couple of basic kinds of encryption available for hello Storage services.</span></span> 

### <a name="encryption-at-rest"></a><span data-ttu-id="e337d-220">휴지 상태의 암호화</span><span class="sxs-lookup"><span data-stu-id="e337d-220">Encryption at rest</span></span> 

<span data-ttu-id="e337d-221">Azure 저장소 계정의 Blob 서비스 hello 하거나 hello 파일 서비스 (미리 보기) 중 하나에 저장소 서비스 암호화 SSE ()를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-221">You can enable Storage Service Encryption (SSE) on either hello Files service (preview) or hello Blob service for an Azure storage account.</span></span> <span data-ttu-id="e337d-222">Toohello 특정 서비스를 작성 하는 모든 데이터는 암호화를 사용 하는 경우 기록 되기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-222">If enabled, all data written toohello specific service is encrypted before written.</span></span> <span data-ttu-id="e337d-223">암호가 해독 된 hello 데이터를 읽을 때 반환 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-223">When you read hello data, it is decrypted before returned.</span></span> 

### <a name="client-side-encryption"></a><span data-ttu-id="e337d-224">클라이언트 쪽 암호화</span><span class="sxs-lookup"><span data-stu-id="e337d-224">Client-side encryption</span></span>

<span data-ttu-id="e337d-225">hello 저장소 클라이언트 라이브러리는 메서드를 호출할 수 tooprogrammatically hello 클라이언트 tooAzure에서 hello 네트워크를 통해 보내기 전에 데이터를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-225">hello storage client libraries have methods you can call tooprogrammatically encrypt data before sending it across hello wire from hello client tooAzure.</span></span> <span data-ttu-id="e337d-226">암호화되어 저장됩니다. 즉, 휴지 시 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-226">It is stored encrypted, which means it also is encrypted at rest.</span></span> <span data-ttu-id="e337d-227">다시 hello 데이터를 읽을 때 받은 이후 hello 정보를 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-227">When reading hello data back, you decrypt hello information after receiving it.</span></span> 

### <a name="encryption-in-transit-with-azure-file-shares"></a><span data-ttu-id="e337d-228">전송 시 Azure 파일 공유에서 암호화</span><span class="sxs-lookup"><span data-stu-id="e337d-228">Encryption in transit with Azure File Shares</span></span>

<span data-ttu-id="e337d-229">공유 액세스 서명에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용](../storage-dotnet-shared-access-signature-part-1.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e337d-229">See [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md) for more information on shared access signatures.</span></span> <span data-ttu-id="e337d-230">참조 [익명 읽기 권한을 toocontainers 및 blob 관리](../blobs/storage-manage-access-to-resources.md) 및 [hello Azure 저장소 서비스에 대 한 인증](https://msdn.microsoft.com/library/azure/dd179428.aspx) 보안 액세스 tooyour 저장소 계정에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-230">See [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md) and [Authentication for hello Azure Storage Services](https://msdn.microsoft.com/library/azure/dd179428.aspx) for more information on secure access tooyour storage account.</span></span>

<span data-ttu-id="e337d-231">저장소 계정 및 암호화 보안에 대 한 자세한 내용은 참조 hello [Azure 저장소 보안 가이드](storage-security-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-231">For more details about securing your storage account and encryption, see hello [Azure Storage security guide](storage-security-guide.md).</span></span>

## <a name="replication"></a><span data-ttu-id="e337d-232">복제</span><span class="sxs-lookup"><span data-stu-id="e337d-232">Replication</span></span>

<span data-ttu-id="e337d-233">데이터가 지속 됩니다 순서 tooensure, Azure 저장소에 hello 기능 tookeep (있고 관리) 데이터의 여러 복사본입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-233">In order tooensure that your data is durable, Azure Storage has hello ability tookeep (and manage) multiple copies of your data.</span></span> <span data-ttu-id="e337d-234">이를 복제 또는 중복성이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-234">This is called replication, or sometimes redundancy.</span></span> <span data-ttu-id="e337d-235">저장소 계정을 설정할 때 복제 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-235">When you set up your storage account, you select replication type.</span></span> <span data-ttu-id="e337d-236">대부분의 경우에서 hello 저장소 계정이 설정 되 면이 설정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-236">In most cases, this setting can be modified after hello storage account is set up.</span></span> 

<span data-ttu-id="e337d-237">모든 저장소 계정에는 **LRS(로컬 중복 저장소)**가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-237">All storage accounts have **locally redundant storage (LRS)**.</span></span> <span data-ttu-id="e337d-238">Hello 데이터 센터에서 Azure 저장소에서 관리 되는 데이터의 세 개의 복사본이 즉 hello 저장소 계정을 설정 되었으므로 설정할 때 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-238">This means three copies of your data are managed by Azure Storage in hello data center specified when hello storage account was set up.</span></span> <span data-ttu-id="e337d-239">때 변경 내용이 커밋된 tooone 복사을 hello 다른 두 개의 복사본이 업데이트 됩니다 성공을 반환 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="e337d-239">When changes are committed tooone copy, hello other two copies are updated before returning success.</span></span> <span data-ttu-id="e337d-240">즉, hello 세 개의 복제본은 항상 동기화 합니다. 또한 hello 세 복사본이 별도 오류 도메인에 있는 및 업그레이드 도메인, 즉, 데이터를 보유 하는 저장소 노드 실패 하거나 오프 라인 toobe 수행한 업데이트 되는 경우에 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-240">This means hello three replicas are always in sync. Also, hello three copies reside in separate fault domains and upgrade domains, which means your data is available even if a storage node holding your data fails or is taken offline toobe updated.</span></span> 

<span data-ttu-id="e337d-241">**LRS(로컬 중복 저장소)**</span><span class="sxs-lookup"><span data-stu-id="e337d-241">**Locally redundant storage (LRS)**</span></span>

<span data-ttu-id="e337d-242">위에서 설명한 대로 LRS에서 세 개의 데이터 복사본이 단일 데이터 센터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-242">As explained above, with LRS you have three copies of your data in a single datacenter.</span></span> <span data-ttu-id="e337d-243">저장소 노드 실패 또는 오프 라인 toobe 업데이트를 수행 하지만 사용할 수 없게 되는 전체 데이터 센터의 대/소문자를 하지 hello 사용 하지 못하게 될 데이터의 hello 문제를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-243">This handles hello problem of data becoming unavailable if a storage node fails or is taken offline toobe updated, but not hello case of an entire datacenter becoming unavailable.</span></span>

<span data-ttu-id="e337d-244">**ZRS(영역 중복 저장소)**</span><span class="sxs-lookup"><span data-stu-id="e337d-244">**Zone redundant storage (ZRS)**</span></span>

<span data-ttu-id="e337d-245">영역 중복 저장소 (ZRS) 데이터의 세 가지 로컬 복사본 hello 뿐만 아니라 다른 3 개 데이터 집합 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-245">Zone-redundant storage (ZRS) maintains hello three local copies of your data as well as another set of three copies of your data.</span></span> <span data-ttu-id="e337d-246">hello 세 복사본이의 두 번째 집합은 비동기적으로 복제 하나 또는 두 개의 영역 내에서 데이터 센터입니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-246">hello second set of three copies is replicated asynchronously across datacenters within one or two regions.</span></span> <span data-ttu-id="e337d-247">ZRS는 범용 저장소 계정에서 블록 Blob에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-247">Note that ZRS is only available for block blobs in general-purpose storage accounts.</span></span> <span data-ttu-id="e337d-248">또한 저장소 계정을 만든 하 고 ZRS를 선택한 후 변환할 수는 없습니다 것 toouse tooany 다른 복제의 경우, 또는 그 반대로 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-248">Also, once you have created your storage account and selected ZRS, you cannot convert it toouse tooany other type of replication, or vice versa.</span></span>

<span data-ttu-id="e337d-249">ZRS 계정은 LRS보다 높은 지속성을 제공하지만 메트릭 또는 로깅 기능은 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-249">ZRS accounts provide higher durability than LRS, but ZRS accounts do not have metrics or logging capability.</span></span> 

<span data-ttu-id="e337d-250">**GRS(지역 중복 저장소)**</span><span class="sxs-lookup"><span data-stu-id="e337d-250">**Geo-redundant storage (GRS)**</span></span>

<span data-ttu-id="e337d-251">지역 중복 저장소 (GRS)에 기본 지역에서 데이터의 세 가지 로컬 복사본 hello 및 다른 3 개 보조 지역 수백 킬로미터 떨어진 hello 기본 지역에서에서 데이터 집합 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-251">Geo-redundant storage (GRS) maintains hello three local copies of your data in a primary region plus another set of three copies of your data in a secondary region hundreds of miles away from hello primary region.</span></span> <span data-ttu-id="e337d-252">Hello 기본 지역에서 작업이 실패의 hello 이벤트에서 Azure 저장소는 toohello 보조 지역의 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-252">In hello event of a failure at hello primary region, Azure Storage will fail over toohello secondary region.</span></span> 

<span data-ttu-id="e337d-253">**RA-GRS(읽기 액세스 지역 중복 저장소)**</span><span class="sxs-lookup"><span data-stu-id="e337d-253">**Read-access geo-redundant storage (RA-GRS)**</span></span> 

<span data-ttu-id="e337d-254">읽기 액세스 지역 중복 저장소는 GRS 똑같이 같지만 hello 보조 위치에 대 한 읽기 액세스 toohello 데이터를 얻게 점에서 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-254">Read-access geo-redundant storage is exactly like GRS except that you get read access toohello data in hello secondary location.</span></span> <span data-ttu-id="e337d-255">기본 데이터 센터 hello 일시적으로 사용할 수 없게 되 tooread hello 데이터 hello 보조 위치에서 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-255">If hello primary data center becomes unavailable temporarily, you can continue tooread hello data from hello secondary location.</span></span> <span data-ttu-id="e337d-256">이는 매우 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-256">This can be very helpful.</span></span> <span data-ttu-id="e337d-257">예를 들어 업데이트를 사용할 수 없는 경우에 일부 액세스할 수 있도록 웹 응용 프로그램을 읽기 전용 모드로 변경 하 고 toohello 보조 복사본이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-257">For example, you could have a web application that changes into read-only mode and points toohello secondary copy, allowing some access even though updates are not available.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e337d-258">어떻게 데이터가 복제 되어 저장소 계정의 만든 후 hello 계정을 만들 때 ZRS를 지정 하지 않으면 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-258">You can change how your data is replicated after your storage account has been created, unless you specified ZRS when you created hello account.</span></span> <span data-ttu-id="e337d-259">그러나는 추가 일회성 데이터 전송 LRS tooGRS 또는 RA-GRS에서 전환 비용을 청구할 수 있습니다 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-259">However, note that you may incur an additional one-time data transfer cost if you switch from LRS tooGRS or RA-GRS.</span></span>
>

<span data-ttu-id="e337d-260">복제에 대한 자세한 내용은 [Azure Storage 복제](storage-redundancy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e337d-260">For more information about replication, see [Azure Storage replication](storage-redundancy.md).</span></span>

<span data-ttu-id="e337d-261">재해 복구 정보를 참조 하십시오. [Azure 저장소 중단이 발생할 경우 어떤 toodo](storage-disaster-recovery-guidance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-261">For disaster recovery information, see [What toodo if an Azure Storage outage occurs](storage-disaster-recovery-guidance.md).</span></span>

<span data-ttu-id="e337d-262">방법의 예에 대 한 RA-GRS 저장소 tooensure 높은 가용성, tooleverage 참조 [항상 사용 가능한 응용 프로그램 설계 RA-GRS를 사용 하 여](storage-designing-ha-apps-with-ragrs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-262">For an example of how tooleverage RA-GRS storage tooensure high availability, see [Designing Highly Available Applications using RA-GRS](storage-designing-ha-apps-with-ragrs.md).</span></span>

## <a name="transferring-data-tooand-from-azure-storage"></a><span data-ttu-id="e337d-263">Azure 저장소에서 데이터 tooand 전송</span><span class="sxs-lookup"><span data-stu-id="e337d-263">Transferring data tooand from Azure Storage</span></span>

<span data-ttu-id="e337d-264">저장소 계정 내에서 또는 저장소 계정에서 hello AzCopy 명령줄 유틸리티 toocopy blob 및 파일 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-264">You can use hello AzCopy command-line utility toocopy blob, and file data within your storage account or across storage accounts.</span></span> <span data-ttu-id="e337d-265">에 대 한 도움말 문서 hello 다음 중 하나를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e337d-265">See one of hello following articles for help:</span></span>

* [<span data-ttu-id="e337d-266">Windows에서 AzCopy를 사용하여 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="e337d-266">Transfer data with AzCopy for Windows</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="e337d-267">Linux에서 AzCopy를 사용하여 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="e337d-267">Transfer data with AzCopy for Linux</span></span>](storage-use-azcopy-linux.md)

<span data-ttu-id="e337d-268">AzCopy hello 위에 빌드됩니다. 따라서 [Azure 데이터 이동을 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), 미리 보기에서 현재 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-268">AzCopy is built on top of hello [Azure Data Movement Library](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), which is currently available in preview.</span></span>

<span data-ttu-id="e337d-269">hello Azure 가져오기/내보내기 서비스에 사용 되는 tooimport 또는 내보내기 많은 양의 저장소 계정에서 blob 데이터 tooor 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-269">hello Azure Import/Export service can be used tooimport or export large amounts of blob data tooor from your storage account.</span></span> <span data-ttu-id="e337d-270">Hello 데이터 hello 하드 드라이브에서 여러 하드 드라이브 tooan Azure 데이터 센터에서는 전송 여기서 메일 및 hello 하드 드라이브 다시 tooyou 보낼 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-270">You prepare and mail multiple hard drives tooan Azure data center, where they will transfer hello data to/from hello hard drives and send hello hard drives back tooyou.</span></span> <span data-ttu-id="e337d-271">Hello 가져오기/내보내기 서비스에 대 한 자세한 내용은 참조 [hello Microsoft Azure 가져오기/내보내기 서비스 tooTransfer 데이터 tooBlob 저장소를 사용 하 여](../storage-import-export-service.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-271">For more information about hello Import/Export service, see [Use hello Microsoft Azure Import/Export Service tooTransfer Data tooBlob Storage](../storage-import-export-service.md).</span></span>

## <a name="pricing"></a><span data-ttu-id="e337d-272">가격</span><span class="sxs-lookup"><span data-stu-id="e337d-272">Pricing</span></span>

<span data-ttu-id="e337d-273">Azure 저장소에 대 한 가격에 대 한 자세한 내용은 참조 hello [가격 책정 페이지](https://azure.microsoft.com/pricing/details/storage/blobs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-273">For detailed information about pricing for Azure Storage, see hello [Pricing page](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>

## <a name="storage-apis-libraries-and-tools"></a><span data-ttu-id="e337d-274">Storage API, 라이브러리 및 도구</span><span class="sxs-lookup"><span data-stu-id="e337d-274">Storage APIs, libraries, and tools</span></span>
<span data-ttu-id="e337d-275">Azure Storage 리소스는 HTTP/HTTPS 요청을 수행할 수 있는 모든 언어로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-275">Azure Storage resources can be accessed by any language that can make HTTP/HTTPS requests.</span></span> <span data-ttu-id="e337d-276">또한 Azure storage는 많이 사용되는 몇 가지 언어를 위한 프로그래밍 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-276">Additionally, Azure Storage offers programming libraries for several popular languages.</span></span> <span data-ttu-id="e337d-277">이 라이브러리는 동기/비동기 호출, 작업 일괄 처리, 예외 관리, 자동 재시도, 작업자 동작 등과 같은 세부 사항을 처리하여 Azure Storage 작업의 많은 측면을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="e337d-277">These libraries simplify many aspects of working with Azure Storage by handling details such as synchronous and asynchronous invocation, batching of operations, exception management, automatic retries, operational behavior, and so forth.</span></span> <span data-ttu-id="e337d-278">다음 언어 hello에 대 한 현재 사용할 수 있는지 확인 하 고 플랫폼에서 다른 사용자와 hello 파이프라인:</span><span class="sxs-lookup"><span data-stu-id="e337d-278">Libraries are currently available for hello following languages and platforms, with others in hello pipeline:</span></span>

### <a name="azure-storage-data-services"></a><span data-ttu-id="e337d-279">Azure Storage 데이터 서비스</span><span class="sxs-lookup"><span data-stu-id="e337d-279">Azure Storage data services</span></span>
* [<span data-ttu-id="e337d-280">저장소 서비스 REST API</span><span class="sxs-lookup"><span data-stu-id="e337d-280">Storage Services REST API</span></span>](/rest/api/storageservices/)
* [<span data-ttu-id="e337d-281">.NET용 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="e337d-281">Storage Client Library for .NET</span></span>](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [<span data-ttu-id="e337d-282">Storage Client Library for C++</span><span class="sxs-lookup"><span data-stu-id="e337d-282">Storage Client Library for C++</span></span>](https://github.com/Azure/azure-storage-cpp)
* [<span data-ttu-id="e337d-283">Java/Android용 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="e337d-283">Storage Client Library for Java/Android</span></span>](https://azure.microsoft.com/develop/java/)
* [<span data-ttu-id="e337d-284">Node.js용 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="e337d-284">Storage Client Library for Node.js</span></span>](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [<span data-ttu-id="e337d-285">PHP용 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="e337d-285">Storage Client Library for PHP</span></span>](https://azure.microsoft.com/develop/php/)
* [<span data-ttu-id="e337d-286">Python용 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="e337d-286">Storage Client Library for Python</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="e337d-287">Ruby용 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="e337d-287">Storage Client Library for Ruby</span></span>](https://azure.microsoft.com/develop/ruby/)
* [<span data-ttu-id="e337d-288">PowerShell용 Storage Cmdlet</span><span class="sxs-lookup"><span data-stu-id="e337d-288">Storage Cmdlets for PowerShell</span></span>](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)
* [<span data-ttu-id="e337d-289">CLI 2.0의 저장소 명령</span><span class="sxs-lookup"><span data-stu-id="e337d-289">Storage Commands for CLI 2.0</span></span>](/cli/azure/storage)

## <a name="next-steps"></a><span data-ttu-id="e337d-290">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e337d-290">Next steps</span></span>

* [<span data-ttu-id="e337d-291">Blob Storage에 대한 세부 정보</span><span class="sxs-lookup"><span data-stu-id="e337d-291">Learn more about Blob storage</span></span>](../blobs/storage-blobs-introduction.md)
* [<span data-ttu-id="e337d-292">File Storage에 대한 세부 정보</span><span class="sxs-lookup"><span data-stu-id="e337d-292">Learn more about File storage</span></span>](../storage-files-introduction.md)
* [<span data-ttu-id="e337d-293">Queue Storage에 대한 세부 정보</span><span class="sxs-lookup"><span data-stu-id="e337d-293">Learn more about Queue storage</span></span>](../queues/storage-queues-introduction.md)

<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->

<!-- FIGURE OUT WHAT tooDO WITH ALL THESE LINKS.

Azure Storage resources can be accessed by any language that can make HTTP/HTTPS requests. Additionally, Azure Storage offers programming libraries for several popular languages. These libraries simplify many aspects of working with Azure Storage by handling details such as synchronous and asynchronous invocation, batching of operations, exception management, automatic retries, operational behavior and so forth. Libraries are currently available for hello following languages and platforms, with others in hello pipeline:

### Azure Storage data services
* [Storage Services REST API](https://docs.microsoft.com/rest/api/storageservices/)
* [Storage Client Library for .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp)
* [Storage Client Library for Java/Android](https://azure.microsoft.com/develop/java/)
* [Storage Client Library for Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Storage Client Library for PHP](https://azure.microsoft.com/develop/php/)
* [Storage Client Library for Python](https://azure.microsoft.com/develop/python/)
* [Storage Client Library for Ruby](https://azure.microsoft.com/develop/ruby/)
* [Storage Cmdlets for PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)

### Azure Storage management services
* [Storage Resource Provider REST API Reference](/rest/api/storagerp/)
* [Storage Resource Provider Client Library for .NET](/dotnet/api/microsoft.azure.management.storage)
* [Storage Resource Provider Cmdlets for PowerShell 1.0](/powershell/module/azure.storage)
* [Storage Service Management REST API (Classic)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### Azure Storage data movement services
* [Storage Import/Export Service REST API](../storage-import-export-service.md)
* [Storage Data Movement Client Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### Tools and utilities
* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.
* [Azure Storage Client Tools](../storage-explorers.md)
* [Azure SDKs and Tools](https://azure.microsoft.com/tools/)
* [Azure Storage Emulator](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy Command-Line Utility](http://aka.ms/downloadazcopy)

## Next steps
toolearn more about Azure Storage, explore these resources:

### Documentation
* [Azure Storage Documentation](https://azure.microsoft.com/documentation/services/storage/)
* [Create a storage account](../storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a><span data-ttu-id="e337d-294">관리자용</span><span class="sxs-lookup"><span data-stu-id="e337d-294">For administrators</span></span>
* [<span data-ttu-id="e337d-295">Azure Storage와 함께 Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="e337d-295">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="e337d-296">Azure Storage에서 Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="e337d-296">Using Azure CLI with Azure Storage</span></span>](../storage-azure-cli.md)

### <a name="for-net-developers"></a><span data-ttu-id="e337d-297">.NET 개발자용</span><span class="sxs-lookup"><span data-stu-id="e337d-297">For .NET developers</span></span>
* [<span data-ttu-id="e337d-298">.NET을 사용하여 Azure Blob 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="e337d-298">Get started with Azure Blob storage using .NET</span></span>](../blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="e337d-299">.NET을 사용하여 Azure 테이블 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="e337d-299">Get started with Azure Table storage using .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="e337d-300">.NET을 사용하여 Azure 큐 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="e337d-300">Get started with Azure Queue storage using .NET</span></span>](../storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="e337d-301">Windows에서 Azure 파일 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="e337d-301">Get started with Azure File storage on Windows</span></span>](../storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a><span data-ttu-id="e337d-302">Java/Android 개발자용</span><span class="sxs-lookup"><span data-stu-id="e337d-302">For Java/Android developers</span></span>
* [<span data-ttu-id="e337d-303">어떻게 toouse Java에서 Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-303">How toouse Blob storage from Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="e337d-304">어떻게 toouse Java에서 테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-304">How toouse Table storage from Java</span></span>](../../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="e337d-305">어떻게 toouse Java에서 큐 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-305">How toouse Queue storage from Java</span></span>](../storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="e337d-306">어떻게 toouse Java에서 파일 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-306">How toouse File storage from Java</span></span>](../storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a><span data-ttu-id="e337d-307">Node.js 개발자용</span><span class="sxs-lookup"><span data-stu-id="e337d-307">For Node.js developers</span></span>
* [<span data-ttu-id="e337d-308">어떻게 toouse Node.js에서 Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-308">How toouse Blob storage from Node.js</span></span>](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="e337d-309">어떻게 toouse Node.js에서 테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-309">How toouse Table storage from Node.js</span></span>](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [<span data-ttu-id="e337d-310">어떻게 toouse Node.js에서 큐 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-310">How toouse Queue storage from Node.js</span></span>](../storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a><span data-ttu-id="e337d-311">PHP 개발자용</span><span class="sxs-lookup"><span data-stu-id="e337d-311">For PHP developers</span></span>
* [<span data-ttu-id="e337d-312">어떻게 toouse PHP에서 Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-312">How toouse Blob storage from PHP</span></span>](../blobs/storage-php-how-to-use-blobs.md)
* [<span data-ttu-id="e337d-313">어떻게 toouse PHP에서 테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-313">How toouse Table storage from PHP</span></span>](../../cosmos-db/table-storage-how-to-use-php.md)
* [<span data-ttu-id="e337d-314">어떻게 toouse PHP에서 큐 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-314">How toouse Queue storage from PHP</span></span>](../storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a><span data-ttu-id="e337d-315">Ruby 개발자용</span><span class="sxs-lookup"><span data-stu-id="e337d-315">For Ruby developers</span></span>
* [<span data-ttu-id="e337d-316">어떻게 toouse Ruby에서 Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-316">How toouse Blob storage from Ruby</span></span>](../blobs/storage-ruby-how-to-use-blob-storage.md)
* [<span data-ttu-id="e337d-317">어떻게 toouse Ruby에서 테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-317">How toouse Table storage from Ruby</span></span>](../../cosmos-db/table-storage-how-to-use-ruby.md)
* [<span data-ttu-id="e337d-318">어떻게 toouse Ruby에서 큐 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-318">How toouse Queue storage from Ruby</span></span>](../storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a><span data-ttu-id="e337d-319">Python 개발자용</span><span class="sxs-lookup"><span data-stu-id="e337d-319">For Python developers</span></span>
* [<span data-ttu-id="e337d-320">어떻게 toouse Python에서 Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-320">How toouse Blob storage from Python</span></span>](../blobs/storage-python-how-to-use-blob-storage.md)
* [<span data-ttu-id="e337d-321">어떻게 toouse Python에서 테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-321">How toouse Table storage from Python</span></span>](../../cosmos-db/table-storage-how-to-use-python.md)
* [<span data-ttu-id="e337d-322">어떻게 toouse Python에서 큐 저장소</span><span class="sxs-lookup"><span data-stu-id="e337d-322">How toouse Queue storage from Python</span></span>](../storage-python-how-to-use-queue-storage.md)   
* <span data-ttu-id="e337d-323">[어떻게 toouse Python에서 파일 저장소](../storage-python-how-to-use-file-storage.md) 
--></span><span class="sxs-lookup"><span data-stu-id="e337d-323">[How toouse File storage from Python](../storage-python-how-to-use-file-storage.md) 
--></span></span>