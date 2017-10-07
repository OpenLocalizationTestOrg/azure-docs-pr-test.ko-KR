---
title: "Blob 저장소 aaaIntroduction tooAzure | Microsoft Docs"
description: "소개 tooAzure Blob 저장소"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: robinsh
ms.openlocfilehash: 3431f826ae51d42dbced084ee60f9ff70a8168d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooblob-storage"></a><span data-ttu-id="682e8-103">소개 tooBlob 저장소</span><span class="sxs-lookup"><span data-stu-id="682e8-103">Introduction tooBlob storage</span></span>

<span data-ttu-id="682e8-104">Azure Blob 저장소는 많은 양의 텍스트 또는 이진 데이터를 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 통해 hello world에 같은 구조화 되지 않은 개체 데이터를 저장 하기 위한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="682e8-104">Azure Blob storage is a service for storing large amounts of unstructured object data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="682e8-105">Blob 저장소 tooexpose 데이터 사용 하 여 공개적으로 toohello 권역 또는 toostore 응용 프로그램 데이터 개인적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="682e8-105">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span>

<span data-ttu-id="682e8-106">Blob 저장소의 일반적인 사용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="682e8-106">Common uses of Blob storage include:</span></span>

* <span data-ttu-id="682e8-107">서비스 제공 이미지 또는 직접 tooa 브라우저에 설명</span><span class="sxs-lookup"><span data-stu-id="682e8-107">Serving images or documents directly tooa browser</span></span>
* <span data-ttu-id="682e8-108">분산 액세스를 위해 파일 저장</span><span class="sxs-lookup"><span data-stu-id="682e8-108">Storing files for distributed access</span></span>
* <span data-ttu-id="682e8-109">동영상 및 오디오 스트리밍</span><span class="sxs-lookup"><span data-stu-id="682e8-109">Streaming video and audio</span></span>
* <span data-ttu-id="682e8-110">백업 및 복원, 재해 복구 및 보관을 위한 데이터 저장</span><span class="sxs-lookup"><span data-stu-id="682e8-110">Storing data for backup and restore, disaster recovery, and archiving</span></span>
* <span data-ttu-id="682e8-111">온-프레미스 또는 Azure 호스티드 서비스에서 분석하기 위해 데이터 저장</span><span class="sxs-lookup"><span data-stu-id="682e8-111">Storing data for analysis by an on-premises or Azure-hosted service</span></span>

## <a name="blob-service-concepts"></a><span data-ttu-id="682e8-112">BLOB 서비스 개념</span><span class="sxs-lookup"><span data-stu-id="682e8-112">Blob service concepts</span></span>

<span data-ttu-id="682e8-113">hello를 Blob 서비스는 hello를 다음과 같은 구성 요소가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682e8-113">hello Blob service contains hello following components:</span></span>

![Blob 아키텍처](./media/storage-blobs-introduction/blob1.png)

* <span data-ttu-id="682e8-115">**저장소 계정:** 저장소 계정을 통해 모든 액세스 tooAzure 저장소 작업은 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="682e8-115">**Storage Account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="682e8-116">이 저장소 계정은 **범용 저장소 계정**이거나, 개체/Blob 저장용으로 특화된 **Blob 저장소 계정**이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682e8-116">This storage account can be a **General-purpose storage account** or a **Blob storage account** that is specialized for storing objects/blobs.</span></span> <span data-ttu-id="682e8-117">자세한 내용은 [Azure Storage 계정 정보](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="682e8-117">See [About Azure storage accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

* <span data-ttu-id="682e8-118">**컨테이너:** 컨테이너는 Blob 집합 그룹화를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="682e8-118">**Container:** A container provides a grouping of a set of blobs.</span></span> <span data-ttu-id="682e8-119">모든 Blob은 컨테이너에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="682e8-119">All blobs must be in a container.</span></span> <span data-ttu-id="682e8-120">한 계정에 포함될 수 있는 컨테이너 수에는 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="682e8-120">An account can contain an unlimited number of containers.</span></span> <span data-ttu-id="682e8-121">한 컨테이너에 저장될 수 있는 Blob 수에도 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="682e8-121">A container can store an unlimited number of blobs.</span></span> <span data-ttu-id="682e8-122">Note 해당 hello 컨테이너 이름은 소문자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="682e8-122">Note that hello container name must be lowercase.</span></span>

* <span data-ttu-id="682e8-123">**Blob:** 모든 형식과 크기의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="682e8-123">**Blob:** A file of any type and size.</span></span> <span data-ttu-id="682e8-124">Azure 저장소에는 블록 Blob, 페이지 Blob 및 추가 Blob의 세 가지 Blob 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682e8-124">Azure Storage offers three types of blobs: block blobs, page blobs, and append blobs.</span></span>
  
    <span data-ttu-id="682e8-125">*블록 Blob* 은 문서 및 미디어 파일과 같은 텍스트 또는 이진 파일을 저장하기에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="682e8-125">*Block blobs* are ideal for storing text or binary files, such as documents and media files.</span></span> <span data-ttu-id="682e8-126">*추가 blob* 는 비슷한 tooblock blob는 블록으로 구성 하지만에 맞게 최적화 된 추가 작업을 로깅 시나리오에 유용한 되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="682e8-126">*Append blobs* are similar tooblock blobs in that they are made up of blocks, but they are optimized for append operations, so they are useful for logging scenarios.</span></span> <span data-ttu-id="682e8-127">단일 블록 blob too50, 각, too100 MB의 000 블록을 포함할 수 있습니다 (100 MB X 50000) 4.75 TB 보다 조금 더 큰의 전체 크기에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="682e8-127">A single block blob can contain up too50,000 blocks of up too100 MB each, for a total size of slightly more than 4.75 TB (100 MB X 50,000).</span></span> <span data-ttu-id="682e8-128">단일 blob too50, 각, too4 MB의 000 블록을 포함할 수 있습니다 (4 MB X 50000) 195 GB 보다 조금 더 큰의 전체 크기에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="682e8-128">A single append blob can contain up too50,000 blocks of up too4 MB each, for a total size of slightly more than 195 GB (4 MB X 50,000).</span></span>
  
    <span data-ttu-id="682e8-129">*페이지 blob* 크기가 too1 TB를 수 있으며 자주 읽기/쓰기 작업에 대 한 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="682e8-129">*Page blobs* can be up too1 TB in size, and are more efficient for frequent read/write operations.</span></span> <span data-ttu-id="682e8-130">Azure Virtual Machines는 OS 및 데이터 디스크로 페이지 Blob을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="682e8-130">Azure Virtual Machines uses page blobs as OS and data disks.</span></span>
  
    <span data-ttu-id="682e8-131">컨테이너 및 Blob를 명명하는 세부 정보는 [컨테이너, Blob 및 메타데이터 명명 및 참조](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="682e8-131">For details about naming containers and blobs, see [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span></span>

## <a name="next-steps"></a><span data-ttu-id="682e8-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="682e8-132">Next steps</span></span>

* [<span data-ttu-id="682e8-133">저장소 계정을 만드는</span><span class="sxs-lookup"><span data-stu-id="682e8-133">Create a storage account</span></span>](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="682e8-134">.NET을 사용하여 Blob 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="682e8-134">Getting started with Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)