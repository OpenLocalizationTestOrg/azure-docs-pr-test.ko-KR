---
title: "Azure Storage 소개 | Microsoft Docs"
description: "클라우드의 Microsoft 데이터 저장소인 Azure Storage 개요입니다."
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
ms.openlocfilehash: 163f35682a4fdaa971f715c7429153bfdcf6a584
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
<!-- this is the same version that is in the MVC branch -->
# <a name="introduction-to-microsoft-azure-storage"></a><span data-ttu-id="b3b27-103">Microsoft Azure Storage 소개</span><span class="sxs-lookup"><span data-stu-id="b3b27-103">Introduction to Microsoft Azure Storage</span></span>

<span data-ttu-id="b3b27-104">Microsoft Azure Storage는 가용성, 보안, 내구성, 확장성 및 중복성이 높은 저장소를 제공하는 Microsoft 관리 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-104">Microsoft Azure Storage is a Microsoft-managed cloud service that provides storage that is highly available, secure, durable, scalable, and redundant.</span></span> <span data-ttu-id="b3b27-105">Microsoft는 유지 관리를 담당하고 사용자에 대한 중요한 문제를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-105">Microsoft takes care of maintenance and handles critical problems for you.</span></span> 

<span data-ttu-id="b3b27-106">Azure Storage는 Blob Storage, File Storage 및 Queue Storage라는 세 개의 데이터 서비스로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-106">Azure Storage consists of three data services: Blob storage, File storage, and Queue storage.</span></span> <span data-ttu-id="b3b27-107">Blob Storage는 가장 빠른 성능을 가진 SSD를 사용하는 프리미엄 저장소에서 표준 및 프리미엄 저장소를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-107">Blob storage supports both standard and premium storage, with premium storage using only SSDs for the fastest performance possible.</span></span> <span data-ttu-id="b3b27-108">다른 기능은 쿨 저장소이며 낮은 비용으로 자주 액세스하지 않는 데이터의 대용량 저장소를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-108">Another feature is cool storage, allowing you to storage large amounts of rarely accessed data for a lower cost.</span></span>

<span data-ttu-id="b3b27-109">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-109">In this article, you learn about the following:</span></span>
* <span data-ttu-id="b3b27-110">Azure Storage 서비스</span><span class="sxs-lookup"><span data-stu-id="b3b27-110">the Azure Storage services</span></span>
* <span data-ttu-id="b3b27-111">저장소 계정 유형</span><span class="sxs-lookup"><span data-stu-id="b3b27-111">the types of storage accounts</span></span>
* <span data-ttu-id="b3b27-112">Blob, 큐 및 파일에 액세스</span><span class="sxs-lookup"><span data-stu-id="b3b27-112">accessing your blobs, queues, and files</span></span>
* <span data-ttu-id="b3b27-113">암호화</span><span class="sxs-lookup"><span data-stu-id="b3b27-113">encryption</span></span>
* <span data-ttu-id="b3b27-114">복제</span><span class="sxs-lookup"><span data-stu-id="b3b27-114">replication</span></span> 
* <span data-ttu-id="b3b27-115">저장소 간에 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="b3b27-115">transferring data into or out of storage</span></span>
* <span data-ttu-id="b3b27-116">사용할 수 있는 여러 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="b3b27-116">the many storage client libraries available.</span></span> 


<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
To get up and running with Azure Storage quickly, check out one of the following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->


## <a name="introducing-the-azure-storage-services"></a><span data-ttu-id="b3b27-117">Azure Storage 서비스 소개</span><span class="sxs-lookup"><span data-stu-id="b3b27-117">Introducing the Azure Storage services</span></span>

<span data-ttu-id="b3b27-118">Blob Storage, File Storage 및 Queue Storage와 같은 Azure Storage에서 제공하는 서비스 중 하나를 사용하려면 먼저 저장소 계정을 만들고 해당 저장소 계정에서 특정 서비스 간에 데이터를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-118">To use any of the services provided by Azure Storage -- Blob storage, File storage, and Queue storage -- you first create a storage account, and then you can transfer data to/from a specific service in that storage account.</span></span> 

## <a name="blob-storage"></a><span data-ttu-id="b3b27-119">Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="b3b27-119">Blob storage</span></span>

<span data-ttu-id="b3b27-120">Blob은 기본적으로 사용자가 컴퓨터(또는 태블릿, 모바일 장치 등)에 저장한 항목과 같은 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-120">Blobs are basically files like those that you store on your computer (or tablet, mobile device, and so on).</span></span> <span data-ttu-id="b3b27-121">사진, Microsoft Excel 파일, HTML 파일, 가상 하드 디스크(VHD), 로그와 같은 빅 데이터, 데이터베이스 백업 등 거의 모든 것이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-121">They can be pictures, Microsoft Excel files, HTML files, virtual hard disks (VHDs), big data such as logs, database backups  -- pretty much anything.</span></span> <span data-ttu-id="b3b27-122">Blob은 폴더와 유사한 컨테이너에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-122">Blobs are stored in containers, which are similar to folders.</span></span> 

<span data-ttu-id="b3b27-123">Blob Storage에 파일을 저장한 후에 URL, REST 인터페이스 또는 Azure SDK 저장소 클라이언트 라이브러리 중 하나를 사용하여 전 세계 어디에서든지 해당 파일에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-123">After storing files in Blob storage, you can access them from anywhere in the world using URLs, the REST interface, or one of the Azure SDK storage client libraries.</span></span> <span data-ttu-id="b3b27-124">저장소 클라이언트 라이브러리는 Node.js, Java, PHP, Ruby, Python 및 .NET을 비롯한 여러 언어에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-124">Storage client libraries are available for multiple languages, including Node.js, Java, PHP, Ruby, Python, and .NET.</span></span> 

<span data-ttu-id="b3b27-125">블록 Blob, 추가 Blob 및 페이지 Blob라는 세 가지 Blob 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-125">There are three types of blobs -- block blobs, append blobs, and page blobs (used for VHD files).</span></span>

* <span data-ttu-id="b3b27-126">블록 Blob은 최대 약 4.7 TB의 일반 파일을 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-126">Block blobs are used to hold ordinary files up to about 4.7 TB.</span></span> 
* <span data-ttu-id="b3b27-127">페이지 Blob은 최대 8TB 크기의 임의 액세스 파일을 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-127">Page blobs are used to hold random access files up to 8 TB in size.</span></span> <span data-ttu-id="b3b27-128">이러한 Blob은 VM을 백업하는 VHD 파일에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-128">These are used for the VHD files that back VMs.</span></span>
* <span data-ttu-id="b3b27-129">추가 Blob은 블록 Blob과 같이 블록으로 구성되지만 추가 작업에 최적화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-129">Append blobs are made up of blocks like the block blobs, but are optimized for append operations.</span></span> <span data-ttu-id="b3b27-130">이러한 Blob은 여러 VM에서 동일한 Blob에 정보를 기록하는 등의 작업에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-130">These are used for things like logging information to the same blob from multiple VMs.</span></span>

<span data-ttu-id="b3b27-131">네트워크 제약 조건으로 인해 네트워크를 통해 Blob 저장소를 대상으로 데이터를 업로드하거나 다운로드하는 것이 불가능한 대규모 데이터 집합의 경우, 일련의 하드 드라이브를 Microsoft로 운송하여 데이터 센터에서 바로 데이터를 가져오거나 내보내도록 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-131">For very large datasets where network constraints make uploading or downloading data to Blob storage over the wire unrealistic, you can ship a set of hard drives to Microsoft to import or export data directly from the data center.</span></span> <span data-ttu-id="b3b27-132">[Microsoft Azure Import/Export 서비스를 사용하여 Blob Storage로 데이터 전송](../storage-import-export-service.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3b27-132">See [Use the Microsoft Azure Import/Export Service to Transfer Data to Blob Storage](../storage-import-export-service.md).</span></span>

## <a name="file-storage"></a><span data-ttu-id="b3b27-133">File Storage</span><span class="sxs-lookup"><span data-stu-id="b3b27-133">File storage</span></span>

<span data-ttu-id="b3b27-134">Azure Files 서비스를 사용하면 표준 SMB(서버 메시지 블록) 프로토콜을 사용하여 액세스할 수 있는 고가용성 네트워크 파일 공유를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-134">The Azure Files service enables you to set up highly available network file shares that can be accessed by using the standard Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="b3b27-135">즉, 여러 VM이 읽기 및 쓰기 권한을 모두 사용하여 동일한 파일을 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-135">That means that multiple VMs can share the same files with both read and write access.</span></span> <span data-ttu-id="b3b27-136">또한 REST 인터페이스 또는 저장소 클라이언트 라이브러리를 사용하여 파일을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-136">You can also read the files using the REST interface or the storage client libraries.</span></span> 

<span data-ttu-id="b3b27-137">Azure File 저장소가 회사 파일 공유의 파일과 다른 점 한 가지는 파일을 가리키고 SAS(공유 액세스 서명) 토큰을 포함하고 있는 URL을 사용하여 전 세계 어디서나 파일에 액세스할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-137">One thing that distinguishes Azure File storage from files on a corporate file share is that you can access the files from anywhere in the world using a URL that points to the file and includes a shared access signature (SAS) token.</span></span> <span data-ttu-id="b3b27-138">SAS 토큰은 생성 가능하며 특정 기간에 개인 자산에 대한 특정 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-138">You can generate SAS tokens; they allow specific access to a private asset for a specific amount of time.</span></span> 

<span data-ttu-id="b3b27-139">파일 공유는 다음과 같은 여러 가지 일반적인 시나리오에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-139">File shares can be used for many common scenarios:</span></span> 

* <span data-ttu-id="b3b27-140">여러 온-프레미스 응용 프로그램에서 파일 공유를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-140">Many on-premises applications use file shares.</span></span> <span data-ttu-id="b3b27-141">이 기능을 사용하면 데이터를 공유하는 응용 프로그램을 Azure로 보다 쉽게 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-141">This feature makes it easier to migrate those applications that share data to Azure.</span></span> <span data-ttu-id="b3b27-142">파일 공유를 온-프레미스 응용 프로그램에서 사용하는 것과 동일한 드라이브 문자에 탑재하면 파일 공유에 액세스하는 응용 프로그램의 일부가 최소한의 변경 내용(있는 경우)으로 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-142">If you mount the file share to the same drive letter that the on-premises application uses, the part of your application that accesses the file share should work with minimal, if any, changes.</span></span>

* <span data-ttu-id="b3b27-143">구성 파일을 파일 공유에 저장하고 여러 VM에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-143">Configuration files can be stored on a file share and accessed from multiple VMs.</span></span> <span data-ttu-id="b3b27-144">그룹의 여러 개발자가 사용하는 도구 및 유틸리티를 파일 공유에 저장할 수 있으며, 이렇게 하면 모든 사람이 찾아서 동일한 버전을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-144">Tools and utilities used by multiple developers in a group can be stored on a file share, ensuring that everybody can find them, and that they use the same version.</span></span>

* <span data-ttu-id="b3b27-145">파일 공유에 쓰고 나중에 처리하거나 분석할 수 있는 데이터의 세 가지 예로 진단 로그, 메트릭 및 크래시 덤프를 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-145">Diagnostic logs, metrics, and crash dumps are just three examples of data that can be written to a file share and processed or analyzed later.</span></span>

<span data-ttu-id="b3b27-146">현재는 Active Directory 기반 인증과 ACL(액세스 제어 목록)이 지원되지 않지만 향후 지원할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-146">At this time, Active Directory-based authentication and access control lists (ACLs) are not supported, but they will be at some time in the future.</span></span> <span data-ttu-id="b3b27-147">파일 공유 액세스에 대한 인증을 제공하기 위해 저장소 계정 자격 증명이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-147">The storage account credentials are used to provide authentication for access to the file share.</span></span> <span data-ttu-id="b3b27-148">즉, 공유가 탑재된 모든 사용자는 공유에 대한 전체 읽기/쓰기 액세스 권한을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-148">This means anybody with the share mounted will have full read/write access to the share.</span></span>

## <a name="queue-storage"></a><span data-ttu-id="b3b27-149">큐 저장소</span><span class="sxs-lookup"><span data-stu-id="b3b27-149">Queue storage</span></span>

<span data-ttu-id="b3b27-150">Azure 큐 서비스는 메시지를 저장하고 검색하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-150">The Azure Queue service is used to store and retrieve messages.</span></span> <span data-ttu-id="b3b27-151">큐 메시지의 크기는 최대 64KB일 수 있고 큐에는 수 많은 메시지가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-151">Queue messages can be up to 64 KB in size, and a queue can contain millions of messages.</span></span> <span data-ttu-id="b3b27-152">큐는 일반적으로 비동기적으로 처리될 메시지의 목록을 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-152">Queues are generally used to store lists of messages to be processed asynchronously.</span></span> 

<span data-ttu-id="b3b27-153">예를 들어 고객이 사진을 업로드하여 각 사진에 대한 썸네일을 만들려고 한다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-153">For example, say you want your customers to be able to upload pictures, and you want to create thumbnails for each picture.</span></span> <span data-ttu-id="b3b27-154">고객이 사진을 업로드하는 동안 썸네일을 만들 때까지 기다리게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-154">You could have your customer wait for you to create the thumbnails while uploading the pictures.</span></span> <span data-ttu-id="b3b27-155">대신 큐를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-155">An alternative would be to use a queue.</span></span> <span data-ttu-id="b3b27-156">고객이 업로드를 완료하면 큐에 메시지를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-156">When the customer finishes his upload, write a message to the queue.</span></span> <span data-ttu-id="b3b27-157">그런 다음 Azure Function에서는 큐의 메시지를 검색하고 썸네일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-157">Then have an Azure Function retrieve the message from the queue and create the thumbnails.</span></span> <span data-ttu-id="b3b27-158">이 프로세스의 일부는 각각 별도로 확장될 수 있으며 사용하기 위해 조정하는 경우 더 세밀하게 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-158">Each of the parts of this processing can be scaled separately, giving you more control when tuning it for your usage.</span></span>

<!-- this bookmark is used by other articles; you'll need to update them before this goes into production ROBIN-->
## <a name="table-storage"></a><span data-ttu-id="b3b27-159">테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="b3b27-159">Table storage</span></span>
<!-- add a link to the old table storage to this paragraph once it's moved -->
<span data-ttu-id="b3b27-160">이제 표준 Azure Table Storage는 Cosmos DB의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-160">Standard Azure Table Storage is now part of Cosmos DB.</span></span> <span data-ttu-id="b3b27-161">또한 처리량 최적화 테이블, 글로벌 분포 및 자동 보조 인덱스를 제공하는 Azure Table Storage에 대한 프리미엄 테이블이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-161">Also available is Premium Tables for Azure Table storage, offering throughput-optimized tables, global distribution, and automatic secondary indexes.</span></span> <span data-ttu-id="b3b27-162">새로운 프리미엄 환경에 대해 알아보고 사용해 보려면 [Azure Cosmos DB: 테이블 API](https://aka.ms/premiumtables)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="b3b27-162">To learn more and try out the new premium experience, please check out [Azure Cosmos DB: Table API](https://aka.ms/premiumtables).</span></span>

## <a name="disk-storage"></a><span data-ttu-id="b3b27-163">디스크 저장소</span><span class="sxs-lookup"><span data-stu-id="b3b27-163">Disk storage</span></span>

<span data-ttu-id="b3b27-164">또한 Azure Storage 팀은 가상 컴퓨터에서 사용하는 관리되는 디스크 및 관리되지 않는 디스크 기능을 모두 포함하는 디스크를 소유합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-164">The Azure Storage team also owns Disks, which includes all of the managed and unmanaged disk capabilities used by virtual machines.</span></span> <span data-ttu-id="b3b27-165">이러한 기능에 대한 자세한 내용은 [Compute Service 설명서](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3b27-165">For more information about these features, please see the [Compute Service documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>

## <a name="types-of-storage-accounts"></a><span data-ttu-id="b3b27-166">저장소 계정 유형</span><span class="sxs-lookup"><span data-stu-id="b3b27-166">Types of storage accounts</span></span> 

<span data-ttu-id="b3b27-167">이 표에서는 개체에서 사용할 수 있는 다양한 종류의 저장소 계정을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-167">This table shows the various kinds of storage accounts and which objects can be used with each.</span></span>

|<span data-ttu-id="b3b27-168">**저장소 계정의 유형**</span><span class="sxs-lookup"><span data-stu-id="b3b27-168">**Type of storage account**</span></span>|<span data-ttu-id="b3b27-169">**범용 표준**</span><span class="sxs-lookup"><span data-stu-id="b3b27-169">**General-purpose Standard**</span></span>|<span data-ttu-id="b3b27-170">**범용 프리미엄**</span><span class="sxs-lookup"><span data-stu-id="b3b27-170">**General-purpose Premium**</span></span>|<span data-ttu-id="b3b27-171">**Blob Storage, 핫 및 쿨 액세스 계층**</span><span class="sxs-lookup"><span data-stu-id="b3b27-171">**Blob storage, hot and cool access tiers**</span></span>|
|-----|-----|-----|-----|
|<span data-ttu-id="b3b27-172">**지원되는 서비스**</span><span class="sxs-lookup"><span data-stu-id="b3b27-172">**Services supported**</span></span>| <span data-ttu-id="b3b27-173">Blob, File, Queue 서비스</span><span class="sxs-lookup"><span data-stu-id="b3b27-173">Blob, File, Queue Services</span></span> | <span data-ttu-id="b3b27-174">Blob Service</span><span class="sxs-lookup"><span data-stu-id="b3b27-174">Blob Service</span></span> | <span data-ttu-id="b3b27-175">Blob Service</span><span class="sxs-lookup"><span data-stu-id="b3b27-175">Blob Service</span></span>|
|<span data-ttu-id="b3b27-176">**지원되는 Blob 유형**</span><span class="sxs-lookup"><span data-stu-id="b3b27-176">**Types of blobs supported**</span></span>|<span data-ttu-id="b3b27-177">블록 Blob, 페이지 Blob 및 추가 Blob</span><span class="sxs-lookup"><span data-stu-id="b3b27-177">Block blobs, page blobs, and append blobs</span></span> | <span data-ttu-id="b3b27-178">페이지 Blob</span><span class="sxs-lookup"><span data-stu-id="b3b27-178">Page blobs</span></span> | <span data-ttu-id="b3b27-179">블록 Blob 및 추가 Blob</span><span class="sxs-lookup"><span data-stu-id="b3b27-179">Block blobs and append blobs</span></span>|

### <a name="general-purpose-storage-accounts"></a><span data-ttu-id="b3b27-180">범용 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="b3b27-180">General-purpose storage accounts</span></span>

<span data-ttu-id="b3b27-181">범용 저장소 계정에는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-181">There are two kinds of general-purpose storage accounts.</span></span> 

#### <a name="standard-storage"></a><span data-ttu-id="b3b27-182">Standard Storage</span><span class="sxs-lookup"><span data-stu-id="b3b27-182">Standard storage</span></span> 

<span data-ttu-id="b3b27-183">가장 널리 사용되는 저장소 계정은 모든 유형의 데이터에 사용할 수 있는 표준 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-183">The most widely used storage accounts are standard storage accounts, which can be used for all types of data.</span></span> <span data-ttu-id="b3b27-184">표준 저장소 계정은 자기 미디어를 사용하여 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-184">Standard storage accounts use magnetic media to store data.</span></span>

#### <a name="premium-storage"></a><span data-ttu-id="b3b27-185">Premium Storage</span><span class="sxs-lookup"><span data-stu-id="b3b27-185">Premium storage</span></span>

<span data-ttu-id="b3b27-186">프리미엄 저장소는 VHD 파일에 주로 사용되는 페이지 Blob에 고성능 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-186">Premium storage provides high-performance storage for page blobs, which are primarily used for VHD files.</span></span> <span data-ttu-id="b3b27-187">프리미엄 저장소 계정은 SSD를 사용하여 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-187">Premium storage accounts use SSD to store data.</span></span> <span data-ttu-id="b3b27-188">모든 VM에 Premium Storage를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-188">Microsoft recommends using Premium Storage for all of your VMs.</span></span>

### <a name="blob-storage-accounts"></a><span data-ttu-id="b3b27-189">Blob Storage 계정</span><span class="sxs-lookup"><span data-stu-id="b3b27-189">Blob Storage accounts</span></span>

<span data-ttu-id="b3b27-190">Blob Storage 계정은 블록 Blob 및 추가 Blob을 저장하는 데 사용되는 특별한 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-190">The Blob Storage account is a specialized storage account used to store block blobs and append blobs.</span></span> <span data-ttu-id="b3b27-191">이러한 계정에 페이지 Blob을 저장할 수 없습니다. 따라서 VHD 파일을 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-191">You can't store page blobs in these accounts, therefore you can't store VHD files.</span></span> <span data-ttu-id="b3b27-192">이러한 계정을 사용하면 액세스 계층을 핫 또는 쿨로 설정할 수 있습니다. 계층은 언제든지 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-192">These accounts allow you to set an access tier to Hot or Cool; the tier can be changed at any time.</span></span> 

<span data-ttu-id="b3b27-193">핫 액세스 계층은 자주 액세스 하는 파일에 대해 사용합니다. 저장소의 경우 비용이 많이 들지만 Blob에 액세스하는 비용이 훨씬 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-193">The hot access tier is used for files that are accessed frequently -- you pay a higher cost for storage, but the cost of accessing the blobs is much lower.</span></span> <span data-ttu-id="b3b27-194">쿨 액세스 계층에 저장된 Blob의 경우 Blob에 액세스하기 위한 비용이 많이 들지만 저장소 비용이 훨씬 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-194">For blobs stored in the cool access tier, you pay a higher cost for accessing the blobs, but the cost of storage is much lower.</span></span>

## <a name="accessing-your-blobs-files-and-queues"></a><span data-ttu-id="b3b27-195">Blob, 파일 및 큐에 액세스</span><span class="sxs-lookup"><span data-stu-id="b3b27-195">Accessing your blobs, files, and queues</span></span>

<span data-ttu-id="b3b27-196">각 저장소 계정에는 모든 작업에 사용할 수 있는 두 개의 인증 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-196">Each storage account has two authentication keys, either of which can be used for any operation.</span></span> <span data-ttu-id="b3b27-197">경우에 따라 보안을 강화하기 위해 키를 롤백할 수 있도록 구 개의 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-197">There are two keys so you can roll over the keys occasionally to enhance security.</span></span> <span data-ttu-id="b3b27-198">키 소유권과 계정 이름이 있으면 저장소 계정의 모든 데이터에 무제한 액세스할 수 있으므로 이러한 키를 안전하게 보관하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-198">It is critical that these keys be kept secure because their possession, along with the account name, allows unlimited access to all data in the storage account.</span></span> 

<span data-ttu-id="b3b27-199">이 섹션에서는 저장소 계정 및 해당 데이터를 보호하는 두 가지 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-199">This section looks two ways to secure the storage account and its data.</span></span> <span data-ttu-id="b3b27-200">저장소 계정 및 데이터를 보호하는 방법에 대한 자세한 내용은 [Azure Storage 보안 가이드](storage-security-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3b27-200">For detailed information about securing your storage account and your data, see the [Azure Storage security guide](storage-security-guide.md).</span></span>

### <a name="securing-access-to-storage-accounts-using-azure-ad"></a><span data-ttu-id="b3b27-201">Azure AD를 사용하여 저장소 계정에 대한 액세스 보호</span><span class="sxs-lookup"><span data-stu-id="b3b27-201">Securing access to storage accounts using Azure AD</span></span>

<span data-ttu-id="b3b27-202">저장소 데이터에 대한 액세스를 보호하는 한 가지 방법은 저장소 계정 키에 대한 액세스를 제어하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-202">One way to secure access to your storage data is by controlling access to the storage account keys.</span></span> <span data-ttu-id="b3b27-203">리소스 관리자 RBAC(역할 기반 액세스 제어)를 사용하여 사용자, 그룹 또는 응용 프로그램에 역할을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-203">With Resource Manager Role-Based Access Control (RBAC), you can assign roles to users, groups, or applications.</span></span> <span data-ttu-id="b3b27-204">이러한 역할은 허용되거나 허용되지 않는 작업의 특정 집합에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-204">These roles are tied to a specific set of actions that are allowed or disallowed.</span></span> <span data-ttu-id="b3b27-205">RBAC를 사용하여 저장소 계정에 대한 액세스 권한을 부여하는 경우 액세스 계층을 변경하는 등 해당 저장소 계정에 대한 관리 작업만을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-205">Using RBAC to grant access to a storage account only handles the management operations for that storage account, such as changing the access tier.</span></span> <span data-ttu-id="b3b27-206">RBAC를 사용하여 특정 컨테이너 또는 파일 공유와 같은 데이터 개체에 대한 액세스 권한을 부여할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-206">You can't use RBAC to grant access to data objects like a specific container or file share.</span></span> <span data-ttu-id="b3b27-207">그러나 RBAC를 사용하여 저장소 계정 키에 대한 액세스 권한을 부여할 수 있습니다. 그러면 데이터 개체를 읽는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-207">You can, however, use RBAC to grant access to the storage account keys, which can then be used to read the data objects.</span></span> 

### <a name="securing-access-using-shared-access-signatures"></a><span data-ttu-id="b3b27-208">공유 액세스 서명을 사용하여 액세스 보호</span><span class="sxs-lookup"><span data-stu-id="b3b27-208">Securing access using shared access signatures</span></span> 

<span data-ttu-id="b3b27-209">공유 액세스 서명 및 저장된 액세스 정책을 사용하여 데이터 개체를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-209">You can use shared access signatures and stored access policies to secure your data objects.</span></span> <span data-ttu-id="b3b27-210">SAS(공유 액세스 서명)은 자산의 URI에 추가할 수 있는 보안 토큰을 포함하는 문자열로, 특정 저장소 개체에 대한 액세스 권한을 위임하고 사용 권한 및 액세스의 날짜/시간 범위와 같은 제한을 지정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-210">A shared access signature (SAS) is a string containing a security token that can be attached to the URI for an asset that allows you to delegate access to specific storage objects and to specify constraints such as permissions and the date/time range of access.</span></span> <span data-ttu-id="b3b27-211">이 기능에는 광범위한 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-211">This feature has extensive capabilities.</span></span> <span data-ttu-id="b3b27-212">자세한 내용은 [SAS(공유 액세스 서명) 사용](storage-dotnet-shared-access-signature-part-1.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3b27-212">For detailed information, refer to [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>

### <a name="public-access-to-blobs"></a><span data-ttu-id="b3b27-213">Blob에 대한 공용 액세스</span><span class="sxs-lookup"><span data-stu-id="b3b27-213">Public access to blobs</span></span>

<span data-ttu-id="b3b27-214">Blob Service를 사용하면 컨테이너와 해당 Blob 또는 특정 Blob에 대한 공용 액세스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-214">The Blob Service allows you to provide public access to a container and its blobs, or a specific blob.</span></span> <span data-ttu-id="b3b27-215">컨테이너 또는 Blob을 공개로 지정하면 모든 사용자가 이 컨테이너 또는 Blob를 익명으로 읽을 수 있으며 인증이 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-215">When you indicate that a container or blob is public, anyone can read it anonymously; no authentication is required.</span></span> <span data-ttu-id="b3b27-216">이 작업을 수행하는 예제는 Blob Storage의 이미지, 비디오 또는 문서를 사용하는 웹 사이트가 있는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-216">An example of when you would want to do this is when you have a website that is using images, video, or documents from Blob storage.</span></span> <span data-ttu-id="b3b27-217">자세한 내용은 [컨테이너 및 Blob에 대한 익명 읽기 권한 관리](../blobs/storage-manage-access-to-resources.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3b27-217">For more information, see [Manage anonymous read access to containers and blobs](../blobs/storage-manage-access-to-resources.md)</span></span> 

## <a name="encryption"></a><span data-ttu-id="b3b27-218">암호화</span><span class="sxs-lookup"><span data-stu-id="b3b27-218">Encryption</span></span>

<span data-ttu-id="b3b27-219">Storage 서비스에 사용할 수 있는 기본적인 종류의 암호화에는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-219">There are a couple of basic kinds of encryption available for the Storage services.</span></span> 

### <a name="encryption-at-rest"></a><span data-ttu-id="b3b27-220">휴지 상태의 암호화</span><span class="sxs-lookup"><span data-stu-id="b3b27-220">Encryption at rest</span></span> 

<span data-ttu-id="b3b27-221">Azure Storage 계정의 파일 서비스(미리 보기) 또는 Blob service에서 SSE(저장소 서비스 암호화)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-221">You can enable Storage Service Encryption (SSE) on either the Files service (preview) or the Blob service for an Azure storage account.</span></span> <span data-ttu-id="b3b27-222">활성화되면 특정 서비스에 작성된 모든 데이터를 작성하기 전에 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-222">If enabled, all data written to the specific service is encrypted before written.</span></span> <span data-ttu-id="b3b27-223">데이터를 읽을 때 반환되기 전에 암호를 해독합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-223">When you read the data, it is decrypted before returned.</span></span> 

### <a name="client-side-encryption"></a><span data-ttu-id="b3b27-224">클라이언트 쪽 암호화</span><span class="sxs-lookup"><span data-stu-id="b3b27-224">Client-side encryption</span></span>

<span data-ttu-id="b3b27-225">저장소 클라이언트 라이브러리에는 네트워크를 통해 데이터를 클라이언트에서 Azure로 보내기 전에 프로그래밍 방식으로 암호화하도록 호출할 수 있는 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-225">The storage client libraries have methods you can call to programmatically encrypt data before sending it across the wire from the client to Azure.</span></span> <span data-ttu-id="b3b27-226">암호화되어 저장됩니다. 즉, 휴지 시 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-226">It is stored encrypted, which means it also is encrypted at rest.</span></span> <span data-ttu-id="b3b27-227">데이터를 다시 읽을 경우 받은 이후 정보의 암호를 해독합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-227">When reading the data back, you decrypt the information after receiving it.</span></span> 

### <a name="encryption-in-transit-with-azure-file-shares"></a><span data-ttu-id="b3b27-228">전송 시 Azure 파일 공유에서 암호화</span><span class="sxs-lookup"><span data-stu-id="b3b27-228">Encryption in transit with Azure File Shares</span></span>

<span data-ttu-id="b3b27-229">공유 액세스 서명에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용](../storage-dotnet-shared-access-signature-part-1.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3b27-229">See [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md) for more information on shared access signatures.</span></span> <span data-ttu-id="b3b27-230">안전한 저장소 계정 액세스에 대한 자세한 내용은 [컨테이너 및 Blob에 대한 익명 읽기 액세스 관리](../blobs/storage-manage-access-to-resources.md) 및 [Azure Storage 서비스에 대한 인증](https://msdn.microsoft.com/library/azure/dd179428.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3b27-230">See [Manage anonymous read access to containers and blobs](../blobs/storage-manage-access-to-resources.md) and [Authentication for the Azure Storage Services](https://msdn.microsoft.com/library/azure/dd179428.aspx) for more information on secure access to your storage account.</span></span>

<span data-ttu-id="b3b27-231">저장소 계정 및 암호화를 보호하는 방법에 대한 자세한 내용은 [Azure Storage 보안 가이드](storage-security-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3b27-231">For more details about securing your storage account and encryption, see the [Azure Storage security guide](storage-security-guide.md).</span></span>

## <a name="replication"></a><span data-ttu-id="b3b27-232">복제</span><span class="sxs-lookup"><span data-stu-id="b3b27-232">Replication</span></span>

<span data-ttu-id="b3b27-233">데이터가 지속되는지 확인하기 위해 Azure Storage에는 데이터의 여러 복사본을 유지(및 관리)하는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-233">In order to ensure that your data is durable, Azure Storage has the ability to keep (and manage) multiple copies of your data.</span></span> <span data-ttu-id="b3b27-234">이를 복제 또는 중복성이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-234">This is called replication, or sometimes redundancy.</span></span> <span data-ttu-id="b3b27-235">저장소 계정을 설정할 때 복제 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-235">When you set up your storage account, you select replication type.</span></span> <span data-ttu-id="b3b27-236">대부분의 경우에서 저장소 계정을 설정한 후에 이 설정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-236">In most cases, this setting can be modified after the storage account is set up.</span></span> 

<span data-ttu-id="b3b27-237">모든 저장소 계정에는 **LRS(로컬 중복 저장소)**가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-237">All storage accounts have **locally redundant storage (LRS)**.</span></span> <span data-ttu-id="b3b27-238">즉, 세 개의 데이터 복사본이 저장소 계정을 설정할 때 지정되는 데이터 센터의 Azure Storage에서 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-238">This means three copies of your data are managed by Azure Storage in the data center specified when the storage account was set up.</span></span> <span data-ttu-id="b3b27-239">변경 내용이 하나의 복사본에 커밋되는 경우 성공을 반환하기 전에 다른 두 개의 복사본이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-239">When changes are committed to one copy, the other two copies are updated before returning success.</span></span> <span data-ttu-id="b3b27-240">즉, 세 개의 복제본은 항상 동기화됩니다. 또한 세 개의 복사본이 별도의 오류 도메인 및 업그레이드 도메인에 위치합니다. 즉, 데이터를 보유하는 저장소 노드에 오류가 발생하거나 업데이트되기 위해 오프라인으로 전환되는 경우에도 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-240">This means the three replicas are always in sync. Also, the three copies reside in separate fault domains and upgrade domains, which means your data is available even if a storage node holding your data fails or is taken offline to be updated.</span></span> 

<span data-ttu-id="b3b27-241">**LRS(로컬 중복 저장소)**</span><span class="sxs-lookup"><span data-stu-id="b3b27-241">**Locally redundant storage (LRS)**</span></span>

<span data-ttu-id="b3b27-242">위에서 설명한 대로 LRS에서 세 개의 데이터 복사본이 단일 데이터 센터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-242">As explained above, with LRS you have three copies of your data in a single datacenter.</span></span> <span data-ttu-id="b3b27-243">저장소 노드에 오류가 발생하거나 업데이트되기 위해 오프라인으로 전환되는 경우 데이터를 사용할 수 없는 문제를 해결하지만 전체 데이터 센터를 사용할 수 없는 경우에는 해결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-243">This handles the problem of data becoming unavailable if a storage node fails or is taken offline to be updated, but not the case of an entire datacenter becoming unavailable.</span></span>

<span data-ttu-id="b3b27-244">**ZRS(영역 중복 저장소)**</span><span class="sxs-lookup"><span data-stu-id="b3b27-244">**Zone redundant storage (ZRS)**</span></span>

<span data-ttu-id="b3b27-245">ZRS(영역 중복 저장소)는 데이터의 세 가지 로컬 복사본뿐만 아니라 데이터의 다른 세 개 복사본 집합도 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-245">Zone-redundant storage (ZRS) maintains the three local copies of your data as well as another set of three copies of your data.</span></span> <span data-ttu-id="b3b27-246">세 개 복사본의 두 번째 집합은 하나 또는 두 개의 지역 내에서 데이터 센터 간에 비동기적으로 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-246">The second set of three copies is replicated asynchronously across datacenters within one or two regions.</span></span> <span data-ttu-id="b3b27-247">ZRS는 범용 저장소 계정에서 블록 Blob에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-247">Note that ZRS is only available for block blobs in general-purpose storage accounts.</span></span> <span data-ttu-id="b3b27-248">또한 저장소 계정을 만들고 ZRS를 선택하면 다른 복제 유형으로 또는 그 반대로 변환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-248">Also, once you have created your storage account and selected ZRS, you cannot convert it to use to any other type of replication, or vice versa.</span></span>

<span data-ttu-id="b3b27-249">ZRS 계정은 LRS보다 높은 지속성을 제공하지만 메트릭 또는 로깅 기능은 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-249">ZRS accounts provide higher durability than LRS, but ZRS accounts do not have metrics or logging capability.</span></span> 

<span data-ttu-id="b3b27-250">**GRS(지역 중복 저장소)**</span><span class="sxs-lookup"><span data-stu-id="b3b27-250">**Geo-redundant storage (GRS)**</span></span>

<span data-ttu-id="b3b27-251">GRS(지역 중복 저장소)는 기본 지역에서 데이터의 세 가지 로컬 복사본을 유지하고 기본 지역에서 수백 킬로미터 떨어진 보조 지역에서 데이터의 세 가지 복사본을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-251">Geo-redundant storage (GRS) maintains the three local copies of your data in a primary region plus another set of three copies of your data in a secondary region hundreds of miles away from the primary region.</span></span> <span data-ttu-id="b3b27-252">기본 지역의 오류 발생 시 Azure Storage는 보조 지역으로 장애 조치(Failover)됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-252">In the event of a failure at the primary region, Azure Storage will fail over to the secondary region.</span></span> 

<span data-ttu-id="b3b27-253">**RA-GRS(읽기 액세스 지역 중복 저장소)**</span><span class="sxs-lookup"><span data-stu-id="b3b27-253">**Read-access geo-redundant storage (RA-GRS)**</span></span> 

<span data-ttu-id="b3b27-254">읽기 액세스 지역 중복 저장소는 보조 위치에서 데이터에 대한 읽기 액세스를 가져온다는 점만 제외하고 GRS와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-254">Read-access geo-redundant storage is exactly like GRS except that you get read access to the data in the secondary location.</span></span> <span data-ttu-id="b3b27-255">기본 데이터 센터를 일시적으로 사용할 수 없는 경우 보조 위치에서 데이터를 계속 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-255">If the primary data center becomes unavailable temporarily, you can continue to read the data from the secondary location.</span></span> <span data-ttu-id="b3b27-256">이는 매우 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-256">This can be very helpful.</span></span> <span data-ttu-id="b3b27-257">예를 들어 읽기 전용 모드로 변경하고 보조 복사본을 가리키는 웹 응용 프로그램이 있으면 업데이트를 사용할 수 없는 경우에도 일부 액세스를 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-257">For example, you could have a web application that changes into read-only mode and points to the secondary copy, allowing some access even though updates are not available.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b3b27-258">계정을 만들 때 ZRS를 지정하지 않았다면 저장소 계정을 만든 후에 데이터가 복제되는 방법을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-258">You can change how your data is replicated after your storage account has been created, unless you specified ZRS when you created the account.</span></span> <span data-ttu-id="b3b27-259">그러나 LRS에서 GRS 또는 RA-GRS로 전환하면 추가적으로 1회 데이터 전송 비용이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-259">However, note that you may incur an additional one-time data transfer cost if you switch from LRS to GRS or RA-GRS.</span></span>
>

<span data-ttu-id="b3b27-260">복제에 대한 자세한 내용은 [Azure Storage 복제](storage-redundancy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3b27-260">For more information about replication, see [Azure Storage replication](storage-redundancy.md).</span></span>

<span data-ttu-id="b3b27-261">재해 복구 정보는 [Azure Storage 중단이 발생할 경우 수행할 작업](storage-disaster-recovery-guidance.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3b27-261">For disaster recovery information, see [What to do if an Azure Storage outage occurs](storage-disaster-recovery-guidance.md).</span></span>

<span data-ttu-id="b3b27-262">RA-GRS 저장소를 활용하여 고가용성을 설정하는 방법의 예제를 보려면 [RA-GRS를 사용하여 항상 사용 가능한 응용 프로그램 설계](storage-designing-ha-apps-with-ragrs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3b27-262">For an example of how to leverage RA-GRS storage to ensure high availability, see [Designing Highly Available Applications using RA-GRS](storage-designing-ha-apps-with-ragrs.md).</span></span>

## <a name="transferring-data-to-and-from-azure-storage"></a><span data-ttu-id="b3b27-263">Azure Storage 간에 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="b3b27-263">Transferring data to and from Azure Storage</span></span>

<span data-ttu-id="b3b27-264">AzCopy 명령줄 유틸리티를 사용하여 저장소 계정 내에서 또는 저장소 계정 간에 Blob 및 파일 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-264">You can use the AzCopy command-line utility to copy blob, and file data within your storage account or across storage accounts.</span></span> <span data-ttu-id="b3b27-265">도움말은 다음 문서 중 하나를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3b27-265">See one of the following articles for help:</span></span>

* [<span data-ttu-id="b3b27-266">Windows에서 AzCopy를 사용하여 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="b3b27-266">Transfer data with AzCopy for Windows</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="b3b27-267">Linux에서 AzCopy를 사용하여 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="b3b27-267">Transfer data with AzCopy for Linux</span></span>](storage-use-azcopy-linux.md)

<span data-ttu-id="b3b27-268">AzCopy는 [Azure 데이터 이동 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)를 기반으로 구축되며 현재 미리 보기에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-268">AzCopy is built on top of the [Azure Data Movement Library](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), which is currently available in preview.</span></span>

<span data-ttu-id="b3b27-269">Azure Import/Export 서비스는 저장소 계정 간에 대량의 Blob 데이터를 가져오거나 내보내는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-269">The Azure Import/Export service can be used to import or export large amounts of blob data to or from your storage account.</span></span> <span data-ttu-id="b3b27-270">여러 하드 드라이브를 준비하고 Azure 데이터 센터에 전자 메일로 보내면 여기에서 하드 드라이브 간에 데이터를 전송하고 하드 드라이브를 다시 사용자에게 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-270">You prepare and mail multiple hard drives to an Azure data center, where they will transfer the data to/from the hard drives and send the hard drives back to you.</span></span> <span data-ttu-id="b3b27-271">Import/Export 서비스에 대한 자세한 내용은 [Microsoft Azure Import/Export 서비스를 사용하여 Blob Storage에 데이터 전송](../storage-import-export-service.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3b27-271">For more information about the Import/Export service, see [Use the Microsoft Azure Import/Export Service to Transfer Data to Blob Storage](../storage-import-export-service.md).</span></span>

## <a name="pricing"></a><span data-ttu-id="b3b27-272">가격</span><span class="sxs-lookup"><span data-stu-id="b3b27-272">Pricing</span></span>

<span data-ttu-id="b3b27-273">Azure Storage에서 가격 책정에 대한 자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/storage/blobs/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3b27-273">For detailed information about pricing for Azure Storage, see the [Pricing page](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>

## <a name="storage-apis-libraries-and-tools"></a><span data-ttu-id="b3b27-274">Storage API, 라이브러리 및 도구</span><span class="sxs-lookup"><span data-stu-id="b3b27-274">Storage APIs, libraries, and tools</span></span>
<span data-ttu-id="b3b27-275">Azure Storage 리소스는 HTTP/HTTPS 요청을 수행할 수 있는 모든 언어로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-275">Azure Storage resources can be accessed by any language that can make HTTP/HTTPS requests.</span></span> <span data-ttu-id="b3b27-276">또한 Azure storage는 많이 사용되는 몇 가지 언어를 위한 프로그래밍 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-276">Additionally, Azure Storage offers programming libraries for several popular languages.</span></span> <span data-ttu-id="b3b27-277">이 라이브러리는 동기/비동기 호출, 작업 일괄 처리, 예외 관리, 자동 재시도, 작업자 동작 등과 같은 세부 사항을 처리하여 Azure Storage 작업의 많은 측면을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-277">These libraries simplify many aspects of working with Azure Storage by handling details such as synchronous and asynchronous invocation, batching of operations, exception management, automatic retries, operational behavior, and so forth.</span></span> <span data-ttu-id="b3b27-278">현재 이 라이브러리는 파이프라인의 다른 라이브러리와 함께 다음 언어 및 플랫폼에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b27-278">Libraries are currently available for the following languages and platforms, with others in the pipeline:</span></span>

### <a name="azure-storage-data-services"></a><span data-ttu-id="b3b27-279">Azure Storage 데이터 서비스</span><span class="sxs-lookup"><span data-stu-id="b3b27-279">Azure Storage data services</span></span>
* [<span data-ttu-id="b3b27-280">저장소 서비스 REST API</span><span class="sxs-lookup"><span data-stu-id="b3b27-280">Storage Services REST API</span></span>](/rest/api/storageservices/)
* [<span data-ttu-id="b3b27-281">.NET용 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="b3b27-281">Storage Client Library for .NET</span></span>](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [<span data-ttu-id="b3b27-282">Storage Client Library for C++</span><span class="sxs-lookup"><span data-stu-id="b3b27-282">Storage Client Library for C++</span></span>](https://github.com/Azure/azure-storage-cpp)
* [<span data-ttu-id="b3b27-283">Java/Android용 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="b3b27-283">Storage Client Library for Java/Android</span></span>](https://azure.microsoft.com/develop/java/)
* [<span data-ttu-id="b3b27-284">Node.js용 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="b3b27-284">Storage Client Library for Node.js</span></span>](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [<span data-ttu-id="b3b27-285">PHP용 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="b3b27-285">Storage Client Library for PHP</span></span>](https://azure.microsoft.com/develop/php/)
* [<span data-ttu-id="b3b27-286">Python용 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="b3b27-286">Storage Client Library for Python</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="b3b27-287">Ruby용 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="b3b27-287">Storage Client Library for Ruby</span></span>](https://azure.microsoft.com/develop/ruby/)
* [<span data-ttu-id="b3b27-288">PowerShell용 Storage Cmdlet</span><span class="sxs-lookup"><span data-stu-id="b3b27-288">Storage Cmdlets for PowerShell</span></span>](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)
* [<span data-ttu-id="b3b27-289">CLI 2.0의 저장소 명령</span><span class="sxs-lookup"><span data-stu-id="b3b27-289">Storage Commands for CLI 2.0</span></span>](/cli/azure/storage)

## <a name="next-steps"></a><span data-ttu-id="b3b27-290">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b3b27-290">Next steps</span></span>

* [<span data-ttu-id="b3b27-291">Blob Storage에 대한 세부 정보</span><span class="sxs-lookup"><span data-stu-id="b3b27-291">Learn more about Blob storage</span></span>](../blobs/storage-blobs-introduction.md)
* [<span data-ttu-id="b3b27-292">File Storage에 대한 세부 정보</span><span class="sxs-lookup"><span data-stu-id="b3b27-292">Learn more about File storage</span></span>](../storage-files-introduction.md)
* [<span data-ttu-id="b3b27-293">Queue Storage에 대한 세부 정보</span><span class="sxs-lookup"><span data-stu-id="b3b27-293">Learn more about Queue storage</span></span>](../queues/storage-queues-introduction.md)

<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
To get up and running with Azure Storage quickly, check out one of the following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->

<!-- FIGURE OUT WHAT TO DO WITH ALL THESE LINKS.

Azure Storage resources can be accessed by any language that can make HTTP/HTTPS requests. Additionally, Azure Storage offers programming libraries for several popular languages. These libraries simplify many aspects of working with Azure Storage by handling details such as synchronous and asynchronous invocation, batching of operations, exception management, automatic retries, operational behavior and so forth. Libraries are currently available for the following languages and platforms, with others in the pipeline:

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
* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.
* [Azure Storage Client Tools](../storage-explorers.md)
* [Azure SDKs and Tools](https://azure.microsoft.com/tools/)
* [Azure Storage Emulator](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy Command-Line Utility](http://aka.ms/downloadazcopy)

## Next steps
To learn more about Azure Storage, explore these resources:

### Documentation
* [Azure Storage Documentation](https://azure.microsoft.com/documentation/services/storage/)
* [Create a storage account](../storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link to one of those. 
Had to remove this article, it refers to the VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a><span data-ttu-id="b3b27-294">관리자용</span><span class="sxs-lookup"><span data-stu-id="b3b27-294">For administrators</span></span>
* [<span data-ttu-id="b3b27-295">Azure Storage와 함께 Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="b3b27-295">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="b3b27-296">Azure Storage에서 Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="b3b27-296">Using Azure CLI with Azure Storage</span></span>](../storage-azure-cli.md)

### <a name="for-net-developers"></a><span data-ttu-id="b3b27-297">.NET 개발자용</span><span class="sxs-lookup"><span data-stu-id="b3b27-297">For .NET developers</span></span>
* [<span data-ttu-id="b3b27-298">.NET을 사용하여 Azure Blob 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="b3b27-298">Get started with Azure Blob storage using .NET</span></span>](../blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="b3b27-299">.NET을 사용하여 Azure 테이블 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="b3b27-299">Get started with Azure Table storage using .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="b3b27-300">.NET을 사용하여 Azure 큐 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="b3b27-300">Get started with Azure Queue storage using .NET</span></span>](../storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="b3b27-301">Windows에서 Azure 파일 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="b3b27-301">Get started with Azure File storage on Windows</span></span>](../storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a><span data-ttu-id="b3b27-302">Java/Android 개발자용</span><span class="sxs-lookup"><span data-stu-id="b3b27-302">For Java/Android developers</span></span>
* [<span data-ttu-id="b3b27-303">Java에서 Blob 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b3b27-303">How to use Blob storage from Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="b3b27-304">Java에서 테이블 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b3b27-304">How to use Table storage from Java</span></span>](../../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="b3b27-305">Java에서 큐 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b3b27-305">How to use Queue storage from Java</span></span>](../storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="b3b27-306">Java에서 파일 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b3b27-306">How to use File storage from Java</span></span>](../storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a><span data-ttu-id="b3b27-307">Node.js 개발자용</span><span class="sxs-lookup"><span data-stu-id="b3b27-307">For Node.js developers</span></span>
* [<span data-ttu-id="b3b27-308">Node.js에서 Blob 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b3b27-308">How to use Blob storage from Node.js</span></span>](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="b3b27-309">Node.js에서 테이블 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b3b27-309">How to use Table storage from Node.js</span></span>](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [<span data-ttu-id="b3b27-310">Node.js에서 큐 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b3b27-310">How to use Queue storage from Node.js</span></span>](../storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a><span data-ttu-id="b3b27-311">PHP 개발자용</span><span class="sxs-lookup"><span data-stu-id="b3b27-311">For PHP developers</span></span>
* [<span data-ttu-id="b3b27-312">PHP에서 Blob 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b3b27-312">How to use Blob storage from PHP</span></span>](../blobs/storage-php-how-to-use-blobs.md)
* [<span data-ttu-id="b3b27-313">PHP에서 테이블 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b3b27-313">How to use Table storage from PHP</span></span>](../../cosmos-db/table-storage-how-to-use-php.md)
* [<span data-ttu-id="b3b27-314">PHP에서 큐 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b3b27-314">How to use Queue storage from PHP</span></span>](../storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a><span data-ttu-id="b3b27-315">Ruby 개발자용</span><span class="sxs-lookup"><span data-stu-id="b3b27-315">For Ruby developers</span></span>
* [<span data-ttu-id="b3b27-316">Ruby에서 Blob 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b3b27-316">How to use Blob storage from Ruby</span></span>](../blobs/storage-ruby-how-to-use-blob-storage.md)
* [<span data-ttu-id="b3b27-317">Ruby에서 테이블 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b3b27-317">How to use Table storage from Ruby</span></span>](../../cosmos-db/table-storage-how-to-use-ruby.md)
* [<span data-ttu-id="b3b27-318">Ruby에서 큐 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b3b27-318">How to use Queue storage from Ruby</span></span>](../storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a><span data-ttu-id="b3b27-319">Python 개발자용</span><span class="sxs-lookup"><span data-stu-id="b3b27-319">For Python developers</span></span>
* [<span data-ttu-id="b3b27-320">Python에서 Blob 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b3b27-320">How to use Blob storage from Python</span></span>](../blobs/storage-python-how-to-use-blob-storage.md)
* [<span data-ttu-id="b3b27-321">Python에서 테이블 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b3b27-321">How to use Table storage from Python</span></span>](../../cosmos-db/table-storage-how-to-use-python.md)
* [<span data-ttu-id="b3b27-322">Python에서 큐 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b3b27-322">How to use Queue storage from Python</span></span>](../storage-python-how-to-use-queue-storage.md)   
* <span data-ttu-id="b3b27-323">[Python에서 File Storage를 사용하는 방법](../storage-python-how-to-use-file-storage.md) 
--></span><span class="sxs-lookup"><span data-stu-id="b3b27-323">[How to use File storage from Python](../storage-python-how-to-use-file-storage.md) 
--></span></span>