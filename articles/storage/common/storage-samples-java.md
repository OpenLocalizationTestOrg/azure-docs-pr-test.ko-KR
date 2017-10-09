---
title: "Java를 사용 하 여 aaaAzure 저장소 샘플 | Microsoft Docs"
description: "Azure 저장소에 대한 샘플 코드 및 응용 프로그램을 확인하고 다운로드하여 실행합니다. Hello Java 저장소 클라이언트 라이브러리를 사용 하 여 blob, 큐, 테이블 및 파일에 대 한 샘플 시작을 검색 합니다."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: 6aec326cbfedc1166fc61037ac39d33c15d28d2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-java"></a><span data-ttu-id="e6237-104">Java를 사용한 Azure Storage 샘플</span><span class="sxs-lookup"><span data-stu-id="e6237-104">Azure Storage samples using Java</span></span>

## <a name="java-sample-index"></a><span data-ttu-id="e6237-105">Java 샘플 인덱스</span><span class="sxs-lookup"><span data-stu-id="e6237-105">Java sample index</span></span>

<span data-ttu-id="e6237-106">hello 다음 표에 간략하게 샘플 리포지토리 및 hello 시나리오 각 샘플에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6237-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="e6237-107">Hello 링크 tooview hello 해당 샘플 코드에 GitHub에서 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6237-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="e6237-108">끝점</span><span class="sxs-lookup"><span data-stu-id="e6237-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="e6237-109">시나리오</span><span class="sxs-lookup"><span data-stu-id="e6237-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="e6237-110">샘플 코드</span><span class="sxs-lookup"><span data-stu-id="e6237-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="e6237-111"><b>Blob</b></span><span class="sxs-lookup"><span data-stu-id="e6237-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="e6237-112">Blob 추가</span><span class="sxs-lookup"><span data-stu-id="e6237-112">Append Blob</span></span></td> 
<td><span data-ttu-id="e6237-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e6237-114">블록 Blob</span><span class="sxs-lookup"><span data-stu-id="e6237-114">Block Blob</span></span></td>
<td><span data-ttu-id="e6237-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e6237-116">클라이언트 쪽 암호화</span><span class="sxs-lookup"><span data-stu-id="e6237-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="e6237-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Java에서 Azure 클라이언트 쪽 암호화 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e6237-118">Blob 복사</span><span class="sxs-lookup"><span data-stu-id="e6237-118">Copy Blob</span></span></td>
<td><span data-ttu-id="e6237-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e6237-120">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="e6237-120">Create Container</span></span></td>
<td><span data-ttu-id="e6237-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e6237-122">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="e6237-122">Delete Blob</span></span></td>
<td><span data-ttu-id="e6237-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e6237-124">컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="e6237-124">Delete Container</span></span></td>
<td><span data-ttu-id="e6237-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e6237-126">BLOB 메타데이터/속성/통계</span><span class="sxs-lookup"><span data-stu-id="e6237-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="e6237-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e6237-128">컨테이너 ACL/메타데이터/속성</span><span class="sxs-lookup"><span data-stu-id="e6237-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="e6237-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e6237-130">페이지 범위 가져오기</span><span class="sxs-lookup"><span data-stu-id="e6237-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="e6237-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">페이지 BLOB 테스트 샘플</a></span><span class="sxs-lookup"><span data-stu-id="e6237-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Page Blob Tests Sample</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e6237-132">BLOB/컨테이너 임대</span><span class="sxs-lookup"><span data-stu-id="e6237-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="e6237-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e6237-134">BLOB/컨테이너 나열</span><span class="sxs-lookup"><span data-stu-id="e6237-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="e6237-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e6237-136">페이지 Blob</span><span class="sxs-lookup"><span data-stu-id="e6237-136">Page Blob</span></span></td>
<td><span data-ttu-id="e6237-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="e6237-138">SAS</span><span class="sxs-lookup"><span data-stu-id="e6237-138">SAS</span></span></td>
<td><span data-ttu-id="e6237-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS 테스트 샘플</a></span><span class="sxs-lookup"><span data-stu-id="e6237-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS Tests Sample</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="e6237-140">서비스 속성</span><span class="sxs-lookup"><span data-stu-id="e6237-140">Service Properties</span></span></td>
<td><span data-ttu-id="e6237-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="e6237-142">Blob 스냅숏</span><span class="sxs-lookup"><span data-stu-id="e6237-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="e6237-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="e6237-144"><b>파일</b></span><span class="sxs-lookup"><span data-stu-id="e6237-144"><b>File</b></span></span></td>
<td><span data-ttu-id="e6237-145">공유/디렉터리/파일 만들기</span><span class="sxs-lookup"><span data-stu-id="e6237-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="e6237-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="e6237-147">공유/디렉터리/파일 삭제</span><span class="sxs-lookup"><span data-stu-id="e6237-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="e6237-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e6237-149">디렉터리 속성/메타데이터</span><span class="sxs-lookup"><span data-stu-id="e6237-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="e6237-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e6237-151">파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="e6237-151">Download Files</span></span></td> 
<td><span data-ttu-id="e6237-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e6237-153">파일 속성/메타데이터/메트릭</span><span class="sxs-lookup"><span data-stu-id="e6237-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="e6237-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e6237-155">파일 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="e6237-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="e6237-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e6237-157">디렉터리 및 파일 나열</span><span class="sxs-lookup"><span data-stu-id="e6237-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="e6237-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="e6237-159">공유 나열</span><span class="sxs-lookup"><span data-stu-id="e6237-159">List Shares</span></span></td> 
<td><span data-ttu-id="e6237-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="e6237-161">속성/메타데이터/통계 공유</span><span class="sxs-lookup"><span data-stu-id="e6237-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="e6237-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="e6237-163"><b>큐</b></span><span class="sxs-lookup"><span data-stu-id="e6237-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="e6237-164">메시지 추가</span><span class="sxs-lookup"><span data-stu-id="e6237-164">Add Message</span></span></td> 
<td><span data-ttu-id="e6237-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java 클라이언트 라이브러리 샘플</a></span><span class="sxs-lookup"><span data-stu-id="e6237-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e6237-166">클라이언트 쪽 암호화</span><span class="sxs-lookup"><span data-stu-id="e6237-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="e6237-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java 클라이언트 라이브러리 샘플</a></span><span class="sxs-lookup"><span data-stu-id="e6237-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e6237-168">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="e6237-168">Create Queues</span></span></td> 
<td><span data-ttu-id="e6237-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java에서 Azure Queue Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e6237-170">메시지/큐 삭제</span><span class="sxs-lookup"><span data-stu-id="e6237-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="e6237-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java에서 Azure Queue Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e6237-172">메시지 보기</span><span class="sxs-lookup"><span data-stu-id="e6237-172">Peek Message</span></span></td> 
<td><span data-ttu-id="e6237-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java에서 Azure Queue Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e6237-174">큐 ACL/메타데이터/통계</span><span class="sxs-lookup"><span data-stu-id="e6237-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="e6237-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Java에서 Azure Queue Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e6237-176">큐 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="e6237-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="e6237-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Java에서 Azure Queue Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e6237-178">메시지 업데이트</span><span class="sxs-lookup"><span data-stu-id="e6237-178">Update Message</span></span></td> 
<td><span data-ttu-id="e6237-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java에서 Azure Queue Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="e6237-180"><b>테이블</b></span><span class="sxs-lookup"><span data-stu-id="e6237-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="e6237-181">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="e6237-181">Create Table</span></span></td> 
<td><span data-ttu-id="e6237-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java에서 Azure Table Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e6237-183">엔터티/테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="e6237-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="e6237-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java에서 Azure Table Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e6237-185">엔터티 삽입/병합/바꾸기</span><span class="sxs-lookup"><span data-stu-id="e6237-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="e6237-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java 클라이언트 라이브러리 샘플</a></span><span class="sxs-lookup"><span data-stu-id="e6237-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e6237-187">엔터티 쿼리</span><span class="sxs-lookup"><span data-stu-id="e6237-187">Query Entities</span></span></td> 
<td><span data-ttu-id="e6237-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java에서 Azure Table Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e6237-189">쿼리 테이블</span><span class="sxs-lookup"><span data-stu-id="e6237-189">Query Tables</span></span></td> 
<td><span data-ttu-id="e6237-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java에서 Azure Table Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e6237-191">테이블 ACL/속성</span><span class="sxs-lookup"><span data-stu-id="e6237-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="e6237-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Java에서 Azure Table Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="e6237-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e6237-193">엔터티 업데이트</span><span class="sxs-lookup"><span data-stu-id="e6237-193">Update Entity</span></span></td> 
<td><span data-ttu-id="e6237-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java 클라이언트 라이브러리 샘플</a></span><span class="sxs-lookup"><span data-stu-id="e6237-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="e6237-195">Azure 코드 샘플 라이브러리</span><span class="sxs-lookup"><span data-stu-id="e6237-195">Azure Code Samples library</span></span>

<span data-ttu-id="e6237-196">tooview hello 전체 예제 라이브러리를 이동 toohello [Azure 코드 예제](https://azure.microsoft.com/resources/samples/?service=storage) 다운로드 하 고 로컬로 실행할 수 있는 Azure 저장소에 대 한 샘플을 포함 하는 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="e6237-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="e6237-197">코드 예제 라이브러리 hello.zip 형식에서 샘플 코드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6237-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="e6237-198">또는 검색 하 고 각 샘플에 대 한 hello GitHub 리포지토리 복제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6237-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-java-samples-include](../../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="e6237-199">시작 가이드</span><span class="sxs-lookup"><span data-stu-id="e6237-199">Getting started guides</span></span>

<span data-ttu-id="e6237-200">체크 아웃 방법에 대 한 원하는 경우 지침을 따라 hello tooinstall 및 Azure 저장소 클라이언트 라이브러리 hello로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6237-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="e6237-201">Java에서 Azure Blob Service 시작</span><span class="sxs-lookup"><span data-stu-id="e6237-201">Getting Started with Azure Blob Service in Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="e6237-202">Java에서 Azure Queue Service 시작</span><span class="sxs-lookup"><span data-stu-id="e6237-202">Getting Started with Azure Queue Service in Java</span></span>](../storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="e6237-203">Java에서 Azure Table Service 시작</span><span class="sxs-lookup"><span data-stu-id="e6237-203">Getting Started with Azure Table Service in Java</span></span>](../../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="e6237-204">Java에서 Azure File Service 시작</span><span class="sxs-lookup"><span data-stu-id="e6237-204">Getting Started with Azure File Service in Java</span></span>](../storage-java-how-to-use-file-storage.md)

## <a name="next-steps"></a><span data-ttu-id="e6237-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e6237-205">Next steps</span></span>

<span data-ttu-id="e6237-206">다른 언어용 샘플에 대한 정보:</span><span class="sxs-lookup"><span data-stu-id="e6237-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="e6237-207">.NET: [.NET을 사용한 Azure Storage 샘플](../storage-samples-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="e6237-207">.NET: [Azure Storage samples using .NET](../storage-samples-dotnet.md)</span></span>
* <span data-ttu-id="e6237-208">다른 모든 언어: [Azure Storage 샘플](../storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="e6237-208">All other languages: [Azure Storage samples](../storage-samples.md)</span></span>
